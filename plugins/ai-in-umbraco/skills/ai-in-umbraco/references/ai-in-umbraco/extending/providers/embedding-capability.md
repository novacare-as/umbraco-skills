# Embedding Capability | AI in Umbraco

Implement the embedding capability for your custom provider.

Base Class

```
public abstract class AIEmbeddingCapabilityBase<TSettings>(IAIProvider provider)
    : AICapabilityBase<TSettings>(provider), IAICapability<TSettings>, IAIEmbeddingCapability
    where TSettings : class
{
    // Override this (or CreateGeneratorAsync) to create an IEmbeddingGenerator
    protected virtual IEmbeddingGenerator<string, Embedding<float>> CreateGenerator(
        TSettings settings, string? modelId) { /* ... */ }

    // Override this for an async variant
    protected virtual Task<IEmbeddingGenerator<string, Embedding<float>>> CreateGeneratorAsync(
        TSettings settings, string? modelId, CancellationToken cancellationToken = default) { /* ... */ }

    // Implement this: Return available models
    protected abstract Task<IReadOnlyList<AIModelDescriptor>> GetModelsAsync(
        TSettings settings,
        CancellationToken cancellationToken = default);
}
```

Basic Implementation

Register in Provider

Implementing IEmbeddingGenerator

Complete IEmbeddingGenerator Example

Using Existing M.E.AI Generators

Handling Batches

Dimension Information

Last updated

Was this helpful?