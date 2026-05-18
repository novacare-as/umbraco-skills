# Chat | AI in Umbraco

Chat completion endpoints for conversational AI via the Management API.

Available Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/umbraco/ai/management/api/v1/chat/complete` | Get a chat completion using the default profile |
| POST | `/umbraco/ai/management/api/v1/chat/{profileIdOrAlias}/complete` | Get a chat completion using a specific profile |

Request Format

```
{
    "messages": [
        {
            "role": "system",
            "content": "You are a helpful assistant."
        },
        {
            "role": "user",
            "content": "Hello, how are you?"
        }
    ]
}
```

Message Roles

| Role | Description |
|---|---|
| `system` | Instructions for the AI (sets behavior) |
| `user` | Messages from the user |
| `assistant` | Previous responses from the AI |

Response Format

In This Section

Last updated

Was this helpful?

## Sub-topics

- [Complete | AI in Umbraco](chat/complete.md)
