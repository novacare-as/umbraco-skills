# Document — API Endpoints

See `schemas/document.md` for field definitions.

## Contents

### Document

- `GET /umbraco/management/api/v1/collection/document/{id}`
- `POST /umbraco/management/api/v1/document`
- `GET /umbraco/management/api/v1/document/{id}`
- `DELETE /umbraco/management/api/v1/document/{id}`
- `PUT /umbraco/management/api/v1/document/{id}`
- `GET /umbraco/management/api/v1/document/{id}/audit-log`
- `GET /umbraco/management/api/v1/document/{id}/available-segment-options`
- `POST /umbraco/management/api/v1/document/{id}/copy`
- `GET /umbraco/management/api/v1/document/{id}/domains`
- `PUT /umbraco/management/api/v1/document/{id}/domains`
- `PUT /umbraco/management/api/v1/document/{id}/move`
- `PUT /umbraco/management/api/v1/document/{id}/move-to-recycle-bin`
- `GET /umbraco/management/api/v1/document/{id}/notifications`
- `PUT /umbraco/management/api/v1/document/{id}/notifications`
- `GET /umbraco/management/api/v1/document/{id}/preview-url`
- `POST /umbraco/management/api/v1/document/{id}/public-access`
- `DELETE /umbraco/management/api/v1/document/{id}/public-access`
- `GET /umbraco/management/api/v1/document/{id}/public-access`
- `PUT /umbraco/management/api/v1/document/{id}/public-access`
- `PUT /umbraco/management/api/v1/document/{id}/publish`
- `PUT /umbraco/management/api/v1/document/{id}/publish-with-descendants`
- `GET /umbraco/management/api/v1/document/{id}/publish-with-descendants/result/{taskId}`
- `GET /umbraco/management/api/v1/document/{id}/published`
- `GET /umbraco/management/api/v1/document/{id}/referenced-by`
- `GET /umbraco/management/api/v1/document/{id}/referenced-descendants`
- `PUT /umbraco/management/api/v1/document/{id}/unpublish`
- `PUT /umbraco/management/api/v1.1/document/{id}/validate`
- `GET /umbraco/management/api/v1/document/are-referenced`
- `GET /umbraco/management/api/v1/document/configuration`
- `PUT /umbraco/management/api/v1/document/sort`
- `GET /umbraco/management/api/v1/document/urls`
- `POST /umbraco/management/api/v1/document/validate`
- `GET /umbraco/management/api/v1/item/document`
- `GET /umbraco/management/api/v1/item/document/ancestors`
- `GET /umbraco/management/api/v1/item/document/search`
- `DELETE /umbraco/management/api/v1/recycle-bin/document`
- `DELETE /umbraco/management/api/v1/recycle-bin/document/{id}`
- `GET /umbraco/management/api/v1/recycle-bin/document/{id}/original-parent`
- `PUT /umbraco/management/api/v1/recycle-bin/document/{id}/restore`
- `GET /umbraco/management/api/v1/recycle-bin/document/children`
- `GET /umbraco/management/api/v1/recycle-bin/document/referenced-by`
- `GET /umbraco/management/api/v1/recycle-bin/document/root`
- `GET /umbraco/management/api/v1/recycle-bin/document/siblings`
- `GET /umbraco/management/api/v1/tree/document/ancestors`
- `GET /umbraco/management/api/v1/tree/document/children`
- `GET /umbraco/management/api/v1/tree/document/root`
- `GET /umbraco/management/api/v1/tree/document/siblings`

---

## Document

### `GET /umbraco/management/api/v1/collection/document/{id}`

**Gets a document collection.**

Operation ID: `GetCollectionDocumentById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `dataTypeId` | query | string (uuid) | No |
| `orderBy` | query | string | No |
| `orderCulture` | query | string | No |
| `orderDirection` | query | → DirectionModel | No |
| `filter` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedDocumentCollectionResponseModel`

---

### `POST /umbraco/management/api/v1/document`

**Creates a new document.**

Operation ID: `PostDocument`

**Request body:** `OneOf: → CreateDocumentRequestModel`


---

### `GET /umbraco/management/api/v1/document/{id}`

**Gets a document.**

Operation ID: `GetDocumentById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → DocumentResponseModel`

---

### `DELETE /umbraco/management/api/v1/document/{id}`

**Deletes a document.**

Operation ID: `DeleteDocumentById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/document/{id}`

**Updates a document.**

Operation ID: `PutDocumentById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateDocumentRequestModel`


---

### `GET /umbraco/management/api/v1/document/{id}/audit-log`

**Gets the audit log for a document.**

