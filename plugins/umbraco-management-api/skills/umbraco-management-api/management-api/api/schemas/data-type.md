# Data Type Schemas

## Schemas in this file

- [BatchResponseModelDataTypeResponseModel](#batchresponsemodeldatatyperesponsemodel)
- [CopyDataTypeRequestModel](#copydatatyperequestmodel)
- [CreateDataTypeRequestModel](#createdatatyperequestmodel)
- [DataTypeResponseModel](#datatyperesponsemodel)
- [DatatypeConfigurationResponseModel](#datatypeconfigurationresponsemodel)
- [MoveDataTypeRequestModel](#movedatatyperequestmodel)
- [PagedDataTypeItemResponseModel](#pageddatatypeitemresponsemodel)
- [PagedDataTypeTreeItemResponseModel](#pageddatatypetreeitemresponsemodel)
- [PagedModelDataTypeItemResponseModel](#pagedmodeldatatypeitemresponsemodel)
- [SubsetDataTypeTreeItemResponseModel](#subsetdatatypetreeitemresponsemodel)
- [UpdateDataTypeRequestModel](#updatedatatyperequestmodel)

---

## BatchResponseModelDataTypeResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int32) **required**

---

## CopyDataTypeRequestModel

**Fields:**

- `target`: object, nullable

---

## CreateDataTypeRequestModel

**Fields:**

- `editorAlias`: string **required**
- `editorUiAlias`: string **required**
- `id`: string (uuid), nullable
- `name`: string **required**
- `parent`: object, nullable
- `values`: List<object> **required**

---

## DataTypeResponseModel

**Fields:**

- `canIgnoreStartNodes`: boolean **required**
- `editorAlias`: string **required**
- `editorUiAlias`: string **required**
- `id`: string (uuid) **required**
- `isDeletable`: boolean **required**
- `name`: string **required**
- `values`: List<object> **required**

---

## DatatypeConfigurationResponseModel

**Fields:**

- `canBeChanged`: → `DataTypeChangeModeModel` **required**
- `documentListViewId`: string (uuid) **required**
- `mediaListViewId`: string (uuid) **required**

---

## MoveDataTypeRequestModel

**Fields:**

- `target`: object, nullable

---

## PagedDataTypeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedDataTypeTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedModelDataTypeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## SubsetDataTypeTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `totalAfter`: integer (int64) **required**
- `totalBefore`: integer (int64) **required**

---

## UpdateDataTypeRequestModel

**Fields:**

- `editorAlias`: string **required**
- `editorUiAlias`: string **required**
- `name`: string **required**
- `values`: List<object> **required**

---
