# The First Profile | AI in Umbraco

Create a profile to configure how AI requests are made and use it in your code.

Prerequisites

Create a Profile

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-2a048e114912c748b6d0e65f115296199199e084%252Fbackoffice-create-profile-modal.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3d84cf60&sv=2)

Configure the Profile

| Field | Description | Example |
|---|---|---|
| Name | A display name for this profile | "Content Assistant" |
| Alias | A unique identifier for lookups | "content-assistant" |
| Capability | The type of AI capability | "Chat" |
| Connection | Which connection to use | "OpenAI Production" |
| Model | The specific model to use | "gpt-4o" |

Chat Settings

| Setting | Description | Default |
|---|---|---|
| Temperature | Controls randomness (0-2). Lower is more focused. | Provider default |
| Max Tokens | Maximum tokens in the response | Provider default |
| System Prompt | Instructions sent with every request | None |

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-c42585c287348e52ecca1b825a9b0ebe93a544b4%252Fbackoffice-create-profile-form.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8f90c70e&sv=2)

Set as Default

Use the Profile in Code

Using the Default Profile

Using a Specific Profile

Understanding Profile Resolution

Multiple Profiles

| Profile | Use Case | Model | Temperature |
|---|---|---|---|
| `content-assistant` | Content suggestions | gpt-4o | 0.7 |
| `code-helper` | Code generation | gpt-4o | 0.2 |
| `translator` | Translation | gpt-4o-mini | 0.3 |

Next Steps

Last updated

Was this helpful?