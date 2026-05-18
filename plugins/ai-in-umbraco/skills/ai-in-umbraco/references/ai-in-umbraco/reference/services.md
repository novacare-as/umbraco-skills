# Services

## Contents

- [IAIAuditLogService | AI in Umbraco](#iaiauditlogservice-ai-in-umbraco)
- [IAIChatService | AI in Umbraco](#iaichatservice-ai-in-umbraco)
- [IAIConnectionService | AI in Umbraco](#iaiconnectionservice-ai-in-umbraco)
- [IAIContextService | AI in Umbraco](#iaicontextservice-ai-in-umbraco)
- [IAIEmbeddingService | AI in Umbraco](#iaiembeddingservice-ai-in-umbraco)
- [IAIEntityVersionService | AI in Umbraco](#iaientityversionservice-ai-in-umbraco)
- [IAIGuardrailService | AI in Umbraco](#iaiguardrailservice-ai-in-umbraco)
- [IAIProfileService | AI in Umbraco](#iaiprofileservice-ai-in-umbraco)
- [IAISettingsService | AI in Umbraco](#iaisettingsservice-ai-in-umbraco)
- [IAIUsageAnalyticsService | AI in Umbraco](#iaiusageanalyticsservice-ai-in-umbraco)

---

## IAIAuditLogService | AI in Umbraco

Service for AI operation audit logging.

Namespace

```
using Umbraco.AI.Core.AuditLog;
```

Interface

```
public interface IAIAuditLogService
{
    // Recording methods (used internally by AI services)
    Task<AIAuditLog> StartAuditLogAsync(AIAuditLog auditLog, CancellationToken ct = default);
    Task CompleteAuditLogAsync(AIAuditLog audit, AIAuditPrompt? prompt, AIAuditResponse? response, CancellationToken ct = default);
    Task RecordAuditLogFailureAsync(AIAuditLog audit, AIAuditPrompt? prompt, Exception exception, CancellationToken ct = default);

    // Fire-and-forget variants (non-blocking)
    ValueTask QueueStartAuditLogAsync(AIAuditLog auditLog, CancellationToken ct = default);
    ValueTask QueueCompleteAuditLogAsync(AIAuditLog audit, AIAuditPrompt? prompt, AIAuditResponse? response, CancellationToken ct = default);
    ValueTask QueueRecordAuditLogFailureAsync(AIAuditLog audit, AIAuditPrompt? prompt, Exception exception, CancellationToken ct = default);

    // Query methods
    Task<AIAuditLog?> GetAuditLogAsync(Guid id, CancellationToken ct = default);

    Task<(IEnumerable<AIAuditLog> Items, int Total)> GetAuditLogsPagedAsync(
        AIAuditLogFilter filter,
        int skip,
        int take,
        CancellationToken ct = default);

    Task<IEnumerable<AIAuditLog>> GetEntityHistoryAsync(
        string entityId,
        string entityType,
        int limit,
        CancellationToken ct = default);

    // Management methods
    Task<bool> DeleteAuditLogAsync(Guid id, CancellationToken ct = default);
    Task<int> CleanupOldAuditLogsAsync(CancellationToken ct = default);
}
```

Query Methods

GetAuditLogAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The audit log ID |
| `ct` | `CancellationToken` | Cancellation token |

GetAuditLogsPagedAsync

| Parameter | Type | Description |
|---|---|---|
| `filter` | `AIAuditLogFilter` | Filter criteria |
| `skip` | `int` | Records to skip |
| `take` | `int` | Records to take (max 100) |
| `ct` | `CancellationToken` | Cancellation token |

GetEntityHistoryAsync

| Parameter | Type | Description |
|---|---|---|
| `entityId` | `string` | The entity ID |
| `entityType` | `string` | The entity type (e.g., "document") |
| `limit` | `int` | Maximum records to return |
| `ct` | `CancellationToken` | Cancellation token |

Management Methods

DeleteAuditLogAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The audit log ID |
| `ct` | `CancellationToken` | Cancellation token |

CleanupOldAuditLogsAsync

Filter Properties

| Property | Type | Description |
|---|---|---|
| `FromDate` | `DateTime?` | Start of date range |
| `ToDate` | `DateTime?` | End of date range |
| `Status` | `AIAuditLogStatus?` | Filter by status |
| `Capability` | `AICapability?` | Filter by capability (Chat, Embedding, etc.) |
| `ProfileId` | `Guid?` | Filter by profile |
| `ProviderId` | `string?` | Filter by provider |
| `UserId` | `string?` | Filter by user |
| `FeatureType` | `string?` | Filter by feature type (e.g., "prompt", "agent") |
| `FeatureId` | `Guid?` | Filter by feature ID |
| `EntityId` | `string?` | Filter by entity ID |
| `EntityType` | `string?` | Filter by entity type (e.g., "content", "media") |
| `ParentAuditLogId` | `Guid?` | Filter by parent audit-log ID (for finding child audits) |
| `SearchText` | `string?` | Search text for filtering by model, error message, etc. |

Notes

Related

Last updated

Was this helpful?

---

## IAIChatService | AI in Umbraco

Service for AI chat completions.

Namespace

```
using Umbraco.AI.Core.Chat;
using Umbraco.AI.Core.InlineChat;
using Microsoft.Extensions.AI;
```

Interface

```
public interface IAIChatService
{
    Task<ChatResponse> GetChatResponseAsync(
        Action<AIChatBuilder> configure,
        IEnumerable<ChatMessage> messages,
        CancellationToken cancellationToken = default);

    IAsyncEnumerable<ChatResponseUpdate> StreamChatResponseAsync(
        Action<AIChatBuilder> configure,
        IEnumerable<ChatMessage> messages,
        CancellationToken cancellationToken = default);

    Task<IChatClient> CreateChatClientAsync(
        Action<AIChatBuilder> configure,
        CancellationToken cancellationToken = default);
}
```

AIChatBuilder

| Method | Description |
|---|---|
| `.WithAlias(string alias)` | Required. Sets an alias for auditing and telemetry. |
| `.WithName(string name)` | Sets a display name for telemetry purposes. |
| `.WithDescription(string? description)` | Sets a description for telemetry purposes. |
| `.WithProfile(Guid profileId)` | Selects a profile by ID. Uses default if omitted. |
| `.WithProfile(string profileAlias)` | Selects a profile by alias. |
| `.WithChatOptions(ChatOptions options)` | Overrides profile defaults for temperature, max tokens, etc. |
| `.WithGuardrails(params Guid[] guardrailIds)` | Applies guardrails by ID. |
| `.WithGuardrails(params string[] guardrailAliases)` | Applies guardrails by alias. |
| `.WithContextItems(IEnumerable<AIRequestContextItem> contextItems)` | Attaches context items to the request. |
| `.WithOutputSchema(AIOutputSchema schema)` | Sets a structured output schema for the response. |
| `.WithAdditionalProperties(IReadOnlyDictionary<string, object?> properties)` | Attaches additional properties to the request. |
| `.AsPassThrough()` | Marks the request as pass-through (bypasses some processing). |

Methods

GetChatResponseAsync

| Parameter | Type | Description |
|---|---|---|
| `configure` | `Action<AIChatBuilder>` | Builder action to set alias, profile, options, etc. |
| `messages` | `IEnumerable<ChatMessage>` | The conversation messages |
| `cancellationToken` | `CancellationToken` | Cancellation token |

StreamChatResponseAsync

| Parameter | Type | Description |
|---|---|---|
| `configure` | `Action<AIChatBuilder>` | Builder action to set alias, profile, options, etc. |
| `messages` | `IEnumerable<ChatMessage>` | The conversation messages |
| `cancellationToken` | `CancellationToken` | Cancellation token |

CreateChatClientAsync

| Parameter | Type | Description |
|---|---|---|
| `configure` | `Action<AIChatBuilder>` | Builder action to set alias, profile, options, etc. |
| `cancellationToken` | `CancellationToken` | Cancellation token |

ChatOptions

Related Types

Last updated

Was this helpful?

---

## IAIConnectionService | AI in Umbraco

Service for managing AI provider connections.

Namespace

```
using Umbraco.AI.Core.Connections;
using Umbraco.AI.Core.Models;
```

Interface

```
public interface IAIConnectionService
{
    Task<AIConnection?> GetConnectionAsync(Guid id, CancellationToken cancellationToken = default);

    Task<AIConnection?> GetConnectionByAliasAsync(string alias, CancellationToken cancellationToken = default);

    Task<IEnumerable<AIConnection>> GetConnectionsAsync(string? providerId = null, CancellationToken cancellationToken = default);

    Task<(IEnumerable<AIConnection> Items, int Total)> GetConnectionsPagedAsync(
        string? filter = null,
        string? providerId = null,
        int skip = 0,
        int take = 100,
        CancellationToken cancellationToken = default);

    Task<IEnumerable<AIConnectionRef>> GetConnectionReferencesAsync(string providerId, CancellationToken cancellationToken = default);

    Task<AIConnection> SaveConnectionAsync(AIConnection connection, CancellationToken cancellationToken = default);

    Task DeleteConnectionAsync(Guid id, CancellationToken cancellationToken = default);

    Task<bool> ValidateConnectionAsync(string providerId, object? settings, CancellationToken cancellationToken = default);

    Task<bool> TestConnectionAsync(Guid id, CancellationToken cancellationToken = default);

    Task<IEnumerable<AICapability>> GetAvailableCapabilitiesAsync(CancellationToken cancellationToken = default);

    Task<IEnumerable<AIConnection>> GetConnectionsByCapabilityAsync(AICapability capability, CancellationToken cancellationToken = default);

    Task<IAIConfiguredProvider?> GetConfiguredProviderAsync(Guid connectionId, CancellationToken cancellationToken = default);

    Task<(IEnumerable<AIEntityVersion> Items, int Total)> GetConnectionVersionHistoryAsync(Guid connectionId, int skip, int take, CancellationToken cancellationToken = default);

    Task<AIConnection?> GetConnectionVersionSnapshotAsync(Guid connectionId, int version, CancellationToken cancellationToken = default);

    Task<AIConnection> RollbackConnectionAsync(Guid connectionId, int targetVersion, CancellationToken cancellationToken = default);

    Task<bool> ConnectionAliasExistsAsync(string alias, Guid? excludeId = null, CancellationToken cancellationToken = default);
}
```

Methods

GetConnectionAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The connection ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetConnectionByAliasAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The connection alias |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetConnectionsAsync

| Parameter | Type | Description |
|---|---|---|
| `providerId` | `string?` | Provider ID to filter by |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetConnectionsPagedAsync

| Parameter | Type | Description |
|---|---|---|
| `filter` | `string?` | Filter by name |
| `providerId` | `string?` | Filter by provider |
| `skip` | `int` | Items to skip |
| `take` | `int` | Items to take |
| `cancellationToken` | `CancellationToken` | Cancellation token |

SaveConnectionAsync

| Parameter | Type | Description |
|---|---|---|
| `connection` | `AIConnection` | The connection to save |
| `cancellationToken` | `CancellationToken` | Cancellation token |

DeleteConnectionAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The connection ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

ValidateConnectionAsync

| Parameter | Type | Description |
|---|---|---|
| `providerId` | `string` | The provider ID |
| `settings` | `object?` | The settings to validate |
| `cancellationToken` | `CancellationToken` | Cancellation token |

TestConnectionAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The connection ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetAvailableCapabilitiesAsync

GetConnectionsByCapabilityAsync

| Parameter | Type | Description |
|---|---|---|
| `capability` | `AICapability` | The capability to filter by |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetConfiguredProviderAsync

| Parameter | Type | Description |
|---|---|---|
| `connectionId` | `Guid` | The connection ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetConnectionVersionHistoryAsync

| Parameter | Type | Description |
|---|---|---|
| `connectionId` | `Guid` | The connection ID |
| `skip` | `int` | Items to skip |
| `take` | `int` | Items to take |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetConnectionVersionSnapshotAsync

| Parameter | Type | Description |
|---|---|---|
| `connectionId` | `Guid` | The connection ID |
| `version` | `int` | The version number |
| `cancellationToken` | `CancellationToken` | Cancellation token |

RollbackConnectionAsync

| Parameter | Type | Description |
|---|---|---|
| `connectionId` | `Guid` | The connection ID |
| `targetVersion` | `int` | The version to roll back to |
| `cancellationToken` | `CancellationToken` | Cancellation token |

ConnectionAliasExistsAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The alias to check |
| `excludeId` | `Guid?` | Optional ID to exclude (for updates) |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Last updated

Was this helpful?

---

## IAIContextService | AI in Umbraco

Service for managing AI contexts.

Namespace

```
using Umbraco.AI.Core.Contexts;
```

Interface

```
public interface IAIContextService
{
    Task<AIContext?> GetContextAsync(Guid id, CancellationToken cancellationToken = default);

    Task<AIContext?> GetContextByAliasAsync(string alias, CancellationToken cancellationToken = default);

    Task<IEnumerable<AIContext>> GetContextsAsync(CancellationToken cancellationToken = default);

    Task<(IEnumerable<AIContext> Items, int Total)> GetContextsPagedAsync(
        string? filter = null,
        int skip = 0,
        int take = 100,
        CancellationToken cancellationToken = default);

    Task<AIContext> SaveContextAsync(AIContext context, CancellationToken cancellationToken = default);

    Task<bool> DeleteContextAsync(Guid id, CancellationToken cancellationToken = default);

    Task<bool> ContextAliasExistsAsync(string alias, Guid? excludeId = null, CancellationToken cancellationToken = default);

    Task<(IEnumerable<AIEntityVersion> Items, int Total)> GetContextVersionHistoryAsync(Guid contextId, int skip, int take, CancellationToken cancellationToken = default);

    Task<AIContext?> GetContextVersionSnapshotAsync(Guid contextId, int version, CancellationToken cancellationToken = default);

    Task<AIContext> RollbackContextAsync(Guid contextId, int targetVersion, CancellationToken cancellationToken = default);
}
```

Methods

GetContextAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The context ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetContextByAliasAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The context alias |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetContextsAsync

GetContextsPagedAsync

| Parameter | Type | Description |
|---|---|---|
| `filter` | `string?` | Filter by name (case-insensitive contains) |
| `skip` | `int` | Items to skip |
| `take` | `int` | Items to take |
| `cancellationToken` | `CancellationToken` | Cancellation token |

SaveContextAsync

| Parameter | Type | Description |
|---|---|---|
| `context` | `AIContext` | The context to save |
| `cancellationToken` | `CancellationToken` | Cancellation token |

DeleteContextAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The context ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

ContextAliasExistsAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The alias to check |
| `excludeId` | `Guid?` | Optional ID to exclude (for updates) |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetContextVersionHistoryAsync

| Parameter | Type | Description |
|---|---|---|
| `contextId` | `Guid` | The context ID |
| `skip` | `int` | Items to skip |
| `take` | `int` | Items to take |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetContextVersionSnapshotAsync

| Parameter | Type | Description |
|---|---|---|
| `contextId` | `Guid` | The context ID |
| `version` | `int` | The version number |
| `cancellationToken` | `CancellationToken` | Cancellation token |

RollbackContextAsync

| Parameter | Type | Description |
|---|---|---|
| `contextId` | `Guid` | The context ID |
| `targetVersion` | `int` | The version to roll back to |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Related

Last updated

Was this helpful?

---

## IAIEmbeddingService | AI in Umbraco

Service for generating text embeddings.

Namespace

```
using Umbraco.AI.Core.Embeddings;
using Microsoft.Extensions.AI;
```

Interface

```
public interface IAIEmbeddingService
{
    Task<Embedding<float>> GenerateEmbeddingAsync(
        Action<AIEmbeddingBuilder> configure,
        string text,
        CancellationToken cancellationToken = default);

    Task<GeneratedEmbeddings<Embedding<float>>> GenerateEmbeddingsAsync(
        Action<AIEmbeddingBuilder> configure,
        IEnumerable<string> texts,
        CancellationToken cancellationToken = default);

    Task<IEmbeddingGenerator<string, Embedding<float>>> CreateEmbeddingGeneratorAsync(
        Action<AIEmbeddingBuilder> configure,
        CancellationToken cancellationToken = default);
}
```

AIEmbeddingBuilder

| Method | Description |
|---|---|
| `.WithAlias(string alias)` | Required. Sets an alias for auditing and telemetry. |
| `.WithName(string name)` | Sets a display name for telemetry purposes. |
| `.WithDescription(string? description)` | Sets a description for telemetry purposes. |
| `.WithProfile(Guid profileId)` | Selects a profile by ID. Uses default if omitted. |
| `.WithProfile(string profileAlias)` | Selects a profile by alias. |
| `.WithEmbeddingOptions(EmbeddingGenerationOptions options)` | Overrides profile defaults (model, dimensions, etc.). |
| `.WithContextItems(IEnumerable<AIRequestContextItem> contextItems)` | Attaches context items to the request. |
| `.WithGuardrails(params Guid[] guardrailIds)` | Applies guardrails by ID. |
| `.WithGuardrails(params string[] guardrailAliases)` | Applies guardrails by alias. |
| `.WithAdditionalProperties(IReadOnlyDictionary<string, object?> properties)` | Attaches additional properties to the request. |
| `.AsPassThrough()` | Marks the request as pass-through (bypasses some processing). |

Methods

GenerateEmbeddingAsync

| Parameter | Type | Description |
|---|---|---|
| `configure` | `Action<AIEmbeddingBuilder>` | Builder action to set alias, profile, options, etc. |
| `text` | `string` | The text to embed |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GenerateEmbeddingsAsync

| Parameter | Type | Description |
|---|---|---|
| `configure` | `Action<AIEmbeddingBuilder>` | Builder action to set alias, profile, options, etc. |
| `texts` | `IEnumerable<string>` | The texts to embed |
| `cancellationToken` | `CancellationToken` | Cancellation token |

CreateEmbeddingGeneratorAsync

| Parameter | Type | Description |
|---|---|---|
| `configure` | `Action<AIEmbeddingBuilder>` | Builder action to set alias, profile, options, etc. |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Use Cases

Semantic Search

Related Types

Last updated

Was this helpful?

---

## IAIEntityVersionService | AI in Umbraco

Service for managing entity version history.

Namespace

```
using Umbraco.AI.Core.Versioning;
```

Interface

```
public interface IAIEntityVersionService
{
    Task<(IEnumerable<AIEntityVersion> Items, int Total)> GetVersionHistoryAsync(
        Guid entityId,
        string entityType,
        int skip,
        int take,
        CancellationToken cancellationToken = default);

    Task<AIEntityVersion?> GetVersionAsync(
        Guid entityId,
        string entityType,
        int version,
        CancellationToken cancellationToken = default);

    Task<TEntity?> GetVersionSnapshotAsync<TEntity>(
        Guid entityId,
        int version,
        CancellationToken cancellationToken = default)
        where TEntity : class, IAIVersionableEntity;

    Task SaveVersionAsync<TEntity>(
        TEntity entity,
        Guid? userId,
        string? changeDescription = null,
        CancellationToken cancellationToken = default)
        where TEntity : class, IAIVersionableEntity;

    Task SaveVersionAsync(
        Guid entityId,
        string entityType,
        int version,
        string snapshot,
        Guid? userId,
        string? changeDescription = null,
        CancellationToken cancellationToken = default);

    Task DeleteVersionsAsync(
        Guid entityId,
        string entityType,
        CancellationToken cancellationToken = default);

    Task<AIVersionComparison?> CompareVersionsAsync(
        Guid entityId,
        string entityType,
        int fromVersion,
        int toVersion,
        CancellationToken cancellationToken = default);

    string CreateSnapshot<TEntity>(TEntity entity)
        where TEntity : class, IAIVersionableEntity;

    TEntity? RestoreFromSnapshot<TEntity>(string snapshot)
        where TEntity : class, IAIVersionableEntity;

    Task<AIVersionCleanupResult> CleanupVersionsAsync(
        CancellationToken cancellationToken = default);
}
```

Methods

GetVersionHistoryAsync

| Parameter | Type | Description |
|---|---|---|
| `entityId` | `Guid` | The entity ID |
| `entityType` | `string` | The entity type (e.g., "profile", "context") |
| `skip` | `int` | Records to skip |
| `take` | `int` | Records to take |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetVersionAsync

| Parameter | Type | Description |
|---|---|---|
| `entityId` | `Guid` | The entity ID |
| `entityType` | `string` | The entity type |
| `version` | `int` | The version number |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetVersionSnapshotAsync

| Parameter | Type | Description |
|---|---|---|
| `entityId` | `Guid` | The entity ID |
| `version` | `int` | The version number |
| `cancellationToken` | `CancellationToken` | Cancellation token |

SaveVersionAsync

| Parameter | Type | Description |
|---|---|---|
| `entity` | `TEntity` | The entity to snapshot |
| `userId` | `Guid?` | User who made the change |
| `changeDescription` | `string?` | Description of changes |
| `cancellationToken` | `CancellationToken` | Cancellation token |

| Parameter | Type | Description |
|---|---|---|
| `entityId` | `Guid` | The entity ID |
| `entityType` | `string` | The entity type name (e.g., "Profile") |
| `version` | `int` | The version number |
| `snapshot` | `string` | The raw JSON snapshot |
| `userId` | `Guid?` | User who made the change |
| `changeDescription` | `string?` | Description of changes |
| `cancellationToken` | `CancellationToken` | Cancellation token |

DeleteVersionsAsync

| Parameter | Type | Description |
|---|---|---|
| `entityId` | `Guid` | The entity ID |
| `entityType` | `string` | The entity type |
| `cancellationToken` | `CancellationToken` | Cancellation token |

CompareVersionsAsync

| Parameter | Type | Description |
|---|---|---|
| `entityId` | `Guid` | The entity ID |
| `entityType` | `string` | The entity type |
| `fromVersion` | `int` | Source version |
| `toVersion` | `int` | Target version |
| `cancellationToken` | `CancellationToken` | Cancellation token |

CreateSnapshot / RestoreFromSnapshot

CleanupVersionsAsync

Entity Types

| Type String | Entity Class |
|---|---|
| `"connection"` | `AIConnection` |
| `"profile"` | `AIProfile` |
| `"context"` | `AIContext` |
| `"prompt"` | `AIPrompt` (requires Umbraco.AI.Prompt) |
| `"agent"` | `AIAgent` (requires Umbraco.AI.Agent) |

Related

Last updated

Was this helpful?

---

## IAIGuardrailService | AI in Umbraco

Service for managing AI guardrails.

Namespace

```
using Umbraco.AI.Core.Guardrails;
```

Interface

```
public interface IAIGuardrailService
{
    Task<AIGuardrail?> GetGuardrailAsync(Guid id, CancellationToken cancellationToken = default);

    Task<AIGuardrail?> GetGuardrailByAliasAsync(string alias, CancellationToken cancellationToken = default);

    Task<IEnumerable<AIGuardrail>> GetGuardrailsAsync(CancellationToken cancellationToken = default);

    Task<(IEnumerable<AIGuardrail> Items, int Total)> GetGuardrailsPagedAsync(
        string? filter = null, int skip = 0, int take = 100,
        CancellationToken cancellationToken = default);

    Task<IEnumerable<AIGuardrail>> GetGuardrailsByIdsAsync(
        IEnumerable<Guid> ids, CancellationToken cancellationToken = default);

    Task<AIGuardrail> SaveGuardrailAsync(AIGuardrail guardrail, CancellationToken cancellationToken = default);

    Task<bool> DeleteGuardrailAsync(Guid id, CancellationToken cancellationToken = default);

    Task<bool> GuardrailAliasExistsAsync(
        string alias, Guid? excludeId = null, CancellationToken cancellationToken = default);

    Task<(IEnumerable<AIEntityVersion> Items, int Total)> GetGuardrailVersionHistoryAsync(
        Guid guardrailId, int skip, int take, CancellationToken cancellationToken = default);

    Task<AIGuardrail?> GetGuardrailVersionSnapshotAsync(
        Guid guardrailId, int version, CancellationToken cancellationToken = default);

    Task<AIGuardrail> RollbackGuardrailAsync(
        Guid guardrailId, int targetVersion, CancellationToken cancellationToken = default);
}
```

Methods

GetGuardrailAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The guardrail ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetGuardrailByAliasAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The guardrail alias |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetGuardrailsAsync

GetGuardrailsPagedAsync

| Parameter | Type | Description |
|---|---|---|
| `filter` | `string?` | Optional filter (case-insensitive contains) |
| `skip` | `int` | Number of items to skip (default: 0) |
| `take` | `int` | Number of items to take (default: 100) |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetGuardrailsByIdsAsync

| Parameter | Type | Description |
|---|---|---|
| `ids` | `IEnumerable<Guid>` | The guardrail IDs to look up |
| `cancellationToken` | `CancellationToken` | Cancellation token |

SaveGuardrailAsync

| Parameter | Type | Description |
|---|---|---|
| `guardrail` | `AIGuardrail` | The guardrail to save |
| `cancellationToken` | `CancellationToken` | Cancellation token |

DeleteGuardrailAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The guardrail ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GuardrailAliasExistsAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The alias to check |
| `excludeId` | `Guid?` | Optional ID to exclude (for updates) |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetGuardrailVersionHistoryAsync

| Parameter | Type | Description |
|---|---|---|
| `guardrailId` | `Guid` | The guardrail ID |
| `skip` | `int` | Number of versions to skip |
| `take` | `int` | Maximum versions to return |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetGuardrailVersionSnapshotAsync

| Parameter | Type | Description |
|---|---|---|
| `guardrailId` | `Guid` | The guardrail ID |
| `version` | `int` | The version to retrieve |
| `cancellationToken` | `CancellationToken` | Cancellation token |

RollbackGuardrailAsync

| Parameter | Type | Description |
|---|---|---|
| `guardrailId` | `Guid` | The guardrail ID |
| `targetVersion` | `int` | The version to rollback to |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Related

Last updated

Was this helpful?

---

## IAIProfileService | AI in Umbraco

Service for managing AI profiles.

Namespace

```
using Umbraco.AI.Core.Profiles;
using Umbraco.AI.Core.Models;
```

Interface

```
public interface IAIProfileService
{
    Task<AIProfile?> GetProfileAsync(Guid id, CancellationToken cancellationToken = default);

    Task<AIProfile?> GetProfileByAliasAsync(string alias, CancellationToken cancellationToken = default);

    Task<IEnumerable<AIProfile>> GetAllProfilesAsync(CancellationToken cancellationToken = default);

    Task<IEnumerable<AIProfile>> GetProfilesAsync(AICapability capability, CancellationToken cancellationToken = default);

    Task<(IEnumerable<AIProfile> Items, int Total)> GetProfilesPagedAsync(
        string? filter = null,
        AICapability? capability = null,
        int skip = 0,
        int take = 100,
        CancellationToken cancellationToken = default);

    Task<AIProfile> GetDefaultProfileAsync(AICapability capability, CancellationToken cancellationToken = default);

    Task<AIProfile> SaveProfileAsync(AIProfile profile, CancellationToken cancellationToken = default);

    Task<bool> DeleteProfileAsync(Guid id, CancellationToken cancellationToken = default);

    Task<bool> HasDefaultProfileAsync(AICapability capability, CancellationToken cancellationToken = default);

    Task<AIProfile> GetClassifierProfileAsync(CancellationToken cancellationToken = default);

    Task<(IEnumerable<AIEntityVersion> Items, int Total)> GetProfileVersionHistoryAsync(
        Guid profileId,
        int skip,
        int take,
        CancellationToken cancellationToken = default);

    Task<AIProfile?> GetProfileVersionSnapshotAsync(
        Guid profileId,
        int version,
        CancellationToken cancellationToken = default);

    Task<AIProfile> RollbackProfileAsync(
        Guid profileId,
        int targetVersion,
        CancellationToken cancellationToken = default);

    Task<bool> ProfileAliasExistsAsync(
        string alias,
        Guid? excludeId = null,
        CancellationToken cancellationToken = default);

    Task<bool> ProfilesExistWithConnectionAsync(
        Guid connectionId,
        CancellationToken cancellationToken = default);
}
```

Methods

GetProfileAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The profile ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetProfileByAliasAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The profile alias |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetAllProfilesAsync

GetProfilesAsync

| Parameter | Type | Description |
|---|---|---|
| `capability` | `AICapability` | The capability to filter by |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetProfilesPagedAsync

| Parameter | Type | Description |
|---|---|---|
| `filter` | `string?` | Filter by name (case-insensitive contains) |
| `capability` | `AICapability?` | Filter by capability |
| `skip` | `int` | Items to skip |
| `take` | `int` | Items to take |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetDefaultProfileAsync

| Parameter | Type | Description |
|---|---|---|
| `capability` | `AICapability` | The capability |
| `cancellationToken` | `CancellationToken` | Cancellation token |

SaveProfileAsync

| Parameter | Type | Description |
|---|---|---|
| `profile` | `AIProfile` | The profile to save |
| `cancellationToken` | `CancellationToken` | Cancellation token |

DeleteProfileAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The profile ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

HasDefaultProfileAsync

| Parameter | Type | Description |
|---|---|---|
| `capability` | `AICapability` | The capability |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetClassifierProfileAsync

| Parameter | Type | Description |
|---|---|---|
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetProfileVersionHistoryAsync

| Parameter | Type | Description |
|---|---|---|
| `profileId` | `Guid` | The profile ID |
| `skip` | `int` | Items to skip |
| `take` | `int` | Items to take |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetProfileVersionSnapshotAsync

| Parameter | Type | Description |
|---|---|---|
| `profileId` | `Guid` | The profile ID |
| `version` | `int` | The version number |
| `cancellationToken` | `CancellationToken` | Cancellation token |

RollbackProfileAsync

| Parameter | Type | Description |
|---|---|---|
| `profileId` | `Guid` | The profile ID |
| `targetVersion` | `int` | The version number to roll back to |
| `cancellationToken` | `CancellationToken` | Cancellation token |

ProfileAliasExistsAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The alias to check |
| `excludeId` | `Guid?` | Profile ID to exclude from the check |
| `cancellationToken` | `CancellationToken` | Cancellation token |

ProfilesExistWithConnectionAsync

| Parameter | Type | Description |
|---|---|---|
| `connectionId` | `Guid` | The connection ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Last updated

Was this helpful?

---

## IAISettingsService | AI in Umbraco

Service for managing global AI settings.

Namespace

```
using Umbraco.AI.Core.Settings;
```

Interface

```
public interface IAISettingsService
{
    Task<AISettings> GetSettingsAsync(CancellationToken cancellationToken = default);

    Task<AISettings> SaveSettingsAsync(AISettings settings, CancellationToken cancellationToken = default);
}
```

Methods

GetSettingsAsync

| Parameter | Type | Description |
|---|---|---|
| `cancellationToken` | `CancellationToken` | Cancellation token |

SaveSettingsAsync

| Parameter | Type | Description |
|---|---|---|
| `settings` | `AISettings` | The settings to save |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Usage Example

Notes

Related

Last updated

Was this helpful?

---

## IAIUsageAnalyticsService | AI in Umbraco

Service for AI usage analytics and reporting.

Namespace

```
using Umbraco.AI.Core.Analytics.Usage;
```

Interface

```
public interface IAIUsageAnalyticsService
{
    Task<AIUsageSummary> GetSummaryAsync(
        DateTime from,
        DateTime to,
        AIUsagePeriod? requestedGranularity = null,
        AIUsageFilter? filter = null,
        CancellationToken cancellationToken = default);

    Task<IEnumerable<AIUsageTimeSeriesPoint>> GetTimeSeriesAsync(
        DateTime from,
        DateTime to,
        AIUsagePeriod? requestedGranularity = null,
        AIUsageFilter? filter = null,
        CancellationToken cancellationToken = default);

    Task<IEnumerable<AIUsageBreakdownItem>> GetBreakdownByProviderAsync(
        DateTime from,
        DateTime to,
        AIUsagePeriod? requestedGranularity = null,
        CancellationToken cancellationToken = default);

    Task<IEnumerable<AIUsageBreakdownItem>> GetBreakdownByModelAsync(
        DateTime from,
        DateTime to,
        AIUsagePeriod? requestedGranularity = null,
        CancellationToken cancellationToken = default);

    Task<IEnumerable<AIUsageBreakdownItem>> GetBreakdownByProfileAsync(
        DateTime from,
        DateTime to,
        AIUsagePeriod? requestedGranularity = null,
        CancellationToken cancellationToken = default);

    Task<IEnumerable<AIUsageBreakdownItem>> GetBreakdownByUserAsync(
        DateTime from,
        DateTime to,
        AIUsagePeriod? requestedGranularity = null,
        CancellationToken cancellationToken = default);
}
```

Methods

GetSummaryAsync

| Parameter | Type | Description |
|---|---|---|
| `from` | `DateTime` | Start of period |
| `to` | `DateTime` | End of period |
| `requestedGranularity` | `AIUsagePeriod?` | Data granularity |
| `filter` | `AIUsageFilter?` | Optional filter |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetTimeSeriesAsync

| Parameter | Type | Description |
|---|---|---|
| `from` | `DateTime` | Start of period |
| `to` | `DateTime` | End of period |
| `requestedGranularity` | `AIUsagePeriod?` | Time interval |
| `filter` | `AIUsageFilter?` | Optional filter |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetBreakdownByProviderAsync

GetBreakdownByModelAsync

GetBreakdownByProfileAsync

GetBreakdownByUserAsync

Model Classes

AIUsageSummary

| Property | Type | Description |
|---|---|---|
| `TotalRequests` | `int` | Number of operations |
| `InputTokens` | `long` | Total input tokens |
| `OutputTokens` | `long` | Total output tokens |
| `TotalTokens` | `long` | Combined tokens |
| `SuccessCount` | `int` | Successful operations |
| `FailureCount` | `int` | Failed operations |
| `SuccessRate` | `double` | Success ratio (0.0-1.0) |
| `AverageDurationMs` | `int` | Average operation time |

AIUsageTimeSeriesPoint

| Property | Type | Description |
|---|---|---|
| `Timestamp` | `DateTime` | Interval start |
| `RequestCount` | `int` | Requests in interval |
| `InputTokens` | `long` | Input tokens |
| `OutputTokens` | `long` | Output tokens |
| `TotalTokens` | `long` | Total tokens |
| `SuccessCount` | `int` | Successes |
| `FailureCount` | `int` | Failures |

AIUsageBreakdownItem

| Property | Type | Description |
|---|---|---|
| `Dimension` | `string` | Identifier |
| `DimensionName` | `string?` | Display name |
| `RequestCount` | `int` | Requests |
| `TotalTokens` | `long` | Tokens used |
| `Percentage` | `double` | Share of total |

AIUsagePeriod

| Value | Description |
|---|---|
| `Hourly` | Hourly intervals |
| `Daily` | Daily intervals |

Usage Example

Related

Last updated

Was this helpful?

---
