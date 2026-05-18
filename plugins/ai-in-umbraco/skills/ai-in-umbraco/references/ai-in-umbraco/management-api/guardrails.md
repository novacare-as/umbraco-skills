# Guardrails | AI in Umbraco

API endpoints for managing AI guardrails.

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET |
| `/umbraco/ai/management/api/v1/guardrails` |

`/umbraco/ai/management/api/v1/guardrails/{guardrailIdOrAlias}`

`/umbraco/ai/management/api/v1/guardrails`

`/umbraco/ai/management/api/v1/guardrails/{guardrailIdOrAlias}`

`/umbraco/ai/management/api/v1/guardrails/{guardrailIdOrAlias}`

`/umbraco/ai/management/api/v1/guardrail-evaluators`

Base URL

```
/umbraco/ai/management/api/v1
```

Guardrail Object

```
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "alias": "content-safety",
    "name": "Content Safety Policy",
    "version": 2,
    "rules": [
        {
            "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "evaluatorId": "contains",
            "name": "Block competitor mentions",
            "phase": "PostGenerate",
            "action": "Block",
            "config": {
                "searchPattern": "CompetitorBrand",
                "ignoreCase": true
            },
            "sortOrder": 0
        },
        {
            "id": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
            "evaluatorId": "regex",
            "name": "Block SSNs in responses",
            "phase": "PostGenerate",
            "action": "Block",
            "config": {
                "pattern": "\\b\\d{3}-\\d{2}-\\d{4}\\b",
                "ignoreCase": false
            },
            "sortOrder": 1
        }
    ],
    "dateCreated": "2024-01-15T10:30:00Z",
    "dateModified": "2024-01-20T14:45:00Z"
}
```

Rule Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `evaluatorId` | string | Registered evaluator ID (e.g., "contains", "regex") |
| `name` | string | Display name |
| `phase` | string | `PreGenerate` or `PostGenerate` |
| `action` | string | `Block` , `Warn` , or `Redact` |
| `config` | object | Evaluator-specific configuration (nullable) |
| `sortOrder` | int | Controls evaluation order |

Related

Last updated

Was this helpful?

## Sub-topics

- [Create Guardrail | AI in Umbraco](guardrails/create.md)
- [Delete Guardrail | AI in Umbraco](guardrails/delete.md)
- [List Evaluators | AI in Umbraco](guardrails/evaluators.md)
- [Get Guardrail | AI in Umbraco](guardrails/get.md)
- [List Guardrails | AI in Umbraco](guardrails/list.md)
- [Update Guardrail | AI in Umbraco](guardrails/update.md)
