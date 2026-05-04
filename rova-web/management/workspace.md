# Workspace Management

Workspaces are the highest level of organization in Rova. They allow you to manage your team, billing, and global settings in one place.

## Managing Your Workspace

### Creating and Naming
When you first sign up, you will set up a workspace as part of your onboarding process. You can rename it in **Settings > General**.
> [!TIP]
> **Best Practice**: Use your company or department name for the workspace to make it easily identifiable for invited members.

### Switching Workspaces
If you belong to multiple workspaces, you can switch between them using the dropdown menu in the top-left corner of the Rova dashboard.

## Membership & Roles

Collaboration is key to a robust testing strategy. Rova provides granular role-based access control (RBAC).

### Available Roles
| Role       | Permissions                                                            |
| :--------- | :--------------------------------------------------------------------- |
| **Owner**  | Full access to all settings, billing, and member management.           |
| **Admin**  | Can manage projects, members, and API keys, but cannot access billing. |
| **Editor** | Can create, edit, and run tests and suites.                            |
| **Viewer** | Read-only access to tests, results, and reports.                       |

### Inviting Team Members
1. Navigate to **Settings > Members**.
2. Click **Invite Member**.
3. Enter their email address and select a role.
4. They will receive an invitation link to join your workspace.


## Usage & Billing

Rova operates on a credit-based system. Each test run consumes a certain number of credits based on the complexity and duration of the execution.
- Monitor your credit balance in **Settings > Billing**.
- Set up **Auto-Reload** to ensure your CI pipelines never fail due to insufficient credits.
