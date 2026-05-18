# Get Version | AI in Umbraco

Get a specific version snapshot.

Request

```
GET /umbraco/ai/management/api/v1/versions/{entityType}/{entityId}/{entityVersion}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `entityType` | string | Entity type (`connection` , `profile` , `context` , `prompt` , `agent` ) |
| `entityId` | guid | Entity unique identifier |
| `entityVersion` | int | Version number to retrieve |

Response

Success

```
{
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "entityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "version": 3,
    "dateCreated": "2024-01-20T14:45:00Z",
    "createdByUserId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "createdByUserName": "[email protected]",
    "changeDescription": "Updated temperature setting"
}
```

Response Properties

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

Last updated

Was this helpful?