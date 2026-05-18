# Common — Part 2: DocumentVariantResponseModel → MemberVariantResponseModel

## DocumentVariantResponseModel

### Schemas in this file

- [DocumentVariantResponseModel](#documentvariantresponsemodel)

---

### DocumentVariantResponseModel

**Fields:**

- `createDate`: string (date-time) **required**
- `culture`: string, nullable
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `name`: string **required**
- `publishDate`: string (date-time), nullable
- `scheduledPublishDate`: string (date-time), nullable
- `scheduledUnpublishDate`: string (date-time), nullable
- `segment`: string, nullable
- `state`: → `DocumentVariantStateModel` **required**
- `updateDate`: string (date-time) **required**

---

---


## DocumentVariantStateModel

### Schemas in this file

- [DocumentVariantStateModel](#documentvariantstatemodel)

---

### DocumentVariantStateModel

**Enum values:** `NotCreated`, `Draft`, `Published`, `PublishedPendingChanges`, `Trashed`

---

---


## DocumentVersionItemResponseModel

### Schemas in this file

- [DocumentVersionItemResponseModel](#documentversionitemresponsemodel)

---

### DocumentVersionItemResponseModel

**Fields:**

- `document`: object **required**
- `documentType`: object **required**
- `id`: string (uuid) **required**
- `isCurrentDraftVersion`: boolean **required**
- `isCurrentPublishedVersion`: boolean **required**
- `preventCleanup`: boolean **required**
- `user`: object **required**
- `versionDate`: string (date-time) **required**

---

---


## DomainPresentationModel

### Schemas in this file

- [DomainPresentationModel](#domainpresentationmodel)

---

### DomainPresentationModel

**Fields:**

- `domainName`: string **required**
- `isoCode`: string **required**

---

---


## DynamicRootContextRequestModel

### Schemas in this file

- [DynamicRootContextRequestModel](#dynamicrootcontextrequestmodel)

---

### DynamicRootContextRequestModel

**Fields:**

- `culture`: string, nullable
- `id`: string (uuid), nullable
- `parent`: object **required**
- `segment`: string, nullable

---

---


## DynamicRootQueryOriginRequestModel

### Schemas in this file

- [DynamicRootQueryOriginRequestModel](#dynamicrootqueryoriginrequestmodel)

---

### DynamicRootQueryOriginRequestModel

**Fields:**

- `alias`: string **required**
- `id`: string (uuid), nullable

---

---


## DynamicRootQueryRequestModel

### Schemas in this file

- [DynamicRootQueryRequestModel](#dynamicrootqueryrequestmodel)

---

### DynamicRootQueryRequestModel

**Fields:**

- `origin`: object **required**
- `steps`: List<object> **required**

---

---


## DynamicRootQueryStepRequestModel

### Schemas in this file

- [DynamicRootQueryStepRequestModel](#dynamicrootquerysteprequestmodel)

---

### DynamicRootQueryStepRequestModel

**Fields:**

- `alias`: string **required**
- `documentTypeIds`: List<string (uuid)> **required**

---

---


## EventMessageTypeModel

### Schemas in this file

- [EventMessageTypeModel](#eventmessagetypemodel)

---

### EventMessageTypeModel

**Enum values:** `Default`, `Info`, `Error`, `Success`, `Warning`

---

---


## FieldPresentationModel

### Schemas in this file

- [FieldPresentationModel](#fieldpresentationmodel)

---

### FieldPresentationModel

**Fields:**

- `name`: string **required**
- `values`: List<string> **required**

---

---


## FileSystemFolderModel

### Schemas in this file

- [FileSystemFolderModel](#filesystemfoldermodel)

---

### FileSystemFolderModel

**Fields:**

- `path`: string **required**

---

---


## FileSystemTreeItemPresentationModel

### Schemas in this file

- [FileSystemTreeItemPresentationModel](#filesystemtreeitempresentationmodel)

---

### FileSystemTreeItemPresentationModel

**Fields:**

- `hasChildren`: boolean **required**
- `isFolder`: boolean **required**
- `name`: string **required**
- `parent`: object, nullable
- `path`: string **required**

---

---


## FlagModel

### Schemas in this file

- [FlagModel](#flagmodel)

---

### FlagModel

**Fields:**

- `alias`: string **required**

---

---


## FolderResponseModel

### Schemas in this file

- [FolderResponseModel](#folderresponsemodel)

---

### FolderResponseModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## HealthCheckGroupResponseModel

### Schemas in this file

- [HealthCheckGroupResponseModel](#healthcheckgroupresponsemodel)

---

### HealthCheckGroupResponseModel

**Fields:**

- `name`: string **required**

---

---


## HealthCheckModel

### Schemas in this file

- [HealthCheckModel](#healthcheckmodel)

---

### HealthCheckModel

**Fields:**

- `description`: string, nullable
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## HealthCheckWithResultPresentationModel

### Schemas in this file

- [HealthCheckWithResultPresentationModel](#healthcheckwithresultpresentationmodel)

---

### HealthCheckWithResultPresentationModel

**Fields:**

- `id`: string (uuid) **required**
- `results`: List<object>, nullable

---

---


## HealthStatusModel

### Schemas in this file

- [HealthStatusModel](#healthstatusmodel)

---

### HealthStatusModel

**Enum values:** `Healthy`, `Unhealthy`, `Rebuilding`, `Corrupt`

---

---


## HealthStatusResponseModel

### Schemas in this file

- [HealthStatusResponseModel](#healthstatusresponsemodel)

---

### HealthStatusResponseModel

**Fields:**

- `message`: string, nullable
- `status`: → `HealthStatusModel` **required**

---

---


## HelpPageResponseModel

### Schemas in this file

- [HelpPageResponseModel](#helppageresponsemodel)

---

### HelpPageResponseModel

**Fields:**

- `description`: string, nullable
- `name`: string, nullable
- `type`: string, nullable
- `url`: string, nullable

---

---


## ItemAncestorsResponseModelDocumentItemResponseModel

### Schemas in this file

- [ItemAncestorsResponseModelDocumentItemResponseModel](#itemancestorsresponsemodeldocumentitemresponsemodel)

---

### ItemAncestorsResponseModelDocumentItemResponseModel

**Fields:**

- `ancestors`: List<object> **required**
- `id`: string (uuid) **required**

---

---


## ItemAncestorsResponseModelMediaItemResponseModel

### Schemas in this file

- [ItemAncestorsResponseModelMediaItemResponseModel](#itemancestorsresponsemodelmediaitemresponsemodel)

---

### ItemAncestorsResponseModelMediaItemResponseModel

**Fields:**

- `ancestors`: List<object> **required**
- `id`: string (uuid) **required**

---

---


## ItemAncestorsResponseModelMemberItemResponseModel

### Schemas in this file

- [ItemAncestorsResponseModelMemberItemResponseModel](#itemancestorsresponsemodelmemberitemresponsemodel)

---

### ItemAncestorsResponseModelMemberItemResponseModel

**Fields:**

- `ancestors`: List<object> **required**
- `id`: string (uuid) **required**

---

---


## ItemAncestorsResponseModelNamedItemResponseModel

### Schemas in this file

- [ItemAncestorsResponseModelNamedItemResponseModel](#itemancestorsresponsemodelnameditemresponsemodel)

---

### ItemAncestorsResponseModelNamedItemResponseModel

**Fields:**

- `ancestors`: List<object> **required**
- `id`: string (uuid) **required**

---

---


## ItemAncestorsResponseModelTemplateItemResponseModel

### Schemas in this file

- [ItemAncestorsResponseModelTemplateItemResponseModel](#itemancestorsresponsemodeltemplateitemresponsemodel)

---

### ItemAncestorsResponseModelTemplateItemResponseModel

**Fields:**

- `ancestors`: List<object> **required**
- `id`: string (uuid) **required**

---

---


## ItemReferenceByIdResponseModel

### Schemas in this file

- [ItemReferenceByIdResponseModel](#itemreferencebyidresponsemodel)

---

### ItemReferenceByIdResponseModel

**Fields:**

- `id`: string (uuid) **required**

---

---


## ItemSortingRequestModel

### Schemas in this file

- [ItemSortingRequestModel](#itemsortingrequestmodel)

---

### ItemSortingRequestModel

**Fields:**

- `id`: string (uuid) **required**
- `sortOrder`: integer (int32) **required**

---

---


## LoggerResponseModel

### Schemas in this file

- [LoggerResponseModel](#loggerresponsemodel)

---

### LoggerResponseModel

**Fields:**

- `level`: → `LogLevelModel` **required**
- `name`: string **required**

---

---


## LogMessagePropertyPresentationModel

### Schemas in this file

- [LogMessagePropertyPresentationModel](#logmessagepropertypresentationmodel)

---

### LogMessagePropertyPresentationModel

**Fields:**

- `name`: string **required**
- `value`: string, nullable

---

---


## LogMessageResponseModel

### Schemas in this file

- [LogMessageResponseModel](#logmessageresponsemodel)

---

### LogMessageResponseModel

**Fields:**

- `exception`: string, nullable
- `level`: → `LogLevelModel` **required**
- `messageTemplate`: string, nullable
- `properties`: List<object> **required**
- `renderedMessage`: string, nullable
- `timestamp`: string (date-time) **required**

---

---


## LogTemplateResponseModel

### Schemas in this file

- [LogTemplateResponseModel](#logtemplateresponsemodel)

---

### LogTemplateResponseModel

**Fields:**

- `count`: integer (int32) **required**
- `messageTemplate`: string, nullable

---

---


## ManifestResponseModel

### Schemas in this file

- [ManifestResponseModel](#manifestresponsemodel)

---

### ManifestResponseModel

**Fields:**

- `extensions`: List<object> **required**
- `id`: string, nullable
- `name`: string **required**
- `version`: string, nullable

---

---


## MediaCollectionResponseModel

### Schemas in this file

- [MediaCollectionResponseModel](#mediacollectionresponsemodel)

---

### MediaCollectionResponseModel

**Fields:**

- `creator`: string, nullable
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `mediaType`: object **required**
- `sortOrder`: integer (int32) **required**
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

---


## MediaItemResponseModel

### Schemas in this file

- [MediaItemResponseModel](#mediaitemresponsemodel)

---

### MediaItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `hasChildren`: boolean **required**
- `id`: string (uuid) **required**
- `isTrashed`: boolean **required**
- `mediaType`: object **required**
- `parent`: object, nullable
- `variants`: List<object> **required**

---

---


## MediaRecycleBinItemResponseModel

### Schemas in this file

- [MediaRecycleBinItemResponseModel](#mediarecyclebinitemresponsemodel)

---

### MediaRecycleBinItemResponseModel

**Fields:**

- `createDate`: string (date-time) **required**
- `hasChildren`: boolean **required**
- `id`: string (uuid) **required**
- `mediaType`: object **required**
- `parent`: object, nullable
- `variants`: List<object> **required**

---

---


## MediaReferenceResponseModel

### Schemas in this file

- [MediaReferenceResponseModel](#mediareferenceresponsemodel)

---

### MediaReferenceResponseModel

**Fields:**

- `$type`: string **required**
- `id`: string (uuid) **required**
- `mediaType`: object **required**
- `name`: string, nullable

---

---


## MediaTreeItemResponseModel

### Schemas in this file

- [MediaTreeItemResponseModel](#mediatreeitemresponsemodel)

---

### MediaTreeItemResponseModel

**Fields:**

- `createDate`: string (date-time) **required**
- `flags`: List<object> **required**
- `hasChildren`: boolean **required**
- `id`: string (uuid) **required**
- `isTrashed`: boolean **required**
- `mediaType`: object **required**
- `noAccess`: boolean **required**
- `parent`: object, nullable
- `variants`: List<object> **required**

---

---


## MediaTypeCollectionReferenceResponseModel

### Schemas in this file

- [MediaTypeCollectionReferenceResponseModel](#mediatypecollectionreferenceresponsemodel)

---

### MediaTypeCollectionReferenceResponseModel

**Fields:**

- `alias`: string **required**
- `collection`: object, nullable
- `icon`: string **required**
- `id`: string (uuid) **required**

---

---


## MediaTypeCompositionModel

### Schemas in this file

- [MediaTypeCompositionModel](#mediatypecompositionmodel)

---

### MediaTypeCompositionModel

**Fields:**

- `compositionType`: → `CompositionTypeModel` **required**
- `mediaType`: object **required**

---

---


## MediaTypeCompositionResponseModel

### Schemas in this file

- [MediaTypeCompositionResponseModel](#mediatypecompositionresponsemodel)

---

### MediaTypeCompositionResponseModel

**Fields:**

- `icon`: string **required**
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## MediaTypeItemResponseModel

### Schemas in this file

- [MediaTypeItemResponseModel](#mediatypeitemresponsemodel)

---

### MediaTypeItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## MediaTypePropertyTypeContainerResponseModel

### Schemas in this file

- [MediaTypePropertyTypeContainerResponseModel](#mediatypepropertytypecontainerresponsemodel)

---

### MediaTypePropertyTypeContainerResponseModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable
- `parent`: object, nullable
- `sortOrder`: integer (int32) **required**
- `type`: string **required**

---

---


## MediaTypePropertyTypeReferenceResponseModel

### Schemas in this file

- [MediaTypePropertyTypeReferenceResponseModel](#mediatypepropertytypereferenceresponsemodel)

---

### MediaTypePropertyTypeReferenceResponseModel

**Fields:**

- `$type`: string **required**
- `alias`: string, nullable
- `id`: string (uuid) **required**
- `mediaType`: object **required**
- `name`: string, nullable

---

---


## MediaTypePropertyTypeResponseModel

### Schemas in this file

- [MediaTypePropertyTypeResponseModel](#mediatypepropertytyperesponsemodel)

---

### MediaTypePropertyTypeResponseModel

**Fields:**

- `alias`: string **required**
- `appearance`: object **required**
- `container`: object, nullable
- `dataType`: object **required**
- `description`: string, nullable
- `id`: string (uuid) **required**
- `name`: string **required**
- `sortOrder`: integer (int32) **required**
- `validation`: object **required**
- `variesByCulture`: boolean **required**
- `variesBySegment`: boolean **required**

---

---


## MediaTypeReferenceResponseModel

### Schemas in this file

- [MediaTypeReferenceResponseModel](#mediatypereferenceresponsemodel)

---

### MediaTypeReferenceResponseModel

**Fields:**

- `collection`: object, nullable
- `icon`: string **required**
- `id`: string (uuid) **required**

---

---


## MediaTypeSortModel

### Schemas in this file

- [MediaTypeSortModel](#mediatypesortmodel)

---

### MediaTypeSortModel

**Fields:**

- `mediaType`: object **required**
- `sortOrder`: integer (int32) **required**

---

---


## MediaTypeTreeItemResponseModel

### Schemas in this file

- [MediaTypeTreeItemResponseModel](#mediatypetreeitemresponsemodel)

---

### MediaTypeTreeItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `hasChildren`: boolean **required**
- `icon`: string **required**
- `id`: string (uuid) **required**
- `isDeletable`: boolean **required**
- `isFolder`: boolean **required**
- `name`: string **required**
- `parent`: object, nullable

---

---


## MediaUrlInfoModel

### Schemas in this file

- [MediaUrlInfoModel](#mediaurlinfomodel)

---

### MediaUrlInfoModel

**Fields:**

- `culture`: string, nullable **required**
- `url`: string, nullable **required**

---

---


## MediaUrlInfoResponseModel

### Schemas in this file

- [MediaUrlInfoResponseModel](#mediaurlinforesponsemodel)

---

### MediaUrlInfoResponseModel

**Fields:**

- `id`: string (uuid) **required**
- `urlInfos`: List<object> **required**

---

---


## MediaValueModel

### Schemas in this file

- [MediaValueModel](#mediavaluemodel)

---

### MediaValueModel

**Fields:**

- `alias`: string **required**
- `culture`: string, nullable
- `segment`: string, nullable
- `value`: object, nullable

---

---


## MediaValueResponseModel

### Schemas in this file

- [MediaValueResponseModel](#mediavalueresponsemodel)

---

### MediaValueResponseModel

**Fields:**

- `alias`: string **required**
- `culture`: string, nullable
- `editorAlias`: string **required**
- `segment`: string, nullable
- `value`: object, nullable

---

---


## MediaVariantRequestModel

### Schemas in this file

- [MediaVariantRequestModel](#mediavariantrequestmodel)

---

### MediaVariantRequestModel

**Fields:**

- `culture`: string, nullable
- `name`: string **required**
- `segment`: string, nullable

---

---


## MediaVariantResponseModel

### Schemas in this file

- [MediaVariantResponseModel](#mediavariantresponsemodel)

---

### MediaVariantResponseModel

**Fields:**

- `createDate`: string (date-time) **required**
- `culture`: string, nullable
- `name`: string **required**
- `segment`: string, nullable
- `updateDate`: string (date-time) **required**

---

---


## MemberGroupItemResponseModel

### Schemas in this file

- [MemberGroupItemResponseModel](#membergroupitemresponsemodel)

---

### MemberGroupItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## MemberItemResponseModel

### Schemas in this file

- [MemberItemResponseModel](#memberitemresponsemodel)

---

### MemberItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `kind`: → `MemberKindModel` **required**
- `memberType`: object **required**
- `variants`: List<object> **required**

---

---


## MemberReferenceResponseModel

### Schemas in this file

- [MemberReferenceResponseModel](#memberreferenceresponsemodel)

---

### MemberReferenceResponseModel

**Fields:**

- `$type`: string **required**
- `id`: string (uuid) **required**
- `memberType`: object **required**
- `name`: string, nullable

---

---


## MemberTypeCompositionModel

### Schemas in this file

- [MemberTypeCompositionModel](#membertypecompositionmodel)

---

### MemberTypeCompositionModel

**Fields:**

- `compositionType`: → `CompositionTypeModel` **required**
- `memberType`: object **required**

---

---


## MemberTypeCompositionResponseModel

### Schemas in this file

- [MemberTypeCompositionResponseModel](#membertypecompositionresponsemodel)

---

### MemberTypeCompositionResponseModel

**Fields:**

- `icon`: string **required**
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## MemberTypeItemResponseModel

### Schemas in this file

- [MemberTypeItemResponseModel](#membertypeitemresponsemodel)

---

### MemberTypeItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## MemberTypePropertyTypeContainerResponseModel

### Schemas in this file

- [MemberTypePropertyTypeContainerResponseModel](#membertypepropertytypecontainerresponsemodel)

---

### MemberTypePropertyTypeContainerResponseModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable
- `parent`: object, nullable
- `sortOrder`: integer (int32) **required**
- `type`: string **required**

---

---


## MemberTypePropertyTypeReferenceResponseModel

### Schemas in this file

- [MemberTypePropertyTypeReferenceResponseModel](#membertypepropertytypereferenceresponsemodel)

---

### MemberTypePropertyTypeReferenceResponseModel

**Fields:**

- `$type`: string **required**
- `alias`: string, nullable
- `id`: string (uuid) **required**
- `memberType`: object **required**
- `name`: string, nullable

---

---


## MemberTypePropertyTypeResponseModel

### Schemas in this file

- [MemberTypePropertyTypeResponseModel](#membertypepropertytyperesponsemodel)

---

### MemberTypePropertyTypeResponseModel

**Fields:**

- `alias`: string **required**
- `appearance`: object **required**
- `container`: object, nullable
- `dataType`: object **required**
- `description`: string, nullable
- `id`: string (uuid) **required**
- `isSensitive`: boolean **required**
- `name`: string **required**
- `sortOrder`: integer (int32) **required**
- `validation`: object **required**
- `variesByCulture`: boolean **required**
- `variesBySegment`: boolean **required**
- `visibility`: object **required**

---

---


## MemberTypePropertyTypeVisibilityModel

### Schemas in this file

- [MemberTypePropertyTypeVisibilityModel](#membertypepropertytypevisibilitymodel)

---

### MemberTypePropertyTypeVisibilityModel

**Fields:**

- `memberCanEdit`: boolean **required**
- `memberCanView`: boolean **required**

---

---


## MemberTypeReferenceResponseModel

### Schemas in this file

- [MemberTypeReferenceResponseModel](#membertypereferenceresponsemodel)

---

### MemberTypeReferenceResponseModel

**Fields:**

- `collection`: object, nullable
- `icon`: string **required**
- `id`: string (uuid) **required**

---

---


## MemberTypeTreeItemResponseModel

### Schemas in this file

- [MemberTypeTreeItemResponseModel](#membertypetreeitemresponsemodel)

---

### MemberTypeTreeItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `hasChildren`: boolean **required**
- `icon`: string **required**
- `id`: string (uuid) **required**
- `isFolder`: boolean **required**
- `name`: string **required**
- `parent`: object, nullable

---

---


## MemberValueModel

### Schemas in this file

- [MemberValueModel](#membervaluemodel)

---

### MemberValueModel

**Fields:**

- `alias`: string **required**
- `culture`: string, nullable
- `segment`: string, nullable
- `value`: object, nullable

---

---


## MemberValueResponseModel

### Schemas in this file

- [MemberValueResponseModel](#membervalueresponsemodel)

---

### MemberValueResponseModel

**Fields:**

- `alias`: string **required**
- `culture`: string, nullable
- `editorAlias`: string **required**
- `segment`: string, nullable
- `value`: object, nullable

---

---


## MemberVariantRequestModel

### Schemas in this file

- [MemberVariantRequestModel](#membervariantrequestmodel)

---

### MemberVariantRequestModel

**Fields:**

- `culture`: string, nullable
- `name`: string **required**
- `segment`: string, nullable

---

---


## MemberVariantResponseModel

### Schemas in this file

- [MemberVariantResponseModel](#membervariantresponsemodel)

---

### MemberVariantResponseModel

**Fields:**

- `createDate`: string (date-time) **required**
- `culture`: string, nullable
- `name`: string **required**
- `segment`: string, nullable
- `updateDate`: string (date-time) **required**

---

---
