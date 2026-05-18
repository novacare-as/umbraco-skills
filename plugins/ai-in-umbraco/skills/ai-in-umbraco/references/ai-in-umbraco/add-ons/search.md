# Semantic Search | AI in Umbraco

Semantic vector search add-on for finding content by meaning.

Installation

```
Install-Package Umbraco.AI.Search
```

```
dotnet add package Umbraco.AI.Search
```

How it works

Features

Configuration

| Option | Default | Description |
|---|---|---|
| `ChunkSize` | `512` | Maximum tokens per text chunk |
| `ChunkOverlap` | `50` | Token overlap between consecutive chunks |
| `DefaultTopK` | `100` | Maximum candidates from vector search before deduplication |
| `MinScore` | `0.3` | Minimum cosine similarity (0.0–1.0) required for a result to be returned |

Separate database

Documentation

| Section | Description |
|---|---|
|

[Custom vector store](/ai-in-umbraco/add-ons/search/custom-vector-store)Related

Last updated

Was this helpful?

## Sub-topics

- [Concepts | AI in Umbraco](search/concepts.md)
- [Custom Vector Store | AI in Umbraco](search/custom-vector-store.md)
