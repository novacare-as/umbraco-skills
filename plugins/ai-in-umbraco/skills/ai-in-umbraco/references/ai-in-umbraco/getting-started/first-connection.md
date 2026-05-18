# The First Connection | AI in Umbraco

Create your first AI connection to start using AI services in Umbraco.

Prerequisites

Create a Connection

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-9491a9ac097a776545e8b3d306e9c8969d453c5a%252Fbackoffice-create-connection-modal.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b2707ca5&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-80c6ff0d1341fa70a9fb086053d1b3ce7fa92dc2%252Fbackoffice-create-connection-form.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=bcdb3ed3&sv=2)

Configure the Connection

| Field | Description | Example |
|---|---|---|
| Name | A display name for this connection | "OpenAI Production" |
| Alias | A unique identifier for programmatic access | "openai-prod" |
| Provider | The AI provider to use | "OpenAI" |
| API Key | Your provider API key | "sk-..." or "$OpenAI:ApiKey" |

Connection Properties

| Property | Description |
|---|---|
| `Id` | Unique GUID identifier |
| `Alias` | Unique string alias for lookups |
| `Name` | Display name |
| `ProviderId` | Which provider this connection uses |
| `Settings` | Provider-specific settings (API key, endpoint, and so on) |
| `IsActive` | Whether the connection is enabled |
| `Version` | Current version number, increments with each save |

Multiple Connections

Next Steps

Last updated

Was this helpful?