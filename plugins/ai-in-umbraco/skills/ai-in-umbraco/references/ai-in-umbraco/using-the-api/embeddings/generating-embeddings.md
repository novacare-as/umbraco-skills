# Generating Embeddings | AI in Umbraco

Generate vector embeddings for individual text values.

Basic Example

```
using Microsoft.Extensions.AI;
using Umbraco.AI.Core.Embeddings;

public class EmbeddingExample
{
    private readonly IAIEmbeddingService _embeddingService;

    public EmbeddingExample(IAIEmbeddingService embeddingService)
    {
        _embeddingService = embeddingService;
    }

    public async Task<float[]> GenerateEmbedding(string text)
    {
        var embedding = await _embeddingService.GenerateEmbeddingAsync(text);

        // The vector is a ReadOnlyMemory<float>
        return embedding.Vector.ToArray();
    }
}
```

Understanding the Response

| Property | Type | Description |
|---|---|---|
| `Vector` | `ReadOnlyMemory<float>` | The embedding vector |
| `ModelId` | `string?` | The model that generated the embedding |
| `CreatedAt` | `DateTimeOffset?` | When the embedding was generated |

Using a Specific Profile

Error Handling

Next Steps

Last updated

Was this helpful?