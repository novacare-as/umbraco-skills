# Get Settings | AI in Umbraco

Get current AI settings.

Request

```
GET /umbraco/ai/management/api/v1/settings
```

Response

Success

```
{
    "id": "672bf83c-97e0-4d04-9d33-23fc2e5ebe42",
    "defaultChatProfileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "defaultEmbeddingProfileId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "defaultSpeechToTextProfileId": null,
    "classifierChatProfileId": null,
    "dateCreated": "2024-01-01T00:00:00Z",
    "dateModified": "2024-01-20T14:45:00Z",
    "createdByUserId": null,
    "modifiedByUserId": "user-guid"
}
```

Examples

Response Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Fixed settings identifier |
| `defaultChatProfileId` | guid | Default profile for chat operations (null if not set) |
| `defaultEmbeddingProfileId` | guid | Default profile for embedding operations (null if not set) |
| `defaultSpeechToTextProfileId` | guid | Default profile for speech-to-text operations (null if not set) |
| `classifierChatProfileId` | guid | Optional profile for classification tasks (null if not set) |
| `dateCreated` | datetime | When settings were first created |
| `dateModified` | datetime | When settings were last modified |
| `modifiedByUserId` | guid | User who last modified settings |

Last updated

Was this helpful?