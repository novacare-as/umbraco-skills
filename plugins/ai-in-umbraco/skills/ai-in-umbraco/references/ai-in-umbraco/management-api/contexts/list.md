# List Contexts | AI in Umbraco

List all AI contexts.

Request

```
GET /umbraco/ai/management/api/v1/contexts
```

Query Parameters

| Parameter | Type | Default | Description |
|---|---|---|---|
| `filter` | string | null | Filter to search by name or alias (case-insensitive contains) |
| `skip` | int | 0 | Number of items to skip |
| `take` | int | 100 | Number of items to return |

Response

Success

```
{
    "items": [
        {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "alias": "brand-voice",
            "name": "Brand Voice",
            "resourceCount": 1,
            "dateCreated": "2024-01-15T10:30:00Z",
            "dateModified": "2024-01-20T14:45:00Z"
        }
    ],
    "total": 5
}
```

Item Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `alias` | string | Unique alias for code references |
| `name` | string | Display name |
| `resourceCount` | int | Number of resources in the context |
| `dateCreated` | datetime | When the context was created |
| `dateModified` | datetime | When the context was last modified |

Examples

Last updated

Was this helpful?