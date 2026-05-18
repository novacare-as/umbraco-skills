# Profiles | AI in Umbraco

API endpoints for managing AI profiles.

Base URL

```
/umbraco/ai/management/api/v1/profiles
```

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/umbraco/ai/management/api/v1/profiles` |
|

`/umbraco/ai/management/api/v1/profiles/{profileIdOrAlias}`

[Get a profile](/ai-in-umbraco/management-api/profiles/get)`/umbraco/ai/management/api/v1/profiles`

[Create a profile](/ai-in-umbraco/management-api/profiles/create)`/umbraco/ai/management/api/v1/profiles/{profileIdOrAlias}`

[Update a profile](/ai-in-umbraco/management-api/profiles/update)`/umbraco/ai/management/api/v1/profiles/{profileIdOrAlias}`

[Delete a profile](/ai-in-umbraco/management-api/profiles/delete)Profile Object

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
        "systemPromptTemplate": "You are a helpful content assistant."
    },
    "tags": ["content", "assistant"]
}
```

Profile Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `alias` | string | Unique alias for code references |
| `name` | string | Display name |
| `capability` | string | Capability type (`Chat` , `Embedding` ) |
| `model` | object | Model reference with `providerId` and `modelId` |
| `connectionId` | guid | ID of the connection to use |
| `settings` | object | Capability-specific settings (polymorphic) |
| `tags` | array | Optional tags for categorization |

Settings Types

Chat Settings

| Property | Type | Description |
|---|---|---|
| `temperature` | float | Randomness (0.0-1.0) |
| `maxTokens` | int | Maximum response tokens |
| `systemPromptTemplate` | string | Default system prompt |

Embedding Settings

ID or Alias

In This Section

Last updated

Was this helpful?

## Sub-topics

- [Create Profile | AI in Umbraco](profiles/create.md)
- [Delete Profile | AI in Umbraco](profiles/delete.md)
- [Get Profile | AI in Umbraco](profiles/get.md)
- [List Profiles | AI in Umbraco](profiles/list.md)
- [Update Profile | AI in Umbraco](profiles/update.md)
