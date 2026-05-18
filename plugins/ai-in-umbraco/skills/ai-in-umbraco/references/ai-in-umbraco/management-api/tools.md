# Tools | AI in Umbraco

Manage AI tools and tool scopes via the Management API.

Available Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/umbraco/ai/management/api/v1/tools` | List all user-configurable tools grouped by scope |
| GET | `/umbraco/ai/management/api/v1/tools/scopes` | List all tool scopes |

Tool Model

```
{
    "id": "get-content-by-id",
    "name": "Get Content By Id",
    "description": "Retrieves a content item by its unique identifier.",
    "scopeId": "content-read",
    "isDestructive": false,
    "tags": ["content", "read"]
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `id` | string | Unique identifier for the tool |
| `name` | string | Display name |
| `description` | string | Description of what the tool does |
| `scopeId` | string | The scope this tool belongs to |
| `isDestructive` | boolean | Whether the tool performs destructive operations |
| `tags` | string[] | Tags for categorization |

Tool Scope Model

Properties

| Property | Type | Description |
|---|---|---|
| `id` | string | Unique identifier for the scope |
| `icon` | string | Icon identifier for the backoffice UI |
| `isDestructive` | boolean | Whether the scope contains destructive tools |
| `domain` | string | The functional domain of the scope |
| `forEntityTypes` | string[] | Entity types this scope applies to |

In This Section

Last updated

Was this helpful?

## Sub-topics

- [List Tools | AI in Umbraco](tools/list.md)
- [List Tool Scopes | AI in Umbraco](tools/scopes.md)
