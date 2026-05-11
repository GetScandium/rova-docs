# Command Reference

The `rova` CLI is the primary way to run autonomous tests locally and integrate Rova into your CI/CD pipeline.

## `rova init`

Initializes a new Rova project in your current directory. It creates a `rova.config.js` file where you can define your project settings and lifecycle hooks.

```bash
rova init
```

## `rova auth`

Manages your Rova credentials. You can log in to either the Web or Mobile product.

* **`rova auth login`**: Authenticate with an API Key.
* **`rova auth whoami`**: Show the currently authenticated workspace.
* **`rova auth logout`**: Clear local credentials.

```bash
# Authenticate for web testing
rova auth login --product web
```

## `rova run`

The core command for executing tests. You provide a product (`web` or `mobile`) and a goal or a file.

### Examples:

*   **Run a Web Test locally**:

    ```bash
    rova run web --url https://example.com --goal "Login and check dashboard" --headed
    ```
*   **Run on the Rova Cloud**:

    ```bash
    rova run web --remote --file ./tests/regression.rova.yml --project-id "PROJ-123"
    ```
*   **Run a Mobile Test locally**:

    ```bash
    rova run mobile --app-id ./apps/my-app.apk --goal "Login"
    ```

### Common Flags:

| Flag             | Description                                                                |
| ---------------- | -------------------------------------------------------------------------- |
| `-g, --goal`     | **Required.** The natural language goal for the AI.                        |
| `-u, --url`      | Target URL (required for web).                                             |
| `--turbo`        | **Turbo Mode**: AI returns action sequences for 2-3x faster execution.     |
| `--interactive`  | **Interactive Mode**: AI will pause and ask you for help if it gets stuck. |
| `--step-by-step` | **Debug Mode**: Pauses after every single action for inspection.           |
| `--headed`       | Run the browser with a visible window (default is headless).               |
| `--max-steps`    | Limit the number of actions the AI can take (default: 50).                 |
| `--json`         | Output the final result as a JSON string (ideal for CI/CD).                |
| `--output`       | File path to save the final execution result (e.g., test-results.json).    |
| `--sync`         | Upload the results, screenshots, and logs to the Rova Dashboard.           |
| `--project-id`   | Associate the execution with a specific Rova Project ID.                   |
| `--suite-name`   | Provide a custom suite name for dashboard reporting.                       |
| `-c, --context`  | **Context Injection**: Pass persistent info (e.g. login credentials).      |
| `--suite-mode`   | **Execution Mode**: `sequential`, `parallel`, or `continuity`.             |
| `--debug`        | Print raw HTTP traffic between CLI and Brain API.                          |
| `-f, --file`     | Path to a **YAML** test definition file (`.rova.yml`)                      |

## `rova generate`

Auto-generate YAML test suites using AI based on your code changes or a prompt.

```bash
# Generate tests based on uncommitted git changes
rova generate

# Generate tests from a specific prompt
rova generate "Test the checkout flow with multiple items"
```

## Flags:

| Flag              | Description |
| ----------------- | ----------- |
| -f --file \<path> |             |
|                   |             |
|                   |             |



***

> \[!TIP] **Pro-Tip**: Use the `--debug` flag on any command to see the raw HTTP traffic between the CLI and the Rova Brain API.
