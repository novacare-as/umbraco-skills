# Embeddings | AI in Umbraco

REST API endpoints for generating text embeddings.

Overview

Base URL

```
/umbraco/ai/management/api/v1/embeddings
```

Authentication

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/umbraco/ai/management/api/v1/embeddings/generate` |
|

Response Model

EmbeddingResponseModel

| Property | Type | Description |
|---|---|---|
| `embeddings` | array | List of embedding results |
| `embeddings[].index` | int | Index of the input value (0-based) |
| `embeddings[].vector` | float[] | The embedding vector |

Vector Dimensions

| Model | Dimensions |
|---|---|
| text-embedding-3-small | 1536 |
| text-embedding-3-large | 3072 |
| text-embedding-ada-002 | 1536 |

Working with Embeddings

Calculating Similarity

Storing Embeddings

In This Section

Last updated

Was this helpful?

## Sub-topics

- [Generate | AI in Umbraco](embeddings/generate.md)
