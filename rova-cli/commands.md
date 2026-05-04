# Rova CLI Command Reference

The `rova` CLI is the primary way to run autonomous tests locally and integrate Rova into your CI/CD pipeline.

## `rova init`
Initializes a new Rova project in your current directory. It creates a `rova.config.js` file where you can define your project settings and lifecycle hooks.

```bash
rova init
```

## `rova auth`
Manages your Rova credentials. You can log in to either the Web or Mobile product.

- **`rova auth login`**: Authenticate with an API Key.
- **`rova auth whoami`**: Show the currently authenticated workspace.
- **`rova auth logout`**: Clear local credentials.

```bash
# Authenticate for web testing
rova auth login --product web
```

## `rova run`
The core command for executing tests. You provide a product (`web` or `mobile`) and a goal or a file.

### Examples:
- **Run a Web Test locally**:
  ```bash
  rova run web --url https://example.com --goal "Login and check dashboard" --headed
  ```
- **Run on the Rova Cloud**:
  ```bash
  rova run web --remote --file ./tests/regression.rova.yml --project-id "PROJ-123"
  ```
- **Run a Mobile Test locally**:
  ```bash
  rova run mobile --app-id ./apps/my-app.apk --goal "Login"
  ```

### Common Flags:
| Flag | Description |
| :--- | :--- |
| `--remote` | Offload execution to Rova's cloud infrastructure. |
| `--headed` | Run local browser tests in a visible window. |
| `--interactive` | Pause and ask for help if the AI gets stuck. |
| `--step-by-step` | Pause after every single action for debugging. |
| `--sync` | Upload results and recordings to the Rova dashboard. |
| `--project-id <id>` | Associate the run with a specific Rova project. |
| `--turbo` | Enable action sequences for faster execution. |

## `rova generate`
Auto-generate YAML test suites using AI based on your code changes or a prompt.

```bash
# Generate tests based on uncommitted git changes
rova generate

# Generate tests from a specific prompt
rova generate "Test the checkout flow with multiple items"
```

## `rova doctor`
Checks your local environment for necessary dependencies (like Playwright browsers for web or ADB for mobile).

```bash
rova doctor
```

---

> [!TIP]
> **Pro-Tip**: Use the `--debug` flag on any command to see the raw HTTP traffic between the CLI and the Rova Brain API.
