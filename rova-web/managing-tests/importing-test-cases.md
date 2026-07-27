# Importing Test Cases

If your team already has an established library of manual or legacy automated test cases, you don't have to rewrite them from scratch. Rova AI features a flexible import system that translates traditional spreadsheets into autonomous AI test goals.

### The Import Workflow

Transforming your spreadsheet into executable Rova goals takes just three simple steps:

#### Step 1: Upload Your Document

Navigate to your Test Library and click Import tests.

* **Supported Formats**: Upload any structured `.csv`, `.xlsx`, or `.xls` file containing your test suites.
* **No Rigid Templates Required**: Rova adapts to your existing format. You don't need to rename your columns or reorganize your data to fit a strict layout before uploading.

#### Step 2: Flexible Column Mapping

Once your file is uploaded, Rova extracts the column headers from your document so you can map them directly to Rova fields.

* **Goal Concatenation** (Required): Select one or more columns that describe what needs to be tested (e.g., _Scenarios_, _Preconditions_, _Steps_, or _Expected Result_). Rova automatically reformats and combines these columns into a single, cohesive AI Test Goal.
* **Test Title**: Map this to your spreadsheet's test name column, or choose to let Rova automatically generate descriptive names using AI.
* **Target URL**: Map this to a specific starting page URL column if your tests begin on different paths. If omitted, tests will automatically drop back to your Project Base URL.
* **Categories / Tags**: Optionally map columns to apply comma-separated organization tags to your newly imported tests.
* **Live Goal Preview**: As you check and uncheck boxes, use the live preview panel on the right side of the screen to see exactly how the AI agent will read the formatted goal.

#### Step 3: Review and Finalize

Click Continue to Preview to inspect your parsed data before it hits your workspace.

* **Smart Validation**: Rova checks each row for completeness. Rows with valid starting targets and clear goals are marked as Valid and automatically selected for import.
* **Deselecting Invalid Rows**: Rows missing crucial testing data are flagged as Invalid and automatically deselected to prevent broken tests from entering your library.
* **Save Status**: Choose whether you want to import your selected test cases immediately as Active flows or save them as Drafts for further refinement.

### Best Practices for Clean Imports

* **Clean Up Preamble Rows**: If your Excel sheet contains metadata or empty design rows at the very top before the actual table starts, use the Preamble rows to skip setting to ensure Rova reads your headers correctly.
* **Combine for Richer Context**: Don't hesitate to check multiple boxes for the Test Goal. The more contextual clues you feed the AI (like combining _Scenarios_ + _Preconditions_), the better the agent will understand your application's business rules during execution.
