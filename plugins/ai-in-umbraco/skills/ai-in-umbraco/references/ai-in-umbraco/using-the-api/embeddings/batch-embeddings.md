# Batch Embeddings | AI in Umbraco

Generate embeddings for multiple texts in a single request for efficiency.

Basic Batch Example

```
using Microsoft.Extensions.AI;
using Umbraco.AI.Core.Embeddings;

public class BatchEmbeddingExample
{
    private readonly IAIEmbeddingService _embeddingService;

    public BatchEmbeddingExample(IAIEmbeddingService embeddingService)
    {
        _embeddingService = embeddingService;
    }

    public async Task<IList<float[]>> GenerateEmbeddings(IEnumerable<string> texts)
    {
        var embeddings = await _embeddingService.GenerateEmbeddingsAsync(texts);

        return embeddings.Select(e => e.Vector.ToArray()).ToList();
    }
}
```

Understanding the Response

| Property | Type | Description |
|---|---|---|
| (collection) | `IList<Embedding<float>>` | The generated embeddings in order |
| `Usage` | `UsageDetails?` | Token usage for the batch |

Batch Indexing

Chunking Large Batches

Using a Specific Profile

Related

Last updated

Was this helpful?