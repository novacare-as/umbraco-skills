# API | AI in Umbraco

Management API endpoints for the Agent add-on.

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET |
| `/agents` |

`/agents/{agentIdOrAlias}`

`/agents`

`/agents/{agentIdOrAlias}`

`/agents/{agentIdOrAlias}`

`/agents/{alias}/exists`

`/agents/surfaces`

`/agents/workflows`

`/agents/{agentIdOrAlias}/run`

`/agents/{agentIdOrAlias}/stream`

`/agents/{agentIdOrAlias}/stream-agui`

Base URL

```
/umbraco/ai/management/api/v1
```

Agent Object

Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Unique identifier |
| `alias` | string | Unique alias for code references |
| `name` | string | Display name |
| `description` | string | Optional description |
| `agentType` | string | `standard` or `orchestrated` |
| `profileId` | guid | Associated AI profile (null uses default) |
| `guardrailIds` | guid[] | Guardrail IDs for safety and compliance checks |
| `surfaceIds` | string[] | Surface IDs for categorization |
| `scope` | object | Optional scope defining where the agent is available (see below) |
| `config` | object | Type-specific configuration (see below) |
| `isActive` | bool | Whether the agent is available |
| `dateCreated` | datetime | When the agent was created (UTC) |
| `dateModified` | datetime | When the agent was last modified (UTC) |
| `version` | int | Current version number |

Scope (

`scope`

)| Property | Type | Description |
|---|---|---|
| `allowRules` | rule[] | Rules where the agent is available (OR between rules) |
| `denyRules` | rule[] | Rules where the agent is denied (takes precedence) |

| Property | Type | Description |
|---|---|---|
| `sections` | string[] | Section pathnames (e.g., `content` , `media` ) |
| `entityTypes` | string[] | Entity types (e.g., `document` , `media` ) |

Standard Config (

`config`

when `agentType`

is `standard`

)| Property | Type | Description |
|---|---|---|
| `$type` | string | Always `"standard"` |
| `contextIds` | guid[] | AI Contexts to inject |
| `instructions` | string | Agent system prompt |
| `allowedToolIds` | string[] | Explicit tool permissions |
| `allowedToolScopeIds` | string[] | Scope-based tool permissions |
| `outputSchema` | object | Optional JSON Schema constraining agent output |
| `userGroupPermissions` | object | Per-user-group permission overrides (keyed by group ID) |

Orchestrated Config (

`config`

when `agentType`

is `orchestrated`

)| Property | Type | Description |
|---|---|---|
| `$type` | string | Always `"orchestrated"` |
| `workflowId` | string | ID of the registered workflow |
| `settings` | object | Workflow-specific settings (JSON) |

Related

Last updated

Was this helpful?

## Sub-topics

- [Create | AI in Umbraco](api/create.md)
- [Delete | AI in Umbraco](api/delete.md)
- [Get | AI in Umbraco](api/get.md)
- [List | AI in Umbraco](api/list.md)
- [Run | AI in Umbraco](api/run.md)
- [Stream (AG-UI) | AI in Umbraco](api/stream-agui.md)
- [Stream | AI in Umbraco](api/stream.md)
- [Update | AI in Umbraco](api/update.md)
