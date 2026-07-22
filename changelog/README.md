# Release Notes

Stay up to date with the latest features, improvements, and bug fixes in Rova.

## \[2026.06.01] - Accessibility (A11y) Audits (Beta)

Automated WCAG Scans & AI-Assisted Fixes<br>

**Feature Activation Hierarchy**

* Conditional Workspace & Project Enablers: Added a global toggle for Accessibility (A11y) Audits under the Beta Features tab in Workspace Settings. Activating this globally reveals a new project-level configuration toggle, Always-on Accessibility Audits, within your Project Settings. Turning the project toggle on subsequently unlocks the accessibility audit configuration options for your individual tests and test suites.

**Execution & Test Suites Configuration**

* Test Suite Controls: Added an Accessibility Audits toggle under the Advanced Configuration section when creating a new or editing an existing Test Suite, ensuring all underlying batch tests inherit the scan.
* Granular Test Controls: Added an Accessibility Audit toggle under individual test Advanced Configuration blocks (under Device & Viewport), allowing users to selectively enable audits on standalone test paths.

**Runs & Insights Dashboard**

* Dedicated A11y Check Tab: A new A11y Check tab is now available within the test run execution details console.
* Compliance Overview: Visual dashboard featuring high-level metrics, including an overall Compliance Grade, a total Health Score percentage, and a Total Issues counter.
* Interactive Severity Filtering: Instantly filter caught accessibility bugs by impact level: _Critical_, _Serious_, _Moderate_, or _Minor_.
* Code-Level Debugging: Elements violating WCAG standards display their strict DOM target selectors and specific rule violations for immediate front-end remediation.
* Downloadable Reports: A new Download Report action button allows teams to export localized compliance data directly from the run dashboard for stakeholders.

## \[2026.05.12] - Test Categorization

### Categories & Test Labelling

**Categories Management**

* New **Categories** page (`/categories`)&#x20;
* Create, edit, and delete categories with a name, optional description, and a 20-color preset picker
* Clicking the test count on a category navigates directly to the Test Library pre-filtered by that category

**Test Library**

* New **Categories** column in the test table — shows the first category pill; if more than one, displays `+N`
* New **Categories** multi-select filter dropdown alongside the existing Status and Timeframe filters; supports selecting multiple categories simultaneously
* **Quick Preview** modal now includes a Categories section showing all associated category pills

**Test Detail**

* Category pills are now displayed below the test status badge in view mode
* Edit form includes a searchable **category dropdown** — selected categories appear as removable color-coded pills; unselected categories are listed in a scrollable, filterable dropdown



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
