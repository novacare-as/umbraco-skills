# Create Profile | AI in Umbraco

Create a new AI profile.

Request

```
POST /umbraco/ai/management/api/v1/profiles
```

Request Body

```
{
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
        "systemPromptTemplate": "You are a helpful content assistant.",
        "contextIds": [],
        "guardrailIds": []
    },
    "tags": ["content", "assistant"]
}
```

Required Fields

| Field | Type | Description |
|---|---|---|
| `alias` | string | Unique alias (used in code) |
| `name` | string | Display name |
| `capability` | string | `Chat` or `Embedding` |
| `model` | object | Model reference |
| `model.providerId` | string | Provider ID (for example, `openai` ) |
| `model.modelId` | string | Model ID (for example, `gpt-4o` ) |
| `connectionId` | guid | ID of an existing connection |

Optional Fields

| Field | Type | Description |
|---|---|---|
| `settings` | object | Capability-specific settings |
| `tags` | array | Categorization tags |

Response

Success

Validation Error

Connection Not Found

Examples

Create Chat Profile

Create Embedding Profile

Minimal Profile

Settings Structure

Chat Settings

| Property | Type | Description |
|---|---|---|
| `$type` | string | Must be `"chat"` |
| `temperature` | float | Response randomness (0.0-1.0) |
| `maxTokens` | int | Maximum output tokens |
| `systemPromptTemplate` | string | Default system prompt |
| `contextIds` | array | Context IDs to include |
| `guardrailIds` | array | Guardrail IDs to apply |

Embedding Settings

| Property | Type | Description |
|---|---|---|
| `$type` | string | Must be `"embedding"` |

Last updated

Was this helpful?