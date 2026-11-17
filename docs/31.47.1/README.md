# EDIE 31.47.1 — Reliability and Voice Upgrade

This improved portable Python release is built from the nine uploaded EDIE
31.46.1 files. It includes the existing application, the new `edie/` services,
external artwork, verified worker launchers, tests and Windows scripts.
`IMPROVEMENTS.md` tracks the entire 100-item review: this release fixes the
reproduced bugs and adds reliability and voice improvements; larger redesigns
remain future work.

## Windows cleanup fix in 31.47.1

This patch fixes `WinError 32` when the self-test deletes its temporary SQLite
database. Initialization and the capability-test helper now close their database
connections explicitly, including failure paths. Six new connection-lifetime
regressions are included. See `CHANGELOG.md`.

## Start on Windows

1. Close the previous EDIE and extract the **whole ZIP** into a new folder.
2. Keep the old folder as a backup. Copy its complete `edie_data` folder into
   the new folder **before the first launch** to retain your work.
3. `EDIE_DATA_DIR` still takes priority. Point it to a copy for an isolated trial.
   This release adds database columns, indexes and triggers. Use the untouched
   old data copy if you roll back.
4. Double-click `START_EDIE.bat`. Python 3.11+ with Tcl/Tk and Ollama are required.
   Your existing installed local chat model remains selected.
5. Open **EDIE → Voice and reliability**, or press **Ctrl+Shift+R**. The EDIE menu
   also provides Home, Conversation, Tasks, Memory, Voice, Settings and the
   existing command palette.

The launcher selects `EDIE_PYTHON`, then `.venv\Scripts\python.exe`, then `py -3`,
then `python`. Set `EDIE_PYTHON` to a full executable path for a custom environment.
The model installer uses the same selection. The existing private Python 3.13
speech runtime remains separate.

`EDIE.py` is the stable entry point. The compatibility implementation is
`EDIE_31_47_1_IMPROVED.py`; new services live in `edie/`. Keep these files,
`assets/`, and the worker scripts together. This is no longer a single-file app.
The old-version filename is retained as a small compatibility launcher.

## Changes

- Fixed malformed performance settings blocking startup, concurrent settings
  saves colliding, successful jobs containing failed health checks, cancellation
  state after profile changes, and voice polling replaying an earlier answer.
- Added serialised atomic JSON writes and locked read/modify/write operations.
- Added continuous audio capture during Whisper transcription, bounded buffers,
  dropped-audio reporting, pre-roll and configurable utterance boundaries.
- Added language/device preferences, CPU/CUDA choice with CPU fallback,
  interruptible SAPI output, generation-aware speech and complete sentence chunks.
- Wake listening pauses while a Whisper microphone session owns the device.
  Fresh defaults disable wake listening; existing explicit choices are retained.
  Safe mode blocks wake capture too.
- Added **Pause microphones and observation** and **Allow capture controls again**.
  Resuming controls does not automatically start a session.
- Added UI-thread dispatch, bounded chat rendering, response timing samples,
  private error logs and recovery of unsent draft text.
- Added FTS5 keyword search where available, embedding identity/dimension
  metadata, overlapping chunks with character offsets, and incremental indexing.
- Added full-data backups with online SQLite snapshots, checksums, reported
  omissions, verification and recovery into a new staging folder.
- Moved the large brain image to `assets/brain.png`, reducing the main source
  from about 5.6 MB to about 2.9 MB.

## Prepare voice

For English wake recognition, double-click `INSTALL_EDIE_VOICE_MODEL.bat`. It
explicitly installs pinned Vosk/sounddevice packages into the main Python and
downloads the official approximately 40 MiB English model. Its SHA-256 is checked
before bounded extraction and installation. `EDIE_DATA_DIR` is honoured.

For Whisper microphone/system-audio sessions:

1. Enable application installation in EDIE's existing Permissions controls.
2. In **Voice and reliability → Voice**, choose and download a Whisper model.
3. Use a multilingual model (`tiny`, `base`, `small`) for other languages;
   models ending in `.en` support English only.
4. Use **Prepare local speech output** when SAPI is needed.
5. Open the existing Voice controls and explicitly start the microphone session.

Whisper now uses cached models only. A missing model produces a setup message
instead of a silent network download during listening. Worker processes stop
when their parent exits or their control pipe closes. OS microphone permissions
still apply. Rate, volume and SAPI voice ID preferences apply to the SAPI backend.
The optional Piper backend keeps its existing provider configuration and still
needs Windows/device verification.

## Data, privacy and backups

Raw microphone and loopback audio remain in bounded memory buffers. Recognised
text becomes normal chat/history or existing awareness summaries. Unsent draft
text is saved locally to `unsent_drafts.json` and is never automatically sent.
It may contain private information; account for it during deletion or backups.
Draft attachments are not automatically reopened.

New error logs contain fixed action labels and exception class names rather
than conversation text. `edie_errors.log` and the existing responsiveness log
rotate. The new Health check contacts only local Ollama and never activates
capture. The supplied dependencies are optional; chat can start without them.

Full backups contain **all profiles** and private personal data. They are ZIP
files, so store them privately. Models, runtimes and OS credentials are excluded.
Credential-like JSON filenames are excluded and reported. Any skipped file makes
the new backup status `partial`.

Use **Voice and reliability → Backups** for the new full-backup format. Inherited
panels retain their older profile/security formats. **Rehearse recovery** restores
verified files into a fresh staging folder and never overwrites live data.
Checksums verify integrity, not the identity of a backup author.

Unknown legacy embeddings are excluded from semantic ranking until rebuilt.
Use the existing embedding tools after selecting a model. Keyword search still
works. FTS5 is optional; fallback and semantic candidate scans are bounded to
5,000 rows. A dedicated vector index and model-digest tracking remain future work.

## Checks and recovery

Double-click `CHECK_EDIE.bat`, or use:

```bat
START_EDIE.bat --self-test
START_EDIE.bat --upgrade-test
START_EDIE.bat --verify-package
START_EDIE.bat --data-dir
START_EDIE.bat --safe-mode
```

The stable launcher's `--self-test` runs the inherited suite and new regressions
using temporary test data. `--upgrade-test` runs only new regressions. Neither
uses a real microphone or a live AI model. The supplied GitHub Actions workflow
covers Windows/Linux and Python 3.11/3.13; it has not been published or run on
GitHub during this session.

`VALIDATION.md` records checks actually performed. Windows scripts, SAPI,
headphones/speakers, device permissions, hotplug and laptop behaviour still
require target-device testing. This package is portable source, not a signed
Windows installer.

To roll back, close this release and launch the old one with its untouched old
data folder. New work remains in the upgrade's copied data folder.
