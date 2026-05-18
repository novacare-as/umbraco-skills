# Custom Providers | AI in Umbraco

Create custom AI providers to support additional AI services.

Provider Architecture

```
MyProvider/
├── MyProvider.cs              # Main provider class
├── MyProviderSettings.cs      # Settings with [AIField] attributes
├── MyChatCapability.cs        # Chat capability implementation
└── MyEmbeddingCapability.cs   # Embedding capability (optional)
```

Quick Start

1. Create a Settings Class

```
using Umbraco.AI.Core.EditableModels;

public class MyProviderSettings
{
    [AIField(Label = "API Key", Description = "Your API key", IsSensitive = true)]
    public string? ApiKey { get; set; }

    [AIField(Label = "Endpoint", Description = "API endpoint URL")]
    public string? Endpoint { get; set; }
}
```

2. Create a Chat Capability

3. Create the Provider Class

How It Works

In This Section

[Creating a Provider chevron-right](/ai-in-umbraco/extending/providers/creating-a-provider)

Last updated

Was this helpful?

## Sub-topics

- [Chat Capability | AI in Umbraco](providers/chat-capability.md)
- [Creating a Provider | AI in Umbraco](providers/creating-a-provider.md)
- [Embedding Capability | AI in Umbraco](providers/embedding-capability.md)
- [Provider Settings | AI in Umbraco](providers/provider-settings.md)
- [Speech-to-Text Capability | AI in Umbraco](providers/speech-to-text-capability.md)
