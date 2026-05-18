# Speech-to-Text Capability | AI in Umbraco

Implement the speech-to-text capability for your custom provider.

Base Class

```
public abstract class AISpeechToTextCapabilityBase<TSettings>(IAIProvider provider)
    : AICapabilityBase<TSettings>(provider), IAICapability<TSettings>, IAISpeechToTextCapability
    where TSettings : class
{
    // Override this (or CreateClientAsync) to create an ISpeechToTextClient
    protected virtual ISpeechToTextClient CreateClient(TSettings settings, string? modelId) { /* ... */ }

    // Override this for an async variant
    protected virtual Task<ISpeechToTextClient> CreateClientAsync(
        TSettings settings, string? modelId, CancellationToken cancellationToken = default) { /* ... */ }

    // Implement this: Return available models
    protected abstract Task<IReadOnlyList<AIModelDescriptor>> GetModelsAsync(
        TSettings settings,
        CancellationToken cancellationToken = default);
}
```

Basic Implementation

Register in Provider

Using Existing

`Microsoft.Extensions.AI`

ClientsRelated

Last updated

Was this helpful?