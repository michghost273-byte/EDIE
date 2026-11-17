# EDIE 31.47.1 — Windows SQLite cleanup fix

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
