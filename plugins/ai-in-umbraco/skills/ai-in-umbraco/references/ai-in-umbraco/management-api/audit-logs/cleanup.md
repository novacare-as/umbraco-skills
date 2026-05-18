# Cleanup | AI in Umbraco

Clean up old audit log entries.

Request

```
POST /umbraco/ai/management/api/v1/audit-logs/cleanup
```

Response

Success

```
1542
```

Examples

Using Default Retention

```
curl -X POST "https://your-site.com/umbraco/ai/management/api/v1/audit-logs/cleanup" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

Configuration

| Setting | Default | Description |
|---|---|---|
| `Enabled` | `true` | Whether audit logging is enabled |
| `RetentionDays` | `14` | Days to retain audit logs before cleanup |

Last updated

Was this helpful?