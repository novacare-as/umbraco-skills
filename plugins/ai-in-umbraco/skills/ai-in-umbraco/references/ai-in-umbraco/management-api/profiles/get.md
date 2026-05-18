# Get Profile | AI in Umbraco

Get a profile by ID or alias.

Request

```
GET /umbraco/ai/management/api/v1/profiles/{profileIdOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `profileIdOrAlias` | string | Profile GUID or alias |

Response

Success

```
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "alias": "content-assistant",
    "name": "Content Assistant",
    "capability": "Chat",
    "model": {
        "providerId": "openai",
        "modelId": "gpt-4o"
    },
    "connectionId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "settings": {
        "$type": "chat",
        "temperature": 0.7,
        "maxTokens": 4096,
        "systemPromptTemplate": "You are a helpful content assistant for a website.",
        "contextIds": [],
        "guardrailIds": []
    },
    "tags": ["content", "assistant"],
    "version": 1,
    "dateCreated": "2024-01-15T10:30:00Z",
    "dateModified": "2024-01-20T14:45:00Z"
}
```

Not Found

Examples

Get by ID

Get by Alias

Response Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `alias` | string | Unique alias for code references |
| `name` | string | Display name |
| `capability` | string | Capability type (`Chat` , `Embedding` ) |
| `model` | object | Model reference with `providerId` and `modelId` |
| `connectionId` | guid | ID of the connection used |
| `settings` | object | Capability-specific settings |
| `tags` | array | Optional categorization tags |
| `version` | int | Current version number |
| `dateCreated` | datetime | When the profile was created |
| `dateModified` | datetime | When the profile was last modified |

Settings by Capability

Chat Profile

Embedding Profile

Last updated

Was this helpful?