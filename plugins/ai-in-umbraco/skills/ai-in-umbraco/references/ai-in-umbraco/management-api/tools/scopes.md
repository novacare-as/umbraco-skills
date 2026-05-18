# List Tool Scopes | AI in Umbraco

List all AI tool scopes that define tool categories and permissions.

Endpoint

```
GET /umbraco/ai/management/api/v1/tools/scopes
```

Response

Success (200 OK)

```
[
    {
        "id": "content-read",
        "icon": "icon-document",
        "isDestructive": false,
        "domain": "content"
    },
    {
        "id": "content-write",
        "icon": "icon-edit",
        "isDestructive": true,
        "domain": "content"
    },
    {
        "id": "media-read",
        "icon": "icon-picture",
        "isDestructive": false,
        "domain": "media"
    },
    {
        "id": "media-write",
        "icon": "icon-picture",
        "isDestructive": true,
        "domain": "media"
    },
    {
        "id": "search",
        "icon": "icon-search",
        "isDestructive": false,
        "domain": "search"
    }
]
```

Item Properties

| Property | Type | Description |
|---|---|---|
| `id` | string | Unique identifier for the scope |
| `icon` | string | Icon identifier for the backoffice UI |
| `isDestructive` | boolean | Whether the scope contains destructive tools |
| `domain` | string | The functional domain of the scope |

Built-in Scopes

| Scope | Domain | Destructive | Description |
|---|---|---|---|
| `content-read` | content | No | Read content items |
| `content-write` | content | Yes | Create, update, and delete content |
| `media-read` | media | No | Read media items |
| `media-write` | media | Yes | Create, update, and delete media |
| `search` | search | No | Search across content and media |
| `navigation` | navigation | No | Navigate content tree structures |
| `translation` | translation | No | Translate content between languages |
| `web` | web | No | Fetch web content and URLs |
| `entity-read` | entity | No | Read generic entities |
| `entity-write` | entity | Yes | Create, update, and delete entities |

Examples

List All Scopes

JavaScript

Last updated

Was this helpful?