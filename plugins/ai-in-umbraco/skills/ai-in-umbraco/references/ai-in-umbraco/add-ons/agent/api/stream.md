# Stream | AI in Umbraco

Stream agent response updates as Server-Sent Events.

Request

```
POST /umbraco/ai/management/api/v1/agents/{agentIdOrAlias}/stream
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `agentIdOrAlias` | string | Agent GUID or alias |

Request Body

```
{
    "messages": [
        {
            "role": "user",
            "content": "Help me write a blog post about AI"
        }
    ]
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `messages` | array | Yes | Conversation messages (must contain at least one message) |
| `messages[].role` | string | Yes | Message role: `user` , `assistant` , `system` , `tool` , `developer` |
| `messages[].content` | string | No | Plain-text message content |
| `messages[].contentParts` | array | No | Multimodal content parts (takes precedence over `content` ) |

Response

Error Handling

Examples

Consume with cURL

Related

Last updated

Was this helpful?