# Relation Type Schemas

## Schemas in this file

- [PagedRelationTypeResponseModel](#pagedrelationtyperesponsemodel)
- [RelationTypeResponseModel](#relationtyperesponsemodel)

---

## PagedRelationTypeResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## RelationTypeResponseModel

**Fields:**

- `alias`: string, nullable
- `childObject`: object, nullable
- `id`: string (uuid) **required**
- `isBidirectional`: boolean **required**
- `isDependency`: boolean **required**
- `name`: string **required**
- `parentObject`: object, nullable

---
