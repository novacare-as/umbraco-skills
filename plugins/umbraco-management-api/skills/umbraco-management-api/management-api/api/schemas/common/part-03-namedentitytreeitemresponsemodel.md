# Common — Part 3: NamedEntityTreeItemResponseModel → WebhookLogResponseModel

## NamedEntityTreeItemResponseModel

### Schemas in this file

- [NamedEntityTreeItemResponseModel](#namedentitytreeitemresponsemodel)

---

### NamedEntityTreeItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `hasChildren`: boolean **required**
- `id`: string (uuid) **required**
- `name`: string **required**
- `parent`: object, nullable

---

---


## NamedItemResponseModel

### Schemas in this file

- [NamedItemResponseModel](#nameditemresponsemodel)

---

### NamedItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## NewsDashboardItemResponseModel

### Schemas in this file

- [NewsDashboardItemResponseModel](#newsdashboarditemresponsemodel)

---

### NewsDashboardItemResponseModel

**Fields:**

- `body`: string, nullable
- `buttonText`: string, nullable
- `header`: string **required**
- `imageAltText`: string, nullable
- `imageUrl`: string, nullable
- `priority`: string **required**
- `url`: string, nullable

---

---


## NotificationHeaderModel

### Schemas in this file

- [NotificationHeaderModel](#notificationheadermodel)

---

### NotificationHeaderModel

**Fields:**

- `category`: string **required**
- `message`: string **required**
- `type`: → `EventMessageTypeModel` **required**

---

---


## ObjectTypeResponseModel

### Schemas in this file

- [ObjectTypeResponseModel](#objecttyperesponsemodel)

---

### ObjectTypeResponseModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable

---

---


## OperatorModel

### Schemas in this file

- [OperatorModel](#operatormodel)

---

### OperatorModel

**Enum values:** `Equals`, `NotEquals`, `Contains`, `NotContains`, `LessThan`, `LessThanEqualTo`, `GreaterThan`, `GreaterThanEqualTo`

---

---


## PackageMigrationStatusResponseModel

### Schemas in this file

- [PackageMigrationStatusResponseModel](#packagemigrationstatusresponsemodel)

---

### PackageMigrationStatusResponseModel

**Fields:**

- `hasPendingMigrations`: boolean **required**
- `packageName`: string **required**

---

---


## PagedAuditLogResponseModel

### Schemas in this file

- [PagedAuditLogResponseModel](#pagedauditlogresponsemodel)

---

### PagedAuditLogResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

---


## PagedFileSystemTreeItemPresentationModel

### Schemas in this file

- [PagedFileSystemTreeItemPresentationModel](#pagedfilesystemtreeitempresentationmodel)

---

### PagedFileSystemTreeItemPresentationModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

---


## PagedIReferenceResponseModel

### Schemas in this file

- [PagedIReferenceResponseModel](#pagedireferenceresponsemodel)

---

### PagedIReferenceResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

---


## PagedNamedEntityTreeItemResponseModel

### Schemas in this file

- [PagedNamedEntityTreeItemResponseModel](#pagednamedentitytreeitemresponsemodel)

---

### PagedNamedEntityTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

---


## PagedProblemDetailsModel

### Schemas in this file

- [PagedProblemDetailsModel](#pagedproblemdetailsmodel)

---

### PagedProblemDetailsModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

---


## PagedReferenceByIdModel

### Schemas in this file

- [PagedReferenceByIdModel](#pagedreferencebyidmodel)

---

### PagedReferenceByIdModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

---


## PagedSegmentResponseModel

### Schemas in this file

- [PagedSegmentResponseModel](#pagedsegmentresponsemodel)

---

### PagedSegmentResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

---


## PartialViewItemResponseModel

### Schemas in this file

- [PartialViewItemResponseModel](#partialviewitemresponsemodel)

---

### PartialViewItemResponseModel

**Fields:**

- `isFolder`: boolean **required**
- `name`: string **required**
- `parent`: object, nullable
- `path`: string **required**

---

---


## PartialViewSnippetItemResponseModel

### Schemas in this file

- [PartialViewSnippetItemResponseModel](#partialviewsnippetitemresponsemodel)

---

### PartialViewSnippetItemResponseModel

**Fields:**

- `id`: string **required**
- `name`: string **required**

---

---


## PasswordConfigurationResponseModel

### Schemas in this file

- [PasswordConfigurationResponseModel](#passwordconfigurationresponsemodel)

---

### PasswordConfigurationResponseModel

**Fields:**

- `minimumPasswordLength`: integer (int32) **required**
- `requireDigit`: boolean **required**
- `requireLowercase`: boolean **required**
- `requireNonLetterOrDigit`: boolean **required**
- `requireUppercase`: boolean **required**

---

---


## ProblemDetails

### Schemas in this file

- [ProblemDetails](#problemdetails)

---

### ProblemDetails

**Fields:**

- `detail`: string, nullable
- `instance`: string, nullable
- `status`: integer (int32), nullable
- `title`: string, nullable
- `type`: string, nullable

---

---


## ProblemDetailsBuilderModel

### Schemas in this file

- [ProblemDetailsBuilderModel](#problemdetailsbuildermodel)

---

### ProblemDetailsBuilderModel

---

---


## PropertyTypeAppearanceModel

### Schemas in this file

- [PropertyTypeAppearanceModel](#propertytypeappearancemodel)

---

### PropertyTypeAppearanceModel

**Fields:**

- `labelOnTop`: boolean **required**

---

---


## PropertyTypeValidationModel

### Schemas in this file

- [PropertyTypeValidationModel](#propertytypevalidationmodel)

---

### PropertyTypeValidationModel

**Fields:**

- `mandatory`: boolean **required**
- `mandatoryMessage`: string, nullable
- `regEx`: string, nullable
- `regExMessage`: string, nullable

---

---


## RedirectUrlResponseModel

### Schemas in this file

- [RedirectUrlResponseModel](#redirecturlresponsemodel)

---

### RedirectUrlResponseModel

**Fields:**

- `created`: string (date-time) **required**
- `culture`: string, nullable
- `destinationUrl`: string **required**
- `document`: object **required**
- `id`: string (uuid) **required**
- `originalUrl`: string **required**

---

---


## ReferenceByIdModel

### Schemas in this file

- [ReferenceByIdModel](#referencebyidmodel)

---

### ReferenceByIdModel

**Fields:**

- `id`: string (uuid) **required**

---

---


## RelationReferenceModel

### Schemas in this file

- [RelationReferenceModel](#relationreferencemodel)

---

### RelationReferenceModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable

---

---


## RelationResponseModel

### Schemas in this file

- [RelationResponseModel](#relationresponsemodel)

---

### RelationResponseModel

**Fields:**

- `child`: object **required**
- `comment`: string, nullable
- `createDate`: string (date-time) **required**
- `id`: string (uuid) **required**
- `parent`: object **required**
- `relationType`: object **required**

---

---


## RelationTypeItemResponseModel

### Schemas in this file

- [RelationTypeItemResponseModel](#relationtypeitemresponsemodel)

---

### RelationTypeItemResponseModel

**Fields:**

- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `isDeletable`: boolean **required**
- `name`: string **required**

---

---


## ScheduleRequestModel

### Schemas in this file

- [ScheduleRequestModel](#schedulerequestmodel)

---

### ScheduleRequestModel

**Fields:**

- `publishTime`: string (date-time), nullable
- `unpublishTime`: string (date-time), nullable

---

---


## ScriptItemResponseModel

### Schemas in this file

- [ScriptItemResponseModel](#scriptitemresponsemodel)

---

### ScriptItemResponseModel

**Fields:**

- `isFolder`: boolean **required**
- `name`: string **required**
- `parent`: object, nullable
- `path`: string **required**

---

---


## SearcherResponseModel

### Schemas in this file

- [SearcherResponseModel](#searcherresponsemodel)

---

### SearcherResponseModel

**Fields:**

- `name`: string **required**

---

---


## SearchResultResponseModel

### Schemas in this file

- [SearchResultResponseModel](#searchresultresponsemodel)

---

### SearchResultResponseModel

**Fields:**

- `fieldCount`: integer (int32) **required**
- `fields`: List<object> **required**
- `id`: string **required**
- `score`: number (float) **required**

---

---


## SegmentResponseModel

### Schemas in this file

- [SegmentResponseModel](#segmentresponsemodel)

---

### SegmentResponseModel

**Fields:**

- `alias`: string **required**
- `cultures`: List<string>, nullable
- `name`: string **required**

---

---


## ServerConfigurationItemResponseModel

### Schemas in this file

- [ServerConfigurationItemResponseModel](#serverconfigurationitemresponsemodel)

---

### ServerConfigurationItemResponseModel

**Fields:**

- `data`: string **required**
- `name`: string **required**

---

---


## SortingRequestModel

### Schemas in this file

- [SortingRequestModel](#sortingrequestmodel)

---

### SortingRequestModel

**Fields:**

- `parent`: object, nullable
- `sorting`: List<object> **required**

---

---


## StaticFileItemResponseModel

### Schemas in this file

- [StaticFileItemResponseModel](#staticfileitemresponsemodel)

---

### StaticFileItemResponseModel

**Fields:**

- `isFolder`: boolean **required**
- `name`: string **required**
- `parent`: object, nullable
- `path`: string **required**

---

---


## StylesheetItemResponseModel

### Schemas in this file

- [StylesheetItemResponseModel](#stylesheetitemresponsemodel)

---

### StylesheetItemResponseModel

**Fields:**

- `isFolder`: boolean **required**
- `name`: string **required**
- `parent`: object, nullable
- `path`: string **required**

---

---


## SubsetFileSystemTreeItemPresentationModel

### Schemas in this file

- [SubsetFileSystemTreeItemPresentationModel](#subsetfilesystemtreeitempresentationmodel)

---

### SubsetFileSystemTreeItemPresentationModel

**Fields:**

- `items`: List<object> **required**
- `totalAfter`: integer (int64) **required**
- `totalBefore`: integer (int64) **required**

---

---


## TagResponseModel

### Schemas in this file

- [TagResponseModel](#tagresponsemodel)

---

### TagResponseModel

**Fields:**

- `group`: string, nullable
- `id`: string (uuid) **required**
- `nodeCount`: integer (int32) **required**
- `text`: string, nullable

---

---


## TemplateItemResponseModel

### Schemas in this file

- [TemplateItemResponseModel](#templateitemresponsemodel)

---

### TemplateItemResponseModel

**Fields:**

- `alias`: string **required**
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## TemplateQueryExecuteFilterPresentationModel

### Schemas in this file

- [TemplateQueryExecuteFilterPresentationModel](#templatequeryexecutefilterpresentationmodel)

---

### TemplateQueryExecuteFilterPresentationModel

**Fields:**

- `constraintValue`: string **required**
- `operator`: → `OperatorModel` **required**
- `propertyAlias`: string **required**

---

---


## TemplateQueryExecuteSortModel

### Schemas in this file

- [TemplateQueryExecuteSortModel](#templatequeryexecutesortmodel)

---

### TemplateQueryExecuteSortModel

**Fields:**

- `direction`: string, nullable
- `propertyAlias`: string **required**

---

---


## TemplateQueryOperatorModel

### Schemas in this file

- [TemplateQueryOperatorModel](#templatequeryoperatormodel)

---

### TemplateQueryOperatorModel

**Fields:**

- `applicableTypes`: List<`TemplateQueryPropertyTypeModel`> **required**
- `operator`: → `OperatorModel` **required**

---

---


## TemplateQueryPropertyPresentationModel

### Schemas in this file

- [TemplateQueryPropertyPresentationModel](#templatequerypropertypresentationmodel)

---

### TemplateQueryPropertyPresentationModel

**Fields:**

- `alias`: string **required**
- `type`: → `TemplateQueryPropertyTypeModel` **required**

---

---


## TemplateQueryPropertyTypeModel

### Schemas in this file

- [TemplateQueryPropertyTypeModel](#templatequerypropertytypemodel)

---

### TemplateQueryPropertyTypeModel

**Enum values:** `String`, `DateTime`, `Integer`

---

---


## TemplateQueryResultItemPresentationModel

### Schemas in this file

- [TemplateQueryResultItemPresentationModel](#templatequeryresultitempresentationmodel)

---

### TemplateQueryResultItemPresentationModel

**Fields:**

- `icon`: string **required**
- `name`: string **required**

---

---


## TrackedReferenceDocumentTypeModel

### Schemas in this file

- [TrackedReferenceDocumentTypeModel](#trackedreferencedocumenttypemodel)

---

### TrackedReferenceDocumentTypeModel

**Fields:**

- `alias`: string, nullable
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `name`: string, nullable

---

---


## TrackedReferenceMediaTypeModel

### Schemas in this file

- [TrackedReferenceMediaTypeModel](#trackedreferencemediatypemodel)

---

### TrackedReferenceMediaTypeModel

**Fields:**

- `alias`: string, nullable
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `name`: string, nullable

---

---


## TrackedReferenceMemberTypeModel

### Schemas in this file

- [TrackedReferenceMemberTypeModel](#trackedreferencemembertypemodel)

---

### TrackedReferenceMemberTypeModel

**Fields:**

- `alias`: string, nullable
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `name`: string, nullable

---

---


## TreeItemKindModel

### Schemas in this file

- [TreeItemKindModel](#treeitemkindmodel)

---

### TreeItemKindModel

**Enum values:** `Item`, `Folder`, `All`

---

---


## UnknownTypePermissionPresentationModel

### Schemas in this file

- [UnknownTypePermissionPresentationModel](#unknowntypepermissionpresentationmodel)

---

### UnknownTypePermissionPresentationModel

**Fields:**

- `$type`: string **required**
- `context`: string **required**
- `verbs`: List<string> **required**

---

---


## UpdateDocumentTypePropertyTypeContainerRequestModel

### Schemas in this file

- [UpdateDocumentTypePropertyTypeContainerRequestModel](#updatedocumenttypepropertytypecontainerrequestmodel)

---

### UpdateDocumentTypePropertyTypeContainerRequestModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable
- `parent`: object, nullable
- `sortOrder`: integer (int32) **required**
- `type`: string **required**

---

---


## UpdateDocumentTypePropertyTypeRequestModel

### Schemas in this file

- [UpdateDocumentTypePropertyTypeRequestModel](#updatedocumenttypepropertytyperequestmodel)

---

### UpdateDocumentTypePropertyTypeRequestModel

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


## UpdateFolderResponseModel

### Schemas in this file

- [UpdateFolderResponseModel](#updatefolderresponsemodel)

---

### UpdateFolderResponseModel

**Fields:**

- `name`: string **required**

---

---


## UpdateMediaTypePropertyTypeContainerRequestModel

### Schemas in this file

- [UpdateMediaTypePropertyTypeContainerRequestModel](#updatemediatypepropertytypecontainerrequestmodel)

---

### UpdateMediaTypePropertyTypeContainerRequestModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable
- `parent`: object, nullable
- `sortOrder`: integer (int32) **required**
- `type`: string **required**

---

---


## UpdateMediaTypePropertyTypeRequestModel

### Schemas in this file

- [UpdateMediaTypePropertyTypeRequestModel](#updatemediatypepropertytyperequestmodel)

---

### UpdateMediaTypePropertyTypeRequestModel

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


## UpdateMemberTypePropertyTypeContainerRequestModel

### Schemas in this file

- [UpdateMemberTypePropertyTypeContainerRequestModel](#updatemembertypepropertytypecontainerrequestmodel)

---

### UpdateMemberTypePropertyTypeContainerRequestModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string, nullable
- `parent`: object, nullable
- `sortOrder`: integer (int32) **required**
- `type`: string **required**

---

---


## UpdateMemberTypePropertyTypeRequestModel

### Schemas in this file

- [UpdateMemberTypePropertyTypeRequestModel](#updatemembertypepropertytyperequestmodel)

---

### UpdateMemberTypePropertyTypeRequestModel

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


## UserDataOperationStatusModel

### Schemas in this file

- [UserDataOperationStatusModel](#userdataoperationstatusmodel)

---

### UserDataOperationStatusModel

**Enum values:** `Success`, `NotFound`, `UserNotFound`, `AlreadyExists`

---

---


## UserDataResponseModel

### Schemas in this file

- [UserDataResponseModel](#userdataresponsemodel)

---

### UserDataResponseModel

**Fields:**

- `group`: string **required**
- `identifier`: string **required**
- `key`: string (uuid) **required**
- `value`: string **required**

---

---


## UserExternalLoginProviderModel

### Schemas in this file

- [UserExternalLoginProviderModel](#userexternalloginprovidermodel)

---

### UserExternalLoginProviderModel

**Fields:**

- `hasManualLinkingEnabled`: boolean **required**
- `isLinkedOnUser`: boolean **required**
- `providerKey`: string, nullable
- `providerSchemeName`: string **required**

---

---


## UserGroupItemResponseModel

### Schemas in this file

- [UserGroupItemResponseModel](#usergroupitemresponsemodel)

---

### UserGroupItemResponseModel

**Fields:**

- `alias`: string, nullable
- `flags`: List<object> **required**
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `name`: string **required**

---

---


## UserInstallRequestModel

### Schemas in this file

- [UserInstallRequestModel](#userinstallrequestmodel)

---

### UserInstallRequestModel

**Fields:**

- `email`: string (email) **required**
- `name`: string **required**
- `password`: string **required**
- `subscribeToNewsletter`: boolean **required**

---

---


## UserItemResponseModel

### Schemas in this file

- [UserItemResponseModel](#useritemresponsemodel)

---

### UserItemResponseModel

**Fields:**

- `avatarUrls`: List<string> **required**
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `kind`: → `UserKindModel` **required**
- `name`: string **required**

---

---


## UserPermissionModel

### Schemas in this file

- [UserPermissionModel](#userpermissionmodel)

---

### UserPermissionModel

**Fields:**

- `nodeKey`: string (uuid) **required**
- `permissions`: List<string> **required**

---

---


## UserSettingsPresentationModel

### Schemas in this file

- [UserSettingsPresentationModel](#usersettingspresentationmodel)

---

### UserSettingsPresentationModel

**Fields:**

- `consentLevels`: List<object> **required**
- `minCharLength`: integer (int32) **required**
- `minNonAlphaNumericLength`: integer (int32) **required**

---

---


## UserTwoFactorProviderModel

### Schemas in this file

- [UserTwoFactorProviderModel](#usertwofactorprovidermodel)

---

### UserTwoFactorProviderModel

**Fields:**

- `isEnabledOnUser`: boolean **required**
- `providerName`: string **required**

---

---


## VariantItemResponseModel

### Schemas in this file

- [VariantItemResponseModel](#variantitemresponsemodel)

---

### VariantItemResponseModel

**Fields:**

- `culture`: string, nullable
- `name`: string **required**

---

---


## WebhookEventModel

### Schemas in this file

- [WebhookEventModel](#webhookeventmodel)

---

### WebhookEventModel

**Fields:**

- `alias`: string **required**
- `eventName`: string **required**
- `eventType`: string **required**

---

---


## WebhookEventResponseModel

### Schemas in this file

- [WebhookEventResponseModel](#webhookeventresponsemodel)

---

### WebhookEventResponseModel

**Fields:**

- `alias`: string **required**
- `eventName`: string **required**
- `eventType`: string **required**

---

---


## WebhookItemResponseModel

### Schemas in this file

- [WebhookItemResponseModel](#webhookitemresponsemodel)

---

### WebhookItemResponseModel

**Fields:**

- `enabled`: boolean **required**
- `events`: string **required**
- `flags`: List<object> **required**
- `id`: string (uuid) **required**
- `name`: string **required**
- `types`: string **required**
- `url`: string **required**

---

---


## WebhookLogResponseModel

### Schemas in this file

- [WebhookLogResponseModel](#webhooklogresponsemodel)

---

### WebhookLogResponseModel

**Fields:**

- `date`: string (date-time) **required**
- `eventAlias`: string **required**
- `exceptionOccured`: boolean **required**
- `isSuccessStatusCode`: boolean **required**
- `key`: string (uuid) **required**
- `requestBody`: string **required**
- `requestHeaders`: string **required**
- `responseBody`: string **required**
- `responseHeaders`: string **required**
- `retryCount`: integer (int32) **required**
- `statusCode`: string **required**
- `url`: string **required**
- `webhookKey`: string (uuid) **required**

---

---
