# Get | AI in Umbraco

Get an agent by ID or alias.

Request

```
GET /umbraco/ai/management/api/v1/agents/{agentIdOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `agentIdOrAlias` | string | Agent GUID or alias |

Response

Standard Agent

```
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
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
        "instructions": "You are a helpful content assistant...",
        "allowedToolIds": [],
        "allowedToolScopeIds": ["content-read", "search"],
        "outputSchema": null,
        "userGroupPermissions": {}
    },
    "isActive": true,
    "dateCreated": "2024-01-15T10:30:00Z",
    "dateModified": "2024-01-20T14:45:00Z",
    "version": 2
}
```

Orchestrated Agent

Not Found

Examples

Last updated

Was this helpful?