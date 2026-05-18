# Version History | AI in Umbraco

View and restore previous versions of AI entities.

Viewing Version History

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-63d531a0722632addf790757c5b5f7b287347206%252Fbackoffice-version-history.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=53126ffa&sv=2)

| Column | Description |
|---|---|
| Version | Sequential version number |
| Date | When the version was created |
| User | Who made the change |
| Description | Change description (if provided) |

Comparing Versions

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-23d3d8049b9ea66b334fb648ac648b9c15493d48%252Fbackoffice-version-compare.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=97b19327&sv=2)

Reading the Comparison

Rolling Back

After Rollback

| Version | Description |
|---|---|
| 6 | Restored from version 3 |
| 5 | Previous state |
| 4 | ... |
| 3 | Target version |

Supported Entities

| Entity | Package | Location |
|---|---|---|
| Connections | Umbraco.AI | AI > Connections |
| Profiles | Umbraco.AI | AI > Profiles |
| Contexts | Umbraco.AI | AI > Contexts |
| Guardrails | Umbraco.AI | AI > Guardrails |
| Prompts | Umbraco.AI.Prompt | AI > Prompts |
| Agents | Umbraco.AI.Agent | AI > Agents |

Version Cleanup

Automatic Cleanup

| Property | Default | Description |
|---|---|---|
| `Enabled` | `true` | Whether automatic version cleanup is enabled |
| `MaxVersionsPerEntity` | `50` | Maximum versions to retain per entity (set to `0` to disable) |
| `RetentionDays` | `90` | Days to retain version history (set to `0` to disable) |

Manual Cleanup

Best Practices

Programmatic Access

Related

Last updated

Was this helpful?