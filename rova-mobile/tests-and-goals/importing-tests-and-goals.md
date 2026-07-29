# Importing Tests & Goals

Bringing existing test suites into Rova Mobile is fast and flexible. You can upload spreadsheet files (`.csv`, `.xlsx`, `.xls`) containing your structured test cases and map their contents directly to Rova Mobile test goals without reformatting your original spreadsheets.

### Key Import Features

* **Target Mobile App Selection**: Specify which mobile app package (Android APK/AAB or iOS IPA/App build) your imported test cases belong to.
* **Goal Concatenation**: Select multiple columns to merge into one comprehensive goal description so the AI agent receives full context for execution.
* **Automatic Row Validation**: Rova automatically checks every row for required fields, separating valid test rows from incomplete ones so you only import runnable tests.

### Step-by-Step Mobile Import Process

To initiate an import, open your Test Library in Rova Mobile and choose Import Tests.

#### Step 1: Target Mobile App & File Upload

1. **Target Mobile App**: Select the target mobile app build (e.g., `Jiji.ng (android)`) from the dropdown menu to link your imported tests directly to that app package.
2. **Upload Excel / CSV File**: Drag and drop your spreadsheet into the upload zone or tap to select a file from your computer.
   * Supported Formats: `.csv`, `.xlsx`, or `.xls` files.

#### Step 2: Preamble & Header Configuration

If your file contains title blocks or notes above your actual data table:

* **Header Row Index**: Select or enter the specific row number where your table column headers are located (e.g., `Row 1: Test ID, Test name, Starting url...`). Any rows prior to this index will be ignored as preamble.

#### Step 3: Field Column Mapping

Map your file's header columns to Rova Mobile fields:

1. **Goal Text Columns (Required)**: Check the box next to each column header you want to combine into the main test goal (e.g., `Precondition`, `Expected result`, `Scenarios`). Selected fields are concatenated into a structured prompt for the mobile test agent.
2. **Priority**: Select a column to define test priority or leave as None (Default to Medium).
3. **Tags**: Optionally map a column containing tags or categories to organize your tests inside Rova Mobile.

#### Step 4: Import Preview & Finalize

Before saving, review your parsed tests in the Import Preview table:

* **Row Status Summary**: At a glance, view the total number of detected rows along with badges indicating Valid rows and Invalid (Will Be Skipped) rows (e.g., rows with empty goal descriptions).
* **Row Breakdown**: Review each row’s generated Goal Description, assigned Priority, Tags, and individual Validation status (`Valid` or `Error`).
* **Finalize Import**: Click **Import Valid Goals** to complete the process and add all valid test cases directly to your Rova Mobile library.

### Best Practices

* **App Context Alignment**: Ensure you select the correct target mobile app package before uploading so tests execute on the correct device build.
* **Combine Steps & Context**: Include columns covering initial app state as well as expected outcomes when mapping Goal Text Columns.
* **Review Invalid Rows**: If rows show up with an `Error` status (e.g., `(Empty Goal)`), verify that your header row index is accurate or check your source file for missing data.
