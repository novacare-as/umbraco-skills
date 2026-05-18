# Dictionary Schemas

## Schemas in this file

- [CreateDictionaryItemRequestModel](#createdictionaryitemrequestmodel)
- [DictionaryItemResponseModel](#dictionaryitemresponsemodel)
- [ImportDictionaryRequestModel](#importdictionaryrequestmodel)
- [MoveDictionaryRequestModel](#movedictionaryrequestmodel)
- [PagedDictionaryOverviewResponseModel](#pageddictionaryoverviewresponsemodel)
- [UpdateDictionaryItemRequestModel](#updatedictionaryitemrequestmodel)

---

## CreateDictionaryItemRequestModel

**Fields:**

- `id`: string (uuid), nullable
- `name`: string **required**
- `parent`: object, nullable
- `translations`: List<object> **required**

---

## DictionaryItemResponseModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string **required**
- `translations`: List<object> **required**

---

## ImportDictionaryRequestModel

**Fields:**

- `parent`: object, nullable
- `temporaryFile`: object **required**

---

## MoveDictionaryRequestModel

**Fields:**

- `target`: object, nullable

---

## PagedDictionaryOverviewResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## UpdateDictionaryItemRequestModel

**Fields:**

- `name`: string **required**
- `translations`: List<object> **required**

---
