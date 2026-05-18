# Basic Chat | AI in Umbraco

Send chat messages and receive complete responses from AI models.

Basic Request

```
using Microsoft.Extensions.AI;
using Umbraco.AI.Core.Chat;

public class ChatController : UmbracoApiController
{
    private readonly IAIChatService _chatService;

    public ChatController(IAIChatService chatService)
    {
        _chatService = chatService;
    }

    [HttpPost]
    public async Task<IActionResult> Ask([FromBody] string question)
    {
        var messages = new List<ChatMessage>
        {
            new(ChatRole.User, question)
        };

        var response = await _chatService.GetChatResponseAsync(
            chat => chat.WithAlias("chat-api"),
            messages);

        return Ok(new
        {
            Answer = response.Message.Text,
            TokensUsed = response.Usage?.TotalTokenCount
        });
    }
}
```

Understanding ChatResponse

| Property | Type | Description |
|---|---|---|
| `Message` | `ChatMessage` | The AI's response message |
| `FinishReason` | `ChatFinishReason?` | Why the response ended |
| `Usage` | `UsageDetails?` | Token usage statistics |
| `ModelId` | `string?` | The model that generated the response |

With System Prompt

Multi-Turn Conversation

Using a Specific Profile

By Profile ID

By Profile Alias

Overriding Profile Settings

Error Handling

Next Steps

Last updated

Was this helpful?