Operation ID: `GetDocumentByIdAuditLog`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `orderDirection` | query | → DirectionModel | No |
| `sinceDate` | query | string (date-time) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedAuditLogResponseModel`

---

### `GET /umbraco/management/api/v1/document/{id}/available-segment-options`

**Gets available segments.**

Operation ID: `GetDocumentByIdAvailableSegmentOptions`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedSegmentResponseModel`

---

### `POST /umbraco/management/api/v1/document/{id}/copy`

**Copies a document.**

Operation ID: `PostDocumentByIdCopy`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → CopyDocumentRequestModel`


---

### `GET /umbraco/management/api/v1/document/{id}/domains`

**Gets domains for a document.**

Operation ID: `GetDocumentByIdDomains`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → DomainsResponseModel`

---

### `PUT /umbraco/management/api/v1/document/{id}/domains`

**Updates the domains for a document.**

Operation ID: `PutDocumentByIdDomains`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateDomainsRequestModel`


---

### `PUT /umbraco/management/api/v1/document/{id}/move`

**Moves a document.**

Operation ID: `PutDocumentByIdMove`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → MoveDocumentRequestModel`


---

### `PUT /umbraco/management/api/v1/document/{id}/move-to-recycle-bin`

**Moves a document to the recycle bin.**

Operation ID: `PutDocumentByIdMoveToRecycleBin`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `GET /umbraco/management/api/v1/document/{id}/notifications`

**Gets notifications for a document.**

Operation ID: `GetDocumentByIdNotifications`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `List<object>`

---

### `PUT /umbraco/management/api/v1/document/{id}/notifications`

**Updates notification subscriptions for a document.**

Operation ID: `PutDocumentByIdNotifications`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateDocumentNotificationsRequestModel`


---

### `GET /umbraco/management/api/v1/document/{id}/preview-url`

**Gets the preview URL for a document.**

Operation ID: `GetDocumentByIdPreviewUrl`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `providerAlias` | query | string | No |
| `culture` | query | string | No |
| `segment` | query | string | No |

**Response 200:** `OneOf: → DocumentUrlInfoModel`

---

### `POST /umbraco/management/api/v1/document/{id}/public-access`

**Creates public access rules for a document.**

Operation ID: `PostDocumentByIdPublicAccess`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → PublicAccessRequestModel`


---

### `DELETE /umbraco/management/api/v1/document/{id}/public-access`

**Removes public access settings for a document.**

Operation ID: `DeleteDocumentByIdPublicAccess`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `GET /umbraco/management/api/v1/document/{id}/public-access`

**Gets public access rules for a document.**

Operation ID: `GetDocumentByIdPublicAccess`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `includeAncestors` | query | boolean | No |

**Response 200:** `OneOf: → PublicAccessResponseModel`

---

### `PUT /umbraco/management/api/v1/document/{id}/public-access`

**Updates public access protection for a document.**

Operation ID: `PutDocumentByIdPublicAccess`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → PublicAccessRequestModel`


---

### `PUT /umbraco/management/api/v1/document/{id}/publish`

**Publishes a document.**

Operation ID: `PutDocumentByIdPublish`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → PublishDocumentRequestModel`


---

### `PUT /umbraco/management/api/v1/document/{id}/publish-with-descendants`

**Publishes a document with its descendants.**

Operation ID: `PutDocumentByIdPublishWithDescendants`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → PublishDocumentWithDescendantsRequestModel`

**Response 200:** `OneOf: → PublishWithDescendantsResultModel`

---

### `GET /umbraco/management/api/v1/document/{id}/publish-with-descendants/result/{taskId}`

**Gets the result of publishing a document with descendants.**

Operation ID: `GetDocumentByIdPublishWithDescendantsResultByTaskId`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `taskId` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → PublishWithDescendantsResultModel`

---

### `GET /umbraco/management/api/v1/document/{id}/published`

**Gets a document.**

Operation ID: `GetDocumentByIdPublished`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → PublishedDocumentResponseModel`

---

### `GET /umbraco/management/api/v1/document/{id}/referenced-by`

**Gets a collection of items that reference documents.**

Operation ID: `GetDocumentByIdReferencedBy`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedIReferenceResponseModel`

---

### `GET /umbraco/management/api/v1/document/{id}/referenced-descendants`

**Gets document descendants that are referenced.**

Operation ID: `GetDocumentByIdReferencedDescendants`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedReferenceByIdModel`

---

### `PUT /umbraco/management/api/v1/document/{id}/unpublish`

**Unpublishes a document.**

Operation ID: `PutDocumentByIdUnpublish`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UnpublishDocumentRequestModel`


---

