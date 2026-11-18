# EDIE 31.47.5

## Stronger local model

- The Local AI Model Lab offers **Install & Select Qwen3.5 9B**. Ollama
  downloads about 6.6 GB on Windows and runs the model on the device.
- EDIE tests the 9B model locally at a 4,096-token context before selecting it.
  Choose an installed model from the list and use **Use Selected Model** to
  switch between models.
- The model lab applies the chosen model to chat and tasks. Full Live Awareness
  uses its configured vision route.

## Dependency alerts in 31.47.4

- Predictive Insight checks whether PyAutoGUI and PyGetWindow can load before
  showing EDIE's past installation errors. It groups duplicate reports for each
  package that still needs attention.
- Press **Ctrl+K** and open **System Dependencies** to see the current package status.

## Vision and diagnostics in 31.47.3

- **Model & Embedding Lab** lets you save an installed vision model. Full Live
  Awareness uses a compatible saved choice such as `llava:latest` and falls
  back to a compact instruct model when needed.
- **Predictive Insight** shows the latest matching error and counts failures
  in the past 24 hours.
- The Windows installer includes PyAutoGUI and PyGetWindow with their
  dependencies.

## Local AI model installation in 31.47.2

The **Install & Select Qwen3.5 4B** button reports download progress and selects
the model after Ollama lists it as installed. A failed pull keeps the current
selection and the displayed model list.

Settings shows **EDIE 31.47.2** in the window title so you can identify the
updated copy. Windows Setup asks you to exit an earlier EDIE session before
opening the updated app.

## Windows SQLite cleanup fix in 31.47.1

Fixes the `PermissionError: [WinError 32]` reported while `CHECK_EDIE.bat`
removed an `edie11-test-.../test.sqlite3` temporary database on Windows Python
3.15. SQLite connection contexts commit or roll back transactions; they do not
close the connection. Initialization was therefore leaving a database handle
open until garbage collection.

- Initialization now uses the store's transaction context, which explicitly
  closes its connection on both success and failure.
- A second leaking connection in the inherited capability self-test helper is
  explicitly closed too.
- Connection setup closes its handle if a PRAGMA fails.
- Legacy backup snapshots close the source even if opening the destination fails.
- Six new regressions retain strong references to every connection and verify
  that it has been closed. The rollback test also verifies no partial write is
  committed. Cleanup errors are not ignored or suppressed.

The temporary self-test database in the traceback is separate from the live
`edie_data` database. Extract this release into a new folder and copy existing
data there only when you want to carry it forward; keep the earlier folder as
your rollback copy.

Run `CHECK_EDIE.bat` for checks, then `START_EDIE.bat` to open the application.
The inherited suite and 37 regression tests pass locally. Native Windows
verification for the package is recorded by the repository's **Verify download**
GitHub Actions workflow. Live Windows voice/device testing remains separate.
