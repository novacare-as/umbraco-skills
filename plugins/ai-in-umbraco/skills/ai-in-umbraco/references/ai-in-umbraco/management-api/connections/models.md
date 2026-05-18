# Get Models | AI in Umbraco

Get available AI models for a connection.

Endpoint

```
GET /umbraco/ai/management/api/v1/connections/{idOrAlias}/models
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `idOrAlias` | string | Connection GUID or alias |

Response

Success (200 OK)

```
{
    "items": [
        {
            "id": "gpt-4o",
            "name": "GPT-4o",
            "capabilities": ["Chat"]
        },
        {
            "id": "gpt-4o-mini",
            "name": "GPT-4o Mini",
            "capabilities": ["Chat"]
        },
        {
            "id": "text-embedding-3-small",
            "name": "Text Embedding 3 Small",
            "capabilities": ["Embedding"]
        },
        {
            "id": "text-embedding-3-large",
            "name": "Text Embedding 3 Large",
            "capabilities": ["Embedding"]
        }
    ]
}
```

Model Properties

| Property | Type | Description |
|---|---|---|
| `id` | string | Model identifier to use in API calls |
| `name` | string | Display name |
| `capabilities` | string[] | Capabilities this model supports |

404 Not Found

Examples

cURL

JavaScript

Filter by Capability

Populate Model Dropdown

Notes

Last updated

Was this helpful?