# Reference | AI in Umbraco

Service for managing and executing prompts.

Namespace

```
using Umbraco.AI.Prompt.Core.Prompts;
```

Interface

```
public interface IAIPromptService
{
    Task<AIPrompt?> GetPromptAsync(Guid id, CancellationToken cancellationToken = default);

    Task<AIPrompt?> GetPromptByAliasAsync(string alias, CancellationToken cancellationToken = default);

    Task<IEnumerable<AIPrompt>> GetPromptsAsync(CancellationToken cancellationToken = default);

    Task<(IEnumerable<AIPrompt> Items, int Total)> GetPromptsPagedAsync(
        int skip,
        int take,
        string? filter = null,
        Guid? profileId = null,
        CancellationToken cancellationToken = default);

    Task<AIPrompt> SavePromptAsync(AIPrompt prompt, CancellationToken cancellationToken = default);

    Task<bool> DeletePromptAsync(Guid id, CancellationToken cancellationToken = default);

    Task<bool> PromptsExistWithProfileAsync(Guid profileId, CancellationToken cancellationToken = default);

    Task<bool> PromptAliasExistsAsync(string alias, Guid? excludeId = null, CancellationToken cancellationToken = default);

    Task<AIPromptExecutionResult> ExecutePromptAsync(
        Guid promptId,
        AIPromptExecutionRequest request,
        CancellationToken cancellationToken = default);

    Task<AIPromptExecutionResult> ExecutePromptAsync(
        Guid promptId,
        AIPromptExecutionRequest request,
        AIPromptExecutionOptions options,
        CancellationToken cancellationToken = default);
}
```

Methods

GetPromptAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The prompt ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetPromptByAliasAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The prompt alias |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetPromptsAsync

GetPromptsPagedAsync

| Parameter | Type | Description |
|---|---|---|
| `skip` | `int` | Items to skip |
| `take` | `int` | Items to take |
| `filter` | `string?` | Filter by name or alias |
| `profileId` | `Guid?` | Filter by profile |
| `cancellationToken` | `CancellationToken` | Cancellation token |

SavePromptAsync

| Parameter | Type | Description |
|---|---|---|
| `prompt` | `AIPrompt` | The prompt to save |
| `cancellationToken` | `CancellationToken` | Cancellation token |

DeletePromptAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The prompt ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

PromptsExistWithProfileAsync

| Parameter | Type | Description |
|---|---|---|
| `profileId` | `Guid` | The profile ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

PromptAliasExistsAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The alias to check |
| `excludeId` | `Guid?` | Optional ID to exclude |
| `cancellationToken` | `CancellationToken` | Cancellation token |

ExecutePromptAsync

| Parameter | Type | Description |
|---|---|---|
| `promptId` | `Guid` | The prompt ID |
| `request` | `AIPromptExecutionRequest` | Execution parameters |
| `options` | `AIPromptExecutionOptions` | (Second overload) Validation and overrides |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Related Models

AIPromptExecutionRequest

| Property | Type | Required | Description |
|---|---|---|---|
| `EntityId` | `Guid` | Yes | The entity (document, media, etc.) key. Used for scope validation and entity context lookup. |
| `EntityType` | `string` | Yes | The entity type (for example `document` or `media` ). |
| `PropertyAlias` | `string` | Yes | The property alias being edited. |
| `ContentTypeAlias` | `string` | Yes | The content type alias (or element type alias when editing a block). |
| `ElementId` | `Guid?` | No | Block content key when executing inside a block element. |
| `ElementType` | `string?` | No | Element type identifier when executing inside a block element. |
| `Culture` | `string?` | No | Culture/language variant (for example `en-US` ). |
| `Segment` | `string?` | No | Segment variant. |
| `Context` | `IReadOnlyList<AIRequestContextItem>?` | No | Additional context items passed from the frontend. Processed by runtime context contributors to populate template variables and system messages. |

AIPromptExecutionResult

| Property | Type | Description |
|---|---|---|
| `Content` | `string` | The generated response content. |
| `Usage` | `UsageDetails?` | Token usage information from `Microsoft.Extensions.AI` . |
| `Messages` | `IReadOnlyList<ChatMessage>?` | The chat messages sent to the AI model (system messages, processed user template). |
| `ResultOptions` | `IReadOnlyList<AIPromptResultOption>` | Result options. Empty for informational prompts, a single entry for single-value prompts, multiple entries when the prompt is configured to generate options. |

| Property | Type | Description |
|---|---|---|
| `Label` | `string` | Short title for the option. |
| `DisplayValue` | `string` | Value displayed in the UI. |
| `Description` | `string?` | Optional explanation for the option. |
| `ValueChange` | `AIValueChange?` | The change to apply when the option is selected (null when the option is informational only). |

AIPromptExecutionOptions

| Property | Type | Description |
|---|---|---|
| `ValidateScope` | `bool` | Whether to enforce the prompt's scope rules before execution (default `true` ). |
| `ProfileIdOverride` | `Guid?` | Overrides the prompt's configured profile (useful for cross-model testing). |
| `ContextIdsOverride` | `IReadOnlyList<Guid>?` | Overrides the prompt's configured context IDs. |
| `GuardrailIdsOverride` | `IReadOnlyList<Guid>?` | Overrides the guardrail IDs evaluated during execution. |

Related

Last updated

Was this helpful?

## Sub-topics

- [AIPrompt | AI in Umbraco](ai-prompt-service/ai-prompt.md)
