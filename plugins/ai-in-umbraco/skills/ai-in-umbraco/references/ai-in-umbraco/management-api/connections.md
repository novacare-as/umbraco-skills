# Connections | AI in Umbraco

Manage AI provider connections via the Management API.

Available Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/umbraco/ai/management/api/v1/connections` | List all connections |
| GET | `/umbraco/ai/management/api/v1/connections/{connectionIdOrAlias}` | Get a specific connection |
| POST | `/umbraco/ai/management/api/v1/connections` | Create a connection |
| PUT | `/umbraco/ai/management/api/v1/connections/{connectionIdOrAlias}` | Update a connection |
| DELETE | `/umbraco/ai/management/api/v1/connections/{connectionIdOrAlias}` | Delete a connection |
| POST | `/umbraco/ai/management/api/v1/connections/{connectionIdOrAlias}/test` | Test a connection |
| GET | `/umbraco/ai/management/api/v1/connections/capabilities` | List available capabilities |
| GET | `/umbraco/ai/management/api/v1/connections/capabilities/{capability}` | Get connections by capability |
| GET | `/umbraco/ai/management/api/v1/connections/{connectionIdOrAlias}/models` | Get available models |

Connection Model

```
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "alias": "openai-prod",
    "name": "OpenAI Production",
    "providerId": "openai",
    "isActive": true,
    "dateCreated": "2024-01-15T10:30:00Z",
    "dateModified": "2024-01-15T10:30:00Z",
    "settings": {
        "apiKey": "sk-***",
        "organization": null
    }
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `alias` | string | Unique alias for lookups |
| `name` | string | Display name |
| `providerId` | string | ID of the provider |
| `isActive` | boolean | Whether connection is enabled |
| `dateCreated` | datetime | Creation timestamp |
| `dateModified` | datetime | Last modification timestamp |
| `settings` | object | Provider-specific settings |

In This Section

[List Connections chevron-right](/ai-in-umbraco/management-api/connections/list)

[Create Connection chevron-right](/ai-in-umbraco/management-api/connections/create)

[Update Connection chevron-right](/ai-in-umbraco/management-api/connections/update)

[Delete Connection chevron-right](/ai-in-umbraco/management-api/connections/delete)

Last updated

Was this helpful?

## Sub-topics

- [List Capabilities | AI in Umbraco](connections/capabilities.md)
- [Create Connection | AI in Umbraco](connections/create.md)
- [Delete Connection | AI in Umbraco](connections/delete.md)
- [Get Connection | AI in Umbraco](connections/get.md)
- [List Connections | AI in Umbraco](connections/list.md)
- [Get Models | AI in Umbraco](connections/models.md)
- [Test Connection | AI in Umbraco](connections/test.md)
- [Update Connection | AI in Umbraco](connections/update.md)
