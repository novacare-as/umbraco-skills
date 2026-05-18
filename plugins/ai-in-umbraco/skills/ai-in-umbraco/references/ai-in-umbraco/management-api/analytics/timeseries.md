# Time Series | AI in Umbraco

Get usage metrics over time.

Request

```
GET /umbraco/ai/management/api/v1/analytics/usage-time-series
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
        "timestamp": "2024-01-01T00:00:00Z",
        "requestCount": 520,
        "totalTokens": 117000,
        "inputTokens": 85000,
        "outputTokens": 32000,
        "successCount": 515,
        "failureCount": 5
    },
    {
        "timestamp": "2024-01-02T00:00:00Z",
        "requestCount": 612,
        "totalTokens": 139000,
        "inputTokens": 98000,
        "outputTokens": 41000,
        "successCount": 608,
        "failureCount": 4
    }
]
```

Examples

Daily Usage for Last Week

Hourly Usage for Today

Response Properties

Time Series Point

| Property | Type | Description |
|---|---|---|
| `timestamp` | datetime | Start of the time interval |
| `requestCount` | int | Number of requests in this interval |
| `totalTokens` | long | Total tokens in this interval |
| `inputTokens` | long | Input tokens in this interval |
| `outputTokens` | long | Output tokens in this interval |
| `successCount` | int | Successful requests |
| `failureCount` | int | Failed requests |

Granularity Options

| Value | Description | Best For |
|---|---|---|
| `Hourly` | Hourly intervals | Last 24-48 hours |
| `Daily` | Daily intervals | Last 7-30 days |

Last updated

Was this helpful?