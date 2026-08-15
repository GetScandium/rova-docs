---
description: >-
  This guide explains how to configure and execute API calls (HTTP requests) as
  part of your Rova test flows.
---

# API Testing in Rova



This guide explains how to configure and execute API calls (HTTP requests) as part of your Rova test flows. You will learn how to set up pre-test environments, perform post-test cleanups, evaluate assertions, and pass data dynamically between API calls and browser steps.

### 1. API Lifecycles

In Rova, you can execute API requests in three different ways depending on your testing needs:

| Phase                  | When It Runs                                              | Common Use Case                                                               | If It Fails                                                          |
| ---------------------- | --------------------------------------------------------- | ----------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Pre-Setup Steps**    | Automatically before the browser starts navigation.       | Authentication, seeding database entries, generating test accounts.           | Test is aborted immediately to avoid running against a broken state. |
| **In-Test Steps**      | Dynamically triggered by the AI planner during execution. | Programmatic backend verification, checking logs/records directly.            | Execution stops and the test run is marked as failed.                |
| **Post-Cleanup Steps** | Automatically after the browser test concludes.           | Deleting created data, tearing down workspaces, resetting account parameters. | Execution continues; all remaining cleanups still execute.           |

### 2. Configuring API Steps (Advanced Settings)

To add API steps, open the **Advanced Settings** panel on your test detail screen. You can toggle between **Form View** (visual editor) and **JSON View** (raw configuration).

#### URL & Method

* **Method:** Choose `GET`, `POST`, `PUT`, `DELETE`, or `PATCH`.
* **Endpoint URL / Path:** Enter an absolute URL (e.g. `https://api.example.com/v1/login`) or a relative path (e.g. `/api/profile`). Relative paths will automatically resolve against the base URL configured for your test.

#### Execution Mode

* **Context-Aware Mode (Default):** Runs sharing the active browser's cookies and sessions. This is ideal when your API calls need to inherit the logged-in state of the web application.
* **Server-Side Mode:** Runs as a standalone query from Rova's backend. Use this for general background setups or integrations that bypass the active browser state.

#### Request Body & Parameters

* **Query Params:** Key-value parameters automatically appended to the URL (e.g. `?limit=10`).
* **Headers:** Custom headers such as `Authorization: Bearer <token>`.
* **Body Type:**
  * `json`: Standard JSON payload.
  * `urlencoded`: Form-urlencoded payload (typically used for basic authentication logins).
  * `form-data`: Multipart uploads (useful for file testing).
  * `raw`: Plain text or customized raw payloads.

### 3. Dynamic Variables & Data Flow

Rova allows you to capture values from API responses and reuse them in subsequent API calls or browser actions.

#### Extracting Variables

To save a response value, define an extraction rule:

* **Variable Name:** A custom name you choose (e.g. `userToken`).
* **JSONPath:** The path to the value in the response JSON.
  * `$.token` (extracts the token root property)
  * `$.data.user.id` (extracts a nested user ID)

#### Referencing Variables

Insert saved variables anywhere in later steps using double curly braces: `{{variable_name}}`.

Rova will dynamically replace these placeholders in:

* **API URL paths:** `/api/users/{{userId}}`
* **Request headers:** `Authorization: Bearer {{userToken}}`
* **Request body payloads:** `{"workspaceId": "{{workspaceId}}"}`
* **Web Browser interactions:** The AI will automatically resolve placeholders when typing into form fields in the browser (e.g., typing `{{userEmail}}` into an email text input).

### 4. Assertions Engine

Verify that your API requests return correct payloads. If any assertion fails, the step is marked as failed.

1. **Status Code:** Verify the HTTP response code (e.g. Expected: `200` or `201`).
2. **JSONPath Match:** Evaluate a specific JSON property against an expected value.
   * Example: Target `$.data.active` expected value `true`.
3. **JS Script:** Run custom JavaScript checks.
   * Example: `response.body.items.length > 0` (verifies that an array is not empty).

***

### 5. Instant Test Sandbox ("Test Request")

Next to your API step inputs, click the **Test Request** button to verify your configuration immediately.

* Runs the request in real time using your active workspace credentials.
* Displays the response status code, round-trip duration, a scrollable **Response Body** preview, and checklist results for assertions.

### 6. End-to-End Workflow Example

Below is an example of seeding a database, using the seeded resource in a browser test, and cleaning it up afterward.

#### Step 1: Pre-Setup API Call (Create User)

* **Method:** `POST`
* **URL:** `/api/v1/register`
* **Body (JSON):** `{"email": "test-user@domain.com", "role": "editor"}`
* **Extraction:**
  * Variable Name: `newUserId`
  * JSONPath: `$.id`
* **Assertion:** Status Code: `201`

#### Step 2: Browser Test (UI Web Page Flow)

1. Navigate to `/login`.
2. Type `test-user@domain.com` into the email field.
3. Click "Log In".
4. Navigate to `/users/{{newUserId}}` to confirm the editor profile dashboard renders.

#### Step 3: Post-Cleanup API Call (Delete User)

* **Method:** `DELETE`
* **URL:** `/api/v1/users/{{newUserId}}`
* **Assertion:** Status Code: `204`

### 7. Known Limitations <a href="#user-content-7-known-limitations" id="user-content-7-known-limitations"></a>

While Rova's API testing tool is highly flexible, it has some technical constraints:

1. **No Support for Binary Response Payloads:** The response assertion engine is optimized for JSON, text, HTML, and XML payloads. Validating binary downloads (e.g. validating PDFs, ZIP archives, image assets, or Excel spreadsheets directly from an API call response body) is not supported.
2. **SSO & Redirect Authentication Restrictions:** The API testing engine cannot bypass interactive logins, CAPTCHAs, or MFA challenges (e.g., Single Sign-On via third parties like "Sign in with Google" or "Sign in with Microsoft Entra") that require redirection or browser-based identity validation.
3. **No Conditional or Branching Logic:** Pre-Setup and Post-Cleanup steps run sequentially from top to bottom. You cannot define branching rules (e.g., "Execute Step 2 only if Step 1 succeeds") or loop steps. If a Pre-Setup step fails, the test aborts.
4. **No Concurrent API Calls:** Pre-configured steps run in a synchronous block one after another. There is no support for parallel dispatching.
5. **Variable Type Coercion:** All values extracted via JSONPath are converted to strings when stored as variables. For instance, extracting the integer ID `102` will result in `"102"`. Keep this in mind when passing variables into payloads that require strict JSON integers or booleans.
6. **No Session Sharing in Server Mode:** Choosing "Execute Server-Side" initiates requests directly from the Rova backend server. This query will not share, inherit, or update cookies or sessions active in the browser test page.
