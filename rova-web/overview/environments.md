# Environments

Applications often run across multiple stages, such as Local, Staging, UAT, and Production. Rova AI allows you to define dedicated Target Execution Environments for your project so you can run the exact same test goals against different deployment URLs and context configurations without duplicating your tests.

### Overview & Key Benefits

* **URL Overrides**: Automatically route test executions to different base URLs (e.g., swapping `[https://app.yourdomain.com](https://app.yourdomain.com)` for `[https://staging.yourdomain.com](https://staging.yourdomain.com)`) without modifying your underlying test steps.
* **Environment-Specific Context**: Inject custom rules, credentials, or flags that only apply to a specific deployment stage (e.g., staging-specific test accounts or bypass flags).
* **Seamless Switching**: Choose your target environment on-the-fly when creating or running test goals.

### Managing Project Environments

You can configure and maintain all execution environments directly within your project's settings.

#### Adding a New Environment

1. Click on Projects in the main navigation menu to view your list of active projects.
2. Select the specific project you want to configure from the list.
3. Locate the Environments section and click + Add Environment.
4. Enter a clear Environment Name (e.g., `Staging`, `UAT`, or `Dev`).
5. Provide the corresponding Base URL (e.g., `[https://saucedemostaging.com](https://saucedemostaging.com)`).
6. Click Save to add it to your project.

### Selecting an Environment in Test Goals

When creating a new test goal or editing an existing one, you can specify which environment the Rova AI agent should execute against:

1. Open the goal editor or creation form.
2. Scroll down to the bottom configuration options and toggle on **Advanced Configuration**.
3. Locate the **Target Execution Environment** dropdown.
4. Select your target environment from the list (e.g., `Staging`).

```
Default Behavior:
If left set to "Default (Project URL & Context)", Rova runs against your primary Project Base URL and global Project Context.
```

### How Environment Overrides Work

When an execution plan or test goal runs under a selected environment:

1. **Base URL Replacement**: Rova automatically replaces the starting/base test URL with the designated environment's base URL.
2. **Context Injection**: Rova combines your global Project Context with any environment-specific context entries, ensuring the AI agent acts with complete situational awareness for that target environment.

### Best Practices

* **Use Consistent Base Paths**: Ensure your target environments mirror the URL path structure of your production app so deep links and relative paths resolve seamlessly.
* **Isolate Test Credentials**: If your staging environment uses separate test accounts or API tokens compared to production, define them within environment-specific notes rather than global project settings.
* **Tag Staging Quirks**: If an environment has known latency, mock data, or feature flags enabled, mention it in the context notes so the AI agent adjusts its expectations during test runs.
