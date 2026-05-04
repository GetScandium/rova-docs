# Use Cases & Capabilities

Rova's AI-first approach enables a wide range of use cases that are difficult or impossible with traditional automation tools.

## Key Capabilities

### 1. AI-Driven Interaction
Rova doesn't rely on brittle CSS selectors. Our agents "see" the UI like a human, understanding visual layout, icons, and text intent.

### 2. Self-Healing Tests
If your UI changes (e.g., a button moves or its text changes from "Login" to "Sign In"), Rova automatically adjusts in real-time, preventing test failures.

### 3. Cross-Browser Support
Execute the exact same natural language test on:
- **Chromium** (Chrome, Edge)
- **Firefox**
- **WebKit** (Safari)

### 4. Continuity Mode
Maintain session state across multiple tests in a suite to model complex, multi-stage user journeys.

---

## Common Use Cases

### 1. End-to-End Regression
Automate your most critical user journeys (e.g., Landing Page -> Search -> Add to Cart -> Checkout).
- **Benefit**: Zero maintenance as your UI evolves.

### 2. Testing Third-Party Integrations
Automate interactions with components that traditional tools struggle with, like:
- Stripe Payment Elements
- Auth0/Okta Login Screens
- Intercom/Zendesk Chat Widgets

### 3. Visual & Functional Audits
Ensure your app looks and behaves correctly across different resolutions and browser engines. Rova can detect visual regressions and functional breaks simultaneously.

### 4. Dynamic Data Handling
Tests that involve random data (e.g., "Create a new user with a random email") are handled natively by the AI, which can generate and remember dynamic values.

## Recommendations

- **Start with the "Happy Path"**: Focus your first Rova tests on the most common user flows where stability is key.
- **Describe Intent, Not Actions**: Instead of "Click on the blue div," say "Click on the 'Add to Cart' button."
- **Leverage Continuity**: Use suites to break long tests into smaller, manageable chunks that share a single session.

> [!TIP]
> **Pro Tip**: Use the `rova generate` CLI command to quickly scaffold new tests by describing the goal in one sentence.
