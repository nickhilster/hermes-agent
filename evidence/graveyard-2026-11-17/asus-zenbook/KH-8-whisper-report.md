# KH-8 — Whisper/STT close-out

Machine: asus-zenbook, hostname `Zen-nik`; observed Tuesday, November 17, 2026 (EST).
Scope: user-level only. No installation or configuration changes were made during this run; the tested runtime already contained faster-whisper and the base model.

## Observed

- `hermes` resolves to `/home/nik/.local/bin/hermes`, which execs `/home/nik/.hermes/hermes-agent/.hermes/bin/hermes`.
- Runtime Python selected by Hermes: `/home/nik/.hermes/installs/d0123adc22cc8fbe/environments/e1c66fbe733d4299a573d2d043585cbd/venv/bin/python3` (Python 3.14 site-packages). This was identified from the actual runtime path, not system Python.
- Effective STT config read through Hermes' own `tools.transcription_tools._load_stt_config()`: enabled `true`; provider resolved `local`; local model `base`; language `en`. `stt.provider` is omitted from YAML and auto-detects as local. The YAML is `/home/nik/.hermes/config.yaml`.
- Runtime imports report faster-whisper 1.2.1 and ctranslate2 4.8.3. Their package directory exists in the runtime. Although the dated brief said it was previously not found, on this run the import succeeded immediately; no install was necessary or attempted.
- Host observed: x86_64, 11th Gen Intel Core i7-1165G7 @ 2.80 GHz, 8 logical CPUs, 14 GiB RAM (9.3 GiB available at inspection), 4 GiB swap. This describes this Zenbook only; the father's reference hardware was not specified or independently checked.
- Whisper base model cache artifact: 145,217,532 bytes (about 138.5 MiB), at `~/.cache/huggingface/hub/blobs/0c/0c4d8d814973160f53608ff0aa1618a90abbce9ed632bbc54930475ba82ce973`. The model snapshot directory itself uses 2.6 MiB because the large blob is stored in the shared Hugging Face blob directory. Total `~/.cache/huggingface` is 142 MiB, including unrelated/support/cache files; not all of that is attributable to this model.
- Relevant installed runtime package directories observed: faster-whisper 1.5 MiB, ctranslate2 63 MiB, PyAV 32 MiB. These directory sizes should not be summed as unique disk use without accounting for shared files.
- Speech synthesis utilities `espeak`, `espeak-ng`, `festival`, and `flite` were not found. `spd-say` exists but did not produce a WAV file with the attempted `-w` invocation. Instead, a short public LibriSpeech dev-clean FLAC was downloaded from OpenSLR; its reference transcript was extracted from the corpus metadata. Temporary audio and the downloaded archive remain under `/home/nik/.hermes/cache/scratch/kh8/`.

## Tested

- Imported `faster_whisper` using the Hermes runtime Python above; import path was under that runtime's Python 3.14 `site-packages`.
- Called Hermes' actual public dispatcher `tools.transcription_tools.transcribe_audio()` on the downloaded speech FLAC. Result: `success=True`, provider `local`, transcript: “The long drizzle had begun, pedestrians had turned up collars and trousers at the bottom.” The corpus reference is “THE LONG DRIZZLE HAD BEGUN PEDESTRIANS HAD TURNED UP COLLARS AND TROUSERS AT THE BOTTOM”; the recognized wording matches, with punctuation/case normalized.
- Timed end-to-end transcription: 1.138 seconds inside the call (1.47 seconds process wall time), on a repeat run with the model cache warm. Peak RSS reported by `/usr/bin/time`: 515,452 KiB. The audio is a short excerpt; this is not a throughput benchmark.
- Separately timed direct `WhisperModel('base', device='cpu', compute_type='int8')` construction using the already-cached model: 0.406 seconds first construction, 0.209 seconds second construction in the same process. This is model object construction, not a fresh-process cold start; transcription timing above includes dispatcher/audio preparation.

## Not checked / limits

- No package install was performed because the required import already worked. No Hermes config mutation was made.
- No microphone, live gateway message, or physical recording was tested. The proof covers Hermes' local transcription dispatcher path with a real speech recording and no microphone.
- The first attempted `spd-say -w` file-generation route failed to create a WAV; that failed attempt was detected before the successful LibriSpeech route.
- Father-demographic hardware/performance suitability cannot be assessed without the specific hardware and workload. The Zenbook measurements are not a fleet or demographic acceptance claim.
- No comparison to other model sizes, sustained-load test, multilingual test, power/battery measurement, or full disk attribution was performed.
- No live install/config baseline from 2026-11-17 was independently retrieved; only the current state and the brief's dated claim are available here.

## Reproduction details

The tested dispatcher was imported with the Hermes runtime Python and Hermes source at `/home/nik/.hermes/hermes-agent`; the audio input was `/home/nik/.hermes/cache/scratch/kh8/sample.flac`. The process called `transcribe_audio(path)` and returned the result quoted above. The sample was LibriSpeech `dev-clean/2277/149896/2277-149896-0026.flac`, whose corresponding reference line was read from `2277-149896.trans.txt` in the downloaded archive.