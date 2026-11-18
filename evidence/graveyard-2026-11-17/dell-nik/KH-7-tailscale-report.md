# KH-7 — Tailscale peer visibility on `dell-nik`

Research-only report | 2026-11-18 | Host: `dell-nik` | Tailscale CLI 1.102.3

## Executive finding

A process running as the ordinary local account `nikhil` (UID 1000) can enumerate the full peer map exposed to this node using `tailscale status` and `tailscale status --json`, without root. On this host, the CLI status socket is world-readable/writable (`srw-rw-rw- root:root`), and the daemon runs as root. Therefore Linux's local operator-user setting does not protect this status surface here: visibility is available even to an unprivileged user. This is metadata exposure, not proof that the process can connect to each peer; access to traffic/services remains governed separately by network policy and peer services.

No Tailscale settings, ACLs, or device configuration were changed.

## 1. What a local unprivileged process learned

Commands actually run as `nikhil`, not via sudo:

```sh
id
# uid=1000(nikhil) gid=1000(nikhil) groups=... (includes sudo group)
tailscale version
# 1.102.3 (commit 53a0d659afa51835dd7a9283873cca44261454f8)
tailscale status
tailscale status --json
```

The tested account is a member of the sudo group but the demonstrations did not use sudo; thus it is unprivileged for these invocations, though not a specially constrained non-admin account. The socket permissions independently show all local users can access it. This was not a test under a separate locked-down UID.

Human-readable status output, reproduced exactly as returned:

```text
100.127.221.71  dell-nik      nickhilster@  linux    -
100.115.214.17  asus-zenbook  nickhilster@  linux    -
100.120.148.20  legion-linux  nickhilster@  linux    offline, last seen 5d ago
100.71.156.28   legion-win    nickhilster@  windows  -
100.64.222.82   muse          nickhilster@           active; relay "nyc", tx 45056 rx 49264
100.76.154.18   xps-plex      nickhilster@  linux    -
```

Nothing in the above was redacted. The user-facing table reveals peer Tailscale IPv4 address, hostname, owner login (displayed in abbreviated form by this CLI), OS when known, and status. Status can disclose online/offline and last-seen age, active/idle state, connection type and sometimes direct endpoint/relay region, plus transmitted/received byte counts. `--header` adds labels; `--active` filters but does not restrict underlying access; `--web` serves the status view locally.

`tailscale status --json` succeeded as the same user. It returned a JSON object with top-level fields `Version`, `TUN`, `BackendState`, `HaveNodeKey`, `AuthURL`, `TailscaleIPs`, `Self`, `Health`, `MagicDNSSuffix`, `CurrentTailnet`, `CertDomains`, `ExtraRecords`, `Peer`, `User`, and `ClientVersion`. The peer map contained five peers. Peer records included node IDs and public node keys, hostname and fully qualified MagicDNS name, OS, user ID, IPv4 and IPv6 Tailscale addresses and allowed prefixes, endpoint/addrs when populated, relay, traffic byte counters, creation/last-write/last-seen/last-handshake timestamps, online/active flags, exit-node flags, peer API URLs in some cases, file-sharing metadata, map/engine membership flags, and key expiry. Self metadata additionally included local interface/public/LAN endpoint addresses and local capabilities. The JSON data also exposed the tailnet MagicDNS suffix, tailnet/account name, user login/display name/profile image URL, and local daemon state/version.

To keep the local-only raw evidence unredacted without duplicating long key material in this report, the complete JSON was captured directly in the terminal output during this run; it was not written to a separate file. A compact, exact-field inventory was independently checked with:

