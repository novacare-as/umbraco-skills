# Generate | AI in Umbraco

Generate vector embeddings from text values.

Request

```
POST /umbraco/ai/management/api/v1/embeddings/generate
```

Headers

| Header | Value |
|---|---|
| `Authorization` | Bearer token or cookie |
| `Content-Type` | `application/json` |

Request Body

```
{
    "profileIdOrAlias": "document-embeddings",
    "values": ["Umbraco is an open-source CMS", "Content management made easy"]
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `profileIdOrAlias` | string/guid | No | Profile ID or alias (uses default if omitted) |
| `values` | string[] | Yes | Text values to embed (min 1) |

Response

Success (200 OK)

Response Properties

| Property | Type | Description |
|---|---|---|
| `embeddings` | array | List of embedding results |
| `embeddings[].index` | int | Index of corresponding input value |
| `embeddings[].vector` | float[] | Embedding vector |

Bad Request (400)

Not Found (404)

Example

cURL

C# HttpClient

JavaScript

Use Cases

Semantic Search Index

Content Similarity

Batch Processing

Notes

Last updated

Was this helpful?