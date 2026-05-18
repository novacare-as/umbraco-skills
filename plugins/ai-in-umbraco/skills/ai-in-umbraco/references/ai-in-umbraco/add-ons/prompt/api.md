# API | AI in Umbraco

Management API endpoints for Prompt add-on.

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET |
| `/prompts` |

`/prompts/{idOrAlias}`

`/prompts/{alias}/exists`

`/prompts`

`/prompts/{idOrAlias}`

`/prompts/{idOrAlias}`

`/prompts/{idOrAlias}/execute`

Base URL

```
/umbraco/ai/management/api/v1
```

Prompt Object

```
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "alias": "meta-description",
    "name": "Generate Meta Description",
    "description": "Creates SEO-friendly meta descriptions",
    "instructions": "Write a meta description for:\n\nTitle: {{pageTitle}}\nContent: {{bodyText}}",
    "profileId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "contextIds": ["e401f2ff-7d65-5c12-a1f7-e812859a1962"],
    "guardrailIds": [],
    "tags": ["seo", "content"],
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
    },
    "version": 3,
    "dateCreated": "2024-01-15T10:30:00Z",
    "dateModified": "2024-01-20T14:45:00Z"
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `alias` | string | Unique alias for code references |
| `name` | string | Display name |
| `description` | string | Optional description |
| `instructions` | string | Prompt template with variables |
| `profileId` | guid | Associated AI profile (optional) |
| `contextIds` | guid[] | AI Contexts to inject |
| `guardrailIds` | guid[] | Guardrails evaluated during execution |
| `tags` | string[] | Organization tags |
| `isActive` | bool | Whether the prompt is available |
| `includeEntityContext` | bool | Include entity in system message |
| `optionCount` | int | Number of result options (0 = informational, 1 = single, 2+) |
| `displayMode` | string | `PropertyAction` or `TipTapTool` |
| `scope` | object | Scope rules (allow/deny) defining where the prompt can run |
| `version` | int | Current version number |
| `dateCreated` | string | Creation timestamp (UTC) |
| `dateModified` | string | Last modification timestamp (UTC) |

Related

Last updated

Was this helpful?

## Sub-topics

- [Check Alias Exists | AI in Umbraco](api/alias-exists.md)
- [Create | AI in Umbraco](api/create.md)
- [Delete | AI in Umbraco](api/delete.md)
- [Execute | AI in Umbraco](api/execute.md)
- [Get | AI in Umbraco](api/get.md)
- [List | AI in Umbraco](api/list.md)
- [Update | AI in Umbraco](api/update.md)
