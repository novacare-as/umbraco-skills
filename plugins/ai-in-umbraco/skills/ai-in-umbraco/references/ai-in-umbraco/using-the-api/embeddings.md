# Embeddings | AI in Umbraco

Generate vector embeddings for semantic search, similarity matching, and RAG applications.

What Are Embeddings

IAIEmbeddingService

```
public interface IAIEmbeddingService
{
    // Single embedding
    Task<Embedding<float>> GenerateEmbeddingAsync(
        string value,
        EmbeddingGenerationOptions? options = null,
        CancellationToken cancellationToken = default);

    Task<Embedding<float>> GenerateEmbeddingAsync(
        Guid profileId,
        string value,
        EmbeddingGenerationOptions? options = null,
        CancellationToken cancellationToken = default);

    // Multiple embeddings
    Task<GeneratedEmbeddings<Embedding<float>>> GenerateEmbeddingsAsync(
        IEnumerable<string> values,
        EmbeddingGenerationOptions? options = null,
        CancellationToken cancellationToken = default);

    Task<GeneratedEmbeddings<Embedding<float>>> GenerateEmbeddingsAsync(
        Guid profileId,
        IEnumerable<string> values,
        EmbeddingGenerationOptions? options = null,
        CancellationToken cancellationToken = default);

    // Advanced: Get the underlying generator
    Task<IEmbeddingGenerator<string, Embedding<float>>> GetEmbeddingGeneratorAsync(
        Guid? profileId = null,
        CancellationToken cancellationToken = default);
}
```

Basic Usage

Choosing a Profile

Default Profile

Specific Profile

Common Use Cases

Semantic Search

Content Similarity

RAG (Retrieval-Augmented Generation)

In This Section

Last updated

Was this helpful?

## Sub-topics

- [Batch Embeddings | AI in Umbraco](embeddings/batch-embeddings.md)
- [Generating Embeddings | AI in Umbraco](embeddings/generating-embeddings.md)
