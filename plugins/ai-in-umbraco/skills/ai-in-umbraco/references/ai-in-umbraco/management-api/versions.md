# Versions | AI in Umbraco

Unified API for accessing version history across all AI entities.

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET |
| `/umbraco/ai/management/api/v1/versions/supported-types` |

`/umbraco/ai/management/api/v1/versions/{entityType}/{entityId}`

`/umbraco/ai/management/api/v1/versions/{entityType}/{entityId}/{version}`

`/umbraco/ai/management/api/v1/versions/{entityType}/{entityId}/{from}/compare/{to}`

`/umbraco/ai/management/api/v1/versions/{entityType}/{entityId}/{version}/rollback`

Base URL

```
/umbraco/ai/management/api/v1
```

Supported Entity Types

| Entity Type | Package | Description |
|---|---|---|
| `connection` | Umbraco.AI | API connections and credentials |
| `profile` | Umbraco.AI | AI profile configurations |
| `context` | Umbraco.AI | Context resources and content |
| `prompt` | Umbraco.AI.Prompt | Prompt templates |
| `agent` | Umbraco.AI.Agent | Agent definitions |

Version Object

Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Version record identifier |
| `entityId` | guid | ID of the versioned entity |
| `entityType` | string | Type discriminator |
| `version` | int | Sequential version number |
| `dateCreated` | datetime | When this version was created |
| `createdByUserId` | guid | User who created this version |
| `changeDescription` | string | Optional description of changes |

Version Snapshots

Related

Last updated

Was this helpful?

## Sub-topics

- [Compare Versions | AI in Umbraco](versions/compare.md)
- [Get Version | AI in Umbraco](versions/get-version.md)
- [Get History | AI in Umbraco](versions/history.md)
- [Rollback | AI in Umbraco](versions/rollback.md)
- [Supported Types | AI in Umbraco](versions/supported-types.md)
