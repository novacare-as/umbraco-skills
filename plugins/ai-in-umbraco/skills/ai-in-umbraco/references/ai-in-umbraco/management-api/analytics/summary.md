# Summary | AI in Umbraco

Get aggregated usage summary for a time period.

Request

```
GET /umbraco/ai/management/api/v1/analytics/usage-summary
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
{
    "totalRequests": 15420,
    "inputTokens": 2450000,
    "outputTokens": 890000,
    "totalTokens": 3340000,
    "successCount": 15210,
    "failureCount": 210,
    "successRate": 0.9864,
    "averageDurationMs": 1245
}
```

Examples

Last 30 Days Summary

With Explicit Granularity

Response Properties

| Property | Type | Description |
|---|---|---|
| `totalRequests` | int | Number of AI operations in the period |
| `inputTokens` | long | Total tokens sent in requests |
| `outputTokens` | long | Total tokens received in responses |
| `totalTokens` | long | Combined input and output tokens |
| `successCount` | int | Number of successful operations |
| `failureCount` | int | Number of failed operations |
| `successRate` | double | Success rate (0.0 to 1.0) |
| `averageDurationMs` | int | Average operation time in milliseconds |

Notes

Last updated

Was this helpful?