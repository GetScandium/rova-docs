---
hidden: true
---

# Sensitivity & Data Privacy

Security and privacy are paramount when testing applications that handle sensitive information (PII, financial data, internal-only features). Rova provides granular controls to ensure your data stays private.

## Sensitivity Levels

Rova allows you to mark project context data as sensitive.

| Level         | Description            | Agent Behavior                                              |
| ------------- | ---------------------- | ----------------------------------------------------------- |
| **Standard**  | Default setting.       | Screenshots and full logs are captured for debugging.       |
| **Sensitive** | Used for private data. | Context data marked as sensitive will be encrypted at rest. |

## Best Practices for Data Privacy

### 1. Masking PII

If your tests involve entering real user data for some reason (though mock data is recommended), always use **Sensitive** mode for those steps.

### 2. Internal Documentation

If your [Project Context](contexts.md) contains internal URLs or non-public documentation, mark the **Context Data** itself as sensitive in the settings.

### 3. Review Permissions

Ensure that only authorized team members have the "Owner" or "Admin" roles.

> \[!CAUTION] **Warning**: Avoid using production databases for automated testing whenever possible. Even with high sensitivity settings, the safest way to handle data is to use isolated staging or test environments with anonymized data.
