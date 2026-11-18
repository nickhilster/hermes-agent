# KH-6 — Wayland GUI-driving gap

Research date: 2026-11-17 (local machine time: America/Toronto)
Target: hermes-dell, user session dell-nik. Research only; no packages/configuration/services were changed. Read-only checks were run on this machine. Where a live interaction would require prompting, installing software, or generating input, it was not performed.

## Decision

For a stock GNOME/Wayland desktop, the strongest least-privilege architecture is the XDG ScreenCast + RemoteDesktop portals (PipeWire video stream plus portal-authorized input), with AT-SPI2 as a semantic companion where applications expose useful accessibility information. It avoids granting an agent raw access to all input devices and is designed around visible user consent. This machine has the GNOME portal backend and advertises both interfaces, but no end-to-end portal session was requested, so actual prompt/session behavior remains unverified.

A local `wtype` binary is installed and works by asking the Wayland compositor to inject virtual-keyboard input; this is narrower than uinput but is text/key oriented and not screen capture. `ydotoold` is already running from a user-local binary, and this user has a per-user ACL on `/dev/uinput`; that is not a stock-package/default setup and carries broad input-injection risk. The initial control-ceiling result is not present in the checked-out repo or its Git tree, so its reported AccessDenied finding is treated as supplied context, not independently revalidated here.

## Evidence checked on this machine

- Session variables: `XDG_SESSION_TYPE=wayland`, `XDG_CURRENT_DESKTOP=ubuntu:GNOME`, `WAYLAND_DISPLAY=wayland-0`, `DISPLAY=:0`; GNOME Shell 50.1.
- User portal bus has `org.freedesktop.portal.Desktop`; GNOME backend `org.freedesktop.impl.portal.desktop.gnome`; GTK backend also present. GNOME backend file declares `RemoteDesktop` and `ScreenCast` interfaces and `UseIn=gnome`.
- Live portal introspection: ScreenCast version 5, RemoteDesktop version 2. RemoteDesktop offers CreateSession, SelectDevices, Start and pointer/keyboard/touch notifications. ScreenCast offers CreateSession, SelectSources, Start, OpenPipeWireRemote. This proves advertised API availability, not that a user-consented capture/control session succeeds.
- Installed packages: xdg-desktop-portal 1.21.1+ds-1ubuntu3.1; xdg-desktop-portal-gnome 50.0-0ubuntu1; xdg-desktop-portal-gtk 1.15.3-2ubuntu1; at-spi2-core 2.60.4-0ubuntu0.1; wtype 0.4-3build1. `python3-pyatspi`, dogtail, and ydotool Debian package are not installed. Apt metadata offers python3-pyatspi 2.58.1-1, dogtail 1.0.7-3 and ydotool 1.0.4-3.
- `/usr/bin/wtype` exists. `~/.local/bin/ydotool` exists outside dpkg and `ydotoold` is already running with a socket under `/run/user/1000`; therefore this is not evidence that stock Ubuntu supplies it.
- `/dev/uinput` is root:root mode 0600, but ACL grants user `nikhil` read/write. User is not in the `input` group. `/dev/input/event*` are root:input 0660. The uinput ACL and active daemon are machine-specific observed state; no change was made.
- AT-SPI D-Bus bus and GNOME accessibility manager are active. `pyatspi` import failed in the current Python environment because the binding is absent there. No AT-SPI client was installed or exercised.
- Xwayland is running on `:0`. `/usr/share/wayland-sessions` contains `ubuntu.desktop`; `/usr/share/xsessions` was absent/empty. Thus Xwayland applications exist, but a stock Xorg login session was not established as available.
- The referenced `evidence/full-access-zenbook-2026-11-17/` path was not found in this checkout, nor in the checked Git tree. Its reported result is context only.

## Options

### 1. XDG Desktop Portals: ScreenCast + RemoteDesktop

What it does: ScreenCast lets a client request selection of a monitor/window and receive frames through PipeWire; RemoteDesktop can request keyboard, pointer and touch devices and send corresponding events after a portal-mediated session start. Used together, this is the most complete supported screen-and-input path. The portal API does not imply silent/unattended access: the desktop backend and policy decide consent and session lifetime.

Permissions / stock status: no root or `input` group membership is inherently required for a normal portal client. A logged-in graphical session, D-Bus, portal frontend/backend and PipeWire stack are prerequisites. Those portal components and interfaces are present here. User approval and persistent-authorization semantics must be tested on the exact Ubuntu/GNOME build; do not assume prior approval survives logout or grants indefinite access.

