# Managing Profiles | AI in Umbraco

Create and manage AI profiles in the Umbraco backoffice.

Viewing Profiles

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-c69e80841d8a7ecb1477699299090ea287a675d7%252Fbackoffice-profiles-list.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=66923f03&sv=2)

Creating a Profile

| Field | Description |
|---|---|
| Name | Display name for the profile |
| Alias | Unique identifier (used in code and as default) |
| Capability | Type of AI operation (Chat, Embedding, Speech-to-Text) |
| Connection | Which connection to use |
| Model | The specific AI model |

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-2a048e114912c748b6d0e65f115296199199e084%252Fbackoffice-create-profile-modal.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3d84cf60&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-c42585c287348e52ecca1b825a9b0ebe93a544b4%252Fbackoffice-create-profile-form.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8f90c70e&sv=2)

Chat Profile Settings

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-2cc632ee01333695d73aee182a07a6a195b79829%252Fbackoffice-chat-profile-settings.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a016f5c8&sv=2)

| Setting | Description | Default |
|---|---|---|
| Temperature | Controls randomness (0-2). Lower = more focused, higher = more creative | Model default |
| Max Tokens | Maximum tokens in the response | Model default |
| System Prompt | Instructions sent with every request | None |

Temperature Guidelines

| Value | Best For |
|---|---|
| 0.0 - 0.3 | Factual responses, code generation, data extraction |
| 0.4 - 0.7 | Balanced responses, general assistance |
| 0.8 - 1.2 | Creative writing, brainstorming |

System Prompts

Embedding Profile Settings

| Model | Dimensions | Best For |
|---|---|---|
| text-embedding-3-small | 1536 | Cost-effective, general purpose |
| text-embedding-3-large | 3072 | Higher accuracy, more storage |

Speech-to-Text Profile Settings

| Setting | Description | Default |
|---|---|---|
| Language | Optional BCP-47 language hint for transcription (for example, `en` , `de` , `ja` ). | Model default |

Governance

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-06488dc8877825ad6a062bde982fe234244d8429%252Fbackoffice-profile-governance-tab.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=980f2a8c&sv=2)

Setting Default Profiles

Editing a Profile

Deleting a Profile

Using Tags

Related

Last updated

Was this helpful?