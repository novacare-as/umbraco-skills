# AI in Umbraco

Umbraco.AI is a provider-agnostic AI integration layer for Umbraco CMS, built on Microsoft.Extensions.AI.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-6c4644bd3608f042b54be713d7d1f13676c6cb4d%252Fbackoffice-ai-section-overview.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fb1fcd49&sv=2)

Key Features

Getting Started

Core Concepts

Using the API

Extending

Quick Example

Requirements

Last updated

Was this helpful?

Umbraco.AI is a provider-agnostic AI integration layer for Umbraco CMS, built on Microsoft.Extensions.AI.

`Umbraco.AI`

brings AI capabilities to your Umbraco CMS installation through a flexible, provider-agnostic architecture. Whether you want to integrate OpenAI, Azure OpenAI, or other AI services, Umbraco.AI provides a consistent API and backoffice experience.

Key Features

**Provider-agnostic**- Install provider packages for the AI services you use**Profile-based configuration**- Create reusable profiles for different use cases**Built on Microsoft.Extensions.AI (M.E.AI)**- Uses standard M.E.AI types like`IChatClient`

and`ChatMessage`

**Extensible middleware**- Add logging, caching, rate limiting, and custom behavior**Backoffice integration**- Manage connections and profiles through the Umbraco UI

Getting Started

New to Umbraco.AI? Start here:

Core Concepts

Understand how Umbraco.AI is structured:

Using the API

Learn how to use AI services in your code:

Extending

Create custom providers, middleware, and tools:

Quick Example

Requirements

Umbraco CMS 17.1 or later

.NET 10.0 or later

At least one AI provider package (for example,

`Umbraco.AI.OpenAI`

)

Last updated

Was this helpful?

Was this helpful?

ChatController.cs

```
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.AI;
using Umbraco.AI.Core.Chat;

[ApiController]
[Route("/api/chat")]
public class ChatController : Controller
{
    private readonly IAIChatService _chatService;

    public ChatController(IAIChatService chatService)
    {
        _chatService = chatService;
    }

    [HttpPost]
    public async Task<IActionResult> Chat([FromBody] string message)
    {
        var messages = new List<ChatMessage>
        {
            new(ChatRole.User, message)
        };

        var response = await _chatService.GetChatResponseAsync(
            chat => chat.WithAlias("quick-chat"),
            messages);

        return Ok(response.Text);
    }
}
```

## Sub-topics