Security: best default posture in this comparison. The user can see/approve what is shared, and access is scoped to an app/session rather than raw device nodes. Still powerful: an approved client can observe sensitive screen content and operate the desktop. Treat the agent/client identity and lifetime as security boundaries.

Verdict: VIABLE, with consent and end-to-end test conditional. Best current option. Evidence: live D-Bus interfaces/versions and local backend configuration above; upstream API references listed below. Not tested: opening a real portal chooser, capturing PipeWire frames, or sending a harmless input event, to avoid prompting/side effects and because the research brief prohibits changes.

### 2. AT-SPI2 accessibility tree (pyatspi / dogtail)

What it does: exposes semantic application objects (roles, names, states, text, actions and hierarchy) over the accessibility bus. It can be a robust non-pixel observation/control channel for applications that implement AT-SPI well. It is not a universal desktop screenshot, does not guarantee access to arbitrary canvas/video/custom widgets, and does not replace physical pointer/keyboard control. Dogtail is a higher-level Python automation library built on accessibility information; pyatspi is the Python binding/client interface.

Permissions / stock status: normally operates as the logged-in user via the accessibility D-Bus; no uinput or input-group membership is needed. AT-SPI core and bus are active here. The Python binding and dogtail are absent; apt offers them, but installing was out of scope. Whether all target applications expose useful trees must be tested individually.

Security: no raw device access, but the tree can disclose on-screen text and semantic content; actions can activate controls. Limit client trust and scope. Accessibility interfaces are not a security sandbox against an authorized same-user process.

Verdict: VIABLE as a complementary channel; conditional for broad coverage. Evidence: active `org.a11y.Bus` and GNOME accessibility manager, installed core, missing Python binding and package metadata. Not tested: tree traversal or action invocation because required client packages are absent and installation prohibited.

### 3. wtype

What it does: Wayland virtual-keyboard protocol client, primarily for key presses and typing. It cannot capture the screen, and should not be mistaken for a full pointer/control API.

Permissions / stock status: runs as an ordinary Wayland client, relying on compositor support/protocol availability; no raw `/dev/input` or uinput permissions should be needed. Installed on this machine but not necessarily part of every stock Ubuntu image. This check established binary/package presence only; no keys were sent.

Security: compositor-mediated input injection is more constrained than raw evdev/uinput, but a process allowed to inject keys can still cause consequential actions. Do not grant it to untrusted code.

Verdict: CONDITIONAL, useful for keyboard-only automation where compositor support exists; not a screen-and-input solution. Evidence: installed package/binary and live Wayland session. Not tested with actual event generation.

### 4. ydotool

What it does: provides mouse movement/click and keyboard/type via Linux uinput, generally through a daemon/socket. It can drive input but does not capture the screen.

Permissions / stock status: daemon needs access to `/dev/uinput`; common deployments arrange this with root/service configuration, udev rules, ACLs, or group permissions. This machine's node is root:root 0600, but its ACL grants this user rw, and a user-local `ydotoold` is already running. The Debian ydotool package is not installed; apt candidate exists. User is not in `input`. Do not infer the user-local binary's origin or setup from package metadata.

Security: raw virtual-device injection is broad and can affect the entire session, including dialogs and security-sensitive UI. A persistent daemon/socket adds an attack surface; constrain socket permissions and lifecycle. Adding a user to `input` or broad udev ACLs can also expose physical keystrokes/device data, so avoid blanket group membership as a shortcut.

Verdict: CONDITIONAL, not a stock-safe default. It may be viable for a deliberately configured trusted agent, but portal input is preferable. Evidence: executable/daemon, node ACL, group list, apt metadata. No input was sent; no config was changed.

### 5. dotool

What it does: Linux input automation commonly implemented using uinput, with keyboard/mouse action support; no screen capture. Some builds offer Wayland-specific modes, so behavior must be assessed for the exact package/build rather than inferred from the name.

Permissions / stock status: uinput-backed operation requires write access to `/dev/uinput` (often privileged setup/udev ACL or group policy); not assumed available on stock Ubuntu. `dotool` binary and package candidate were not found by the local checks; no installation attempted.

Security: same fundamental concern as ydotool for uinput: a trusted process can inject broad input. Avoid granting raw device access to arbitrary agent workloads.

Verdict: CONDITIONAL / currently unverified here, not recommended over portal or existing wtype. Evidence is limited: no local binary/package candidate surfaced in the queried package set. Its exact upstream build and distribution packaging were not independently verified in this run.

### 6. XWayland and X11 fallback

