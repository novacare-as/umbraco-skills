# Member Type Schemas

## Schemas in this file

- [BatchResponseModelMemberTypeResponseModel](#batchresponsemodelmembertyperesponsemodel)
- [CopyMemberTypeRequestModel](#copymembertyperequestmodel)
- [CreateMemberTypeRequestModel](#createmembertyperequestmodel)
- [ImportMemberTypeRequestModel](#importmembertyperequestmodel)
- [MemberTypeCompositionRequestModel](#membertypecompositionrequestmodel)
- [MemberTypeConfigurationResponseModel](#membertypeconfigurationresponsemodel)
- [MemberTypeResponseModel](#membertyperesponsemodel)
- [MoveMemberTypeRequestModel](#movemembertyperequestmodel)
- [PagedMemberTypeTreeItemResponseModel](#pagedmembertypetreeitemresponsemodel)
- [PagedModelMemberTypeItemResponseModel](#pagedmodelmembertypeitemresponsemodel)
- [SubsetMemberTypeTreeItemResponseModel](#subsetmembertypetreeitemresponsemodel)
- [UpdateMemberTypeRequestModel](#updatemembertyperequestmodel)

---

## BatchResponseModelMemberTypeResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int32) **required**

---

## CopyMemberTypeRequestModel

**Fields:**

- `target`: object, nullable

---

## CreateMemberTypeRequestModel

**Fields:**

- `alias`: string **required**
- `allowedAsRoot`: boolean **required**
- `collection`: object, nullable
- `compositions`: List<object> **required**
- `containers`: List<object> **required**
- `description`: string, nullable
- `icon`: string **required**
- `id`: string (uuid), nullable
- `isElement`: boolean **required**
- `name`: string **required**
- `parent`: object, nullable
- `properties`: List<object> **required**
- `variesByCulture`: boolean **required**
- `variesBySegment`: boolean **required**

---

## ImportMemberTypeRequestModel

**Fields:**

- `file`: object **required**

---

## MemberTypeCompositionRequestModel

**Fields:**

- `currentCompositeIds`: List<string (uuid)> **required**
- `currentPropertyAliases`: List<string> **required**
- `id`: string (uuid), nullable

---

## MemberTypeConfigurationResponseModel

**Fields:**

- `reservedFieldNames`: List<string> **required**

---

## MemberTypeResponseModel

**Fields:**

- `alias`: string **required**
- `allowedAsRoot`: boolean **required**
- `collection`: object, nullable
- `compositions`: List<object> **required**
- `containers`: List<object> **required**
- `description`: string, nullable
- `icon`: string **required**
- `id`: string (uuid) **required**
- `isElement`: boolean **required**
- `name`: string **required**
- `properties`: List<object> **required**
- `variesByCulture`: boolean **required**
- `variesBySegment`: boolean **required**

---

## MoveMemberTypeRequestModel

**Fields:**

- `target`: object, nullable

---

## PagedMemberTypeTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedModelMemberTypeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## SubsetMemberTypeTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `totalAfter`: integer (int64) **required**
- `totalBefore`: integer (int64) **required**

---

## UpdateMemberTypeRequestModel

**Fields:**

- `alias`: string **required**
- `allowedAsRoot`: boolean **required**
- `collection`: object, nullable
- `compositions`: List<object> **required**
- `containers`: List<object> **required**
- `description`: string, nullable
- `icon`: string **required**
- `isElement`: boolean **required**
- `name`: string **required**
- `properties`: List<object> **required**
- `variesByCulture`: boolean **required**
- `variesBySegment`: boolean **required**

---
