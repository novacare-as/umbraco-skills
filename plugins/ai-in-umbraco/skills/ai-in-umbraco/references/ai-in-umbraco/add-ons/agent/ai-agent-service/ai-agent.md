# AIAgent | AI in Umbraco

Model representing an AI agent.

Namespace

```
using Umbraco.AI.Agent.Core.Agents;
```

Definition

```
public sealed class AIAgent : IAIVersionableEntity
{
    public Guid Id { get; internal set; }
    public required string Alias { get; set; }
    public required string Name { get; set; }
    public string? Description { get; set; }
    public AIAgentType AgentType { get; init; } = AIAgentType.Standard;
    public IAIAgentConfig? Config { get; set; }
    public Guid? ProfileId { get; set; }
    public IReadOnlyList<Guid> GuardrailIds { get; set; } = [];
    public IReadOnlyList<string> SurfaceIds { get; set; } = [];
    public AIAgentScope? Scope { get; set; }
    public bool IsActive { get; set; } = true;

    // Audit properties
    public DateTime DateCreated { get; set; } = DateTime.UtcNow;
    public DateTime DateModified { get; set; } = DateTime.UtcNow;
    public Guid? CreatedByUserId { get; set; }
    public Guid? ModifiedByUserId { get; set; }

    // Versioning
    public int Version { get; internal set; } = 1;
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Unique identifier |
| `Alias` | `string` | Unique alias for code references (required) |
| `Name` | `string` | Display name (required) |
| `Description` | `string?` | Optional description |
| `AgentType` | `AIAgentType` | `Standard` or `Orchestrated` (immutable) |
| `Config` | `IAIAgentConfig?` | Type-specific configuration (see below) |
| `ProfileId` | `Guid?` | Associated AI profile (null uses default) |
| `GuardrailIds` | `IReadOnlyList<Guid>` | Guardrails applied during agent execution |
| `SurfaceIds` | `IReadOnlyList<string>` | Surface IDs for categorization |
| `Scope` | `AIAgentScope?` | Optional scoping rules |
| `IsActive` | `bool` | Whether agent is available |
| `DateCreated` | `DateTime` | When created |
| `DateModified` | `DateTime` | When last modified |
| `Version` | `int` | Current version number |

Agent Types

Configuration

Standard Agent Config

| Property | Type | Description |
|---|---|---|
| `ContextIds` | `IReadOnlyList<Guid>` | AI Contexts to inject |
| `Instructions` | `string?` | Agent system prompt |
| `AllowedToolIds` | `IReadOnlyList<string>` | Explicit tool permissions |
| `AllowedToolScopeIds` | `IReadOnlyList<string>` | Scope-based tool permissions |
| `OutputSchema` | `JsonElement?` | Optional JSON Schema to constrain the agent's output |
| `UserGroupPermissions` | `IReadOnlyDictionary<Guid, AIAgentUserGroupPermissions>` | Per-user-group permission overrides |

Orchestrated Agent Config

| Property | Type | Description |
|---|---|---|
| `WorkflowId` | `string?` | ID of the registered workflow |
| `Settings` | `JsonElement?` | Workflow-specific settings (JSON) |

Examples

Standard Agent

Orchestrated Agent

Related

Last updated

Was this helpful?