# API Keys

API Keys are used to authenticate the Rova CLI and other third-party integrations with your mobile workspace. They allow you to perform actions programmatically without using your personal login credentials.

### Generating an API Key

1. Navigate to **Settings > API Keys** in your Rova Mobile dashboard.
2. Click **New API Key**.
3. Give your key a descriptive name (e.g., `CI-Bitrise-Production`) and optionally set an expiration date.
4. **Copy the key immediately**. For security reasons, Rova will not show the key again after you close the dialog.

### Using API Keys

#### In the Rova CLI

The CLI will automatically look for a `ROVA_API_KEY` environment variable.

```
export ROVA_API_KEY="your_api_key_here"

# Run a mobile test on Rova's cloud-hosted devices
rova run mobile --remote --goal "Verify onboarding screen" --project-id "PROJ_123"
```

### Security Best Practices

#### 1. One Key Per Integration

Don't use the same API key for local development and your production CI/CD pipeline. Generate unique keys for each use case. This makes it much easier to revoke a single key if it ever gets compromised.

#### 2. Set Expiry Dates

When generating a key, you can optionally set an expiry date. This is highly recommended for temporary integrations, automated scripts, or external consultants.

#### 3. Rotate Keys Regularly

It's a good security habit to regenerate and replace your CI/CD API keys every 90 days.

#### 4. Use "Least Privilege"

API keys inherit the permissions of the user who generated them. If a key only needs to trigger mobile tests in a pipeline, make sure it is assigned a role with limited permissions rather than using an "Owner" key.

> Warning: Never commit your API keys directly to your app's source code repository. Always use environment variables or a secure secret management system (like GitHub Secrets, Bitrise Environment Variables, or Doppler).

### Revoking a Key

If an API key is no longer needed or has been accidentally leaked (e.g., in a public build log), you can revoke it immediately from the Settings > API Keys page. All active connections using that key will be cut off instantly.
