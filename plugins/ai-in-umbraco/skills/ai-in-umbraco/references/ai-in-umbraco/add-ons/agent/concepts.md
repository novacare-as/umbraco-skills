# Concepts | AI in Umbraco

Core concepts for Agent Runtime.

What is an Agent?

Agent Types

Standard Agent

Orchestrated Agent

Agent Properties

Common Properties

| Property | Description |
|---|---|
| `Alias` | Unique identifier for code references |
| `Name` | Display name in the backoffice |
| `Description` | Optional description |
| `AgentType` | `Standard` or `Orchestrated` (immutable) |
| `ProfileId` | Associated AI profile (or uses default) |
| `GuardrailIds` | Guardrails applied during agent execution |
| `SurfaceIds` | Surface IDs for categorization (e.g., "copilot") |
| `Scope` | Optional scoping rules (sections, entity types) |
| `IsActive` | Whether the agent is available |

Standard Agent Configuration

| Property | Description |
|---|---|
| `Instructions` | System prompt defining agent behavior |
| `ContextIds` | AI Contexts to inject |
| `AllowedToolIds` | Explicit tool permissions |
| `AllowedToolScopeIds` | Scope-based tool permissions |
| `OutputSchema` | Optional JSON Schema constraining output |
| `UserGroupPermissions` | Per-user-group permission overrides |

Orchestrated Agent Configuration

| Property | Description |
|---|---|
| `WorkflowId` | ID of the registered workflow to use |
| `Settings` | Workflow-specific settings (JSON) |

AG-UI Protocol

Event Categories

Lifecycle Events

| Event | Description |
|---|---|
| `RUN_STARTED` | Agent run has begun |
| `RUN_FINISHED` | Agent run completed successfully |
| `RUN_ERROR` | Agent run failed with error |

Text Message Events

| Event | Description |
|---|---|
| `TEXT_MESSAGE_START` | Beginning of a text message |
| `TEXT_MESSAGE_CONTENT` | Text content chunk |
| `TEXT_MESSAGE_END` | End of a text message |

Tool Events

| Event | Description |
|---|---|
| `TOOL_CALL_START` | Tool call initiated |
| `TOOL_CALL_ARGS` | Tool argument chunk |
| `TOOL_CALL_END` | Tool call complete |
| `TOOL_CALL_RESULT` | Tool execution result |

State Events

| Event | Description |
|---|---|
| `STATE_SNAPSHOT` | Complete state update |
| `STATE_DELTA` | Incremental state change |

Agent vs Prompt

| Aspect | Prompt | Agent |
|---|---|---|
| Execution | Single request/response | Streaming conversation |
| Protocol | Simple HTTP | SSE with AG-UI events |
| Tools | No tool support | Frontend tool definitions |
| Use Case | One-shot generation | Interactive assistance |
| Complexity | Simple | More complex |

How Agents Work

Standard Agent Execution

Orchestrated Agent Execution

Frontend Tools

Version History

Best Practices

Related

Last updated

Was this helpful?