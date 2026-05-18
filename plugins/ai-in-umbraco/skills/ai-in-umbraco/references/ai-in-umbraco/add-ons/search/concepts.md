# Concepts | AI in Umbraco

How semantic vector search indexes and retrieves content.

A vector embedding is a list of numbers that represents the meaning of a piece of text. Texts about similar topics produce similar vectors. By comparing vectors, you can find content that is related by meaning rather than matching keywords.

Umbraco.AI.Search uses the configured embedding profile to generate vectors. Any provider that supports the embedding capability works, including OpenAI and Amazon Bedrock.

The search add-on registers an index called `UmbAI_Search`

with the CMS Search framework. The index receives the same content change notifications as other indexes such as Examine.

When content is published:

**Text extraction**- The CMS Search property value handlers extract text from all fields, including nested block content.**HTML stripping**- Tags and entities are removed, whitespace is normalized.**Chunking**- Long text is split into smaller chunks that fit within the embedding model's token limit.**Embedding**- Each chunk is sent to the embedding provider to generate a vector.**Storage**- Vectors are stored in the database with the document ID, culture, and chunk index.

For multilingual content, the indexer generates separate embeddings per culture. Each language variant has its own set of chunks and vectors. Searches can filter by culture to return results in a specific language.

The recursive text chunker splits content by trying paragraph boundaries first, then sentences, then words. Text chunking preserves semantic coherence within each chunk.

Overlap between chunks ensures that concepts spanning a boundary are captured in both chunks. Configure chunk size and overlap in `appsettings.json`

under `Umbraco:AI:Search`.


Searches work by embedding the query text and finding stored vectors with the highest cosine similarity. Multiple chunks from the same document are deduplicated, keeping the best score.

The index is available through the standard CMS Search API. Send a POST request to the search endpoint with the `UmbAI_Search`

index alias:

When the Agent add-on is installed, the `semantic_search`

tool is available in chat. It supports two modes:

**Text query**- Find content about a topic.**Document ID**- Find content similar to an existing page.

The document mode retrieves stored embeddings directly, so there is no extra embedding call.

Protected content (pages with member login restrictions) is filtered based on the `AccessContext`

passed in the search request. Public content is always returned. Protected content is only returned when the caller's principal or group IDs match the allowed access IDs stored during indexing.

The agent tool runs in the backoffice and respects the current user's start node restrictions. Users with restricted content or media start nodes only see results under their allowed tree branches. If content cannot be resolved to verify the path, the result is excluded when restrictions are in place.

On SQL Server 2025 and Azure SQL, the store uses `VECTOR_DISTANCE()`

for server-side similarity search. On older versions, vectors are loaded into memory and compared using cosine similarity in .NET.

Vectors are persisted as JSON arrays in an `nvarchar(max)`

column for compatibility across all SQL Server versions. On SQL Server 2025, the column value is cast to the native `vector(N)`

type at query time.

The SQL Server `vector`

type supports a maximum of 1998 dimensions. If the configured embedding model produces more than 1998 dimensions, the store falls back to brute-force cosine similarity in .NET even on SQL Server 2025. To keep native `VECTOR_DISTANCE()`

enabled, choose an embedding model within this limit (for example, `text-embedding-3-small`

at 1536 dimensions) or reduce the dimensions on a larger model.

SQLite uses in-memory cosine similarity. This is suitable for local development and testing but not recommended for production workloads.

You can replace the built-in store by implementing `IAIVectorStore`

and registering it in a Composer. See [Custom vector store](/ai-in-umbraco/add-ons/search/custom-vector-store) for details.

Last updated

Was this helpful?