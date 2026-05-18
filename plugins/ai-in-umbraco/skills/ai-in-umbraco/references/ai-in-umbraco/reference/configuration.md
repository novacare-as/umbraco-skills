# Configuration | AI in Umbraco

Configuration options for Umbraco.AI.

Default Profiles

```
{
    "Umbraco": {
        "AI": {
            "DefaultChatProfileAlias": "default-chat",
            "DefaultEmbeddingProfileAlias": "default-embedding"
        }
    }
}
```

Available Options

| Class | Section | Description |
|---|---|---|
|

`Umbraco:AI`

`AIAuditLogOptions`

`Umbraco:AI:AuditLog`

`AIAnalyticsOptions`

`Umbraco:AI:Analytics`

`AIVersionCleanupPolicy`

`Umbraco:AI:VersionCleanupPolicy`

`AIMediaOptions`

`Umbraco:AI:Media`

`AIWebFetchOptions`

`Umbraco:AI:Tools:WebFetch`

`AIAgentOptions`

`Umbraco:AI:Agent`

Media

| Property | Type | Default | Description |
|---|---|---|---|
| `AutoDownscale` | `bool` | `true` | Automatically downscale oversized images before sending to providers |
| `MaxSizeBytes` | `long` | `4194304` | Maximum image payload size in bytes (4 MB) before re-encoding |
| `MaxDimension` | `int` | `2048` | Maximum pixel dimension (longest edge) before proportional resizing |
| `JpegQuality` | `int` | `85` | JPEG quality (1-100) used when re-encoding oversized images |

Web Fetch Tool

| Property | Type | Default | Description |
|---|---|---|---|
| `Enabled` | `bool` | `true` | Whether the web fetch tool is enabled |
| `MaxResponseSizeBytes` | `long` | `5242880` | Maximum response size in bytes (5 MB) |
| `TimeoutSeconds` | `int` | `30` | Request timeout in seconds |
| `MaxRedirects` | `int` | `5` | Maximum number of redirects to follow |
| `AllowedDomains` | `List<string>` | `[]` | Domain allow list (empty means no allow list filtering) |
| `BlockedDomains` | `List<string>` | `[]` | Domain block list (blocks specific domains even if allowed) |
| `EnableCaching` | `bool` | `true` | Whether fetched content is cached |
| `CacheDurationMinutes` | `int` | `60` | Cache duration in minutes |

Agent

| Property | Type | Default | Description |
|---|---|---|---|
| `FileRetentionHours` | `int` | `24` | Retention period (in hours) for uploaded file attachments on agent threads |

Provider Credentials

Environment-Specific Configuration

Related

In This Section

Last updated

Was this helpful?

## Sub-topics

- [AIOptions | AI in Umbraco](configuration/ai-options.md)
