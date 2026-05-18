# Searcher — API Endpoints

See `schemas/searcher.md` for field definitions.

## Contents

### Searcher

- `GET /umbraco/management/api/v1/searcher`
- `GET /umbraco/management/api/v1/searcher/{searcherName}/query`

---

## Searcher

### `GET /umbraco/management/api/v1/searcher`

**Gets a collection of searchers.**

Operation ID: `GetSearcher`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedSearcherResponseModel`

---

### `GET /umbraco/management/api/v1/searcher/{searcherName}/query`

Operation ID: `GetSearcherBySearcherNameQuery`

| Param | In | Type | Required |
|-------|----|------|----------|
| `searcherName` | path | string | Yes |
| `term` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedSearchResultResponseModel`

---
