# Get History | AI in Umbraco

Get version history for an entity.

Request

```
GET /umbraco/ai/management/api/v1/versions/{entityType}/{entityId}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `entityType` | string | Entity type (`connection` , `profile` , `context` , `prompt` , `agent` ) |
| `entityId` | guid | Entity unique identifier |

Query Parameters

| Parameter | Type | Default | Description |
|---|---|---|---|
| `skip` | int | 0 | Number of versions to skip |
| `take` | int | 10 | Number of versions to return |

Response

Success

```
{
    "currentVersion": 5,
    "totalVersions": 5,
    "versions": [
        {
            "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "entityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "version": 5,
            "dateCreated": "2024-01-25T09:15:00Z",
            "createdByUserId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
            "createdByUserName": "[email protected]",
            "changeDescription": "Updated system prompt"
        },
        {
            "id": "b2c3d4e5-f6a7-8901-bcde-f23456789012",
            "entityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "version": 4,
            "dateCreated": "2024-01-22T16:30:00Z",
            "createdByUserId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
            "createdByUserName": "[email protected]",
            "changeDescription": "Changed temperature to 0.8"
        },
        {
            "id": "c3d4e5f6-a7b8-9012-cdef-345678901234",
            "entityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "version": 3,
            "dateCreated": "2024-01-20T14:45:00Z",
            "createdByUserId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
            "createdByUserName": "[email protected]",
            "changeDescription": null
        }
    ]
}
```

Response Properties

| Property | Type | Description |
|---|---|---|
| `currentVersion` | int | The current version of the entity |
| `totalVersions` | int | The total number of versions available |
| `versions` | array | List of version entries |

Version Entry Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier of the version record |
| `entityId` | guid | ID of the entity this version belongs to |
| `version` | int | The version number |
| `dateCreated` | datetime | When this version was created |
| `createdByUserId` | guid | User key of the user who created this version |
| `createdByUserName` | string | Display name of the user who created this version |
| `changeDescription` | string | Optional description of what changed in this version |

Not Found

Examples

Notes

Last updated

Was this helpful?