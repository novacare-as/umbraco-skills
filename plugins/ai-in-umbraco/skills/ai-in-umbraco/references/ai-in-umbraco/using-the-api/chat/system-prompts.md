# System Prompts | AI in Umbraco

Control AI behavior with system prompts in chat requests.

Adding a System Prompt

```
var messages = new List<ChatMessage>
{
    new(ChatRole.System, "You are a helpful content editor for an Umbraco website. " +
                         "Always respond in a professional tone. " +
                         "Keep answers concise and actionable."),
    new(ChatRole.User, "Suggest a better title for my blog post about CMS platforms.")
};

var response = await _chatService.GetChatResponseAsync(
    chat => chat.WithAlias("content-editor"),
    messages);
```

Profile-Level System Prompts

```
var profile = new AIProfile
{
    Alias = "content-assistant",
    Name = "Content Assistant",
    Capability = AICapability.Chat,
    ConnectionId = connectionId,
    Model = new AIModelRef("openai", "gpt-4o"),
    Settings = new AIChatProfileSettings
    {
        SystemPromptTemplate = "You are a content assistant for an Umbraco website. " +
                               "Help editors write engaging content."
    }
};

await _profileService.SaveProfileAsync(profile);
```

System Prompt Best Practices

Related

Last updated

Was this helpful?

Control AI behavior with system prompts in chat requests.

System prompts set the AI model's role, personality, and constraints. They are sent as the first message in a conversation and shape how the model responds to all subsequent messages.

Adding a System Prompt

Include a `ChatRole.System`

message at the start of your messages list:

SystemPrompt.cs

```
var messages = new List<ChatMessage>
{
    new(ChatRole.System, "You are a helpful content editor for an Umbraco website. " +
                         "Always respond in a professional tone. " +
                         "Keep answers concise and actionable."),
    new(ChatRole.User, "Suggest a better title for my blog post about CMS platforms.")
};

var response = await _chatService.GetChatResponseAsync(
    chat => chat.WithAlias("content-editor"),
    messages);
```

Profile-Level System Prompts

Rather than including system prompts in every request, configure them on the profile. The system prompt is then applied automatically:

ProfileSystemPrompt.cs

```
var profile = new AIProfile
{
    Alias = "content-assistant",
    Name = "Content Assistant",
    Capability = AICapability.Chat,
    ConnectionId = connectionId,
    Model = new AIModelRef("openai", "gpt-4o"),
    Settings = new AIChatProfileSettings
    {
        SystemPromptTemplate = "You are a content assistant for an Umbraco website. " +
                               "Help editors write engaging content."
    }
};

await _profileService.SaveProfileAsync(profile);
```

When using this profile, the system prompt is injected automatically. You only need to send user messages:

If you include a system message in your request and the profile also has a system prompt, both are sent. The profile's system prompt comes first.

System Prompt Best Practices

**Be specific about the role**- "You are a content editor" is better than "You are helpful"**Set constraints early**- Include tone, length, and format requirements**Use profiles for reuse**- Configure system prompts on profiles rather than hardcoding them in every request

Related

[Basic Chat](/ai-in-umbraco/using-the-api/chat/basic-chat)- Sending chat requests[Profiles](/ai-in-umbraco/concepts/profiles)- Configuring profile settings

Last updated

Was this helpful?

Was this helpful?

UsingProfilePrompt.cs

```
var messages = new List<ChatMessage>
{
    new(ChatRole.User, "Write a meta description for our About page.")
};

// The profile's system prompt is prepended automatically
var response = await _chatService.GetChatResponseAsync(
    chat => chat.WithAlias("content-assistant").WithProfile(profileId),
    messages);
```