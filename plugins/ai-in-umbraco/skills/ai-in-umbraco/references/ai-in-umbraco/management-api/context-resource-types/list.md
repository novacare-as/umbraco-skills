# List Resource Types | AI in Umbraco

List all available context resource types.

Endpoint

```
GET /umbraco/ai/management/api/v1/context-resource-types
```

Response

Success (200 OK)

```
[
    {
        "id": "text",
        "name": "Text",
        "description": "Plain text content.",
        "icon": "icon-document"
    },
    {
        "id": "document",
        "name": "Document",
        "description": "Document/content node reference.",
        "icon": "icon-picture"
    },
    {
        "id": "url",
        "name": "URL",
        "description": "Web URL resource.",
        "icon": "icon-link"
    }
]
```

Item Properties

| Property | Type | Description |
|---|---|---|
| `id` | string | Unique identifier for the type |
| `name` | string | Display name |
| `description` | string | Description of the resource type |
| `icon` | string | Icon identifier for the backoffice UI |

Examples

List All Resource Types

JavaScript

Last updated

Was this helpful?