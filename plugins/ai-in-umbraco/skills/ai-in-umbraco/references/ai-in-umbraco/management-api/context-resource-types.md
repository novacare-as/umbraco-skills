# Context Resource Types | AI in Umbraco

Query context resource types via the Management API.

Available Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/umbraco/ai/management/api/v1/context-resource-types` | List all resource types |
| GET | `/umbraco/ai/management/api/v1/context-resource-types/{id}` | Get a resource type with its settings schema |

Resource Type Model

```
{
    "id": "content",
    "name": "Content",
    "description": "Adds content items as context resources.",
    "icon": "icon-document"
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `id` | string | Unique identifier for the type |
| `name` | string | Display name |
| `description` | string | Description of the resource type |
| `icon` | string | Icon identifier for the backoffice UI |

In This Section

Last updated

Was this helpful?

## Sub-topics

- [Get Resource Type | AI in Umbraco](context-resource-types/get.md)
- [List Resource Types | AI in Umbraco](context-resource-types/list.md)
