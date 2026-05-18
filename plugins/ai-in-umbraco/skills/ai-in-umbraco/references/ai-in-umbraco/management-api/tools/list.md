# List Tools | AI in Umbraco

List all user-configurable AI tools grouped by scope.

Endpoint

```
GET /umbraco/ai/management/api/v1/tools
```

Response

Success (200 OK)

```
[
    {
        "id": "get-content-by-id",
        "name": "Get Content By Id",
        "description": "Retrieves a content item by its unique identifier.",
        "scopeId": "content-read",
        "isDestructive": false,
        "tags": ["content", "read"]
    },
    {
        "id": "update-content",
        "name": "Update Content",
        "description": "Updates an existing content item with new property values.",
        "scopeId": "content-write",
        "isDestructive": true,
        "tags": ["content", "write"]
    },
    {
        "id": "search-content",
        "name": "Search Content",
        "description": "Searches for content items matching the given query.",
        "scopeId": "search",
        "isDestructive": false,
        "tags": ["search"]
    }
]
```

Item Properties

| Property | Type | Description |
|---|---|---|
| `id` | string | Unique identifier for the tool |
| `name` | string | Display name |
| `description` | string | Description of what the tool does |
| `scopeId` | string | The scope this tool belongs to |
| `isDestructive` | boolean | Whether the tool performs destructive operations |
| `tags` | string[] | Tags for categorization |

Examples

List All Tools

JavaScript

Last updated

Was this helpful?