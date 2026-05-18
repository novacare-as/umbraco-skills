# By Provider | AI in Umbraco

Get usage breakdown by AI provider.

Request

```
GET /umbraco/ai/management/api/v1/analytics/usage-by-provider
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
        "dimension": "openai",
        "dimensionName": "OpenAI",
        "requestCount": 12500,
        "totalTokens": 2850000,
        "percentage": 0.75
    },
    {
        "dimension": "anthropic",
        "dimensionName": "Anthropic",
        "requestCount": 3200,
        "totalTokens": 890000,
        "percentage": 0.19
    },
    {
        "dimension": "google",
        "dimensionName": "Google",
        "requestCount": 980,
        "totalTokens": 245000,
        "percentage": 0.06
    }
]
```

Examples

Response Properties

| Property | Type | Description |
|---|---|---|
| `dimension` | string | Provider ID |
| `dimensionName` | string | Provider display name |
| `requestCount` | int | Number of requests |
| `totalTokens` | long | Total tokens used |
| `percentage` | double | Share of total requests (0.0-1.0) |

Use Cases

Last updated

Was this helpful?