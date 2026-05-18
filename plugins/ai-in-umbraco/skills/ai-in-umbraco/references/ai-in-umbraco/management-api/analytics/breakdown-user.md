# By User | AI in Umbraco

Get usage breakdown by user.

Request

```
GET /umbraco/ai/management/api/v1/analytics/usage-by-user
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
        "dimension": "user-guid-1",
        "dimensionName": "[email protected]",
        "requestCount": 5200,
        "totalTokens": 1150000,
        "percentage": 0.31
    },
    {
        "dimension": "user-guid-2",
        "dimensionName": "[email protected]",
        "requestCount": 4100,
        "totalTokens": 920000,
        "percentage": 0.25
    },
    {
        "dimension": "",
        "dimensionName": "System/API",
        "requestCount": 3580,
        "totalTokens": 485000,
        "percentage": 0.21
    }
]
```

Examples

Response Properties

| Property | Type | Description |
|---|---|---|
| `dimension` | string | User ID (empty string for system/API calls) |
| `dimensionName` | string | User name (nullable) |
| `requestCount` | int | Number of requests |
| `totalTokens` | long | Total tokens used |
| `percentage` | double | Share of total requests (0.0-1.0) |

Notes

Use Cases

Last updated

Was this helpful?