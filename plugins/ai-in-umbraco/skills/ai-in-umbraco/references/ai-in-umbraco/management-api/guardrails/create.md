# Create Guardrail | AI in Umbraco

Create a new AI guardrail.

Request

```
POST /umbraco/ai/management/api/v1/guardrails
```

Request Body

```
{
    "alias": "content-safety",
    "name": "Content Safety Policy",
    "rules": [
        {
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
    ]
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `alias` | string | Yes | Unique alias (URL-safe) |
| `name` | string | Yes | Display name |
| `rules` | array | No | Collection of rules |

Rule Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `evaluatorId` | string | Yes | Registered evaluator ID (e.g., "contains") |
| `name` | string | Yes | Display name |
| `phase` | string | Yes | `PreGenerate` or `PostGenerate` |
| `action` | string | Yes | `Block` , `Warn` , or `Redact` |
| `config` | object | No | Evaluator-specific configuration |
| `sortOrder` | int | No | Evaluation order (default: 0) |

Response

Success

Validation Error

Examples

Last updated

Was this helpful?