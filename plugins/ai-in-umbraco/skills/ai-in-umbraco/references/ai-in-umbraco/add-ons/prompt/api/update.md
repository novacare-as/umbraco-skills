# Update | AI in Umbraco

Update an existing prompt.

Request

```
PUT /umbraco/ai/management/api/v1/prompts/{idOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `idOrAlias` | string | Prompt GUID or alias |

Request Body

```
{
    "alias": "meta-description",
    "name": "Generate Meta Description (Updated)",
    "description": "Creates SEO-friendly meta descriptions for web pages",
    "instructions": "Write a compelling meta description...",
    "profileId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "contextIds": ["e401f2ff-7d65-5c12-a1f7-e812859a1962"],
    "guardrailIds": [],
    "tags": ["seo", "content", "updated"],
    "isActive": true,
    "includeEntityContext": true,
    "optionCount": 1,
    "displayMode": "PropertyAction",
    "scope": {
        "allowRules": [
            {
                "contentTypeAliases": ["article", "blogPost"]
            }
        ],
        "denyRules": []
    }
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `alias` | string | Yes | Unique alias (letters, numbers, hyphens and underscores only, max 100) |
| `name` | string | Yes | Display name (max 255) |
| `instructions` | string | Yes | Prompt template text |
| `description` | string | No | Optional description (max 1000) |
| `profileId` | guid | No | Associated AI profile |
| `contextIds` | guid[] | No | AI Contexts to inject |
| `guardrailIds` | guid[] | No | Guardrails evaluated during execution |
| `tags` | string[] | No | Organization tags |
| `isActive` | bool | No | Whether the prompt is available (default: `true` ) |
| `includeEntityContext` | bool | No | Include entity in system message (default: `true` ) |
| `optionCount` | int | No | Number of result options: 0 = informational, 1 = single (default), 2+ = options |
| `displayMode` | string | No | `PropertyAction` (default) or `TipTapTool` |
| `scope` | object | No | Scope rules (allow/deny) defining where the prompt can run |

Response

Success

Not Found

Examples

Last updated

Was this helpful?