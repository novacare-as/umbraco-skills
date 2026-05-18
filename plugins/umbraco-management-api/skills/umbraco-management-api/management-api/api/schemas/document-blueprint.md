# Document Blueprint Schemas

## Schemas in this file

- [CreateDocumentBlueprintFromDocumentRequestModel](#createdocumentblueprintfromdocumentrequestmodel)
- [CreateDocumentBlueprintRequestModel](#createdocumentblueprintrequestmodel)
- [DocumentBlueprintResponseModel](#documentblueprintresponsemodel)
- [MoveDocumentBlueprintRequestModel](#movedocumentblueprintrequestmodel)
- [PagedDocumentBlueprintTreeItemResponseModel](#pageddocumentblueprinttreeitemresponsemodel)
- [SubsetDocumentBlueprintTreeItemResponseModel](#subsetdocumentblueprinttreeitemresponsemodel)
- [UpdateDocumentBlueprintRequestModel](#updatedocumentblueprintrequestmodel)

---

## CreateDocumentBlueprintFromDocumentRequestModel

**Fields:**

- `document`: object **required**
- `id`: string (uuid), nullable
- `name`: string **required**
- `parent`: object, nullable

---

## CreateDocumentBlueprintRequestModel

**Fields:**

- `documentType`: object **required**
- `id`: string (uuid), nullable
- `parent`: object, nullable
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

## DocumentBlueprintResponseModel

**Fields:**

- `documentType`: object **required**
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

## MoveDocumentBlueprintRequestModel

**Fields:**

- `target`: object, nullable

---

## PagedDocumentBlueprintTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## SubsetDocumentBlueprintTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `totalAfter`: integer (int64) **required**
- `totalBefore`: integer (int64) **required**

---

## UpdateDocumentBlueprintRequestModel

**Fields:**

- `values`: List<object> **required**
- `variants`: List<object> **required**

---
