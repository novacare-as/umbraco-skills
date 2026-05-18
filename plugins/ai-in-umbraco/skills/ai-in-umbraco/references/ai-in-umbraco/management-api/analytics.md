# Analytics | AI in Umbraco

API endpoints for AI usage analytics and reporting.

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET |
| `/umbraco/ai/management/api/v1/analytics/usage-summary` |

`/umbraco/ai/management/api/v1/analytics/usage-time-series`

`/umbraco/ai/management/api/v1/analytics/usage-by-provider`

`/umbraco/ai/management/api/v1/analytics/usage-by-model`

`/umbraco/ai/management/api/v1/analytics/usage-by-profile`

`/umbraco/ai/management/api/v1/analytics/usage-by-user`

Base URL

```
/umbraco/ai/management/api/v1
```

Common Query Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `from` | datetime | Yes | Start of period (inclusive) |
| `to` | datetime | Yes | End of period (inclusive) |
| `granularity` | string | No | Data granularity: `hour` , `day` , `week` , `month` |

Analytics Concepts

Summary Metrics

| Metric | Description |
|---|---|
| `totalRequests` | Number of AI operations |
| `inputTokens` | Total tokens in requests |
| `outputTokens` | Total tokens in responses |
| `totalTokens` | Combined token count |
| `successCount` | Successful operations |
| `failureCount` | Failed operations |
| `successRate` | Success percentage (0.0-1.0) |
| `averageDurationMs` | Mean operation time in milliseconds |

Time Series

Breakdowns

Example: Dashboard Query

Related

Last updated

Was this helpful?

## Sub-topics

- [By Model | AI in Umbraco](analytics/breakdown-model.md)
- [By Profile | AI in Umbraco](analytics/breakdown-profile.md)
- [By Provider | AI in Umbraco](analytics/breakdown-provider.md)
- [By User | AI in Umbraco](analytics/breakdown-user.md)
- [Summary | AI in Umbraco](analytics/summary.md)
- [Time Series | AI in Umbraco](analytics/timeseries.md)
