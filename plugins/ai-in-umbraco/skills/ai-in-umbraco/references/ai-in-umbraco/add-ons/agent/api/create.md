# Create | AI in Umbraco

Create a new agent.

Request

```
POST /umbraco/ai/management/api/v1/agents
```

Request Body (Standard Agent)

```
{
    "alias": "content-assistant",
    "name": "Content Assistant",
    "description": "Helps users write and improve content",
    "agentType": "standard",
    "profileId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "guardrailIds": [],
    "surfaceIds": ["copilot"],
    "scope": null,
    "config": {
        "$type": "standard",
        "contextIds": ["e401f2ff-7d65-5c12-a1f7-e812859a1962"],
        "instructions": "You are a helpful content assistant.\n\nYour role is to help users write and improve content.",
        "allowedToolIds": [],
        "allowedToolScopeIds": ["content-read", "search"],
        "userGroupPermissions": {}
    }
}
```

Request Body (Orchestrated Agent)

Common Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `alias` | string | Yes | Unique alias (URL-safe, max 100 chars, letters, numbers, hyphens, underscores) |
| `name` | string | Yes | Display name (max 255 chars) |
| `description` | string | No | Optional description (max 1000 chars) |
| `agentType` | string | Yes | `standard` or `orchestrated` |
| `profileId` | guid | No | Associated AI profile (null uses default) |
| `guardrailIds` | guid[] | No | Guardrail IDs for safety and compliance checks |
| `surfaceIds` | string[] | No | Surface IDs for categorization |
| `scope` | object | No | Optional scope defining where the agent is available |
| `config` | object | No | Type-specific configuration (see below) |

Standard Config (

`$type: "standard"`

)| Property | Type | Description |
|---|---|---|
| `contextIds` | guid[] | AI Contexts to inject |
| `instructions` | string | Agent system prompt |
| `allowedToolIds` | string[] | Explicit tool permissions |
| `allowedToolScopeIds` | string[] | Scope-based tool permissions |
| `outputSchema` | object | Optional JSON Schema constraining agent output |
| `userGroupPermissions` | object | Per-user-group overrides (keyed by group ID) |

Orchestrated Config (

`$type: "orchestrated"`

)| Property | Type | Description |
|---|---|---|
| `workflowId` | string | ID of the registered workflow |
| `settings` | object | Workflow-specific settings (JSON) |

Response

Success

Alias Conflict

Validation Error

Examples

Create Standard Agent

Create Orchestrated Agent

Last updated

Was this helpful?