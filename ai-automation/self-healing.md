# Self-Healing Tests

Traditional automation is notorious for "flakiness." A small change in a CSS class or a slightly different UI layout can break hundreds of tests. Rova solves this with **AI-Powered Self-Healing**.

## How Self-Healing Works

Unlike standard tools that fail the moment a selector isn't found, Rova's agent follows a multi-step recovery process:

1. **Selector Failure**: The primary selector (if provided) fails to find the element.
2. **Visual Re-Identification**: The agent analyzes the screen's visual state and accessibility tree to find elements that *look* or *act* like the target.
3. **Intent Matching**: The agent compares available elements against the **Test Goal** and **Step Description**.
4. **Autonomous Correction**: The agent decides which element is the correct one and continues the test.
5. **Auto-Update (Coming Soon)**: Rova can suggest updates to your test scripts based on these successful recoveries.

## Real-World Examples

### Example 1: Button Renaming
- **Old Button**: "Submit Order"
- **New Button**: "Place Order"
- **Traditional Result**: ❌ Test Fails (Button not found).
- **Rova Result**: ✅ Test Passes. The agent understands that "Place Order" fulfills the intent of submitting the order in the checkout context.

### Example 2: DOM Restructuring
- **Old Path**: `div > span > button`
- **New Path**: `main > section > div > button`
- **Traditional Result**: ❌ Test Fails (Broken XPath/CSS).
- **Rova Result**: ✅ Test Passes. The agent sees the button is still in the same visual area and has the same label.

## Best Practices for Self-Healing

### 1. Write Intent-Based Descriptions
The better your description, the easier it is for Rova to heal.
- **Bad**: "Click the blue button."
- **Good**: "Click the button to confirm the deletion of the project."

### 2. Provide Context
If your app has multiple buttons that look the same (e.g., several "Edit" buttons in a list), use context in your steps.
*Example*: "Click the 'Edit' button in the row for the user 'John Doe'."

### 3. Review Healing Events
In the Rova Web dashboard, you can see when a test has "healed." Review these events to see if your app's UI changes were intentional and if the agent made the right choice.

> [!TIP]
> **Recommendation**: Don't rely *entirely* on self-healing for critical paths. If an element's identity changes significantly, it's still good practice to update your test description for clarity.
