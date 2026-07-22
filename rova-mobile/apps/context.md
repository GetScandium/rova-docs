# App Context

App Context is a powerful way to inject domain-specific knowledge directly into Rova’s AI brain. It allows the agent to truly understand your mobile application's unique terminology, layout patterns, and runtime logic.

### Why use App Context?

Standard automation tools are completely blind to the meaning of your mobile UI components. While Rova's AI can visually understand layout structures, it doesn’t automatically know your specific business rules or staging configurations. Providing App Context bridges this gap so the AI can navigate your app smarter and execute tests much faster.

### Types of Context You Can Add

Based on what Rova needs to know before executing your tests, you can configure three types of context:

#### 1. Login Credentials

Save time by storing test account details so you don't have to write explicit login instructions for every single test case.

* What to enter: The default `Email / Username` and `Password` for your mobile test environment.
* Example: Providing a pre-registered QA user profile so Rova can bypass onboarding screens and handle authentication seamlessly.

#### 2. Environment Note

Provide critical insights regarding your server environments, mock flags, or backend testing rules.

* What to enter: Specific configurations like staging info, active feature flags, or custom test data behavior.
* Example: `"The OTP code is always 123456 in staging."` (This prevents the AI from getting stuck on two-factor verification screens!).

#### 3. Additional Info

Use this for layout quirks, custom components, or complex device behaviors unique to your application.

* What to enter: Any other relevant hints written in plain English.
* Example: `"The Checkout button only appears after selecting a delivery address."` or `"The profile settings panel must be accessed by dragging open the left drawer navigation."`

### How to Manage App Context

1. Navigate to the **Apps listing page** in the Rova Mobile dashboard.
2. Click on the **specific app** you want to configure.
3. Switch over to the **Test Context** tab.
4. Select the card type you want to add (Login Credentials, Environment Note, or Additional Info), fill out the field, and click Add.

### Tips for Writing Effective Context

* Keep it Concise: The AI handles short, declarative sentences best. You don't need to write an exhaustive technical manual, just outline the basic rules.
* Update as UI Evolves: If you redesign your app’s navigation flow or change the staging server credentials, remember to update your context here to prevent test failures.
* Use for Known Bottlenecks: If a certain transition or screen takes longer to load due to native background processes, add a note so the agent knows exactly what to expect.
