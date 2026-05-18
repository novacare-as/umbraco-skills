# Update Settings | AI in Umbraco

Update global AI settings.

Request

```
PUT /umbraco/ai/management/api/v1/settings
```

Request Body

```
{
    "defaultChatProfileId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "defaultEmbeddingProfileId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "defaultSpeechToTextProfileId": null,
    "classifierChatProfileId": null
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `defaultChatProfileId` | guid | No | Default profile for chat operations |
| `defaultEmbeddingProfileId` | guid | No | Default profile for embedding operations |
| `defaultSpeechToTextProfileId` | guid | No | Default profile for speech-to-text operations |
| `classifierChatProfileId` | guid | No | Optional profile for classification tasks |

Response

Success

Validation Error

Examples

Notes

Last updated

Was this helpful?