# Common — Part 1: Contents → DocumentVariantRequestModel

## Contents

- [AllowedDocumentTypeModel](#alloweddocumenttypemodel)
- [AllowedMediaTypeItemResponseModel](#allowedmediatypeitemresponsemodel)
- [AllowedMediaTypeModel](#allowedmediatypemodel)
- [AuditLogResponseModel](#auditlogresponsemodel)
- [AuditTypeModel](#audittypemodel)
- [AvailableDocumentTypeCompositionResponseModel](#availabledocumenttypecompositionresponsemodel)
- [AvailableMediaTypeCompositionResponseModel](#availablemediatypecompositionresponsemodel)
- [AvailableMemberTypeCompositionResponseModel](#availablemembertypecompositionresponsemodel)
- [CompositionTypeModel](#compositiontypemodel)
- [ConsentLevelPresentationModel](#consentlevelpresentationmodel)
- [CreateDocumentTypePropertyTypeContainerRequestModel](#createdocumenttypepropertytypecontainerrequestmodel)
- [CreateDocumentTypePropertyTypeRequestModel](#createdocumenttypepropertytyperequestmodel)
- [CreateFolderRequestModel](#createfolderrequestmodel)
- [CreateMediaTypePropertyTypeContainerRequestModel](#createmediatypepropertytypecontainerrequestmodel)
- [CreateMediaTypePropertyTypeRequestModel](#createmediatypepropertytyperequestmodel)
- [CreateMemberTypePropertyTypeContainerRequestModel](#createmembertypepropertytypecontainerrequestmodel)
- [CreateMemberTypePropertyTypeRequestModel](#createmembertypepropertytyperequestmodel)
- [CultureAndScheduleRequestModel](#cultureandschedulerequestmodel)
- [CultureReponseModel](#culturereponsemodel)
- [DatabaseSettingsPresentationModel](#databasesettingspresentationmodel)
- [DataTypeChangeModeModel](#datatypechangemodemodel)
- [DataTypeItemResponseModel](#datatypeitemresponsemodel)
- [DataTypePropertyPresentationModel](#datatypepropertypresentationmodel)
- [DataTypeTreeItemResponseModel](#datatypetreeitemresponsemodel)
- [DefaultReferenceResponseModel](#defaultreferenceresponsemodel)
- [DictionaryItemItemResponseModel](#dictionaryitemitemresponsemodel)
- [DictionaryItemTranslationModel](#dictionaryitemtranslationmodel)
- [DictionaryOverviewResponseModel](#dictionaryoverviewresponsemodel)
- [DirectionModel](#directionmodel)
- [DocumentBlueprintItemResponseModel](#documentblueprintitemresponsemodel)
- [DocumentBlueprintTreeItemResponseModel](#documentblueprinttreeitemresponsemodel)
- [DocumentCollectionResponseModel](#documentcollectionresponsemodel)
- [DocumentItemResponseModel](#documentitemresponsemodel)
- [DocumentNotificationResponseModel](#documentnotificationresponsemodel)
- [DocumentPermissionPresentationModel](#documentpermissionpresentationmodel)
- [DocumentPropertyValuePermissionPresentationModel](#documentpropertyvaluepermissionpresentationmodel)
- [DocumentRecycleBinItemResponseModel](#documentrecyclebinitemresponsemodel)
- [DocumentReferenceResponseModel](#documentreferenceresponsemodel)
- [DocumentTreeItemResponseModel](#documenttreeitemresponsemodel)
- [DocumentTypeBlueprintItemResponseModel](#documenttypeblueprintitemresponsemodel)
- [DocumentTypeCleanupModel](#documenttypecleanupmodel)
- [DocumentTypeCollectionReferenceResponseModel](#documenttypecollectionreferenceresponsemodel)
- [DocumentTypeCompositionModel](#documenttypecompositionmodel)
- [DocumentTypeCompositionResponseModel](#documenttypecompositionresponsemodel)
- [DocumentTypeItemResponseModel](#documenttypeitemresponsemodel)
- [DocumentTypePropertyTypeContainerResponseModel](#documenttypepropertytypecontainerresponsemodel)
- [DocumentTypePropertyTypeReferenceResponseModel](#documenttypepropertytypereferenceresponsemodel)
- [DocumentTypePropertyTypeResponseModel](#documenttypepropertytyperesponsemodel)
- [DocumentTypeReferenceResponseModel](#documenttypereferenceresponsemodel)
- [DocumentTypeSortModel](#documenttypesortmodel)
- [DocumentTypeTreeItemResponseModel](#documenttypetreeitemresponsemodel)
- [DocumentUrlInfoResponseModel](#documenturlinforesponsemodel)
- [DocumentValueModel](#documentvaluemodel)
- [DocumentValueResponseModel](#documentvalueresponsemodel)
- [DocumentVariantItemResponseModel](#documentvariantitemresponsemodel)
- [DocumentVariantRequestModel](#documentvariantrequestmodel)
- [DocumentVariantResponseModel](#documentvariantresponsemodel)
- [DocumentVariantStateModel](#documentvariantstatemodel)
- [DocumentVersionItemResponseModel](#documentversionitemresponsemodel)
- [DomainPresentationModel](#domainpresentationmodel)
- [DynamicRootContextRequestModel](#dynamicrootcontextrequestmodel)
- [DynamicRootQueryOriginRequestModel](#dynamicrootqueryoriginrequestmodel)
- [DynamicRootQueryRequestModel](#dynamicrootqueryrequestmodel)
- [DynamicRootQueryStepRequestModel](#dynamicrootquerysteprequestmodel)
- [EventMessageTypeModel](#eventmessagetypemodel)
- [FieldPresentationModel](#fieldpresentationmodel)
- [FileSystemFolderModel](#filesystemfoldermodel)
- [FileSystemTreeItemPresentationModel](#filesystemtreeitempresentationmodel)
- [FlagModel](#flagmodel)
- [FolderResponseModel](#folderresponsemodel)
- [HealthCheckGroupResponseModel](#healthcheckgroupresponsemodel)
- [HealthCheckModel](#healthcheckmodel)
- [HealthCheckWithResultPresentationModel](#healthcheckwithresultpresentationmodel)
- [HealthStatusModel](#healthstatusmodel)
- [HealthStatusResponseModel](#healthstatusresponsemodel)
- [HelpPageResponseModel](#helppageresponsemodel)
- [ItemAncestorsResponseModelDocumentItemResponseModel](#itemancestorsresponsemodeldocumentitemresponsemodel)
- [ItemAncestorsResponseModelMediaItemResponseModel](#itemancestorsresponsemodelmediaitemresponsemodel)
- [ItemAncestorsResponseModelMemberItemResponseModel](#itemancestorsresponsemodelmemberitemresponsemodel)
- [ItemAncestorsResponseModelNamedItemResponseModel](#itemancestorsresponsemodelnameditemresponsemodel)
- [ItemAncestorsResponseModelTemplateItemResponseModel](#itemancestorsresponsemodeltemplateitemresponsemodel)
- [ItemReferenceByIdResponseModel](#itemreferencebyidresponsemodel)
- [ItemSortingRequestModel](#itemsortingrequestmodel)
- [LoggerResponseModel](#loggerresponsemodel)
- [LogMessagePropertyPresentationModel](#logmessagepropertypresentationmodel)
- [LogMessageResponseModel](#logmessageresponsemodel)
- [LogTemplateResponseModel](#logtemplateresponsemodel)
- [ManifestResponseModel](#manifestresponsemodel)
- [MediaCollectionResponseModel](#mediacollectionresponsemodel)
- [MediaItemResponseModel](#mediaitemresponsemodel)
- [MediaRecycleBinItemResponseModel](#mediarecyclebinitemresponsemodel)
- [MediaReferenceResponseModel](#mediareferenceresponsemodel)
- [MediaTreeItemResponseModel](#mediatreeitemresponsemodel)
- [MediaTypeCollectionReferenceResponseModel](#mediatypecollectionreferenceresponsemodel)
- [MediaTypeCompositionModel](#mediatypecompositionmodel)
- [MediaTypeCompositionResponseModel](#mediatypecompositionresponsemodel)
- [MediaTypeItemResponseModel](#mediatypeitemresponsemodel)
- [MediaTypePropertyTypeContainerResponseModel](#mediatypepropertytypecontainerresponsemodel)
- [MediaTypePropertyTypeReferenceResponseModel](#mediatypepropertytypereferenceresponsemodel)
- [MediaTypePropertyTypeResponseModel](#mediatypepropertytyperesponsemodel)
- [MediaTypeReferenceResponseModel](#mediatypereferenceresponsemodel)
- [MediaTypeSortModel](#mediatypesortmodel)
- [MediaTypeTreeItemResponseModel](#mediatypetreeitemresponsemodel)
- [MediaUrlInfoModel](#mediaurlinfomodel)
- [MediaUrlInfoResponseModel](#mediaurlinforesponsemodel)
- [MediaValueModel](#mediavaluemodel)
- [MediaValueResponseModel](#mediavalueresponsemodel)
- [MediaVariantRequestModel](#mediavariantrequestmodel)
- [MediaVariantResponseModel](#mediavariantresponsemodel)
- [MemberGroupItemResponseModel](#membergroupitemresponsemodel)
- [MemberItemResponseModel](#memberitemresponsemodel)
- [MemberReferenceResponseModel](#memberreferenceresponsemodel)
- [MemberTypeCompositionModel](#membertypecompositionmodel)
- [MemberTypeCompositionResponseModel](#membertypecompositionresponsemodel)
- [MemberTypeItemResponseModel](#membertypeitemresponsemodel)
- [MemberTypePropertyTypeContainerResponseModel](#membertypepropertytypecontainerresponsemodel)
- [MemberTypePropertyTypeReferenceResponseModel](#membertypepropertytypereferenceresponsemodel)
- [MemberTypePropertyTypeResponseModel](#membertypepropertytyperesponsemodel)
- [MemberTypePropertyTypeVisibilityModel](#membertypepropertytypevisibilitymodel)
- [MemberTypeReferenceResponseModel](#membertypereferenceresponsemodel)
- [MemberTypeTreeItemResponseModel](#membertypetreeitemresponsemodel)
- [MemberValueModel](#membervaluemodel)
- [MemberValueResponseModel](#membervalueresponsemodel)
- [MemberVariantRequestModel](#membervariantrequestmodel)
- [MemberVariantResponseModel](#membervariantresponsemodel)
- [NamedEntityTreeItemResponseModel](#namedentitytreeitemresponsemodel)
- [NamedItemResponseModel](#nameditemresponsemodel)
- [NewsDashboardItemResponseModel](#newsdashboarditemresponsemodel)
- [NotificationHeaderModel](#notificationheadermodel)
- [ObjectTypeResponseModel](#objecttyperesponsemodel)
- [OperatorModel](#operatormodel)
- [PackageMigrationStatusResponseModel](#packagemigrationstatusresponsemodel)
- [PagedAuditLogResponseModel](#pagedauditlogresponsemodel)
- [PagedFileSystemTreeItemPresentationModel](#pagedfilesystemtreeitempresentationmodel)
- [PagedIReferenceResponseModel](#pagedireferenceresponsemodel)
- [PagedNamedEntityTreeItemResponseModel](#pagednamedentitytreeitemresponsemodel)
- [PagedProblemDetailsModel](#pagedproblemdetailsmodel)
- [PagedReferenceByIdModel](#pagedreferencebyidmodel)
- [PagedSegmentResponseModel](#pagedsegmentresponsemodel)
- [PartialViewItemResponseModel](#partialviewitemresponsemodel)
- [PartialViewSnippetItemResponseModel](#partialviewsnippetitemresponsemodel)
- [PasswordConfigurationResponseModel](#passwordconfigurationresponsemodel)
- [ProblemDetails](#problemdetails)
- [ProblemDetailsBuilderModel](#problemdetailsbuildermodel)
- [PropertyTypeAppearanceModel](#propertytypeappearancemodel)
- [PropertyTypeValidationModel](#propertytypevalidationmodel)
- [RedirectUrlResponseModel](#redirecturlresponsemodel)
- [ReferenceByIdModel](#referencebyidmodel)
- [RelationReferenceModel](#relationreferencemodel)
- [RelationResponseModel](#relationresponsemodel)
- [RelationTypeItemResponseModel](#relationtypeitemresponsemodel)
- [ScheduleRequestModel](#schedulerequestmodel)
- [ScriptItemResponseModel](#scriptitemresponsemodel)
- [SearcherResponseModel](#searcherresponsemodel)
- [SearchResultResponseModel](#searchresultresponsemodel)
- [SegmentResponseModel](#segmentresponsemodel)
- [ServerConfigurationItemResponseModel](#serverconfigurationitemresponsemodel)
- [SortingRequestModel](#sortingrequestmodel)
- [StaticFileItemResponseModel](#staticfileitemresponsemodel)
- [StylesheetItemResponseModel](#stylesheetitemresponsemodel)
- [SubsetFileSystemTreeItemPresentationModel](#subsetfilesystemtreeitempresentationmodel)
- [TagResponseModel](#tagresponsemodel)
- [TemplateItemResponseModel](#templateitemresponsemodel)
- [TemplateQueryExecuteFilterPresentationModel](#templatequeryexecutefilterpresentationmodel)
- [TemplateQueryExecuteSortModel](#templatequeryexecutesortmodel)
- [TemplateQueryOperatorModel](#templatequeryoperatormodel)
- [TemplateQueryPropertyPresentationModel](#templatequerypropertypresentationmodel)
- [TemplateQueryPropertyTypeModel](#templatequerypropertytypemodel)
- [TemplateQueryResultItemPresentationModel](#templatequeryresultitempresentationmodel)
- [TrackedReferenceDocumentTypeModel](#trackedreferencedocumenttypemodel)
- [TrackedReferenceMediaTypeModel](#trackedreferencemediatypemodel)
- [TrackedReferenceMemberTypeModel](#trackedreferencemembertypemodel)
- [TreeItemKindModel](#treeitemkindmodel)
- [UnknownTypePermissionPresentationModel](#unknowntypepermissionpresentationmodel)
- [UpdateDocumentTypePropertyTypeContainerRequestModel](#updatedocumenttypepropertytypecontainerrequestmodel)
- [UpdateDocumentTypePropertyTypeRequestModel](#updatedocumenttypepropertytyperequestmodel)
- [UpdateFolderResponseModel](#updatefolderresponsemodel)
- [UpdateMediaTypePropertyTypeContainerRequestModel](#updatemediatypepropertytypecontainerrequestmodel)
- [UpdateMediaTypePropertyTypeRequestModel](#updatemediatypepropertytyperequestmodel)
- [UpdateMemberTypePropertyTypeContainerRequestModel](#updatemembertypepropertytypecontainerrequestmodel)
- [UpdateMemberTypePropertyTypeRequestModel](#updatemembertypepropertytyperequestmodel)
- [UserDataOperationStatusModel](#userdataoperationstatusmodel)
- [UserDataResponseModel](#userdataresponsemodel)
- [UserExternalLoginProviderModel](#userexternalloginprovidermodel)
- [UserGroupItemResponseModel](#usergroupitemresponsemodel)
- [UserInstallRequestModel](#userinstallrequestmodel)
- [UserItemResponseModel](#useritemresponsemodel)
- [UserPermissionModel](#userpermissionmodel)
- [UserSettingsPresentationModel](#usersettingspresentationmodel)
- [UserTwoFactorProviderModel](#usertwofactorprovidermodel)
- [VariantItemResponseModel](#variantitemresponsemodel)
- [WebhookEventModel](#webhookeventmodel)
- [WebhookEventResponseModel](#webhookeventresponsemodel)
- [WebhookItemResponseModel](#webhookitemresponsemodel)
- [WebhookLogResponseModel](#webhooklogresponsemodel)

---


## AllowedDocumentTypeModel

### Schemas in this file

- [AllowedDocumentTypeModel](#alloweddocumenttypemodel)

---

### AllowedDocumentTypeModel

**Fields:**

- `description`: string, nullable
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## AllowedMediaTypeItemResponseModel

### Schemas in this file

- [AllowedMediaTypeItemResponseModel](#allowedmediatypeitemresponsemodel)

---

### AllowedMediaTypeItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `matchedFileExtension`: boolean **required**
- `name`: string **required**

---

---


## AllowedMediaTypeModel

### Schemas in this file

- [AllowedMediaTypeModel](#allowedmediatypemodel)

---

### AllowedMediaTypeModel

**Fields:**

- `description`: string, nullable
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## AuditLogResponseModel

### Schemas in this file

- [AuditLogResponseModel](#auditlogresponsemodel)

---

### AuditLogResponseModel

**Fields:**

- `comment`: string, nullable
- `logType`: → `AuditTypeModel` **required**
- `parameters`: string, nullable
- `timestamp`: string (date-time) **required**
- `user`: object **required**

---

---


## AuditTypeModel

### Schemas in this file

- [AuditTypeModel](#audittypemodel)

---

### AuditTypeModel

**Enum values:** `New`, `Save`, `SaveVariant`, `Open`, `Delete`, `Publish`, `PublishVariant`, `SendToPublish`, `SendToPublishVariant`, `Unpublish`, `UnpublishVariant`, `Move`, `Copy`, `AssignDomain`, `PublicAccess`, `Sort`, `Notify`, `System`, `RollBack`, `PackagerInstall`, `PackagerUninstall`, `Custom`, `ContentVersionPreventCleanup`, `ContentVersionEnableCleanup`

---

---


## AvailableDocumentTypeCompositionResponseModel

### Schemas in this file

- [AvailableDocumentTypeCompositionResponseModel](#availabledocumenttypecompositionresponsemodel)

---

### AvailableDocumentTypeCompositionResponseModel

**Fields:**

- `folderPath`: List<string> **required**
- `icon`: string **required**
- `id`: string (uuid) **required**
- `isCompatible`: boolean **required**
- `name`: string **required**

---

---


## AvailableMediaTypeCompositionResponseModel

### Schemas in this file

- [AvailableMediaTypeCompositionResponseModel](#availablemediatypecompositionresponsemodel)

---

### AvailableMediaTypeCompositionResponseModel

**Fields:**

- `folderPath`: List<string> **required**
- `icon`: string **required**
- `id`: string (uuid) **required**
- `isCompatible`: boolean **required**
- `name`: string **required**

---

---


## AvailableMemberTypeCompositionResponseModel

### Schemas in this file

- [AvailableMemberTypeCompositionResponseModel](#availablemembertypecompositionresponsemodel)

---

### AvailableMemberTypeCompositionResponseModel

**Fields:**

- `folderPath`: List<string> **required**
- `icon`: string **required**
- `id`: string (uuid) **required**
- `isCompatible`: boolean **required**
- `name`: string **required**

---

---


## CompositionTypeModel

### Schemas in this file

- [CompositionTypeModel](#compositiontypemodel)

---

### CompositionTypeModel

**Enum values:** `Composition`, `Inheritance`

---

---


## ConsentLevelPresentationModel

### Schemas in this file

- [ConsentLevelPresentationModel](#consentlevelpresentationmodel)

---

### ConsentLevelPresentationModel

**Fields:**

- `description`: string **required**
- `level`: → `TelemetryLevelModel` **required**

---

---


## CreateDocumentTypePropertyTypeContainerRequestModel

### Schemas in this file

- [CreateDocumentTypePropertyTypeContainerRequestModel](#createdocumenttypepropertytypecontainerrequestmodel)

---

### CreateDocumentTypePropertyTypeContainerRequestModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable
- `parent`: object, nullable
- `sortOrder`: integer (int32) **required**
- `type`: string **required**

---

---


## CreateDocumentTypePropertyTypeRequestModel

### Schemas in this file

- [CreateDocumentTypePropertyTypeRequestModel](#createdocumenttypepropertytyperequestmodel)

---

### CreateDocumentTypePropertyTypeRequestModel

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


## CreateFolderRequestModel

### Schemas in this file

- [CreateFolderRequestModel](#createfolderrequestmodel)

---

### CreateFolderRequestModel

**Fields:**

- `id`: string (uuid), nullable
- `name`: string **required**
- `parent`: object, nullable

---

---


## CreateMediaTypePropertyTypeContainerRequestModel

### Schemas in this file

- [CreateMediaTypePropertyTypeContainerRequestModel](#createmediatypepropertytypecontainerrequestmodel)

---

### CreateMediaTypePropertyTypeContainerRequestModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable
- `parent`: object, nullable
- `sortOrder`: integer (int32) **required**
- `type`: string **required**

---

---


## CreateMediaTypePropertyTypeRequestModel

### Schemas in this file

- [CreateMediaTypePropertyTypeRequestModel](#createmediatypepropertytyperequestmodel)

---

### CreateMediaTypePropertyTypeRequestModel

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


## CreateMemberTypePropertyTypeContainerRequestModel

### Schemas in this file

- [CreateMemberTypePropertyTypeContainerRequestModel](#createmembertypepropertytypecontainerrequestmodel)

---

### CreateMemberTypePropertyTypeContainerRequestModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable
- `parent`: object, nullable
- `sortOrder`: integer (int32) **required**
- `type`: string **required**

---

---


## CreateMemberTypePropertyTypeRequestModel

### Schemas in this file

- [CreateMemberTypePropertyTypeRequestModel](#createmembertypepropertytyperequestmodel)

---

### CreateMemberTypePropertyTypeRequestModel

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


## CultureAndScheduleRequestModel

### Schemas in this file

- [CultureAndScheduleRequestModel](#cultureandschedulerequestmodel)

---

### CultureAndScheduleRequestModel

**Fields:**

- `culture`: string, nullable
- `schedule`: object, nullable

---

---


## CultureReponseModel

### Schemas in this file

- [CultureReponseModel](#culturereponsemodel)

---

### CultureReponseModel

**Fields:**

- `englishName`: string **required**
- `name`: string **required**

---

---


## DatabaseSettingsPresentationModel

### Schemas in this file

- [DatabaseSettingsPresentationModel](#databasesettingspresentationmodel)

---

### DatabaseSettingsPresentationModel

**Fields:**

- `defaultDatabaseName`: string **required**
- `displayName`: string **required**
- `id`: string (uuid) **required**
- `isConfigured`: boolean **required**
- `providerName`: string **required**
- `requiresConnectionTest`: boolean **required**
- `requiresCredentials`: boolean **required**
- `requiresServer`: boolean **required**
- `serverPlaceholder`: string **required**
- `sortOrder`: integer (int32) **required**
- `supportsIntegratedAuthentication`: boolean **required**
- `supportsTrustServerCertificate`: boolean **required**

---

---


## DataTypeChangeModeModel

### Schemas in this file

- [DataTypeChangeModeModel](#datatypechangemodemodel)

---

### DataTypeChangeModeModel

**Enum values:** `True`, `False`, `FalseWithHelpText`

---

---


## DataTypeItemResponseModel

### Schemas in this file

- [DataTypeItemResponseModel](#datatypeitemresponsemodel)

---

### DataTypeItemResponseModel

**Fields:**

- `editorAlias`: string **required**
- `editorUiAlias`: string, nullable
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `isDeletable`: boolean **required**
- `name`: string **required**

---

---


## DataTypePropertyPresentationModel

### Schemas in this file

- [DataTypePropertyPresentationModel](#datatypepropertypresentationmodel)

---

### DataTypePropertyPresentationModel

**Fields:**

- `alias`: string **required**
- `value`: object, nullable

---

---


## DataTypeTreeItemResponseModel

### Schemas in this file

- [DataTypeTreeItemResponseModel](#datatypetreeitemresponsemodel)

---

### DataTypeTreeItemResponseModel

**Fields:**

- `editorUiAlias`: string, nullable
- `flags`: List<object> **required**
- `hasChildren`: boolean **required**
- `id`: string (uuid) **required**
- `isDeletable`: boolean **required**
- `isFolder`: boolean **required**
- `name`: string **required**
- `parent`: object, nullable

---

---


## DefaultReferenceResponseModel

### Schemas in this file

- [DefaultReferenceResponseModel](#defaultreferenceresponsemodel)

---

### DefaultReferenceResponseModel

**Fields:**

- `$type`: string **required**
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `name`: string, nullable
- `type`: string, nullable

---

---


## DictionaryItemItemResponseModel

### Schemas in this file

- [DictionaryItemItemResponseModel](#dictionaryitemitemresponsemodel)

---

### DictionaryItemItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## DictionaryItemTranslationModel

### Schemas in this file

- [DictionaryItemTranslationModel](#dictionaryitemtranslationmodel)

---

### DictionaryItemTranslationModel

**Fields:**

- `isoCode`: string **required**
- `translation`: string **required**

---

---


## DictionaryOverviewResponseModel

### Schemas in this file

- [DictionaryOverviewResponseModel](#dictionaryoverviewresponsemodel)

---

### DictionaryOverviewResponseModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable
- `parent`: object, nullable
- `translatedIsoCodes`: List<string> **required**

---

---


## DirectionModel

### Schemas in this file

- [DirectionModel](#directionmodel)

---

### DirectionModel

**Enum values:** `Ascending`, `Descending`

---

---


## DocumentBlueprintItemResponseModel

### Schemas in this file

- [DocumentBlueprintItemResponseModel](#documentblueprintitemresponsemodel)

---

### DocumentBlueprintItemResponseModel

**Fields:**

- `documentType`: object **required**
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## DocumentBlueprintTreeItemResponseModel

### Schemas in this file

- [DocumentBlueprintTreeItemResponseModel](#documentblueprinttreeitemresponsemodel)

---

### DocumentBlueprintTreeItemResponseModel

**Fields:**

- `documentType`: object, nullable
- `flags`: List<object> **required**
- `hasChildren`: boolean **required**
- `id`: string (uuid) **required**
- `isFolder`: boolean **required**
- `name`: string **required**
- `parent`: object, nullable

---

---


## DocumentCollectionResponseModel

### Schemas in this file

- [DocumentCollectionResponseModel](#documentcollectionresponsemodel)

---

### DocumentCollectionResponseModel

**Fields:**

- `ancestors`: List<object> **required**
- `creator`: string, nullable
- `documentType`: object **required**
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `isProtected`: boolean **required**
- `isTrashed`: boolean **required**
- `sortOrder`: integer (int32) **required**
- `updater`: string, nullable
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

---


## DocumentItemResponseModel

### Schemas in this file

- [DocumentItemResponseModel](#documentitemresponsemodel)

---

### DocumentItemResponseModel

**Fields:**

- `documentType`: object **required**
- `flags`: List<object> **required**
- `hasChildren`: boolean **required**
- `id`: string (uuid) **required**
- `isProtected`: boolean **required**
- `isTrashed`: boolean **required**
- `parent`: object, nullable
- `variants`: List<object> **required**

---

---


## DocumentNotificationResponseModel

### Schemas in this file

- [DocumentNotificationResponseModel](#documentnotificationresponsemodel)

---

### DocumentNotificationResponseModel

**Fields:**

- `actionId`: string **required**
- `alias`: string **required**
- `subscribed`: boolean **required**

---

---


## DocumentPermissionPresentationModel

### Schemas in this file

- [DocumentPermissionPresentationModel](#documentpermissionpresentationmodel)

---

### DocumentPermissionPresentationModel

**Fields:**

- `$type`: string **required**
- `document`: object **required**
- `verbs`: List<string> **required**

---

---


## DocumentPropertyValuePermissionPresentationModel

### Schemas in this file

- [DocumentPropertyValuePermissionPresentationModel](#documentpropertyvaluepermissionpresentationmodel)

---

### DocumentPropertyValuePermissionPresentationModel

**Fields:**

- `$type`: string **required**
- `documentType`: object **required**
- `propertyType`: object **required**
- `verbs`: List<string> **required**

---

---


## DocumentRecycleBinItemResponseModel

### Schemas in this file

- [DocumentRecycleBinItemResponseModel](#documentrecyclebinitemresponsemodel)

---

### DocumentRecycleBinItemResponseModel

**Fields:**

- `createDate`: string (date-time) **required**
- `documentType`: object **required**
- `hasChildren`: boolean **required**
- `id`: string (uuid) **required**
- `parent`: object, nullable
- `variants`: List<object> **required**

---

---


## DocumentReferenceResponseModel

### Schemas in this file

- [DocumentReferenceResponseModel](#documentreferenceresponsemodel)

---

### DocumentReferenceResponseModel

**Fields:**

- `$type`: string **required**
- `documentType`: object **required**
- `id`: string (uuid) **required**
- `name`: string, nullable
- `published`: boolean, nullable
- `variants`: List<object> **required**

---

---


## DocumentTreeItemResponseModel

### Schemas in this file

- [DocumentTreeItemResponseModel](#documenttreeitemresponsemodel)

---

### DocumentTreeItemResponseModel

**Fields:**

- `ancestors`: List<object> **required**
- `createDate`: string (date-time) **required**
- `documentType`: object **required**
- `flags`: List<object> **required**
- `hasChildren`: boolean **required**
- `id`: string (uuid) **required**
- `isProtected`: boolean **required**
- `isTrashed`: boolean **required**
- `noAccess`: boolean **required**
- `parent`: object, nullable
- `variants`: List<object> **required**

---

---


## DocumentTypeBlueprintItemResponseModel

### Schemas in this file

- [DocumentTypeBlueprintItemResponseModel](#documenttypeblueprintitemresponsemodel)

---

### DocumentTypeBlueprintItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## DocumentTypeCleanupModel

### Schemas in this file

- [DocumentTypeCleanupModel](#documenttypecleanupmodel)

---

### DocumentTypeCleanupModel

**Fields:**

- `keepAllVersionsNewerThanDays`: integer (int32), nullable
- `keepLatestVersionPerDayForDays`: integer (int32), nullable
- `preventCleanup`: boolean **required**

---

---


## DocumentTypeCollectionReferenceResponseModel

### Schemas in this file

- [DocumentTypeCollectionReferenceResponseModel](#documenttypecollectionreferenceresponsemodel)

---

### DocumentTypeCollectionReferenceResponseModel

**Fields:**

- `alias`: string **required**
- `collection`: object, nullable
- `icon`: string **required**
- `id`: string (uuid) **required**

---

---


## DocumentTypeCompositionModel

### Schemas in this file

- [DocumentTypeCompositionModel](#documenttypecompositionmodel)

---

### DocumentTypeCompositionModel

**Fields:**

- `compositionType`: → `CompositionTypeModel` **required**
- `documentType`: object **required**

---

---


## DocumentTypeCompositionResponseModel

### Schemas in this file

- [DocumentTypeCompositionResponseModel](#documenttypecompositionresponsemodel)

---

### DocumentTypeCompositionResponseModel

**Fields:**

- `icon`: string **required**
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## DocumentTypeItemResponseModel

### Schemas in this file

- [DocumentTypeItemResponseModel](#documenttypeitemresponsemodel)

---

### DocumentTypeItemResponseModel

**Fields:**

- `description`: string, nullable
- `flags`: List<object> **required**
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `isElement`: boolean **required**
- `name`: string **required**

---

---


## DocumentTypePropertyTypeContainerResponseModel

### Schemas in this file

- [DocumentTypePropertyTypeContainerResponseModel](#documenttypepropertytypecontainerresponsemodel)

---

### DocumentTypePropertyTypeContainerResponseModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable
- `parent`: object, nullable
- `sortOrder`: integer (int32) **required**
- `type`: string **required**

---

---


## DocumentTypePropertyTypeReferenceResponseModel

### Schemas in this file

- [DocumentTypePropertyTypeReferenceResponseModel](#documenttypepropertytypereferenceresponsemodel)

---

### DocumentTypePropertyTypeReferenceResponseModel

**Fields:**

- `$type`: string **required**
- `alias`: string, nullable
- `documentType`: object **required**
- `id`: string (uuid) **required**
- `name`: string, nullable

---

---


## DocumentTypePropertyTypeResponseModel

### Schemas in this file

- [DocumentTypePropertyTypeResponseModel](#documenttypepropertytyperesponsemodel)

---

### DocumentTypePropertyTypeResponseModel

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


## DocumentTypeReferenceResponseModel

### Schemas in this file

- [DocumentTypeReferenceResponseModel](#documenttypereferenceresponsemodel)

---

### DocumentTypeReferenceResponseModel

**Fields:**

- `collection`: object, nullable
- `icon`: string **required**
- `id`: string (uuid) **required**

---

---


## DocumentTypeSortModel

### Schemas in this file

- [DocumentTypeSortModel](#documenttypesortmodel)

---

### DocumentTypeSortModel

**Fields:**

- `documentType`: object **required**
- `sortOrder`: integer (int32) **required**

---

---


## DocumentTypeTreeItemResponseModel

### Schemas in this file

- [DocumentTypeTreeItemResponseModel](#documenttypetreeitemresponsemodel)

---

### DocumentTypeTreeItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `hasChildren`: boolean **required**
- `icon`: string **required**
- `id`: string (uuid) **required**
- `isElement`: boolean **required**
- `isFolder`: boolean **required**
- `name`: string **required**
- `parent`: object, nullable

---

---


## DocumentUrlInfoResponseModel

### Schemas in this file

- [DocumentUrlInfoResponseModel](#documenturlinforesponsemodel)

---

### DocumentUrlInfoResponseModel

**Fields:**

- `id`: string (uuid) **required**
- `urlInfos`: List<object> **required**

---

---


## DocumentValueModel

### Schemas in this file

- [DocumentValueModel](#documentvaluemodel)

---

### DocumentValueModel

**Fields:**

- `alias`: string **required**
- `culture`: string, nullable
- `segment`: string, nullable
- `value`: object, nullable

---

---


## DocumentValueResponseModel

### Schemas in this file

- [DocumentValueResponseModel](#documentvalueresponsemodel)

---

### DocumentValueResponseModel

**Fields:**

- `alias`: string **required**
- `culture`: string, nullable
- `editorAlias`: string **required**
- `segment`: string, nullable
- `value`: object, nullable

---

---


## DocumentVariantItemResponseModel

### Schemas in this file

- [DocumentVariantItemResponseModel](#documentvariantitemresponsemodel)

---

### DocumentVariantItemResponseModel

**Fields:**

- `culture`: string, nullable
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `name`: string **required**
- `state`: → `DocumentVariantStateModel` **required**

---

---


## DocumentVariantRequestModel

### Schemas in this file

- [DocumentVariantRequestModel](#documentvariantrequestmodel)

---

### DocumentVariantRequestModel

**Fields:**

- `culture`: string, nullable
- `name`: string **required**
- `segment`: string, nullable

---

---
