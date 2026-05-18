# Usage Analytics | AI in Umbraco

Understand AI usage patterns with the analytics dashboard.

Accessing Analytics

Dashboard Overview

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-03cba8dbc7fd2e9f8a233f36cd3f3f5ae65eaff4%252Fbackoffice-analytics-dashboard.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=27cf5e96&sv=2)

Summary Metrics

| Metric | Description |
|---|---|
| Total Requests | Number of AI operations in the selected period |
| Input Tokens | Tokens sent to AI providers |
| Output Tokens | Tokens received from AI providers |
| Total Tokens | Combined input and output tokens |
| Success Rate | Percentage of successful operations |
| Avg Duration | Average operation response time |

Usage Over Time

Breakdowns

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-57f460ac3b5947e24aea2f910fe8dce8bf49a18a%252Fbackoffice-analytics-breakdowns.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3f2e78a3&sv=2)

Date Range

| Range | Description |
|---|---|
| Last 24 Hours | Real-time monitoring |
| Last 7 Days | Weekly trends |
| Last 30 Days | Monthly analysis |

Programmatic Access

Configuration

| Property | Default | Description |
|---|---|---|
| `Enabled` | `true` | Whether usage analytics is enabled |
| `UsageHourlyRetentionDays` | `30` | Retention period for hourly aggregated statistics (valid: 30-90) |
| `UsageDailyRetentionDays` | `365` | Retention period for daily aggregated statistics |
| `IncludeUsageUserDimension` | `true` | Include user ID as a dimension in aggregations (privacy consideration) |
| `IncludeUsageEntityTypeDimension` | `true` | Include entity type (for example, `content` , `media` ) as a dimension |
| `IncludeUsageFeatureTypeDimension` | `true` | Include feature type (for example, `prompt` , `agent` ) as a dimension |

Related

Last updated

Was this helpful?