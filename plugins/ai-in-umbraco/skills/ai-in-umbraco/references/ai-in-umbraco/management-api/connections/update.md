# Update Connection | AI in Umbraco

Update an existing AI provider connection.

Endpoint

```
PUT /umbraco/ai/management/api/v1/connections/{id}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `id` | guid | Connection ID (GUID only, not alias) |

Request

Headers

| Header | Value |
|---|---|
| Content-Type | `application/json` |

Body

```
{
    "name": "OpenAI Production (Updated)",
    "isActive": true,
    "settings": {
        "apiKey": "$OpenAI:ApiKey",
        "organization": "org-123"
    }
}
```

Updatable Fields

| Field | Type | Description |
|---|---|---|
| `alias` | string | Unique alias (URL-safe) |
| `name` | string | Display name |
| `isActive` | boolean | Whether connection is enabled |
| `settings` | object | Provider-specific settings |

Response

Success (200 OK)

404 Not Found

400 Bad Request

Examples

cURL

JavaScript

Last updated

Was this helpful?