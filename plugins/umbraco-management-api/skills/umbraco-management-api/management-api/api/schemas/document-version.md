# Document Version Schemas

## Schemas in this file

- [DocumentVersionResponseModel](#documentversionresponsemodel)
- [PagedDocumentVersionItemResponseModel](#pageddocumentversionitemresponsemodel)

---

## DocumentVersionResponseModel

**Fields:**

- `document`: object, nullable
- `documentType`: object **required**
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

## PagedDocumentVersionItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---
