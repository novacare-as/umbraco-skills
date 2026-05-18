# Stream (AG-UI) | AI in Umbraco

Stream AG-UI protocol events as Server-Sent Events.

Request

```
POST /umbraco/ai/management/api/v1/agents/{agentIdOrAlias}/stream-agui
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `agentIdOrAlias` | string | Agent GUID, alias, or the special value `auto` for automatic selection |

Request Body

```
{
    "threadId": "thread-123",
    "runId": "run-456",
    "messages": [
        {
            "id": "msg-1",
            "role": "user",
            "content": "Help me write a blog post about AI"
        }
    ],
    "tools": [
        {
            "name": "insert_content",
            "description": "Insert content at the cursor",
            "parameters": {
                "type": "object",
                "properties": {
                    "content": { "type": "string" }
                },
                "required": ["content"]
            }
        }
    ],
    "context": [
        { "description": "surface", "value": "copilot" }
    ],
    "state": null,
    "forwardedProps": {
        "toolMetadata": [
            { "toolName": "insert_content", "scope": "content-write", "isDestructive": false }
        ]
    }
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `threadId` | string | Yes | The conversation thread identifier |
| `runId` | string | Yes | The run identifier |
| `messages` | array | Yes | Conversation messages in AG-UI format |
| `tools` | array | No | Frontend tool definitions available to the agent |
| `context` | array | No | AG-UI context items (each has `description` and `value` ) |
| `state` | object | No | Current state as JSON |
| `resume` | object | No | Resume information for continuing from an interrupt |
| `forwardedProps` | object | No | Additional properties forwarded to the agent |

Response

Event Types

| Event type | Category | Description |
|---|---|---|
| `RUN_STARTED` | Lifecycle | Agent run has begun |
| `RUN_FINISHED` | Lifecycle | Agent run completed successfully |
| `RUN_ERROR` | Lifecycle | Agent run failed |
| `STEP_STARTED` | Lifecycle | A step within the run has begun |
| `STEP_FINISHED` | Lifecycle | A step within the run has finished |
| `TEXT_MESSAGE_START` | Message | Beginning of a text message |
| `TEXT_MESSAGE_CONTENT` | Message | Text content delta |
| `TEXT_MESSAGE_END` | Message | End of a text message |
| `TEXT_MESSAGE_CHUNK` | Message | Combined message chunk |
| `TOOL_CALL_START` | Tools | Tool call initiated |
| `TOOL_CALL_ARGS` | Tools | Tool arguments delta |
| `TOOL_CALL_END` | Tools | Tool call arguments complete |
| `TOOL_CALL_RESULT` | Tools | Tool result |
| `TOOL_CALL_CHUNK` | Tools | Combined tool call chunk |
| `STATE_SNAPSHOT` | State | Full state snapshot |
| `STATE_DELTA` | State | State change (JSON Patch) |
| `MESSAGES_SNAPSHOT` | State | Full messages snapshot |
| `ACTIVITY_SNAPSHOT` | Activity | Activity snapshot |
| `ACTIVITY_DELTA` | Activity | Activity change |
| `CUSTOM` | Special | Custom event (used for e.g. `agent_selected` in auto mode) |
| `RAW` | Special | Passthrough raw event |

Auto Agent Selection

Error Responses

Examples

Consume with cURL

Related

Last updated

Was this helpful?