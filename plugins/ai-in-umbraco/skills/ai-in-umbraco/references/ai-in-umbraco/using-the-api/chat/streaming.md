# Streaming | AI in Umbraco

Stream chat responses in real-time for a better user experience.

Why Use Streaming

| Approach | Best For |
|---|---|
| Non-streaming | Short responses, background processing |
| Streaming | User-facing chat, long responses, real-time feedback |

Basic Streaming

```
using Microsoft.Extensions.AI;
using Umbraco.AI.Core.Chat;

public class StreamingExample
{
    private readonly IAIChatService _chatService;

    public StreamingExample(IAIChatService chatService)
    {
        _chatService = chatService;
    }

    public async Task StreamToConsole(string question)
    {
        var messages = new List<ChatMessage>
        {
            new(ChatRole.User, question)
        };

        await foreach (var update in _chatService.StreamChatResponseAsync(
            chat => chat.WithAlias("console-stream"),
            messages))
        {
            // Each update contains a chunk of text
            Console.Write(update.Text);
        }

        Console.WriteLine(); // New line at end
    }
}
```

Understanding ChatResponseUpdate

| Property | Type | Description |
|---|---|---|
| `Text` | `string?` | The text content of this chunk |
| `Role` | `ChatRole?` | The role (usually only in first chunk) |
| `FinishReason` | `ChatFinishReason?` | Set in the final chunk |

Streaming in an API Controller

Collecting the Full Response

Using a Specific Profile

Next Steps

Last updated

Was this helpful?