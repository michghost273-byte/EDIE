# EDIE

## Download EDIE 31.47.1

**[Download the EDIE 31.47.1 upgrade ZIP](https://github.com/michghost273-byte/EDIE/raw/refs/heads/main/downloads/EDIE_31_47_1_UPGRADE.zip)**

Version 31.47.1 fixes the Windows `WinError 32` self-test cleanup failure by explicitly closing SQLite connections. Extract this patch into a new folder; keep the previous data copy for rollback.

1. Extract the **whole ZIP** into a new folder.
2. Copy your existing `edie_data` folder into the new folder before the first launch. If you use `EDIE_DATA_DIR`, point it to a copy for an isolated trial.
3. Run `START_EDIE.bat`.

Requires Python 3.11+ with Tcl/Tk and your local Ollama installation.

This upgrade fixes the five reproduced bugs and adds continuous voice capture, safer settings, improved backups, document indexing, and Voice and Reliability controls. The inherited suite and 37 regression tests passed locally. Live Windows audio still needs device testing.

The full 100-item roadmap contains **23 complete, 36 partial and 41 planned** items.

- [Setup, voice preparation and rollback](docs/31.47.1/README.md)
- [Full improvement status](docs/31.47.1/IMPROVEMENTS.md)
- [Validation and remaining Windows checks](docs/31.47.1/VALIDATION.md)
- [ZIP SHA-256 checksum](downloads/EDIE_31_47_1_UPGRADE.zip.sha256)

- [SQLite cleanup fix details](docs/31.47.1/CHANGELOG.md)
- [Native Windows Python 3.15 and Linux package checks](https://github.com/michghost273-byte/EDIE/actions/workflows/verify-download.yml)
