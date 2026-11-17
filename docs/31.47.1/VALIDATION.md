# EDIE 31.47.1 validation

Checks performed on the delivered source in this Linux execution environment:

- All 33 Python source files compile successfully.
- The complete inherited EDIE self-test passes.
- All 37 regression tests pass through the stable `EDIE.py --self-test`
  command, with temporary data and no live AI or microphone.
- Six new connection-lifetime tests keep strong references to SQLite connections
  to detect leaks even on platforms that allow deleting open files. The reported
  cleanup problem was reproduced as failed closure checks before the fix.
- Tests cover all five reproduced bugs, cross-thread/process JSON updates,
  speech cancellation while an utterance remains active, stale speech events,
  bounded buffering, segmentation/pre-roll, split Markdown fences, FTS triggers,
  embedding identity, chunk offsets, backup WAL snapshots and staged recovery,
  malformed settings, unsafe archives and safe-mode capture gating.
- The preceding 31.47.0 desktop and Voice and Reliability window passed an
  isolated Linux UI smoke check. This patch changes database lifetime handling
  and adds a compatibility launcher; it does not claim a new Windows UI test.
- The official Vosk 0.15 English archive was downloaded for verification only.
  Its SHA-256 matched the release pin, and bounded extraction/required-file
  validation passed. The downloaded model is not included in this package.
- Worker entry-point hashes match the embedded recovery copies. New modules
  and artwork are covered by `SHA256SUMS.json`.

The final ZIP is also read back, extracted into a fresh directory, checked with
`--verify-package`, and tested with `--upgrade-test` before delivery.

## Target-device checks still required

- Native Windows 11 start, exit, custom Python selection and batch error paths.
- SAPI5 speech playback/cancellation and the optional Piper backend.
- Microphone permission, real noise/acoustics, selected input/output devices,
  headphones versus speakers, and hardware-supported sample rates.
- Real Ollama model generation, CUDA availability and model-download networking
  on the user's computer.
- Sleep/resume, device hotplug, long sessions, low disk space and actual user
  data migrations/restoration on a copied data folder.
- Check the repository's Verify download GitHub Actions result for native
  Windows/Python 3.15 package verification. This result is separate from live
  microphone, SAPI and desktop-device tests.

The package is portable Python source. It is not a signed Windows installer.
`SHA256SUMS.json` checks file integrity; it is not a publisher signature.

The complete improvement tracker contains 23 complete changes, 36 partial
improvements and 41 planned items. Complete describes implemented code and
available checks, not certification of untested hardware.
