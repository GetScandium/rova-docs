# API Keys

API Keys are used to authenticate the Rova CLI and other third-party integrations with your workspace. They allow you to perform actions programmatically without using your personal login credentials.

## Generating an API Key

1. Navigate to **Settings > API Keys** in the Rova dashboard.
2. Click **Generate New Key**.
3. Give your key a descriptive name (e.g., `CI-GitHub-Actions-Production`).
4. **Copy the key immediately.** For security reasons, Rova will not show the key again after you close the dialog.

## Using API Keys

### In the Rova CLI
The CLI will automatically look for a `ROVA_API_KEY` environment variable.

```bash
export ROVA_API_KEY="your_api_key_here"
# Run a web test on Rova cloud infrastructure
rova run web --remote --goal "Verify landing page" --project-id "PROJ_123"
```

<!-- ### In GitHub Actions
Store your API Key as a **GitHub Secret** (usually named `ROVA_API_KEY`) and reference it in your workflow file.

```yaml
- name: Run Rova Tests
  uses: GetScandium/rova-upload-action@v1
  with:
    api-key: ${{ secrets.ROVA_API_KEY }}
    ...
``` -->

## Security Best Practices

### 1. One Key Per Integration
Don't use the same API key for your local development and your production CI. Generate unique keys for each use case. This makes it easier to revoke a single key if it becomes compromised.

### 2. Set Expiry Dates
When generating a key, you can optionally set an expiry date. This is recommended for temporary integrations or external consultants.

### 3. Rotate Keys Regularly
It's a good practice to regenerate your CI API keys every 90 days.

### 4. Use "Least Privilege"
API keys are tied to the permissions of the person who generated them (or the role assigned to the key). If a key only needs to run tests, don't use an "Owner" key.

> [!CAUTION]
> **Warning**: Never commit your API keys to your source code repository. Always use environment variables or a secure secret management system.

## Revoking a Key
If an API key is no longer needed or has been leaked, you can revoke it immediately from the **Settings > API Keys** page. All active connections using that key will be terminated.
