# Project Contexts

Project Context is a powerful way to inject domain-specific knowledge into Rova's AI brain. It allows the agent to understand your application's unique terminology, patterns, and logic.

## Why use Project Context?

Standard automation tools are "blind" to the meaning of your UI. Rova's AI understands the UI, but it doesn't always know your specific business rules. Project Context bridges this gap.

### Common Context Examples

#### 1. Terminology

"In this application, 'Organization' and 'Workspace' are used interchangeably." _Benefit_: If a test says "Go to Workspace settings" but the button says "Manage Organization," the agent will know they are the same thing.

#### 2. Complex Components

"The 'Date Range Picker' requires you to select the start date first, then the end date. Clicking 'Apply' is mandatory." _Benefit_: The agent won't get stuck trying to click outside the picker to close it.

#### 3. Navigation Logic

"The 'Logout' button is hidden inside the user avatar menu in the top-right corner." _Benefit_: The agent knows it needs to click the avatar first without being explicitly told in every test.

## How to Manage Context

1. Navigate to your **Project > Settings > Test Context**.
2. Add context entries in plain English.

## Recommendations for Effective Context

* **Manage Credentials:** Put credentials in project text instead of having to specify them in each test.
* **Keep it Concise**: The AI is efficient; you don't need to write a manual. Short, declarative sentences work best.
* **Update Frequently**: As your UI evolves, update your context to prevent the agent from using outdated logic.
* **Use for "Known Quirks"**: If there's a bug you haven't fixed yet or a "slow" part of your app, mention it in the context so the agent knows what to expect.

### Example Context Entry

```
The sidebar is collapsible. If you can't see the 'Billing' link, first click the 'Menu' (hamburger) icon in the header to expand the sidebar.
```

> \[!IMPORTANT] Context data can be marked as **Sensitive**. Use this for any internal-only URLs or documentation that should be handled with higher privacy protocols.
