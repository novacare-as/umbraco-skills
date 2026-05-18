# AIAuditLog | AI in Umbraco

Model representing an AI operation audit log entry.

Namespace

```
using Umbraco.AI.Core.AuditLog;
```

Definition

```
public sealed class AIAuditLog
{
    public Guid Id { get; internal set; }

    // Timing
    public DateTime StartTime { get; init; }
    public DateTime? EndTime { get; set; }
    public TimeSpan? Duration => EndTime.HasValue ? EndTime.Value - StartTime : null;

    // Status
    public AIAuditLogStatus Status { get; set; }
    public AIAuditLogErrorCategory? ErrorCategory { get; set; }
    public string? ErrorMessage { get; set; }

    // User context
    public string? UserId { get; init; }
    public string? UserName { get; init; }

    // Entity context (content being processed)
    public string? EntityId { get; init; }
    public string? EntityType { get; init; }

    // AI configuration
    public AICapability Capability { get; init; }
    public Guid ProfileId { get; init; }
    public string ProfileAlias { get; init; } = string.Empty;
    public int? ProfileVersion { get; init; }
    public string ProviderId { get; init; } = string.Empty;
    public string ModelId { get; init; } = string.Empty;

    // Feature context (prompt or agent)
    public string? FeatureType { get; init; }
    public Guid? FeatureId { get; init; }
    public int? FeatureVersion { get; init; }

    // Token usage
    public int? InputTokens { get; set; }
    public int? OutputTokens { get; set; }
    public int? TotalTokens { get; set; }

    // Content snapshots (if configured to persist)
    public string? PromptSnapshot { get; set; }
    public string? ResponseSnapshot { get; set; }

    // Tracing
    public string? TraceId { get; set; }

    // Relationships
    public Guid? ParentAuditLogId { get; internal set; }
    public IReadOnlyDictionary<string, string>? Metadata { get; init; }
}
```

Properties

Core Properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Unique identifier |
| `StartTime` | `DateTime` | When operation started |
| `EndTime` | `DateTime?` | When operation completed |
| `Duration` | `TimeSpan?` | Computed duration |

Status Properties

| Property | Type | Description |
|---|---|---|
| `Status` | `AIAuditLogStatus` | Operation outcome |
| `ErrorCategory` | `AIAuditLogErrorCategory?` | Error classification |
| `ErrorMessage` | `string?` | Error details |

Context Properties

| Property | Type | Description |
|---|---|---|
| `UserId` | `string?` | User who initiated |
| `UserName` | `string?` | User display name |
| `EntityId` | `string?` | Content item ID |
| `EntityType` | `string?` | Content item type |

AI Configuration

| Property | Type | Description |
|---|---|---|
| `Capability` | `AICapability` | Chat, Embedding, etc. |
| `ProfileId` | `Guid` | Profile used |
| `ProfileAlias` | `string` | Profile alias at time |
| `ProfileVersion` | `int?` | Profile version at time |
| `ProviderId` | `string` | Provider ID |
| `ModelId` | `string` | Model ID |

Feature Context

| Property | Type | Description |
|---|---|---|
| `FeatureType` | `string?` | "prompt", "agent", or null |
| `FeatureId` | `Guid?` | Feature ID |
| `FeatureVersion` | `int?` | Feature version at time |

Token Usage

| Property | Type | Description |
|---|---|---|
| `InputTokens` | `int?` | Tokens in request |
| `OutputTokens` | `int?` | Tokens in response |
| `TotalTokens` | `int?` | Combined tokens |

Content Snapshots

| Property | Type | Description |
|---|---|---|
| `PromptSnapshot` | `string?` | Request content (if configured to persist) |
| `ResponseSnapshot` | `string?` | Response content (if configured to persist) |

AIAuditLogStatus

AIAuditLogErrorCategory

AIAuditLogFilter

Related

Last updated

Was this helpful?