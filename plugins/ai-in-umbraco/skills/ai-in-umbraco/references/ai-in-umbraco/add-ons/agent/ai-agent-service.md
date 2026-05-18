# Reference | AI in Umbraco

Service for managing and running agents.

Namespace

```
using Umbraco.AI.Agent.Core.Agents;
```

Interface

```
public interface IAIAgentService
{
    Task<AIAgent?> GetAgentAsync(Guid id, CancellationToken cancellationToken = default);

    Task<AIAgent?> GetAgentByAliasAsync(string alias, CancellationToken cancellationToken = default);

    Task<IEnumerable<AIAgent>> GetAgentsAsync(CancellationToken cancellationToken = default);

    Task<(IEnumerable<AIAgent> Items, int Total)> GetAgentsPagedAsync(
        int skip,
        int take,
        string? filter = null,
        Guid? profileId = null,
        string? surfaceId = null,
        bool? isActive = null,
        AIAgentType? agentType = null,
        CancellationToken cancellationToken = default);

    Task<IEnumerable<AIAgent>> GetAgentsBySurfaceAsync(
        string surfaceId,
        CancellationToken cancellationToken = default);

    Task<AIAgent> SaveAgentAsync(AIAgent agent, CancellationToken cancellationToken = default);

    Task<bool> DeleteAgentAsync(Guid id, CancellationToken cancellationToken = default);

    Task<bool> AgentAliasExistsAsync(
        string alias,
        Guid? excludeId = null,
        CancellationToken cancellationToken = default);

    Task<bool> AgentsExistWithProfileAsync(
        Guid profileId,
        CancellationToken cancellationToken = default);

    Task<IReadOnlyList<string>> GetAllowedToolIdsAsync(
        AIAgent agent,
        IEnumerable<Guid>? userGroupIds = null,
        CancellationToken cancellationToken = default);

    Task<bool> IsToolAllowedAsync(
        AIAgent agent,
        string toolId,
        IEnumerable<Guid>? userGroupIds = null,
        CancellationToken cancellationToken = default);

    Task<AIAgent?> SelectAgentForPromptAsync(
        string userPrompt,
        string surfaceId,
        AgentAvailabilityContext context,
        CancellationToken cancellationToken = default);

    Task<AgentResponse> RunAgentAsync(
        Guid agentId,
        IEnumerable<ChatMessage> messages,
        AIAgentExecutionOptions? options = null,
        CancellationToken cancellationToken = default);

    Task<AgentResponse> RunAgentAsync(
        string agentAlias,
        IEnumerable<ChatMessage> messages,
        AIAgentExecutionOptions? options = null,
        CancellationToken cancellationToken = default);

    IAsyncEnumerable<AgentResponseUpdate> StreamAgentAsync(
        Guid agentId,
        IEnumerable<ChatMessage> messages,
        AIAgentExecutionOptions? options = null,
        CancellationToken cancellationToken = default);

    IAsyncEnumerable<AgentResponseUpdate> StreamAgentAsync(
        string agentAlias,
        IEnumerable<ChatMessage> messages,
        AIAgentExecutionOptions? options = null,
        CancellationToken cancellationToken = default);

    IAsyncEnumerable<IAGUIEvent> StreamAgentAGUIAsync(
        Guid agentId,
        AGUIRunRequest request,
        IEnumerable<AIFrontendTool>? frontendTools,
        CancellationToken cancellationToken = default);

    IAsyncEnumerable<IAGUIEvent> StreamAgentAGUIAsync(
        Guid agentId,
        AGUIRunRequest request,
        IEnumerable<AIFrontendTool>? frontendTools,
        AIAgentExecutionOptions options,
        CancellationToken cancellationToken = default);

    Task<Microsoft.Agents.AI.AIAgent> CreateInlineAgentAsync(
        Action<AIInlineAgentBuilder> configure,
        CancellationToken cancellationToken = default);

    Task<AgentResponse> RunAgentAsync(
        Action<AIInlineAgentBuilder> configure,
        IEnumerable<ChatMessage> messages,
        CancellationToken cancellationToken = default);

    IAsyncEnumerable<AgentResponseUpdate> StreamAgentAsync(
        Action<AIInlineAgentBuilder> configure,
        IEnumerable<ChatMessage> messages,
        CancellationToken cancellationToken = default);
}
```

Read methods

GetAgentAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The agent ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetAgentByAliasAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The agent alias |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetAgentsAsync

GetAgentsPagedAsync

| Parameter | Type | Description |
|---|---|---|
| `skip` | `int` | Items to skip |
| `take` | `int` | Items to take |
| `filter` | `string?` | Filter by name or alias |
| `profileId` | `Guid?` | Filter by profile |
| `surfaceId` | `string?` | Filter by surface (e.g., "copilot") |
| `isActive` | `bool?` | Filter by active status |
| `agentType` | `AIAgentType?` | Filter by agent type |
| `cancellationToken` | `CancellationToken` | Cancellation token |

