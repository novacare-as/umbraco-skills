# Chat | AI in Umbraco

Use the chat API for conversational AI, text generation, and completions.

IAIChatService

```
public interface IAIChatService
{
    // Non-streaming responses
    Task<ChatResponse> GetChatResponseAsync(
        Action<AIChatBuilder> configure,
        IEnumerable<ChatMessage> messages,
        CancellationToken cancellationToken = default);

    // Streaming responses
    IAsyncEnumerable<ChatResponseUpdate> StreamChatResponseAsync(
        Action<AIChatBuilder> configure,
        IEnumerable<ChatMessage> messages,
        CancellationToken cancellationToken = default);

    // Advanced: Create the underlying client
    Task<IChatClient> CreateChatClientAsync(
        Action<AIChatBuilder> configure,
        CancellationToken cancellationToken = default);
}
```

Basic Usage

Message Roles

| Role | Description |
|---|---|
| `ChatRole.System` | Instructions for the AI (set behavior, context) |
| `ChatRole.User` | Messages from the user |
| `ChatRole.Assistant` | Previous responses from the AI |
| `ChatRole.Tool` | Results from tool/function calls |

Multi-Turn Conversations

Choosing a Profile

Default Profile

Specific Profile

In This Section

Last updated

Was this helpful?

## Sub-topics

- [Advanced Options | AI in Umbraco](chat/advanced-options.md)
- [Basic Chat | AI in Umbraco](chat/basic-chat.md)
- [Streaming | AI in Umbraco](chat/streaming.md)
- [Structured Output | AI in Umbraco](chat/structured-output.md)
- [System Prompts | AI in Umbraco](chat/system-prompts.md)
