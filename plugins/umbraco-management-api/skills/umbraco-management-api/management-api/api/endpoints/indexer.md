# Indexer — API Endpoints

See `schemas/indexer.md` for field definitions.

## Contents

### Indexer

- `GET /umbraco/management/api/v1/indexer`
- `GET /umbraco/management/api/v1/indexer/{indexName}`
- `POST /umbraco/management/api/v1/indexer/{indexName}/rebuild`

---

## Indexer

### `GET /umbraco/management/api/v1/indexer`

**Gets a collection of indexers.**

Operation ID: `GetIndexer`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedIndexResponseModel`

---

### `GET /umbraco/management/api/v1/indexer/{indexName}`

**Gets indexer details.**

Operation ID: `GetIndexerByIndexName`

| Param | In | Type | Required |
|-------|----|------|----------|
| `indexName` | path | string | Yes |

**Response 200:** `OneOf: → IndexResponseModel`

---

### `POST /umbraco/management/api/v1/indexer/{indexName}/rebuild`

**Rebuilds an indexer.**

Operation ID: `PostIndexerByIndexNameRebuild`

| Param | In | Type | Required |
|-------|----|------|----------|
| `indexName` | path | string | Yes |


---
