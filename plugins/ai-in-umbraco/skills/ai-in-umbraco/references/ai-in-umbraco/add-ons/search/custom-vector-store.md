# Custom Vector Store | AI in Umbraco

Replace the built-in vector store with a custom implementation.

Interface

```
public interface IAIVectorStore
{
    Task UpsertAsync(string indexName, string documentId, string? culture,
        int chunkIndex, ReadOnlyMemory<float> vector,
        IDictionary<string, object>? metadata = null,
        CancellationToken cancellationToken = default);

    Task DeleteAsync(string indexName, string documentId, string? culture,
        CancellationToken cancellationToken = default);

    Task DeleteDocumentAsync(string indexName, string documentId,
        CancellationToken cancellationToken = default);

    Task<IReadOnlyList<AIVectorSearchResult>> SearchAsync(string indexName,
        ReadOnlyMemory<float> queryVector, string? culture = null,
        int topK = 10, CancellationToken cancellationToken = default);

    Task<IReadOnlyList<AIVectorEntry>> GetVectorsByDocumentAsync(
        string indexName, string documentId, string? culture = null,
        CancellationToken cancellationToken = default);

    Task ResetAsync(string indexName,
        CancellationToken cancellationToken = default);

    Task<long> GetDocumentCountAsync(string indexName,
        CancellationToken cancellationToken = default);
}
```

Key methods

| Method | Purpose |
|---|---|
| `UpsertAsync` | Insert or update a single chunk vector |
| `DeleteAsync` | Remove all chunks for a document and culture |
| `DeleteDocumentAsync` | Remove all chunks for a document across all cultures |
| `SearchAsync` | Find similar vectors by cosine similarity |
| `GetVectorsByDocumentAsync` | Retrieve stored vectors for a document |
| `ResetAsync` | Clear all entries for an index |
| `GetDocumentCountAsync` | Return the number of stored entries |

Registration

In-memory store for testing

Parameters

Culture

Metadata

| Key | Type | Description |
|---|---|---|
| `objectType` | `string` | Umbraco object type, for example `Document` or `Media` |
| `chunkIndex` | `int` | Zero-based position of the chunk within the document |
| `totalChunks` | `int` | Total number of chunks for the document |
| `accessIds` | `string` | Comma-separated access IDs for protected content. Only present when the document has `ContentProtection.AccessIds` . Used by the searcher to filter results for public members and group membership. |

Related

Last updated

Was this helpful?