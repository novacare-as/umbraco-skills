# Get Connection | AI in Umbraco

Get details of a specific connection by ID or alias.

Endpoint

```
GET /umbraco/ai/management/api/v1/connections/{idOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `idOrAlias` | string | Connection GUID or alias |

Response

Success (200 OK)

```
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "alias": "openai-prod",
    "name": "OpenAI Production",
    "providerId": "openai",
    "isActive": true,
    "version": 1,
    "dateCreated": "2024-01-15T10:30:00Z",
    "dateModified": "2024-01-15T10:30:00Z",
    "createdByUserId": null,
    "modifiedByUserId": null,
    "settings": {
        "apiKey": "sk-***",
        "organization": null
    }
}
```

404 Not Found

Examples

Get by ID

Get by Alias

JavaScript

Last updated

Was this helpful?