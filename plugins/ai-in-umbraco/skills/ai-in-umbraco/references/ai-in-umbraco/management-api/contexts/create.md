# Create Context | AI in Umbraco

Create a new AI context.

Request

```
POST /umbraco/ai/management/api/v1/contexts
```

Request Body

```
{
    "alias": "brand-voice",
    "name": "Brand Voice",
    "resources": [
        {
            "resourceTypeId": "text",
            "name": "Tone of Voice",
            "description": "Writing style guidelines",
            "sortOrder": 0,
            "settings": "Always use a friendly, professional tone...",
            "injectionMode": "Always"
        }
    ]
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `alias` | string | Yes | Unique alias (URL-safe) |
| `name` | string | Yes | Display name |
| `resources` | array | No | Collection of resources |

Resource Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `resourceTypeId` | string | Yes | Type of resource |
| `name` | string | Yes | Display name |
| `description` | string | No | Optional description |
| `sortOrder` | int | No | Order for injection (default: 0) |
| `settings` | object | No | Resource content |
| `injectionMode` | string | No | `Always` (default) or `OnDemand` |

Response

Success

Validation Error

Examples

Last updated

Was this helpful?