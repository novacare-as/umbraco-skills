# Document Schemas

## Schemas in this file

- [CopyDocumentRequestModel](#copydocumentrequestmodel)
- [CreateDocumentRequestModel](#createdocumentrequestmodel)
- [DocumentConfigurationResponseModel](#documentconfigurationresponsemodel)
- [DocumentResponseModel](#documentresponsemodel)
- [DocumentUrlInfoModel](#documenturlinfomodel)
- [DomainsResponseModel](#domainsresponsemodel)
- [MoveDocumentRequestModel](#movedocumentrequestmodel)
- [PagedDocumentCollectionResponseModel](#pageddocumentcollectionresponsemodel)
- [PagedDocumentRecycleBinItemResponseModel](#pageddocumentrecyclebinitemresponsemodel)
- [PagedDocumentTreeItemResponseModel](#pageddocumenttreeitemresponsemodel)
- [PagedModelDocumentItemResponseModel](#pagedmodeldocumentitemresponsemodel)
- [PublicAccessRequestModel](#publicaccessrequestmodel)
- [PublicAccessResponseModel](#publicaccessresponsemodel)
- [PublishDocumentRequestModel](#publishdocumentrequestmodel)
- [PublishDocumentWithDescendantsRequestModel](#publishdocumentwithdescendantsrequestmodel)
- [PublishWithDescendantsResultModel](#publishwithdescendantsresultmodel)
- [PublishedDocumentResponseModel](#publisheddocumentresponsemodel)
- [SubsetDocumentRecycleBinItemResponseModel](#subsetdocumentrecyclebinitemresponsemodel)
- [SubsetDocumentTreeItemResponseModel](#subsetdocumenttreeitemresponsemodel)
- [UnpublishDocumentRequestModel](#unpublishdocumentrequestmodel)
- [UpdateDocumentNotificationsRequestModel](#updatedocumentnotificationsrequestmodel)
- [UpdateDocumentRequestModel](#updatedocumentrequestmodel)
- [UpdateDomainsRequestModel](#updatedomainsrequestmodel)
- [ValidateUpdateDocumentRequestModel](#validateupdatedocumentrequestmodel)

---

## CopyDocumentRequestModel

**Fields:**

- `includeDescendants`: boolean **required**
- `relateToOriginal`: boolean **required**
- `target`: object, nullable

---

## CreateDocumentRequestModel

**Fields:**

- `documentType`: object **required**
- `id`: string (uuid), nullable
- `parent`: object, nullable
- `template`: object, nullable **required**
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

## DocumentConfigurationResponseModel

**Fields:**

- `allowEditInvariantFromNonDefault`: boolean **required**
- `allowNonExistingSegmentsCreation`: boolean **required**
- `disableDeleteWhenReferenced`: boolean **required**
- `disableUnpublishWhenReferenced`: boolean **required**

---

## DocumentResponseModel

**Fields:**

- `documentType`: object **required**
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `isTrashed`: boolean **required**
- `template`: object, nullable
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

## DocumentUrlInfoModel

**Fields:**

- `culture`: string, nullable **required**
- `message`: string, nullable **required**
- `provider`: string **required**
- `url`: string, nullable **required**

---

## DomainsResponseModel

**Fields:**

- `defaultIsoCode`: string, nullable
- `domains`: List<object> **required**

---

## MoveDocumentRequestModel

**Fields:**

- `target`: object, nullable

---

## PagedDocumentCollectionResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedDocumentRecycleBinItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedDocumentTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedModelDocumentItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PublicAccessRequestModel

**Fields:**

- `errorDocument`: object **required**
- `loginDocument`: object **required**
- `memberGroupNames`: List<string> **required**
- `memberUserNames`: List<string> **required**

---

## PublicAccessResponseModel

**Fields:**

- `errorDocument`: object **required**
- `groups`: List<object> **required**
- `isProtectedByAncestor`: boolean **required**
- `loginDocument`: object **required**
- `members`: List<object> **required**

---

## PublishDocumentRequestModel

**Fields:**

- `publishSchedules`: List<object> **required**

---

## PublishDocumentWithDescendantsRequestModel

**Fields:**

- `cultures`: List<string> **required**
- `includeUnpublishedDescendants`: boolean **required**

---

## PublishWithDescendantsResultModel

**Fields:**

- `isComplete`: boolean **required**
- `taskId`: string (uuid) **required**

---

## PublishedDocumentResponseModel

**Fields:**

- `documentType`: object **required**
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `isTrashed`: boolean **required**
- `template`: object, nullable
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

## SubsetDocumentRecycleBinItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `totalAfter`: integer (int64) **required**
- `totalBefore`: integer (int64) **required**

---

## SubsetDocumentTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `totalAfter`: integer (int64) **required**
- `totalBefore`: integer (int64) **required**

---

## UnpublishDocumentRequestModel

**Fields:**

- `cultures`: List<string>, nullable

---

## UpdateDocumentNotificationsRequestModel

**Fields:**

- `subscribedActionIds`: List<string> **required**

---

## UpdateDocumentRequestModel

**Fields:**

- `template`: object, nullable
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

## UpdateDomainsRequestModel

**Fields:**

- `defaultIsoCode`: string, nullable
- `domains`: List<object> **required**

---

## ValidateUpdateDocumentRequestModel

**Fields:**

- `cultures`: List<string>, nullable
- `template`: object, nullable
- `values`: List<object> **required**
- `variants`: List<object> **required**

---