GetAgentsBySurfaceAsync

| Parameter | Type | Description |
|---|---|---|
| `surfaceId` | `string` | The surface ID to filter by |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Write methods

SaveAgentAsync

| Parameter | Type | Description |
|---|---|---|
| `agent` | `AIAgent` | The agent to save |
| `cancellationToken` | `CancellationToken` | Cancellation token |

DeleteAgentAsync

| Parameter | Type | Description |
|---|---|---|
| `id` | `Guid` | The agent ID |
| `cancellationToken` | `CancellationToken` | Cancellation token |

AgentAliasExistsAsync

| Parameter | Type | Description |
|---|---|---|
| `alias` | `string` | The alias to check |
| `excludeId` | `Guid?` | Optional ID to exclude |
| `cancellationToken` | `CancellationToken` | Cancellation token |

AgentsExistWithProfileAsync

| Parameter | Type | Description |
|---|---|---|
| `profileId` | `Guid` | The profile ID to check |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Permission methods

GetAllowedToolIdsAsync

| Parameter | Type | Description |
|---|---|---|
| `agent` | `AIAgent` | The agent |
| `userGroupIds` | `IEnumerable<Guid>?` | Optional user group IDs. If `null` , uses the current BackOffice user's groups. |
| `cancellationToken` | `CancellationToken` | Cancellation token |

IsToolAllowedAsync

| Parameter | Type | Description |
|---|---|---|
| `agent` | `AIAgent` | The agent |
| `toolId` | `string` | The tool ID being called |
| `userGroupIds` | `IEnumerable<Guid>?` | Optional user group IDs. If `null` , uses the current BackOffice user's groups. |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Selection and execution

SelectAgentForPromptAsync

| Parameter | Type | Description |
|---|---|---|
| `userPrompt` | `string` | The user's message |
| `surfaceId` | `string` | The surface to search (e.g., `"copilot"` ) |
| `context` | `AgentAvailabilityContext` | Context for scope-based filtering |
| `cancellationToken` | `CancellationToken` | Cancellation token |

RunAgentAsync (persisted agent, by ID)

| Parameter | Type | Description |
|---|---|---|
| `agentId` | `Guid` | The agent ID |
| `messages` | `IEnumerable<ChatMessage>` | The chat messages (from `Microsoft.Extensions.AI` ) |
| `options` | `AIAgentExecutionOptions?` | Optional overrides (profile, context, guardrails) |
| `cancellationToken` | `CancellationToken` | Cancellation token |

RunAgentAsync (persisted agent, by alias)

StreamAgentAsync (persisted agent)

| Parameter | Type | Description |
|---|---|---|
| `agentId` / `agentAlias` | `Guid` / `string` | The agent ID or alias |
| `messages` | `IEnumerable<ChatMessage>` | The chat messages |
| `options` | `AIAgentExecutionOptions?` | Optional overrides |
| `cancellationToken` | `CancellationToken` | Cancellation token |

StreamAgentAGUIAsync

| Parameter | Type | Description |
|---|---|---|
| `agentId` | `Guid` | The agent ID |
| `request` | `AGUIRunRequest` | AG-UI run request (messages, tools, context, state) |
| `frontendTools` | `IEnumerable<AIFrontendTool>?` | Frontend tools with scope and destructiveness metadata |
| `options` | `AIAgentExecutionOptions` | (Overload) Execution options for overrides |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Inline agents

CreateInlineAgentAsync

| Parameter | Type | Description |
|---|---|---|
| `configure` | `Action<AIInlineAgentBuilder>` | Builder configuration |
| `cancellationToken` | `CancellationToken` | Cancellation token |

RunAgentAsync (inline)

| Parameter | Type | Description |
|---|---|---|
| `configure` | `Action<AIInlineAgentBuilder>` | Builder configuration |
| `messages` | `IEnumerable<ChatMessage>` | The chat messages |
| `cancellationToken` | `CancellationToken` | Cancellation token |

StreamAgentAsync (inline)

| Parameter | Type | Description |
|---|---|---|
| `configure` | `Action<AIInlineAgentBuilder>` | Builder configuration |
| `messages` | `IEnumerable<ChatMessage>` | The chat messages |
| `cancellationToken` | `CancellationToken` | Cancellation token |

Related models

AIFrontendTool

AIAgentUserGroupPermissions

AIAgentExecutionOptions

Related

Last updated

Was this helpful?

## Sub-topics

- [AIAgent | AI in Umbraco](ai-agent-service/ai-agent.md)
- [UaiAgentRepository | AI in Umbraco](ai-agent-service/uai-agent-repository.md)
