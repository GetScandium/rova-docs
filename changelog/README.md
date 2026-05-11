# Release Notes

Stay up to date with the latest features, improvements, and bug fixes in Rova.

## \[2026.05.03] - Continuity Mode & Mobile Grid

### Added

* **Continuity Mode (Web)**: You can now enable "Continuity Mode" in Test Suites to maintain browser session state across multiple tests.
* **Coordinate Grid Overlay (Mobile)**: Improved interaction with complex mobile components and system dialogs using a visual grid mapping system.
* **ABI-Based Routing**: Cloud emulators now automatically route APKs to the most efficient architecture (x86\_64 vs ARM64).

### Changed

* **CLI Performance**: The `rova run` command is now 20% faster when executing local web tests.
* **Reporting UI**: The execution history page now features a more detailed step-by-step breakdown with synchronized video playback.

### Fixed

* Resolved an issue where some custom checkboxes were not being correctly identified by the AI agent.
* Fixed a bug in `rova auth` that caused intermittent login failures on macOS Sonoma.

***

## \[2026.04.15] - Initial Beta Release

### Added

* Core AI execution engine for Web and Mobile.
* Rova CLI with `init`, `auth`, `run`, and `generate` commands.
* Web Dashboard for test management and reporting.
* Support for local Android emulators and iOS simulators.