What it does: XWayland permits X11 applications inside the Wayland session, but it is not a general escape hatch: X11 clients ordinarily see/control only the X server environment they connect to, not the whole GNOME Wayland desktop. A separate Xorg session can enable traditional X11 screenshot/input automation tools with broader desktop access.

Permissions / stock status: XWayland is running here (`:0`). A separate Xorg session requires an installed/display-manager-provided Xorg session; this machine exposed only `ubuntu.desktop` under Wayland sessions and no Xsessions entry. Availability depends on Ubuntu release/image and may require extra packages or display-manager configuration, neither tested nor changed.

Security: X11's broad client trust model means a client in the same display can often observe/drive other clients. This is less isolated than portal consent and may expose credentials or sensitive UI to any same-display client. Use only in a dedicated, trusted environment if necessary.

Verdict: XWayland-only as a whole-desktop solution is a DEAD END; separate Xorg is CONDITIONAL legacy fallback with material security trade-offs. Evidence: live Xwayland process and session files; no separate Xorg login was attempted.

### 7. GNOME Shell extensions

What it does: an extension can run inside GNOME Shell and expose custom capture/control hooks or coordinate Shell APIs. Capability varies by extension and GNOME version; it is not a standard general-purpose agent GUI-control API. A Shell extension may access privileged compositor context unavailable to ordinary clients, which is also why it is security-sensitive.

Permissions / stock status: extensions are not a dependable stock-Ubuntu agent interface; installation/enabling typically requires user action and compatibility with the exact GNOME Shell release. GNOME Shell 50.1 here lists several enabled extensions, but none was established as an agent control bridge. No extension was installed or modified.

Security: very high trust. Extension code runs in the desktop shell context and could observe or manipulate user UI. Installation should require explicit human review and provenance/maintenance checks; an extension should not be a silent workaround for portal consent.

Verdict: CONDITIONAL for a purpose-built, reviewed, version-compatible extension; otherwise not recommended. Evidence: local extension list and Shell version. No capability test or extension installation was performed.

## Recommendation and unblock path

1. Prototype a short-lived, explicitly user-approved ScreenCast + RemoteDesktop portal client on this exact desktop. Verify consent UI, stream delivery, input-device selection, graceful stop/revocation, and behavior after logout/restart. Keep the client identity, visible status, and session lifecycle clear.
2. Add AT-SPI2 for semantic targeting and verification; install pyatspi/dogtail only after the human approves package installation. Validate coverage against the actual applications in scope.
3. Use wtype only for a narrowly scoped keyboard fallback if portal input cannot meet a defined need. Avoid expanding uinput ACL/group access; the existing per-user ACL and daemon are local state that should be audited separately, not treated as a stock deployment recipe.
4. Do not switch to Xorg or install a Shell extension unless a concrete requirement defeats portal/accessibility APIs and a human accepts the weaker isolation or privileged extension risk.

What could not be tested without installation/approval: pyatspi/dogtail behavior; packaged ydotool/dotool behavior; portal consent/session end-to-end; actual input generation; a separate Xorg session; any new GNOME extension. No install, configuration edit, persistent service start, or input event was initiated by this research.

## Receipts

Local receipts are the read-only commands/results summarized above: `date -Is`; session environment and `gnome-shell --version`; `busctl --user list`; D-Bus introspection of `org.freedesktop.portal.Desktop`; `busctl get-property` for ScreenCast/RemoteDesktop versions; contents of `/usr/share/xdg-desktop-portal/portals/gnome.portal`; `dpkg-query`, `apt-cache policy/show`; `id`, `ls -l`, and `getfacl` on input devices; process inspection for Xwayland and ydotoold; `gnome-extensions list --enabled`; and repository tree search for the cited Zenbook evidence.

Upstream API references checked for definitions (not relied on to establish local availability):
- XDG ScreenCast portal API: https://flatpak.github.io/xdg-desktop-portal/docs/doc-org.freedesktop.portal.ScreenCast.html
- XDG RemoteDesktop portal API: https://flatpak.github.io/xdg-desktop-portal/docs/doc-org.freedesktop.portal.RemoteDesktop.html
- AT-SPI2 project documentation: https://gnome.pages.gitlab.gnome.org/at-spi2-core/
- dogtail project: https://gitlab.com/dogtail/dogtail
- ydotool project: https://github.com/ReimuNotMoe/ydotool
- wtype project: https://github.com/atx/wtype
- dotool project: https://git.sr.ht/~geb/dotool

The references describe APIs/projects; local package, bus, ACL and process observations above are the receipts for this host. No claim is made that a cited project is installed unless explicitly stated.