```text
Top-level: Version, TUN, BackendState, HaveNodeKey, AuthURL, TailscaleIPs, Self, Health, MagicDNSSuffix, CurrentTailnet, CertDomains, ExtraRecords, Peer, User, ClientVersion
Peer count: 5
Peer fields: ID, NodeID, PublicKey, HostName, DNSName, OS, UserID, TailscaleIPs, AllowedIPs, Addrs, CurAddr, Relay, PeerRelay, RxBytes, TxBytes, Created, LastWrite, LastSeen, LastHandshake, Online, ExitNode, ExitNodeOption, Active, PeerAPIURL, TaildropTarget, NoFileSharingReason, InNetworkMap, InMagicSock, InEngine, KeyExpiry
```

Additional read-only probes: `tailscale whois 100.64.222.82` revealed that address's MagicDNS name, stable node ID, IPv4/IPv6 addresses, account login and numeric user ID. `tailscale ping -c 1 --timeout=2s 100.64.222.82` timed out; this demonstrates that enumeration does not establish successful peer reachability. `tailscale debug prefs` returned local preferences/account profile, but its output includes internal configuration fields and should not be treated as a peer-list mitigation. `tailscale debug netmap` was denied to this user with “debug access denied” and a suggestion to use sudo. Thus not every debug endpoint is available to an ordinary user.

Local daemon/socket observations:

```text
root ... /snap/tailscale/169/bin/tailscaled --socket /var/snap/tailscale/common/socket/tailscaled.sock ...
srw-rw-rw- root:root /var/snap/tailscale/common/socket/tailscaled.sock
```

The successful status query uses this Snap socket. The regular `/var/run/tailscale` socket path was absent. This host-specific socket ACL is direct evidence for why the CLI query worked here.

## 2. Relevant Tailscale controls and boundaries

- **Status surface:** Tailscale's CLI reference documents `status` as reporting connections to other devices; JSON is specifically described as a detailed list of peers and users plus local metadata. JSON schema is warned to be version-sensitive. ACLs/grants govern permitted connections; they are not a mechanism for concealing the peer inventory delivered to a node. The local observation confirms that on this host `status` and its JSON form are available without sudo.
- **ACLs / grants and posture:** Tailnet policy can restrict which source devices/users may connect to which destinations/ports. Current Tailscale documentation recommends grants for new policy work; ACL syntax remains supported. Device posture predicates add conditions such as OS/version/client version to an access rule. These enforce connectivity authorization; they do not, by themselves, make an already-authorized node's status output omit other nodes. Admin policy changes are required and can break existing flows if too restrictive.
- **Tailnet Lock:** This protects node admission/key distribution by requiring trusted signatures for new nodes. It is not a peer-list confidentiality control and does not hide the current network map from a connected device. It requires tailnet-level enablement and operational key management; adding devices becomes more involved.
- **Linux local access model:** Tailscale documents `tailscaled` as a privileged daemon (typically systemd on Linux) with the CLI as its client. Its CLI supports an `--operator=<user>` option to authorize a Unix user to operate the daemon without root; this is an operational delegation, not a documented peer-visibility filter. In this Snap installation the socket is mode 0666, so all local users can reach it. Other installations may use different socket ownership/modes; inspect the actual socket and daemon configuration rather than infer from distro defaults. A separate unprivileged user is not automatically isolated from a world-accessible socket.
- **Local API:** CLI communicates with the local daemon through its Unix socket. This host's socket permissions are permissive. Some debug/local API calls are separately denied (as observed for `debug netmap`), but the public status command is allowed. Restricting permissions only helps if the agent process runs under a distinct UID and the service/socket setup truly denies it; same-UID processes remain equivalent for filesystem permission checks.

## 3. Mitigation options for a KinOS-style deployment

