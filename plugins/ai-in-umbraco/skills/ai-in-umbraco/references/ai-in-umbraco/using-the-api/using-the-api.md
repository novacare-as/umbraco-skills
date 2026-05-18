# Overview | AI in Umbraco

Learn how to use Umbraco.AI services in your code for chat, embeddings, and more.

Primary Services

| Service | Purpose |
|---|---|
| `IAIChatService` | Chat completions and conversational AI |
| `IAIEmbeddingService` | Generate vector embeddings for text |

Dependency Injection (DI)

```
public class MyController : UmbracoApiController
{
    private readonly IAIChatService _chatService;
    private readonly IAIEmbeddingService _embeddingService;

    public MyController(
        IAIChatService chatService,
        IAIEmbeddingService embeddingService)
    {
        _chatService = chatService;
        _embeddingService = embeddingService;
    }
}
```

Using M.E.AI Types

| Type | Namespace | Purpose |
|---|---|---|
| `ChatMessage` | `Microsoft.Extensions.AI` | A message in a conversation |
| `ChatRole` | `Microsoft.Extensions.AI` | User, Assistant, System, Tool |
| `ChatResponse` | `Microsoft.Extensions.AI` | Complete response from chat |
| `ChatResponseUpdate` | `Microsoft.Extensions.AI` | Streaming response chunk |
| `ChatOptions` | `Microsoft.Extensions.AI` | Request options (temperature, and so on) |

Quick Examples

Chat Completion

Streaming Chat

Generate Embedding

In This Section

Last updated

Was this helpful?