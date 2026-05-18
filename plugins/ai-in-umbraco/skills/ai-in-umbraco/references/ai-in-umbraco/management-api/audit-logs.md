# Audit Logs | AI in Umbraco

API endpoints for accessing AI operation audit logs.

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET |
| `/umbraco/ai/management/api/v1/audit-logs` |

`/umbraco/ai/management/api/v1/audit-logs/{id}`

`/umbraco/ai/management/api/v1/audit-logs?entityId={entityId}`

`/umbraco/ai/management/api/v1/audit-logs/{id}`

`/umbraco/ai/management/api/v1/audit-logs/cleanup`

Base URL

```
/umbraco/ai/management/api/v1
```

Audit Log Object

```
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "startTime": "2024-01-25T09:15:00Z",
    "endTime": "2024-01-25T09:15:02Z",
    "duration": "00:00:02.345",
    "status": "Succeeded",
    "errorCategory": null,
    "errorMessage": null,
    "userId": "user-guid",
    "userName": "[email protected]",
    "entityId": "content-guid",
    "entityType": "document",
    "capability": "Chat",
    "profileId": "profile-guid",
    "profileAlias": "content-assistant",
    "profileVersion": 5,
    "providerId": "openai",
    "modelId": "gpt-4o",
    "featureType": "prompt",
    "featureId": "prompt-guid",
    "featureVersion": 2,
    "inputTokens": 150,
    "outputTokens": 420,
    "totalTokens": 570,
    "detailLevel": "Standard",
    "parentAuditLogId": null
}
```

Status Values

| Status | Description |
|---|---|
| `Running` | Operation is in progress |
| `Succeeded` | Operation completed successfully |
| `Failed` | Operation failed with an error |
| `Cancelled` | Operation was cancelled |
| `PartialSuccess` | Operation partially completed |

Error Categories

| Category | Description |
|---|---|
| `Authentication` | API key or credential issues |
| `RateLimit` | Provider rate limit exceeded |
| `Timeout` | Request timed out |
| `InvalidRequest` | Malformed request |
| `ModelError` | Model processing error |
| `NetworkError` | Connection issues |
| `Unknown` | Unclassified error |

Detail Levels

| Level | Includes |
|---|---|
| `Minimal` | Timing, status, tokens only |
| `Standard` | Above + profile, model, user info |
| `Full` | Above + prompt/response snapshots |

Related

Last updated

Was this helpful?

## Sub-topics

- [Cleanup | AI in Umbraco](audit-logs/cleanup.md)
- [Delete Audit Log | AI in Umbraco](audit-logs/delete.md)
- [Entity History | AI in Umbraco](audit-logs/entity-history.md)
- [Get Audit Log | AI in Umbraco](audit-logs/get.md)
- [List Audit Logs | AI in Umbraco](audit-logs/list.md)
