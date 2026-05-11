# Authentication

Before you can run tests or generate scripts, you must authenticate the Rova CLI with your account. Rova uses **API Keys** to securely connect the CLI to your workspaces.

## Logging In

The `auth login` command handles the authentication process. You can use it interactively or by providing your API key directly.

### 1. Identify your Product

Rova has separate platforms for Web and Mobile. You need to authenticate with the product you intend to use.

* **Rova Web**: [https://app.rova.qa/settings/workspace/apikeys](https://app.rova.qa/settings/workspace/apikeys)
* **Rova Mobile**: [https://mobile.rova.qa/settings/api-keys](https://mobile.rova.qa/settings/api-keys)

### 2. Run the Login Command

**Interactive Mode:**

```bash
# Pick your product from a list
rova auth login
```

**Direct Mode (Recommended for CI):**

```bash
# Authenticate for Web
rova auth login --product web

# Authenticate for Mobile
rova auth login --product mobile
```

## Verifying Authentication

To check which workspace you are currently connected to, use the `whoami` command:

```bash
rova auth whoami
```

This will display the status for both Web and Mobile products, including the Workspace Name and the last time the credentials were verified.

## Logging Out

To remove stored credentials from your local machine:

```bash
# Log out from a specific product
rova auth logout --product web

# Log out from all products
rova auth logout --product all
```

## Credentials Location

Rova CLI stores your credentials securely in a JSON file on your local machine

> \[!WARNING] Never share your `credentials.json` file or commit it to a version control system.

## Using Environment Variables (CI/CD)

In non-interactive environments like GitHub Actions, you don't need to run `rova auth login`. Instead, set the `ROVA_API_KEY` environment variable. The CLI will automatically use this key for authentication.

```bash
export ROVA_API_KEY="rova_your_key_here"
rova run web --remote --goal "Verify login" --project-id "PROJ-123"
```
