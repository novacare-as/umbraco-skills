# Run | AI in Umbraco

Run an agent and get the complete response as JSON.

Request

```
POST /umbraco/ai/management/api/v1/agents/{agentIdOrAlias}/run
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

Success

Error Responses

Examples

Basic Run

With Conversation History

Related

Last updated

Was this helpful?