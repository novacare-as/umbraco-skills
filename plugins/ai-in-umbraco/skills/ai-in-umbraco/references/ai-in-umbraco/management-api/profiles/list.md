# List Profiles | AI in Umbraco

Get a paginated list of all profiles.

Request

```
GET /umbraco/ai/management/api/v1/profiles
```

Query Parameters

| Parameter | Type | Default | Description |
|---|---|---|---|
| `filter` | string | - | Filter by name (case-insensitive contains) |
| `capability` | string | - | Filter by capability (`Chat` , `Embedding` ) |
| `skip` | int | 0 | Number of items to skip |
| `take` | int | 100 | Number of items to return |

Response

```
{
    "total": 3,
    "items": [
        {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "alias": "content-assistant",
            "name": "Content Assistant",
            "capability": "Chat",
            "model": {
                "providerId": "openai",
                "modelId": "gpt-4o"
            }
        },
        {
            "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
            "alias": "summarizer",
            "name": "Content Summarizer",
            "capability": "Chat",
            "model": {
                "providerId": "openai",
                "modelId": "gpt-4o-mini"
            }
        },
        {
            "id": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
            "alias": "embeddings",
            "name": "Document Embeddings",
            "capability": "Embedding",
            "model": {
                "providerId": "openai",
                "modelId": "text-embedding-3-small"
            }
        }
    ]
}
```

Examples

List All Profiles

Filter by Name

Filter by Capability

Paginate Results

Response Properties

Item Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `alias` | string | Unique alias |
| `name` | string | Display name |
| `capability` | string | Capability type |
| `model` | object | Model reference |

Last updated

Was this helpful?