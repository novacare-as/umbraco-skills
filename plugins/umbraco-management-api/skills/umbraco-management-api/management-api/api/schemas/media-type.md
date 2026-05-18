# Media Type Schemas

## Schemas in this file

- [BatchResponseModelMediaTypeResponseModel](#batchresponsemodelmediatyperesponsemodel)
- [CopyMediaTypeRequestModel](#copymediatyperequestmodel)
- [CreateMediaTypeRequestModel](#createmediatyperequestmodel)
- [ImportMediaTypeRequestModel](#importmediatyperequestmodel)
- [MediaTypeAllowedParentsResponseModel](#mediatypeallowedparentsresponsemodel)
- [MediaTypeCompositionRequestModel](#mediatypecompositionrequestmodel)
- [MediaTypeConfigurationResponseModel](#mediatypeconfigurationresponsemodel)
- [MediaTypeResponseModel](#mediatyperesponsemodel)
- [MoveMediaTypeRequestModel](#movemediatyperequestmodel)
- [PagedAllowedMediaTypeModel](#pagedallowedmediatypemodel)
- [PagedMediaTypeTreeItemResponseModel](#pagedmediatypetreeitemresponsemodel)
- [PagedModelAllowedMediaTypeItemResponseModel](#pagedmodelallowedmediatypeitemresponsemodel)
- [PagedModelMediaTypeItemResponseModel](#pagedmodelmediatypeitemresponsemodel)
- [SubsetMediaTypeTreeItemResponseModel](#subsetmediatypetreeitemresponsemodel)
- [UpdateMediaTypeRequestModel](#updatemediatyperequestmodel)

---

## BatchResponseModelMediaTypeResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int32) **required**

---

## CopyMediaTypeRequestModel

**Fields:**

- `target`: object, nullable

---

## CreateMediaTypeRequestModel

**Fields:**

- `alias`: string **required**
- `allowedAsRoot`: boolean **required**
- `allowedMediaTypes`: List<object> **required**
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

## ImportMediaTypeRequestModel

**Fields:**

- `file`: object **required**

---

## MediaTypeAllowedParentsResponseModel

**Fields:**

- `allowedParentIds`: List<object> **required**

---

## MediaTypeCompositionRequestModel

**Fields:**

- `currentCompositeIds`: List<string (uuid)> **required**
- `currentPropertyAliases`: List<string> **required**
- `id`: string (uuid), nullable

---

## MediaTypeConfigurationResponseModel

**Fields:**

- `reservedFieldNames`: List<string> **required**

---

## MediaTypeResponseModel

**Fields:**

- `alias`: string **required**
- `aliasCanBeChanged`: boolean **required**
- `allowedAsRoot`: boolean **required**
- `allowedMediaTypes`: List<object> **required**
- `collection`: object, nullable
- `compositions`: List<object> **required**
- `containers`: List<object> **required**
- `description`: string, nullable
- `icon`: string **required**
- `id`: string (uuid) **required**
- `isDeletable`: boolean **required**
- `isElement`: boolean **required**
- `name`: string **required**
- `properties`: List<object> **required**
- `variesByCulture`: boolean **required**
- `variesBySegment`: boolean **required**

---

## MoveMediaTypeRequestModel

**Fields:**

- `target`: object, nullable

---

## PagedAllowedMediaTypeModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedMediaTypeTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedModelAllowedMediaTypeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedModelMediaTypeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## SubsetMediaTypeTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `totalAfter`: integer (int64) **required**
- `totalBefore`: integer (int64) **required**

---

## UpdateMediaTypeRequestModel

**Fields:**

- `alias`: string **required**
- `allowedAsRoot`: boolean **required**
- `allowedMediaTypes`: List<object> **required**
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
