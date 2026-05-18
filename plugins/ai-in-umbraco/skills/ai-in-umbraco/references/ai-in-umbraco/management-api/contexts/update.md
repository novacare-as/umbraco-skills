# Update Context | AI in Umbraco

Update an existing AI context.

Request

```
PUT /umbraco/ai/management/api/v1/contexts/{contextIdOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `contextIdOrAlias` | string | Context GUID or alias |

Request Body

```
{
    "alias": "brand-voice",
    "name": "Brand Voice Updated",
    "resources": [
        {
            "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
            "resourceTypeId": "text",
            "name": "Tone of Voice",
            "description": "Updated writing style guidelines",
            "sortOrder": 0,
            "settings": "Always use a friendly, professional, and engaging tone...",
            "injectionMode": "Always"
        },
        {
            "resourceTypeId": "text",
            "name": "Key Messages",
            "sortOrder": 1,
            "settings": "Our core values are...",
            "injectionMode": "Always"
        }
    ]
}
```

Response

Success

Not Found

Validation Error

Examples

Last updated

Was this helpful?