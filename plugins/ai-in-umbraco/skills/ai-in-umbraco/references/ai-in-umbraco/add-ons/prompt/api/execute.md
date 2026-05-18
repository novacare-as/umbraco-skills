# Execute | AI in Umbraco

Execute a prompt template.

Request

```
POST /umbraco/ai/management/api/v1/prompts/{idOrAlias}/execute
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `idOrAlias` | string | Prompt GUID or alias |

Request Body

```
{
    "entityId": "8c9a4e8f-2e89-4b3e-9a6f-1c2d3e4f5a6b",
    "entityType": "document",
    "propertyAlias": "metaDescription",
    "contentTypeAlias": "article",
    "culture": "en-US",
    "context": [
        {
            "description": "Currently editing: How to Bake Sourdough Bread",
            "value": "{\"documentName\":\"How to Bake Sourdough Bread\"}"
        }
    ]
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `entityId` | guid | Yes | The entity (document, media, etc.) key. Used for scope validation and entity context lookup. |
| `entityType` | string | Yes | The entity type (for example `document` or `media` ). |
| `propertyAlias` | string | Yes | The property alias being edited. |
| `contentTypeAlias` | string | Yes | The content type alias (or the element type alias when editing a block). |
| `elementId` | guid | No | Block content key when executing inside a block element. `entityId` then refers to the parent document. |
| `elementType` | string | No | Element type identifier when executing inside a block element. |
| `culture` | string | No | Culture/language variant (for example `en-US` ). |
| `segment` | string | No | Segment variant. |
| `context` | object[] | No | Flexible context items. Each item has `description` (required) and `value` (optional JSON string). |

Response

Success

Response Properties

| Property | Type | Description |
|---|---|---|
| `content` | string | The generated response content. |
| `usage` | object | Token usage information (may be omitted if the provider does not report usage). |
| `resultOptions` | object[] | Available result options. Empty for informational prompts, a single entry for single-value prompts, multiple entries when the prompt is configured to generate options. |

| Property | Type | Description |
|---|---|---|
| `label` | string | Short label/title for the option. |
| `displayValue` | string | Value displayed in the UI. |
| `description` | string | Optional explanation for the option. |
| `valueChange` | object | The change to apply when the option is selected. `null` for informational options. |

Not Found

Execution Failure

Examples

Last updated

Was this helpful?