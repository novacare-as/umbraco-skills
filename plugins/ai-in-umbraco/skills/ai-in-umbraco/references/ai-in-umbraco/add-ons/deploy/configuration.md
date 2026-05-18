# Configuration | AI in Umbraco

Configure sensitive data filtering and deployment settings for Umbraco AI Deploy.

Default Behavior

Configuration Settings

```
{
  "Umbraco": {
    "AI": {
      "Deploy": {
        "Connections": {
          "IgnoreEncrypted": true,
          "IgnoreSensitive": false,
          "IgnoreSettings": []
        }
      }
    }
  }
}
```

IgnoreEncrypted

| Value in Database | Deployed? |
|---|---|
| `$OpenAI:ApiKey` | ✅ Yes (configuration reference) |
| `ENC:abc123...` | ❌ No (encrypted value) |
| `https://api.openai.com` | ✅ Yes (plain value) |

IgnoreSensitive

| Value in Database | Deployed? |
|---|---|
| `$OpenAI:ApiKey` | ✅ Yes (configuration reference allowed) |
| `ENC:abc123...` | ❌ No (blocked by IgnoreEncrypted) |
| `sk-abc123...` | ✅ Yes (plain value allowed - not recommended) |

IgnoreSettings

Filtering Priority

Recommended Configurations

Balanced Security (Default)

Maximum Security

Block Specific Fields Only

Using Configuration References

1. Store Secrets in appsettings.json

2. Reference in Connection Settings

3. Verify

Environment-Specific Secrets

Troubleshooting

API Keys Appearing in Deployment Files

Configuration References Not Working

Next Steps

Last updated

Was this helpful?