# Document Type Schemas

## Schemas in this file

- [BatchResponseModelDocumentTypeResponseModel](#batchresponsemodeldocumenttyperesponsemodel)
- [CopyDocumentTypeRequestModel](#copydocumenttyperequestmodel)
- [CreateDocumentTypeRequestModel](#createdocumenttyperequestmodel)
- [CreateDocumentTypeTemplateRequestModel](#createdocumenttypetemplaterequestmodel)
- [DocumentTypeAllowedParentsResponseModel](#documenttypeallowedparentsresponsemodel)
- [DocumentTypeCompositionRequestModel](#documenttypecompositionrequestmodel)
- [DocumentTypeConfigurationResponseModel](#documenttypeconfigurationresponsemodel)
- [DocumentTypeResponseModel](#documenttyperesponsemodel)
- [ImportDocumentTypeRequestModel](#importdocumenttyperequestmodel)
- [MoveDocumentTypeRequestModel](#movedocumenttyperequestmodel)
- [PagedAllowedDocumentTypeModel](#pagedalloweddocumenttypemodel)
- [PagedDocumentTypeBlueprintItemResponseModel](#pageddocumenttypeblueprintitemresponsemodel)
- [PagedDocumentTypeTreeItemResponseModel](#pageddocumenttypetreeitemresponsemodel)
- [PagedModelDocumentTypeItemResponseModel](#pagedmodeldocumenttypeitemresponsemodel)
- [SubsetDocumentTypeTreeItemResponseModel](#subsetdocumenttypetreeitemresponsemodel)
- [UpdateDocumentTypeRequestModel](#updatedocumenttyperequestmodel)

---

## BatchResponseModelDocumentTypeResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int32) **required**

---

## CopyDocumentTypeRequestModel

**Fields:**

- `target`: object, nullable

---

## CreateDocumentTypeRequestModel

**Fields:**

- `alias`: string **required**
- `allowedAsRoot`: boolean **required**
- `allowedDocumentTypes`: List<object> **required**
- `allowedTemplates`: List<object> **required**
- `cleanup`: object **required**
- `collection`: object, nullable
- `compositions`: List<object> **required**
- `containers`: List<object> **required**
- `defaultTemplate`: object, nullable
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

## CreateDocumentTypeTemplateRequestModel

**Fields:**

- `alias`: string **required**
- `isDefault`: boolean **required**
- `name`: string **required**

---

## DocumentTypeAllowedParentsResponseModel

**Fields:**

- `allowedParentIds`: List<object> **required**

---

## DocumentTypeCompositionRequestModel

**Fields:**

- `currentCompositeIds`: List<string (uuid)> **required**
- `currentPropertyAliases`: List<string> **required**
- `id`: string (uuid), nullable
- `isElement`: boolean **required**

---

## DocumentTypeConfigurationResponseModel

**Fields:**

- `dataTypesCanBeChanged`: → `DataTypeChangeModeModel` **required**
- `disableTemplates`: boolean **required**
- `reservedFieldNames`: List<string> **required**
- `useSegments`: boolean **required**

---

## DocumentTypeResponseModel

**Fields:**

- `alias`: string **required**
- `allowedAsRoot`: boolean **required**
- `allowedDocumentTypes`: List<object> **required**
- `allowedTemplates`: List<object> **required**
- `cleanup`: object **required**
- `collection`: object, nullable
- `compositions`: List<object> **required**
- `containers`: List<object> **required**
- `defaultTemplate`: object, nullable
- `description`: string, nullable
- `icon`: string **required**
- `id`: string (uuid) **required**
- `isElement`: boolean **required**
- `name`: string **required**
- `properties`: List<object> **required**
- `variesByCulture`: boolean **required**
- `variesBySegment`: boolean **required**

---

## ImportDocumentTypeRequestModel

**Fields:**

- `file`: object **required**

---

## MoveDocumentTypeRequestModel

**Fields:**

- `target`: object, nullable

---

## PagedAllowedDocumentTypeModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedDocumentTypeBlueprintItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedDocumentTypeTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedModelDocumentTypeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## SubsetDocumentTypeTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `totalAfter`: integer (int64) **required**
- `totalBefore`: integer (int64) **required**

---

## UpdateDocumentTypeRequestModel

**Fields:**

- `alias`: string **required**
- `allowedAsRoot`: boolean **required**
- `allowedDocumentTypes`: List<object> **required**
- `allowedTemplates`: List<object> **required**
- `cleanup`: object **required**
- `collection`: object, nullable
- `compositions`: List<object> **required**
- `containers`: List<object> **required**
- `defaultTemplate`: object, nullable
- `description`: string, nullable
- `icon`: string **required**
- `isElement`: boolean **required**
- `name`: string **required**
- `properties`: List<object> **required**
- `variesByCulture`: boolean **required**
- `variesBySegment`: boolean **required**

---
