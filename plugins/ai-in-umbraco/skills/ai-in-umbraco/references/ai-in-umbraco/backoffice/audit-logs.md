# Audit Logs | AI in Umbraco

View and analyze AI operation audit logs.

Accessing Audit Logs

Understanding the Log List

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-7381269c5764c2b4c521f142edbd97ff9124fd9d%252Fbackoffice-audit-log-list.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=71f6528a&sv=2)

| Column | Description |
|---|---|
| Time | When the operation started |
| Status | Outcome (Succeeded, Failed, etc.) |
| Capability | Type of operation (Chat, Embedding, Speech-to-Text) |
| Profile | Which profile was used |
| Provider | AI provider (OpenAI, Anthropic, etc.) |
| Model | Specific model used |
| User | Who initiated the operation |
| Tokens | Total tokens used |
| Duration | How long the operation took |

Filtering Logs

| Filter | Description |
|---|---|
| Date Range | From and To dates |
| Status | Succeeded, Failed, Blocked, Running |
| Capability | Chat, Embedding, Speech-to-Text |
| Profile | Specific profile |
| Provider | Specific provider |
| User | Specific user |

Example Filters

Viewing Log Details

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-46622bf4dad77161e6dc06ea6fbafee3b23e401a%252Fbackoffice-audit-log-detail.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=13016bee&sv=2)

Summary

AI Configuration

Token Usage

Content (if captured)

Status Values

| Status | Description |
|---|---|
| Succeeded | Operation completed successfully. |
| Failed | Operation encountered an error. |
| Running | Operation is in progress. |
| Blocked | Blocked by a guardrail rule. |
| Cancelled | Operation was cancelled. |
| PartialSuccess | Some parts succeeded, some failed. |

Error Categories

| Category | Description |
|---|---|
| Authentication | Authentication failure |
| RateLimiting | Provider rate limit exceeded |
| ModelNotFound | Requested model not available |
| InvalidRequest | Invalid request parameters |
| ServerError | Provider server error |
| NetworkError | Network connectivity issue |
| ContextResolution | Context resolution failure |
| ToolExecution | Tool execution failure |
| GuardrailBlocked | Blocked by guardrail rule |
| Unknown | Unclassified error |

Deleting Logs

Cleanup

Automatic Cleanup

| Property | Default | Description |
|---|---|---|
| `Enabled` | `true` | Whether audit logging is enabled |
| `RetentionDays` | `14` | Number of days to retain logs before cleanup |
| `PersistPrompts` | `true` | Store prompt snapshots in logs |
| `PersistResponses` | `true` | Store response snapshots in logs |
| `PersistFailureDetails` | `true` | Store failure details in logs |
| `RedactionPatterns` | `[]` | Regex patterns for redacting sensitive content |

Related

Last updated

Was this helpful?