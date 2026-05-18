# Indexer Schemas

## Schemas in this file

- [IndexResponseModel](#indexresponsemodel)
- [PagedIndexResponseModel](#pagedindexresponsemodel)

---

## IndexResponseModel

**Fields:**

- `canRebuild`: boolean **required**
- `documentCount`: integer (int64) **required**
- `fieldCount`: integer (int32) **required**
- `healthStatus`: object **required**
- `name`: string **required**
- `providerProperties`: object, nullable
- `searcherName`: string **required**

---

## PagedIndexResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---
