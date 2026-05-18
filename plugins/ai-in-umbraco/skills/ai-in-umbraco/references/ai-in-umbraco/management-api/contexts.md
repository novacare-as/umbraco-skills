# Contexts | AI in Umbraco

API endpoints for managing AI contexts.

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET |
| `/umbraco/ai/management/api/v1/contexts` |

`/umbraco/ai/management/api/v1/contexts/{contextIdOrAlias}`

`/umbraco/ai/management/api/v1/contexts`

`/umbraco/ai/management/api/v1/contexts/{contextIdOrAlias}`

`/umbraco/ai/management/api/v1/contexts/{contextIdOrAlias}`

Base URL

```
/umbraco/ai/management/api/v1
```

Context Object

```
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "alias": "brand-voice",
    "name": "Brand Voice",
    "version": 3,
    "resources": [
        {
            "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
            "resourceTypeId": "text",
            "name": "Tone of Voice",
            "description": "Writing style guidelines",
            "sortOrder": 0,
            "settings": "Always use a friendly, professional tone...",
            "injectionMode": "Always"
        }
    ],
    "dateCreated": "2024-01-15T10:30:00Z",
    "dateModified": "2024-01-20T14:45:00Z",
    "createdByUserId": "user-guid",
    "modifiedByUserId": "user-guid"
}
```

Resource Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `resourceTypeId` | string | Type of resource (e.g., "text", "document") |
| `name` | string | Display name |
| `description` | string | Optional description |
| `sortOrder` | int | Controls injection order |
| `settings` | object | Type-specific resource data |
| `injectionMode` | string | When to inject: `Always` or `OnDemand` |

Related

Last updated

Was this helpful?

## Sub-topics

- [Create Context | AI in Umbraco](contexts/create.md)
- [Delete Context | AI in Umbraco](contexts/delete.md)
- [Get Context | AI in Umbraco](contexts/get.md)
- [List Contexts | AI in Umbraco](contexts/list.md)
- [Update Context | AI in Umbraco](contexts/update.md)