### `PUT /umbraco/management/api/v1.1/document/{id}/validate`

**Validates updating a document.**

Operation ID: `PutUmbracoManagementApiV1.1DocumentByIdValidate1.1`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → ValidateUpdateDocumentRequestModel`


---

### `GET /umbraco/management/api/v1/document/are-referenced`

**Gets a collection of items that reference documents.**

Operation ID: `GetDocumentAreReferenced`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedReferenceByIdModel`

---

### `GET /umbraco/management/api/v1/document/configuration`

**Gets the document configuration.**

Operation ID: `GetDocumentConfiguration`

**Response 200:** `OneOf: → DocumentConfigurationResponseModel`

---

### `PUT /umbraco/management/api/v1/document/sort`

**Sorts documents.**

Operation ID: `PutDocumentSort`

**Request body:** `OneOf: → SortingRequestModel`


---

### `GET /umbraco/management/api/v1/document/urls`

**Gets URLs for a document.**

Operation ID: `GetDocumentUrls`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `POST /umbraco/management/api/v1/document/validate`

**Validates creating a document.**

Operation ID: `PostDocumentValidate`

**Request body:** `OneOf: → CreateDocumentRequestModel`


---

### `GET /umbraco/management/api/v1/item/document`

**Gets a collection of document items.**

Operation ID: `GetItemDocument`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/document/ancestors`

**Gets ancestors for a collection of document items.**

Operation ID: `GetItemDocumentAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/document/search`

**Searches document items.**

Operation ID: `GetItemDocumentSearch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `query` | query | string | No |
| `trashed` | query | boolean | No |
| `culture` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `parentId` | query | string (uuid) | No |
| `allowedDocumentTypes` | query | List<string (uuid)> | No |
| `dataTypeId` | query | string (uuid) | No |

**Response 200:** `OneOf: → PagedModelDocumentItemResponseModel`

---

### `DELETE /umbraco/management/api/v1/recycle-bin/document`

**Empties the document recycle bin.**

Operation ID: `DeleteRecycleBinDocument`


---

### `DELETE /umbraco/management/api/v1/recycle-bin/document/{id}`

**Deletes a document.**

Operation ID: `DeleteRecycleBinDocumentById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `GET /umbraco/management/api/v1/recycle-bin/document/{id}/original-parent`

**Gets the original parent of a document in the recycle bin.**

Operation ID: `GetRecycleBinDocumentByIdOriginalParent`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → ReferenceByIdModel`

---

### `PUT /umbraco/management/api/v1/recycle-bin/document/{id}/restore`

**Restores a document from the recycle bin.**

Operation ID: `PutRecycleBinDocumentByIdRestore`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → MoveMediaRequestModel`


---

### `GET /umbraco/management/api/v1/recycle-bin/document/children`

**Gets a collection of documents in the recycle bin.**

Operation ID: `GetRecycleBinDocumentChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentId` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedDocumentRecycleBinItemResponseModel`

---

### `GET /umbraco/management/api/v1/recycle-bin/document/referenced-by`

**Gets items referencing a document in the recycle bin.**

Operation ID: `GetRecycleBinDocumentReferencedBy`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedIReferenceResponseModel`

---

### `GET /umbraco/management/api/v1/recycle-bin/document/root`

**Gets documents at the root of the recycle bin.**

Operation ID: `GetRecycleBinDocumentRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedDocumentRecycleBinItemResponseModel`

---

### `GET /umbraco/management/api/v1/recycle-bin/document/siblings`

**Gets sibling documents in the recycle bin.**

Operation ID: `GetRecycleBinDocumentSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `target` | query | string (uuid) | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |
| `dataTypeId` | query | string (uuid) | No |

**Response 200:** `OneOf: → SubsetDocumentRecycleBinItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/document/ancestors`

**Gets a collection of ancestor document items.**

Operation ID: `GetTreeDocumentAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantId` | query | string (uuid) | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/document/children`

**Gets a collection of document tree child items.**

Operation ID: `GetTreeDocumentChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentId` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `dataTypeId` | query | string (uuid) | No |

**Response 200:** `OneOf: → PagedDocumentTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/document/root`

**Gets a collection of document items from the root of the tree.**

Operation ID: `GetTreeDocumentRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `dataTypeId` | query | string (uuid) | No |

**Response 200:** `OneOf: → PagedDocumentTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/document/siblings`

**Gets a collection of document tree sibling items.**

Operation ID: `GetTreeDocumentSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `target` | query | string (uuid) | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |
| `dataTypeId` | query | string (uuid) | No |

**Response 200:** `OneOf: → SubsetDocumentTreeItemResponseModel`

---
