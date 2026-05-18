# Streaming | AI in Umbraco

Handling SSE streaming and AG-UI events.

```
data: {"type":"RUN_STARTED","threadId":"t-1","runId":"r-1"}

data: {"type":"TEXT_MESSAGE_START","messageId":"m-1","role":"assistant"}

data: {"type":"TEXT_MESSAGE_CONTENT","messageId":"m-1","delta":"Hello"}

data: {"type":"TEXT_MESSAGE_CONTENT","messageId":"m-1","delta":" world"}

data: {"type":"TEXT_MESSAGE_END","messageId":"m-1"}

data: {"type":"RUN_FINISHED","threadId":"t-1","runId":"r-1","outcome":"success"}
```

| Property | Type | Description |
|---|---|---|
| `timestamp` | `number` | Optional Unix milliseconds timestamp. |
| `rawEvent` | `object` | Optional passthrough of the underlying provider event. |

| Property | Type | Required | Description |
|---|---|---|---|
| `threadId` | `string` | Yes | Conversation thread identifier. |
| `runId` | `string` | Yes | Identifier for this run. |
| `parentRunId` | `string` | No | Set when this run is nested inside another run. |
| `input` | `JsonElement` | No | Optional input payload captured at the start. |

| Property | Type | Required | Description |
|---|---|---|---|
| `threadId` | `string` | Yes | Conversation thread identifier. |
| `runId` | `string` | Yes | Identifier for the completed run. |
| `outcome` | `string` | Yes | `success` or `interrupt` . Defaults to `success` . |
| `interrupt` | `object` | No | Set when `outcome` is `interrupt` . |
| `error` | `string` | No | Optional error message string. |
| `result` | `object` | No | Optional result payload. |

| Property | Type | Required | Description |
|---|---|---|---|
| `message` | `string` | Yes | Human-readable error message. |
| `code` | `string` | No | Optional machine-readable error code. |

| Property | Type | Required | Description |
|---|---|---|---|
| `messageId` | `string` | Yes | Identifier of the message being streamed. |
| `role` | `string` | Yes | Message role (`user` , `assistant` , `system` , `tool` , etc.) |

| Property | Type | Required | Description |
|---|---|---|---|
| `messageId` | `string` | Yes | Identifier of the message being streamed |
| `delta` | `string` | Yes | Text fragment to append to the message. |

| Property | Type | Required | Description |
|---|---|---|---|
| `toolCallId` | `string` | Yes | Unique identifier for this tool call. |
| `toolCallName` | `string` | Yes | Name of the tool being invoked. |
| `parentMessageId` | `string` | No | Optional ID of the assistant message this call belongs to. |

| Property | Type | Required | Description |
|---|---|---|---|
| `messageId` | `string` | Yes | Identifier of the tool result message. |
| `toolCallId` | `string` | Yes | Identifier of the tool call being answered. |
| `content` | `string` | Yes | Serialised result content. |
| `role` | `string` | No | Role for the result (typically `"tool"` ). |

| Property | Type | Required | Description |
|---|---|---|---|
| `messageId` | `string` | Yes | Identifier of the activity message. |
| `activityType` | `string` | Yes | Activity category (e.g., `thinking` , `searching` , `processing` ). |
| `content` | `string` | Yes | Activity content to display. |
| `replace` | `boolean` | No | When `true` , replaces any existing activity with the same `messageId` . |

Last updated

Was this helpful?