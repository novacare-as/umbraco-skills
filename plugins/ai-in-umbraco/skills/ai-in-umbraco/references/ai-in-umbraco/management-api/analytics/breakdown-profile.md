# By Profile | AI in Umbraco

Get usage breakdown by AI profile.

Request

```
GET /umbraco/ai/management/api/v1/analytics/usage-by-profile
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
        "dimension": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "dimensionName": "content-assistant",
        "requestCount": 9200,
        "totalTokens": 2100000,
        "percentage": 0.55
    },
    {
        "dimension": "d290f1ee-6c54-4b01-90e6-d701748f0851",
        "dimensionName": "translator",
        "requestCount": 4800,
        "totalTokens": 890000,
        "percentage": 0.29
    },
    {
        "dimension": "e401f2ff-7d65-5c12-a1f7-e812859a1962",
        "dimensionName": "search-embeddings",
        "requestCount": 2680,
        "totalTokens": 345000,
        "percentage": 0.16
    }
]
```

Examples

Response Properties

| Property | Type | Description |
|---|---|---|
| `dimension` | string | Profile ID |
| `dimensionName` | string | Profile alias |
| `requestCount` | int | Number of requests |
| `totalTokens` | long | Total tokens used |
| `percentage` | double | Share of total requests (0.0-1.0) |

Use Cases

Last updated

Was this helpful?