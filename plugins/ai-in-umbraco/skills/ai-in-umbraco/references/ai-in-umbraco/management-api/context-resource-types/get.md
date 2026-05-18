# Get Resource Type | AI in Umbraco

Get a context resource type with its settings schema.

Endpoint

```
GET /umbraco/ai/management/api/v1/context-resource-types/{id}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `id` | string | The resource type identifier |

Response

Success (200 OK)

```
{
    "id": "document",
    "name": "Document",
    "description": "Adds content items as context resources.",
    "icon": "icon-document",
    "settingsSchema": {
        "fields": [
            {
                "key": "contentId",
                "label": "Content",
                "description": "The unique identifier of the content item.",
                "editorUiAlias": "Umb.PropertyEditorUi.DocumentPicker",
                "defaultValue": null,
                "sortOrder": 0,
                "isRequired": true
            },
            {
                "key": "includeDescendants",
                "label": "Include Descendants",
                "description": "Whether to include descendant content items.",
                "editorUiAlias": "Umb.PropertyEditorUi.Toggle",
                "defaultValue": false,
                "sortOrder": 1,
                "isRequired": false
            }
        ]
    }
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `id` | string | Unique identifier for the type |
| `name` | string | Display name |
| `description` | string | Description of the resource type |
| `icon` | string | Icon identifier for the backoffice UI |
| `settingsSchema` | object | Settings schema (nullable if type has no settings) |

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

Examples

Get a Resource Type

JavaScript

Last updated

Was this helpful?