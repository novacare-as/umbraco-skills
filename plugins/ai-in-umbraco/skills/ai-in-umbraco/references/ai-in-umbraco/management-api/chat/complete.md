# Complete | AI in Umbraco

Get a complete chat response from the AI model.

Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/umbraco/ai/management/api/v1/chat/complete` | Use default chat profile |
| POST | `/umbraco/ai/management/api/v1/chat/{profileIdOrAlias}/complete` | Use specific profile |

Request

Headers

| Header | Value |
|---|---|
| Content-Type | `application/json` |

Body

```
{
    "messages": [
        {
            "role": "user",
            "content": "What is Umbraco CMS?"
        }
    ]
}
```

With Conversation History

Response

Success (200 OK)

Response Properties

| Property | Type | Description |
|---|---|---|
| `message.role` | string | Always "assistant" |
| `message.content` | string | The AI's response text |
| `finishReason` | string | Why the response ended (stop, length, and so on) |
| `usage.inputTokens` | int | Tokens in the request |
| `usage.outputTokens` | int | Tokens in the response |
| `usage.totalTokens` | int | Total tokens used |

Finish Reasons

| Reason | Description |
|---|---|
| `stop` | Natural completion |
| `length` | Max tokens reached |
| `contentFilter` | Content was filtered |

Errors

400 Bad Request

404 Not Found

Examples

cURL - Default Profile

cURL - Specific Profile

JavaScript (Fetch)

C# (HttpClient)

Last updated

Was this helpful?