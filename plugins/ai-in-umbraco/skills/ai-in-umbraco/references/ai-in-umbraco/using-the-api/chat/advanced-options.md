# Advanced Options | AI in Umbraco

Fine-tune AI responses with ChatOptions for temperature, token limits, and more.

ChatOptions

```
var messages = new List<ChatMessage>
{
    new(ChatRole.User, "Write three tagline options for a coffee shop.")
};

var options = new ChatOptions
{
    Temperature = 0.9f,
    MaxOutputTokens = 200,
    TopP = 0.95f,
    StopSequences = ["---"]
};

var response = await _chatService.GetChatResponseAsync(
    chat => chat.WithAlias("tagline-writer").WithChatOptions(options),
    messages);
```

Available Options

| Option | Type | Description |
|---|---|---|
| `Temperature` | `float?` | Controls randomness (0 = deterministic, 1 = creative) |
| `MaxOutputTokens` | `int?` | Maximum tokens in the response |
| `TopP` | `float?` | Nucleus sampling threshold |
| `StopSequences` | `IList<string>?` | Sequences that stop generation |
| `FrequencyPenalty` | `float?` | Penalizes repeated tokens |
| `PresencePenalty` | `float?` | Penalizes tokens already present |
| `Seed` | `long?` | Seed for reproducible outputs |
| `ResponseFormat` | `ChatResponseFormat?` | Request JSON or text output |

Requesting JSON Output

Combining with Profiles

Related

Last updated

Was this helpful?