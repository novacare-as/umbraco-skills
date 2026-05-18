# Get Provider | AI in Umbraco

Get detailed information about a specific AI provider.

Request

```
GET /umbraco/ai/management/api/v1/providers/{id}
```

Headers

| Header | Value |
|---|---|
| `Authorization` | Bearer token or cookie |

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `id` | string | The provider's unique identifier |

Response

Success (200 OK)

```
{
    "id": "openai",
    "name": "OpenAI",
    "capabilities": ["Chat", "Embedding"],
    "settingsSchema": {
        "fields": [
            {
                "key": "apiKey",
                "label": "API Key",
                "description": "Your OpenAI API key from platform.openai.com",
                "editorUiAlias": "Umb.PropertyEditorUi.TextBox",
                "defaultValue": null,
                "sortOrder": 0,
                "isRequired": true
            },
            {
                "key": "organizationId",
                "label": "Organization ID",
                "description": "Optional organization identifier",
                "editorUiAlias": "Umb.PropertyEditorUi.TextBox",
                "defaultValue": null,
                "sortOrder": 1,
                "isRequired": false
            },
            {
                "key": "baseUrl",
                "label": "Base URL",
                "description": "Custom API endpoint (for proxies)",
                "editorUiAlias": "Umb.PropertyEditorUi.TextBox",
                "defaultValue": "https://api.openai.com/v1",
                "sortOrder": 2,
                "isRequired": false
            }
        ]
    }
}
```

Response Properties

| Property | Type | Description |
|---|---|---|
| `id` | string | Unique provider identifier |
| `name` | string | Display name |
| `capabilities` | string[] | Supported capabilities |
| `settingsSchema` | object | Settings schema (nullable if provider has no settings) |

Settings Schema Field Properties

| Property | Type | Description |
|---|---|---|
| `key` | string | Unique key identifying the setting |
| `label` | string | Display label for the setting |
| `description` | string | Help text for the setting |
| `editorUiAlias` | string | UI alias of the editor used for the setting |
| `editorConfig` | object | Configuration for the editor |
| `defaultValue` | object | Default value for the setting |
| `sortOrder` | int | Sort order of the setting in the UI |
| `isRequired` | boolean | Whether the setting must be provided |
| `group` | string | Optional group name for visual grouping in the UI |

Not Found (404)

Example

cURL

C# HttpClient

JavaScript

Use Cases

Building Connection Forms

Validating Connection Settings

Notes

Last updated

Was this helpful?