# Embedding Middleware | AI in Umbraco

Create middleware to intercept and modify embedding operations.

Interface

```
public interface IAIEmbeddingMiddleware
{
    IEmbeddingGenerator<string, Embedding<float>> Apply(
        IEmbeddingGenerator<string, Embedding<float>> generator);
}
```

Basic Implementation

```
using Microsoft.Extensions.AI;
using Umbraco.AI.Core.Embeddings;

public class SimpleEmbeddingMiddleware : IAIEmbeddingMiddleware
{
    public IEmbeddingGenerator<string, Embedding<float>> Apply(
        IEmbeddingGenerator<string, Embedding<float>> generator)
    {
        return new SimpleEmbeddingWrapper(generator);
    }
}
```

Creating a Custom Wrapper

Using M.E.AI Built-in Middleware

Registering Embedding Middleware

Example: Caching Middleware

Example: Normalization Middleware

Last updated

Was this helpful?