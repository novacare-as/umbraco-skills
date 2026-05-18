# Update | AI in Umbraco

Update an existing agent.

Request

```
PUT /umbraco/ai/management/api/v1/agents/{agentIdOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `agentIdOrAlias` | string | Agent GUID or alias |

Request Body

```
{
    "alias": "content-assistant",
    "name": "Content Assistant (Updated)",
    "description": "Helps users write and improve content with AI",
    "profileId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "guardrailIds": [],
    "surfaceIds": ["copilot"],
    "scope": null,
    "config": {
        "$type": "standard",
        "contextIds": ["e401f2ff-7d65-5c12-a1f7-e812859a1962"],
        "instructions": "Updated instructions...",
        "allowedToolIds": [],
        "allowedToolScopeIds": ["content-read", "content-write", "search"],
        "userGroupPermissions": {}
    },
    "isActive": true
}
```

Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `alias` | string | Yes | Unique alias (URL-safe, max 100 chars) |
| `name` | string | Yes | Display name (max 255 chars) |
| `description` | string | No | Optional description (max 1000 chars) |
| `profileId` | guid | No | Associated AI profile (null uses default) |
| `guardrailIds` | guid[] | No | Guardrail IDs for safety and compliance checks |
| `surfaceIds` | string[] | No | Surface IDs for categorization |
| `scope` | object | No | Optional scope defining where the agent is available |
`config` | object | No | Type-specific configuration (see
|

`isActive`

Response

Success

Not Found

Examples

Last updated

Was this helpful?