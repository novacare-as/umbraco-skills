# Chat Capability | AI in Umbraco

Implement the chat capability for your custom provider.

Base Class

```
public abstract class AIChatCapabilityBase<TSettings>(IAIProvider provider)
    : AICapabilityBase<TSettings>(provider), IAICapability<TSettings>, IAIChatCapability
    where TSettings : class
{
    // Override this (or CreateClientAsync) to create an IChatClient
    protected virtual IChatClient CreateClient(TSettings settings, string? modelId) { /* ... */ }

    // Override this for an async variant
    protected virtual Task<IChatClient> CreateClientAsync(
        TSettings settings, string? modelId, CancellationToken cancellationToken = default) { /* ... */ }

    // Implement this: Return available models
    protected abstract Task<IReadOnlyList<AIModelDescriptor>> GetModelsAsync(
        TSettings settings,
        CancellationToken cancellationToken = default);
}
```

Basic Implementation

Implementing IChatClient

Complete IChatClient Example

Using Existing M.E.AI Clients

Handling ChatOptions

Last updated

Was this helpful?