# Update Profile | AI in Umbraco

Update an existing AI profile.

Request

```
PUT /umbraco/ai/management/api/v1/profiles/{profileIdOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `profileIdOrAlias` | string | Profile GUID or alias |

Request Body

```
{
    "alias": "content-assistant",
    "name": "Content Assistant (Updated)",
    "model": {
        "providerId": "openai",
        "modelId": "gpt-4o"
    },
    "connectionId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "settings": {
        "$type": "chat",
        "temperature": 0.5,
        "maxTokens": 8192,
        "systemPromptTemplate": "You are an expert content assistant."
    },
    "tags": ["content", "expert"]
}
```

Required Fields

| Field | Type | Description |
|---|---|---|
| `alias` | string | Unique alias |
| `name` | string | Display name |
| `model` | object | Model reference |
| `model.providerId` | string | Provider ID |
| `model.modelId` | string | Model ID |
| `connectionId` | guid | Connection ID |

Optional Fields

| Field | Type | Description |
|---|---|---|
| `settings` | object | Capability-specific settings |
| `tags` | array | Categorization tags |

Response

Success

Not Found

Validation Error

Examples

Update by ID

Update by Alias

Change Model

Update Tags

Common Updates

Adjusting Temperature

Updating System Prompt

Last updated

Was this helpful?