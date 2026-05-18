# List Providers | AI in Umbraco

List all registered AI providers.

Request

```
GET /umbraco/ai/management/api/v1/providers
```

Headers

| Header | Value |
|---|---|
| `Authorization` | Bearer token or cookie |

Query Parameters

Response

Success (200 OK)

```
[
    {
        "id": "openai",
        "name": "OpenAI",
        "capabilities": ["Chat", "Embedding"]
    },
    {
        "id": "azure-openai",
        "name": "Azure OpenAI",
        "capabilities": ["Chat", "Embedding"]
    }
]
```

Response Properties

| Property | Type | Description |
|---|---|---|
| `id` | string | Unique provider identifier |
| `name` | string | Display name |
| `capabilities` | string[] | Supported capabilities |

Capabilities

| Value | Description |
|---|---|
| `Chat` | Conversational AI / chat completions |
| `Embedding` | Text to vector embeddings |

Example

cURL

C# HttpClient

JavaScript

Notes

Last updated

Was this helpful?