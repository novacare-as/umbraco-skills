# List Capabilities | AI in Umbraco

List available AI capabilities and find connections that support them.

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/umbraco/ai/management/api/v1/connections/capabilities` | List all available capabilities |
| GET | `/umbraco/ai/management/api/v1/connections/capabilities/{capability}` | Get connections that support a capability |
| GET | `/umbraco/ai/management/api/v1/connections/{connectionIdOrAlias}/capabilities` | Get capabilities supported by a specific connection |

List All Capabilities

Endpoint

```
GET /umbraco/ai/management/api/v1/connections/capabilities
```

Response (200 OK)

```
{
    "items": ["Chat", "Embedding"]
}
```

Example

Get Connections by Capability

Endpoint

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `capability` | string | Capability name (Chat, Embedding) |

Response (200 OK)

Example

Get Capabilities for a Connection

Endpoint

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `connectionIdOrAlias` | string | Connection GUID or alias |

Response (200 OK)

Example

Available Capabilities

| Capability | Description |
|---|---|
| `Chat` | Conversational AI and text generation |
| `Embedding` | Vector embeddings for semantic search |

Use Cases

Check Before Creating Profile

Get Available Capabilities

Last updated

Was this helpful?