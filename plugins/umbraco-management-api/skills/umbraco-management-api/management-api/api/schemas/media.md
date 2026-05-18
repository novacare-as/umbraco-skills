# Media Schemas

## Schemas in this file

- [CreateMediaRequestModel](#createmediarequestmodel)
- [MediaConfigurationResponseModel](#mediaconfigurationresponsemodel)
- [MediaResponseModel](#mediaresponsemodel)
- [MoveMediaRequestModel](#movemediarequestmodel)
- [PagedMediaCollectionResponseModel](#pagedmediacollectionresponsemodel)
- [PagedMediaRecycleBinItemResponseModel](#pagedmediarecyclebinitemresponsemodel)
- [PagedMediaTreeItemResponseModel](#pagedmediatreeitemresponsemodel)
- [PagedModelMediaItemResponseModel](#pagedmodelmediaitemresponsemodel)
- [SubsetMediaRecycleBinItemResponseModel](#subsetmediarecyclebinitemresponsemodel)
- [SubsetMediaTreeItemResponseModel](#subsetmediatreeitemresponsemodel)
- [UpdateMediaRequestModel](#updatemediarequestmodel)

---

## CreateMediaRequestModel

**Fields:**

- `id`: string (uuid), nullable
- `mediaType`: object **required**
- `parent`: object, nullable
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

## MediaConfigurationResponseModel

**Fields:**

- `disableDeleteWhenReferenced`: boolean **required**
- `disableUnpublishWhenReferenced`: boolean **required**

---

## MediaResponseModel

**Fields:**

- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `isTrashed`: boolean **required**
- `mediaType`: object **required**
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

## MoveMediaRequestModel

**Fields:**

- `target`: object, nullable

---

## PagedMediaCollectionResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedMediaRecycleBinItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedMediaTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedModelMediaItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## SubsetMediaRecycleBinItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `totalAfter`: integer (int64) **required**
- `totalBefore`: integer (int64) **required**

---

## SubsetMediaTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `totalAfter`: integer (int64) **required**
- `totalBefore`: integer (int64) **required**

---

## UpdateMediaRequestModel

**Fields:**

- `values`: List<object> **required**
- `variants`: List<object> **required**

---
