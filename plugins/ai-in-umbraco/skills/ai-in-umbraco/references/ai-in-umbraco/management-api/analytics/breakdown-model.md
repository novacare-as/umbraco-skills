# By Model | AI in Umbraco

Get usage breakdown by AI model.

Request

```
GET /umbraco/ai/management/api/v1/analytics/usage-by-model
```

Query Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `from` | datetime | Yes | Start of period (inclusive) |
| `to` | datetime | Yes | End of period (exclusive) |
| `granularity` | string | No | Aggregation granularity: `Hourly` or `Daily` (auto-selected if omitted) |

Response

Success

```
[
    {
        "dimension": "openai/gpt-4o",
        "dimensionName": null,
        "requestCount": 8500,
        "totalTokens": 1950000,
        "percentage": 0.51
    },
    {
        "dimension": "openai/gpt-4o-mini",
        "dimensionName": null,
        "requestCount": 4000,
        "totalTokens": 520000,
        "percentage": 0.24
    },
    {
        "dimension": "anthropic/claude-3-5-sonnet-20241022",
        "dimensionName": null,
        "requestCount": 3200,
        "totalTokens": 890000,
        "percentage": 0.19
    }
]
```

Examples

Response Properties

| Property | Type | Description |
|---|---|---|
| `dimension` | string | Model reference (`providerId/modelId` ) |
| `dimensionName` | string | Model display name |
| `requestCount` | int | Number of requests |
| `totalTokens` | long | Total tokens used |
| `percentage` | double | Share of total requests (0.0-1.0) |

Use Cases

Last updated

Was this helpful?