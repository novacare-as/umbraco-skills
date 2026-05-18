# Entity History | AI in Umbraco

Get audit history for a specific entity.

Request

```
GET /umbraco/ai/management/api/v1/audit-logs?entityId={entityId}
```

Query Parameters

| Parameter | Type | Default | Description |
|---|---|---|---|
| `entityId` | string | - | Entity identifier to filter audit logs by |
| `skip` | int | 0 | Number of records to skip |
| `take` | int | 100 | Number of records to return |

Response

Success

```
{
    "items": [
        {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "startTime": "2024-01-25T09:15:00Z",
            "durationMs": 2345,
            "status": "Succeeded",
            "userId": "admin-user-guid",
            "userName": "[email protected]",
            "entityId": "content-guid",
            "capability": "Chat",
            "profileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "profileAlias": "content-assistant",
            "profileVersion": 5,
            "providerId": "openai",
            "modelId": "gpt-4o",
            "featureType": "prompt",
            "featureId": "b2c3d4e5-f6a7-8901-bcde-f23456789012",
            "featureVersion": 2,
            "inputTokens": 150,
            "outputTokens": 420
        }
    ],
    "total": 2
}
```

Examples

Use Cases

Last updated

Was this helpful?