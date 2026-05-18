# Middleware | AI in Umbraco

Add cross-cutting concerns to AI operations with middleware.

How Middleware Works

Middleware Types

| Type | Interface | Wraps |
|---|---|---|
| Chat | `IAIChatMiddleware` | `IChatClient` |
| Embedding | `IAIEmbeddingMiddleware` | `IEmbeddingGenerator<string, Embedding<float>>` |

Quick Example

```
using Microsoft.Extensions.AI;
using Microsoft.Extensions.Logging;
using Umbraco.AI.Core.Chat;

public class LoggingChatMiddleware : IAIChatMiddleware
{
    private readonly ILoggerFactory _loggerFactory;

    public LoggingChatMiddleware(ILoggerFactory loggerFactory)
    {
        _loggerFactory = loggerFactory;
    }

    public IChatClient Apply(IChatClient client)
    {
        return client.AsBuilder()
            .UseLogging(_loggerFactory)
            .Build();
    }
}
```

Key Concepts

Middleware Order Matters

Middleware Receives Dependencies

Using M.E.AI Middleware

In This Section

Last updated

Was this helpful?

## Sub-topics

- [Chat Middleware | AI in Umbraco](middleware/chat-middleware.md)
- [Embedding Middleware | AI in Umbraco](middleware/embedding-middleware.md)
- [Middleware Ordering | AI in Umbraco](middleware/middleware-ordering.md)
