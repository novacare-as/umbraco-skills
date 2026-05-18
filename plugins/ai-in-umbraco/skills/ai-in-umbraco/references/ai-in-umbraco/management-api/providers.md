# Providers | AI in Umbraco

REST API endpoints for querying registered AI providers.

Overview

Base URL

```
/umbraco/ai/management/api/v1/providers
```

Authentication

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/umbraco/ai/management/api/v1/providers` |
|

`/umbraco/ai/management/api/v1/providers/{id}`

[Get provider details](/ai-in-umbraco/management-api/providers/get)Response Models

ProviderItemResponseModel

ProviderResponseModel

Settings Schema

| Property | Type | Description |
|---|---|---|
| `alias` | string | Setting identifier |
| `name` | string | Display name |
| `description` | string? | Help text |
| `type` | string | Data type (`string` , `number` , `boolean` ) |
| `isRequired` | bool | Whether the setting must be provided |
| `isSensitive` | bool | Whether to mask the value in UI |
| `defaultValue` | string? | Default value if not specified |
| `options` | string[]? | Valid options for selection |

In This Section

Last updated

Was this helpful?

## Sub-topics

- [Get Provider | AI in Umbraco](providers/get.md)
- [List Providers | AI in Umbraco](providers/list.md)
