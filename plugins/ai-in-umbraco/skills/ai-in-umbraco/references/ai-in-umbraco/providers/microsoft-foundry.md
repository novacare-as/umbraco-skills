# Microsoft AI Foundry | AI in Umbraco

Configure Microsoft AI Foundry as an AI provider for chat and embedding capabilities.

Installation

```
Install-Package Umbraco.AI.MicrosoftFoundry
```

```
dotnet add package Umbraco.AI.MicrosoftFoundry
```

Connection Settings

Entra ID Authentication (Recommended)

| Setting | Required | Description |
|---|---|---|
| Endpoint | Yes | Your AI Foundry endpoint URL |
| Project Name | No | AI Foundry project name (enables deployed model listing) |
| Tenant ID | No | Microsoft Entra ID tenant ID |
| Client ID | No | Service principal application (client) ID |
| Client Secret | No | Service principal secret |

API Key Authentication (Legacy)

| Setting | Required | Description |
|---|---|---|
| Endpoint | Yes | Your AI Foundry endpoint URL |
| API Key | Yes | Your AI Foundry API key |

Advanced Settings

| Setting | Required | Description |
|---|---|---|
| Use Responses API | No | When enabled, uses the OpenAI Responses API instead of Chat Completions. Only available in certain Azure regions. |

Getting Your Credentials

For Entra ID

For API Key

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-590e839a47644330ef6f9974a99dc777a0204cd9%252Fmicrosoft-foundry-create-connection.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=481ff984&sv=2)

Related

Last updated

Was this helpful?