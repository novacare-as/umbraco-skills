# List Audit Logs | AI in Umbraco

List audit logs with filtering and pagination.

Request

```
GET /umbraco/ai/management/api/v1/audit-logs
```

Query Parameters

| Parameter | Type | Default | Description |
|---|---|---|---|
| `status` | string | null | Filter by status (Running, Succeeded, Failed) |
| `userId` | string | null | Filter by user ID |
| `profileId` | guid | null | Filter by profile |
| `providerId` | string | null | Filter by provider |
| `entityId` | string | null | Filter by entity ID |
| `fromDate` | datetime | null | Filter by start date (inclusive) |
| `toDate` | datetime | null | Filter by end date (inclusive) |
| `searchText` | string | null | Search text across multiple fields |
| `skip` | int | 0 | Number of records to skip |
| `take` | int | 100 | Number of records to return |

Response

Success

Item Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `startTime` | datetime | When the operation started |
| `durationMs` | long | Operation duration in milliseconds |
| `status` | string | Operation status |
| `userId` | string | User who initiated the operation |
| `userName` | string | User display name |
| `entityId` | string | ID of content/item being processed |
| `capability` | string | AI capability used |
| `profileId` | string | Profile used |
| `profileAlias` | string | Profile alias at time of operation |
| `profileVersion` | int | Profile version at time of operation |
| `providerId` | string | Provider used |
| `modelId` | string | Model used |
| `featureType` | string | Feature type (prompt, agent) if applicable |
| `featureId` | guid | Feature ID if applicable |
| `featureVersion` | int | Feature version if applicable |
| `parentAuditLogId` | guid | Parent operation ID for nested operations |
| `inputTokens` | int | Tokens in the request |
| `outputTokens` | int | Tokens in the response |
| `errorMessage` | string | Error details if failed |

Examples

Basic List

Filtered by Date Range

Filtered by Status

Multiple Filters

Notes

Last updated

Was this helpful?