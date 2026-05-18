# Managing Settings | AI in Umbraco

Configure global AI settings in the Umbraco backoffice.

Accessing Settings

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-8c376b5e753e36ce547bf6c334b5822a02196e98%252Fbackoffice-ai-settings-page.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fc5a895c&sv=2)

Available Settings

Default Chat Profile

| Field | Description |
|---|---|
| Default Chat Profile | Select from available chat profiles |

Classifier Chat Profile

| Field | Description |
|---|---|
| Classifier Chat Profile | Select from available chat profiles |

Default Embedding Profile

| Field | Description |
|---|---|
| Default Embedding Profile | Select from available embedding profiles |

Default Speech-to-Text Profile

| Field | Description |
|---|---|
| Default Speech-to-Text Profile | Select from available speech-to-text profiles |

Configuring Settings

Settings Precedence

When Defaults Are Used

| Scenario | Default Used |
|---|---|
| `_chatService.GetChatResponseAsync(chat => chat.WithAlias("my-feature"), messages)` | Yes |
| `_chatService.GetChatResponseAsync(chat => chat.WithAlias("my-feature").WithProfile(profileId), messages)` | No (explicit) |
| Prompt without ProfileId | Yes |
| Prompt with ProfileId | No (explicit) |
| Agent without ProfileId | Yes |
| Agent with ProfileId | No (explicit) |

Clearing Defaults

Related

Last updated

Was this helpful?