| Option | What it buys | Breakage / usability cost | Tailnet admin action? |
|---|---|---|---|
| Leave current global Tailscale client; rely on grants/ACLs to prevent connections | Limits data-plane reachability while retaining current simple host integration | Does not solve peer inventory disclosure; agent can still learn names/addresses/status. | Yes, if policy needs tightening; no for visibility itself. |
| Run KinOS under a dedicated Unix UID; restrict daemon socket to root/explicit operator | Can deny that UID access to the CLI/local API if socket permissions and daemon installation are configured accordingly | Agent loses Tailscale status/control and may still reach peers through ordinary network routing if allowed; changes may conflict with Snap-managed socket permissions. Must validate after package/service updates. | No, local admin action needed. |
| Put KinOS in a network namespace/container without Tailscale socket, TUN, host networking, or host socket mounts; apply narrow egress | Strong local boundary: no daemon status API and no direct Tailscale interface access; can allow only required outbound services | More packaging/network complexity; peer access through host proxy or shared network reintroduces paths. Must avoid mounting the socket or inheriting host networking. | No tailnet action for local isolation; admin needed if peers/services must be re-authorized. |
| Separate tailnet / separate Tailscale identity for KinOS, with only required devices/services enrolled and a deny-by-default policy | Limits the actual network map KinOS can receive, rather than merely hiding a CLI from it; best fit when KinOS needs selected tailnet services | Extra account/device/key lifecycle and possible duplicated onboarding; services need deliberate sharing/routing. | Yes: tailnet owner/admin must create/configure the restricted tailnet or sharing/policy. This violates the “father must do nothing” constraint unless Nik provisions it completely. |
| Disable Tailscale on the KinOS host and use a narrowly scoped application relay/API instead | Removes local Tailscale inventory exposure entirely | Tailnet connectivity from KinOS is lost; relay must be built/secured/maintained. | No tailnet changes necessarily; Nik must build and operate relay. |
| Tailnet Lock | Helps prevent unauthorized node enrollment and key substitution | Does not mitigate enumeration by a connected device; adds signing/recovery workflow. | Yes, tailnet admin setup and ongoing signer/key operations. |
| Strip/redact status output in a KinOS wrapper | Reduces what the application itself is shown if all access is mediated through that wrapper | Not a security boundary if the agent can invoke `tailscale` directly, access socket, inspect host, or execute another client. | No, but local engineering; insufficient alone. |

## Recommendation ranked for a home deployment

1. **Preferred: isolate KinOS from the host Tailscale daemon at the OS boundary**—dedicated UID plus a container/network namespace with no LocalAPI socket, no TUN device, no host networking, and explicit outbound allowlisting. Nik provisions it once; the father does nothing. Do not rely on a wrapper or prompt policy. Validate that the agent cannot read the socket or access the Tailscale interface and that required KinOS functions still work.
2. **If KinOS genuinely needs tailnet resources, give it a separately scoped tailnet identity/network** containing only required devices, with deny-by-default grants. This is the strongest way to reduce the peer map the agent can learn, but requires Nik to perform tailnet admin/setup work and service migration. It need not require the father to act if Nik completes provisioning.
3. **If requirements are narrow, replace direct tailnet access with a small, allowlisted relay** operated by Nik. This preserves selected capabilities without exposing the full network map, at the cost of relay maintenance.
4. **Do not count ACLs alone, Tailnet Lock, `--active`, JSON filtering, or prompt-level rules as visibility mitigations.** They can be useful for connection security or output presentation, but don't satisfy the stated confidentiality goal on their own.

For this reference user, the practical default is option 1, with no user-facing setup or recurring action. If a test proves KinOS requires access to particular tailnet services, move those functions behind option 2 or 3 rather than restoring broad host LocalAPI visibility.

## Sources

1. Tailscale CLI reference: https://tailscale.com/docs/reference/tailscale-cli
2. Manage permissions using ACLs: https://tailscale.com/kb/1018/acls
3. Device posture management: https://tailscale.com/kb/1288/device-posture
4. Tailnet Lock: https://tailscale.com/kb/1226
5. tailscaled daemon: https://tailscale.com/kb/1278/tailscaled
6. Tailscale CLI: https://tailscale.com/kb/1080/cli/

Sources are official Tailscale documentation. Host observations are from direct read-only commands on `dell-nik` on 2026-11-18. No settings or policies were modified.
