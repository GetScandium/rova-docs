# Use Cases

Rova Mobile's AI-first approach enables a wide range of use cases that are difficult or impossible with traditional mobile automation tools.

### Key Capabilities

#### 1. AI-Driven Interaction

Rova Mobile doesn't rely on brittle accessibility IDs or complex XPath locators. Our agents "see" the mobile UI just like a human user, understanding native visual layouts, system icons, and text intent.

#### 2. Self-Healing Tests

If your app's UI changes (e.g., a button moves during a redesign, or its text changes from "Login" to "Sign In"), Rova automatically adapts in real-time on the device, preventing false test failures and saving hours of maintenance.

#### 3. Cross-Platform Support

Execute the exact same natural language test across different mobile operating systems:

* Android (Virtual and real devices)
* iOS (Virtual and real devices)

#### 4. Shared Context Session

Maintain device session state across multiple goals within an Execution Plan. This allows you to model complex, multi-stage mobile user journeys without resetting the app state between steps.

### Common Use Cases

#### 1. End-to-End Regression

Automate your most critical mobile user journeys (e.g., App Launch -> Onboarding -> Product Search -> Add to Cart -> In-App Checkout).

* Benefit: Zero test maintenance as your mobile app layout and features evolve.

#### 2. Testing Third-Party Mobile SDKs

Automate interactions with native components and external overlays that traditional tools struggle to capture, such as:

* Stripe or Apple/Google Pay mobile sheets
* Auth0, Okta, or Firebase web-view authentication screens
* Customer support chat sheets and permission dialogs (e.g., Location, Notifications)

#### 3. Device & UI Audits

Ensure your application looks and behaves correctly across different screen resolutions, aspect ratios, and OS versions. Rova Mobile can detect visual regressions, overlapping elements, and functional breaks simultaneously.

#### 4. Dynamic Data Handling

Tests that require randomized input (e.g., "Register a new user with a random email") are handled natively by the AI, which can generate, input, and remember dynamic values throughout the execution.

### Recommendations

* Start with the "Happy Path": Focus your initial Rova Mobile tests on the most common user flows where app stability is absolute key.
* Describe Intent, Not Gestures: Instead of saying "Swipe up and tap the blue element," just say "Tap on the 'Submit' button." Let the AI handle the scrolling and coordination.
* Leverage Execution Plans: Use plans to break exceptionally long mobile tests into smaller, manageable goals that share a single continuous device session.