- [Overview | AI in Umbraco](ai-in-umbraco/add-ons/add-ons.md)
- [Agent Copilot | AI in Umbraco](ai-in-umbraco/add-ons/agent-copilot.md)
- [Agent Runtime | AI in Umbraco](ai-in-umbraco/add-ons/agent.md)
- [Deploy Support | AI in Umbraco](ai-in-umbraco/add-ons/deploy.md)
- [Prompt Management | AI in Umbraco](ai-in-umbraco/add-ons/prompt.md)
- [Semantic Search | AI in Umbraco](ai-in-umbraco/add-ons/search.md)
- [Audit Logs | AI in Umbraco](ai-in-umbraco/backoffice/audit-logs.md)
- [Overview | AI in Umbraco](ai-in-umbraco/backoffice/backoffice.md)
- [Managing Connections | AI in Umbraco](ai-in-umbraco/backoffice/managing-connections.md)
- [Managing Contexts | AI in Umbraco](ai-in-umbraco/backoffice/managing-contexts.md)
- [Managing Guardrails | AI in Umbraco](ai-in-umbraco/backoffice/managing-guardrails.md)
- [Managing Profiles | AI in Umbraco](ai-in-umbraco/backoffice/managing-profiles.md)
- [Managing Settings | AI in Umbraco](ai-in-umbraco/backoffice/managing-settings.md)
- [Usage Analytics | AI in Umbraco](ai-in-umbraco/backoffice/usage-analytics.md)
- [Version History | AI in Umbraco](ai-in-umbraco/backoffice/version-history.md)
- [Concepts](ai-in-umbraco/concepts.md)
- [Overview | AI in Umbraco](ai-in-umbraco/extending/extending.md)
- [Custom Guardrail Evaluators | AI in Umbraco](ai-in-umbraco/extending/guardrails.md)
- [Middleware | AI in Umbraco](ai-in-umbraco/extending/middleware.md)
- [Notifications | AI in Umbraco](ai-in-umbraco/extending/notifications.md)
- [Custom Providers | AI in Umbraco](ai-in-umbraco/extending/providers.md)
- [Custom Tools | AI in Umbraco](ai-in-umbraco/extending/tools.md)
- [Chat Controller | AI in Umbraco](ai-in-umbraco/frontend/chat-controller.md)
- [Chat Repository | AI in Umbraco](ai-in-umbraco/frontend/chat-repository.md)
- [Embeddings Controller | AI in Umbraco](ai-in-umbraco/frontend/embeddings-controller.md)
- [Overview | AI in Umbraco](ai-in-umbraco/frontend/frontend.md)
- [Speech-to-Text Controller | AI in Umbraco](ai-in-umbraco/frontend/speech-to-text-controller.md)
- [Tool Controller | AI in Umbraco](ai-in-umbraco/frontend/tool-controller.md)
- [Types | AI in Umbraco](ai-in-umbraco/frontend/types.md)
- [The First Connection | AI in Umbraco](ai-in-umbraco/getting-started/first-connection.md)
- [The First Profile | AI in Umbraco](ai-in-umbraco/getting-started/first-profile.md)
- [Overview | AI in Umbraco](ai-in-umbraco/getting-started/getting-started.md)
- [Installation | AI in Umbraco](ai-in-umbraco/getting-started/installation.md)
- [Analytics | AI in Umbraco](ai-in-umbraco/management-api/analytics.md)
- [Audit Logs | AI in Umbraco](ai-in-umbraco/management-api/audit-logs.md)
- [Chat | AI in Umbraco](ai-in-umbraco/management-api/chat.md)
- [Connections | AI in Umbraco](ai-in-umbraco/management-api/connections.md)
- [Context Resource Types | AI in Umbraco](ai-in-umbraco/management-api/context-resource-types.md)
- [Contexts | AI in Umbraco](ai-in-umbraco/management-api/contexts.md)
- [Embeddings | AI in Umbraco](ai-in-umbraco/management-api/embeddings.md)
- [Guardrails | AI in Umbraco](ai-in-umbraco/management-api/guardrails.md)
- [Overview | AI in Umbraco](ai-in-umbraco/management-api/management-api.md)
- [Profiles | AI in Umbraco](ai-in-umbraco/management-api/profiles.md)
- [Providers | AI in Umbraco](ai-in-umbraco/management-api/providers.md)
- [Settings | AI in Umbraco](ai-in-umbraco/management-api/settings.md)
- [Tools | AI in Umbraco](ai-in-umbraco/management-api/tools.md)
- [Versions | AI in Umbraco](ai-in-umbraco/management-api/versions.md)
- [Amazon Bedrock | AI in Umbraco](ai-in-umbraco/providers/amazon.md)
- [Anthropic | AI in Umbraco](ai-in-umbraco/providers/anthropic.md)
- [Google Gemini | AI in Umbraco](ai-in-umbraco/providers/google.md)
- [Microsoft AI Foundry | AI in Umbraco](ai-in-umbraco/providers/microsoft-foundry.md)
- [OpenAI | AI in Umbraco](ai-in-umbraco/providers/openai.md)
- [Overview | AI in Umbraco](ai-in-umbraco/providers/providers.md)
- [Configuration | AI in Umbraco](ai-in-umbraco/reference/configuration.md)
- [Models | AI in Umbraco](ai-in-umbraco/reference/models.md)
- [Overview | AI in Umbraco](ai-in-umbraco/reference/reference.md)
- [Services](ai-in-umbraco/reference/services.md)
- [Api](ai-in-umbraco/testing-and-evaluation/api.md)
- [Concepts | AI in Umbraco](ai-in-umbraco/testing-and-evaluation/concepts.md)
- [Getting Started | AI in Umbraco](ai-in-umbraco/testing-and-evaluation/getting-started.md)
- [Graders | AI in Umbraco](ai-in-umbraco/testing-and-evaluation/graders.md)
- [Overview | AI in Umbraco](ai-in-umbraco/testing-and-evaluation/tests.md)
- [Variations | AI in Umbraco](ai-in-umbraco/testing-and-evaluation/variations.md)
- [Chat | AI in Umbraco](ai-in-umbraco/using-the-api/chat.md)
- [Embeddings | AI in Umbraco](ai-in-umbraco/using-the-api/embeddings.md)
- [Speech-to-Text | AI in Umbraco](ai-in-umbraco/using-the-api/speech-to-text.md)
- [Tools | AI in Umbraco](ai-in-umbraco/using-the-api/tools.md)
- [Overview | AI in Umbraco](ai-in-umbraco/using-the-api/using-the-api.md)
