# AI Test Generation

Writing tests shouldn't be a chore. With Rova's `generate` command, you can automatically scaffold entire test suites based on your current code changes or a natural language description.

## How it Works

The `rova generate` command uses Rova's AI engine to analyze your application's state or code diffs and create a structured YAML test file (`tests.rova.yml`).

## Generation Strategies

### 1. From Git Diffs (Recommended)
This is the most powerful way to use Rova. The AI analyzes your uncommitted changes (or a target branch) and suggests relevant tests that cover the new or modified logic.

```bash
# Analyze current changes
rova generate

# Analyze changes against origin/main
rova generate --diff-target origin/main
```

### 2. From a Prompt
If you have a specific test scenario in mind, you can describe it in plain English.

```bash
rova generate "Create a suite for the new user registration flow, including edge cases for invalid emails"
```

## Command Options

| Flag | Description | Default |
| :--- | :--- | :--- |
| `[prompt]` | Optional natural language instructions. | |
| `-f, --file` | Path to the YAML file to append/create. | `tests.rova.yml` |
| `--diff-target` | Git branch or commit to diff against. | `origin/main` |
| `-p, --product` | Target product: `web` or `mobile`. | (auto-detected) |

## Best Practices

### 1. Run Frequently
Run `rova generate` before every commit to ensure you have coverage for your changes. It's much faster than writing YAML from scratch.

### 2. Review and Refine
The AI provides a great starting point, but you should always review the generated `tests.rova.yml` file to:
- Adjust `goal` descriptions for clarity.
- Add specific `context` (e.g., login credentials).
- Refine `assertions` to match your exact business requirements.

### 3. Use with Turbo Mode
When generating tests, Rova will often suggest using `turbo: true`. This allows the agent to execute multiple actions in a single step, significantly speeding up your local and CI runs.

## Auto-Detection
The CLI attempts to auto-detect whether your project is `web` or `mobile` by inspecting your `package.json` for dependencies like `react-native` or `expo`. If detection fails, use the `--product` flag.
