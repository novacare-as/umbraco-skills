# Frontend Tools | AI in Umbraco

Defining frontend tools that agents can call from the Copilot chat UI.

How Frontend Tools Work

Anatomy of a Frontend Tool

Defining a Tool

1. Implement the Tool Api

2. Register the Manifests

`uaiAgentFrontendTool`

meta reference| Field | Required | Description |
|---|---|---|
| `toolName` | Yes | Name sent to the LLM and matched in AG-UI `TOOL_CALL_START` events. |
| `description` | Yes | Description shown to the LLM so it can choose the tool. |
| `parameters` | Yes | JSON Schema describing the arguments object. |
| `scope` | No | Permission grouping string (for example `"entity-write"` , `"navigation"` ). Used by agent permissions to decide which tools an agent may call. |
| `isDestructive` | No | When `true` , signals a destructive action. Used together with `scope` for permission filtering. |

`uaiAgentToolRenderer`

meta reference| Field | Required | Description |
|---|---|---|
| `toolName` | Yes | Must match the `toolName` of the corresponding frontend tool. |
| `label` | No | Display label used in the transcript and in approval dialogs. |
| `icon` | No | Icon shown next to the tool call. |
`approval` | No | HITL approval configuration — see
|

Human-in-the-Loop Approval

Generative UI

Tool Schema

Best Practices

Related

Last updated

Was this helpful?