# Chat Middleware | AI in Umbraco

Create middleware to intercept and modify chat operations.

Interface

```
public interface IAIChatMiddleware
{
    IChatClient Apply(IChatClient client);
}
```

Basic Implementation

```
using Microsoft.Extensions.AI;
using Umbraco.AI.Core.Chat;

public class SimpleChatMiddleware : IAIChatMiddleware
{
    public IChatClient Apply(IChatClient client)
    {
        return new SimpleChatClientWrapper(client);
    }
}
```

Creating a Custom Wrapper

Using M.E.AI Built-in Middleware

Available M.E.AI Middleware

| Method | Purpose |
|---|---|
| `UseLogging()` | Log requests and responses |
| `UseOpenTelemetry()` | Add OpenTelemetry tracing |
| `UseFunctionInvocation()` | Enable tool/function calling |
| `UseDistributedCache()` | Cache responses |

Registering Chat Middleware

Last updated

Was this helpful?