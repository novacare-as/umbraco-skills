# Compare Versions | AI in Umbraco

Compare two versions of an entity.

Request

```
GET /umbraco/ai/management/api/v1/versions/{entityType}/{entityId}/{fromEntityVersion}/compare/{toEntityVersion}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `entityType` | string | Entity type (`connection` , `profile` , `context` , `prompt` , `agent` ) |
| `entityId` | guid | Entity unique identifier |
| `fromEntityVersion` | int | Source version number |
| `toEntityVersion` | int | Target version number |

Response

Success

```
{
    "fromVersion": 2,
    "toVersion": 5,
    "changes": [
        {
            "path": "settings.temperature",
            "oldValue": "0.5",
            "newValue": "0.8"
        },
        {
            "path": "settings.systemPromptTemplate",
            "oldValue": "You are an assistant.",
            "newValue": "You are a helpful content assistant for a website."
        },
        {
            "path": "tags[1]",
            "oldValue": null,
            "newValue": "content"
        }
    ]
}
```

Not Found

Examples

Response Properties

| Property | Type | Description |
|---|---|---|
| `fromVersion` | int | Source version number |
| `toVersion` | int | Target version number |
| `changes` | array | List of detected value changes |

Value Change Properties

| Property | Type | Description |
|---|---|---|
| `path` | string | The path of the value that changed |
| `oldValue` | string | The old value (from the source version) |
| `newValue` | string | The new value (from the target version) |

Last updated

Was this helpful?