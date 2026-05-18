# List Guardrails | AI in Umbraco

List all AI guardrails.

Request

```
GET /umbraco/ai/management/api/v1/guardrails
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
            "alias": "content-safety",
            "name": "Content Safety Policy",
            "ruleCount": 1,
            "dateCreated": "2024-01-15T10:30:00Z",
            "dateModified": "2024-01-20T14:45:00Z"
        }
    ],
    "total": 3
}
```

Item Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `alias` | string | Unique alias for code references |
| `name` | string | Display name |
| `ruleCount` | int | Number of rules in the guardrail |
| `dateCreated` | datetime | When the guardrail was created |
| `dateModified` | datetime | When the guardrail was last modified |

Examples

Last updated

Was this helpful?