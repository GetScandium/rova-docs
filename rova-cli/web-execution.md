# Local Web Execution

One of the most powerful features of the Rova CLI is the ability to run AI-driven tests on your local machine. This is ideal for development, debugging, and rapid iteration.

## Running a Test locally

When you run a web test locally, Rova uses a local browser (Chromium) but connects to our **AI Brain** to handle the logic and element interaction.

### Commands

```bash
rova run web --file ./tests/my-test.yaml
```

### Key Options

| Flag              | Description                                                                |
| ----------------- | -------------------------------------------------------------------------- |
| `--headed`        | Open the browser window so you can watch the agent work.                   |
| `--interactive`   | **Interactive Mode**: AI will pause and ask you for help if it gets stuck. |
| `--step-by-step`  | **Debug Mode**: Pauses after every action and applies a slow-motion delay. |
| `--max-steps <n>` | Limit the number of actions the AI can take (default: 50).                 |
| `--turbo`         | **Turbo Mode**: AI returns action sequences for 2-3x faster execution.     |

> \[!TIP] **Best Practice**: Use `--headed` and `--step-by-step` during development to see exactly where a test fails and inspect the page state manually.
>
> See [#common-flags](commands.md#common-flags "mention") for all options

## Why Run Locally?

1. **Zero Cost**: Local runs do not consume cloud execution minutes (though they may consume small amounts of AI reasoning credits depending on your plan).
2. **Instant Feedback**: No need to wait for a cloud environment to spin up.
3. **Internal Testing**: Test applications running on `localhost` or behind a VPN that aren't accessible to the Rova cloud.

## Debugging Local Runs

If a local run fails:

* **Check the Logs**: The CLI outputs the agent's step-by-step reasoning.
* **Review Artifacts**: Rova saves screenshots of the failure in the `./rova_results` directory.
* **Run with Debug**: Use the `--debug` flag to see the raw HTTP communication between the CLI and the AI engine.

> \[!IMPORTANT] Ensure your local machine has a stable internet connection. While the browser is local, the "intelligence" that drives the agent resides in the Rova cloud.
