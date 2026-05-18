# List Connections | AI in Umbraco

List all AI connections with optional filtering and pagination.

Endpoint

```
GET /umbraco/ai/management/api/v1/connections
```

Query Parameters

| Parameter | Type | Default | Description |
|---|---|---|---|
| `skip` | int | 0 | Number of items to skip |
| `take` | int | 100 | Number of items to return |
| `filter` | string | null | Filter by name (contains, case-insensitive) |
| `providerId` | string | null | Filter by provider ID |

Response

Success (200 OK)

```
{
    "items": [
        {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "alias": "openai-prod",
            "name": "OpenAI Production",
            "providerId": "openai",
            "isActive": true
        },
        {
            "id": "7ca85f64-5717-4562-b3fc-2c963f66afa7",
            "alias": "openai-dev",
            "name": "OpenAI Development",
            "providerId": "openai",
            "isActive": true
        }
    ],
    "total": 2
}
```

Item Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `alias` | string | Unique alias |
| `name` | string | Display name |
| `providerId` | string | Provider ID |
| `isActive` | boolean | Whether enabled |

Examples

List All Connections

With Pagination

Filter by Name

Filter by Provider

JavaScript

Last updated

Was this helpful?