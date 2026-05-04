# Rova Web Core Concepts

Understanding the building blocks of the Rova Web platform will help you design more effective automation workflows.

## 1. Tests
A **Test** is the smallest unit of automation in Rova. Unlike traditional automation scripts that rely on brittle CSS selectors or XPaths, a Rova test is defined by its **Goal** and **Steps** described in natural language.

> [!TIP]
> **Best Practice**: Keep your tests focused on a single user journey (e.g., "User can reset password"). This makes debugging easier and reporting more granular.

## 2. Test Suites
A **Suite** is a collection of tests that are logically grouped together. Suites are typically used for:
- **Smoke Tests**: Verifying critical path functionality.
- **Regression**: Ensuring new changes don't break existing features.
- **Feature-specific testing**: Grouping all tests related to a specific module (e.g., "Checkout Flow").

## 3. Continuity Mode
Continuity Mode is a powerful feature unique to Rova. When enabled for a suite, the AI agent maintains the **Browser Session State** (cookies, local storage, session storage) across all tests in that suite.

- **Without Continuity**: Each test starts with a fresh, empty browser.
- **With Continuity**: Test B starts exactly where Test A finished.

> [!IMPORTANT]
> Use Continuity Mode for complex workflows where Test B depends on the outcome of Test A (e.g., "Create a Project" followed by "Edit the Project").

## 4. Workspaces & Projects
- **Workspaces**: Your top-level organizational unit. It contains your team members, billing, and API keys.
- **Projects**: Sub-divisions within a workspace (e.g., "Marketing Site", "Admin Dashboard"). Projects allow you to isolate test suites and configuration data.

## 5. Project Context
Project Context is a shared "knowledge base" for the AI agent. You can provide documentation, common UI patterns, or specific business logic that the agent should keep in mind while executing tests in that project.

### Best Practices for Context
- **Include common selectors**: If your app has a very complex custom component, mention it in the context.
- **Define terminology**: If "Account" and "Profile" mean different things in your app, clarify it here.
- **Use Sensitivity Settings**: Mark context data as sensitive if it contains internal URLs or non-public terminology to ensure it is handled with extra privacy.

## 6. Agents
An **Agent** is the AI engine that "reads" your application UI. It doesn't just look at the code; it perceives the visual layout, accessibility labels, and interactive elements to make decisions in real-time.
