# Media — API Endpoints

See `schemas/media.md` for field definitions.

## Contents

### Media

- `GET /umbraco/management/api/v1/collection/media`
- `GET /umbraco/management/api/v1/item/media`
- `GET /umbraco/management/api/v1/item/media/ancestors`
- `GET /umbraco/management/api/v1/item/media/search`
- `POST /umbraco/management/api/v1/media`
- `GET /umbraco/management/api/v1/media/{id}`
- `DELETE /umbraco/management/api/v1/media/{id}`
- `PUT /umbraco/management/api/v1/media/{id}`
- `GET /umbraco/management/api/v1/media/{id}/audit-log`
- `PUT /umbraco/management/api/v1/media/{id}/move`
- `PUT /umbraco/management/api/v1/media/{id}/move-to-recycle-bin`
- `GET /umbraco/management/api/v1/media/{id}/referenced-by`
- `GET /umbraco/management/api/v1/media/{id}/referenced-descendants`
- `PUT /umbraco/management/api/v1/media/{id}/validate`
- `GET /umbraco/management/api/v1/media/are-referenced`
- `GET /umbraco/management/api/v1/media/configuration`
- `PUT /umbraco/management/api/v1/media/sort`
- `GET /umbraco/management/api/v1/media/urls`
- `POST /umbraco/management/api/v1/media/validate`
- `DELETE /umbraco/management/api/v1/recycle-bin/media`
- `DELETE /umbraco/management/api/v1/recycle-bin/media/{id}`
- `GET /umbraco/management/api/v1/recycle-bin/media/{id}/original-parent`
- `PUT /umbraco/management/api/v1/recycle-bin/media/{id}/restore`
- `GET /umbraco/management/api/v1/recycle-bin/media/children`
- `GET /umbraco/management/api/v1/recycle-bin/media/referenced-by`
- `GET /umbraco/management/api/v1/recycle-bin/media/root`
- `GET /umbraco/management/api/v1/recycle-bin/media/siblings`
- `GET /umbraco/management/api/v1/tree/media/ancestors`
- `GET /umbraco/management/api/v1/tree/media/children`
- `GET /umbraco/management/api/v1/tree/media/root`
- `GET /umbraco/management/api/v1/tree/media/siblings`

---

## Media

### `GET /umbraco/management/api/v1/collection/media`

**Gets a collection of media items.**

Operation ID: `GetCollectionMedia`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | string (uuid) | No |
| `dataTypeId` | query | string (uuid) | No |
| `orderBy` | query | string | No |
| `orderDirection` | query | → DirectionModel | No |
| `filter` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedMediaCollectionResponseModel`

---

### `GET /umbraco/management/api/v1/item/media`

**Gets a collection of media items.**

Operation ID: `GetItemMedia`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/media/ancestors`

**Gets ancestors for a collection of media items.**

Operation ID: `GetItemMediaAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/media/search`

**Searches media items.**

Operation ID: `GetItemMediaSearch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `query` | query | string | No |
| `trashed` | query | boolean | No |
| `culture` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `parentId` | query | string (uuid) | No |
| `allowedMediaTypes` | query | List<string (uuid)> | No |
| `dataTypeId` | query | string (uuid) | No |

**Response 200:** `OneOf: → PagedModelMediaItemResponseModel`

---

### `POST /umbraco/management/api/v1/media`

**Creates a new media.**

Operation ID: `PostMedia`

**Request body:** `OneOf: → CreateMediaRequestModel`


---

### `GET /umbraco/management/api/v1/media/{id}`

**Gets a media item.**

Operation ID: `GetMediaById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → MediaResponseModel`

---

### `DELETE /umbraco/management/api/v1/media/{id}`

**Deletes a media item.**

Operation ID: `DeleteMediaById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/media/{id}`

**Updates a media item.**

Operation ID: `PutMediaById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateMediaRequestModel`


---

### `GET /umbraco/management/api/v1/media/{id}/audit-log`

**Gets the audit log for a media item.**

Operation ID: `GetMediaByIdAuditLog`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `orderDirection` | query | → DirectionModel | No |
| `sinceDate` | query | string (date-time) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedAuditLogResponseModel`

---

### `PUT /umbraco/management/api/v1/media/{id}/move`

**Moves a media item.**

Operation ID: `PutMediaByIdMove`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → MoveMediaRequestModel`


---

### `PUT /umbraco/management/api/v1/media/{id}/move-to-recycle-bin`

**Moves a media item to the recycle bin.**

Operation ID: `PutMediaByIdMoveToRecycleBin`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `GET /umbraco/management/api/v1/media/{id}/referenced-by`

**Gets a collection of items that reference a media item.**

Operation ID: `GetMediaByIdReferencedBy`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedIReferenceResponseModel`

---

### `GET /umbraco/management/api/v1/media/{id}/referenced-descendants`

**Gets media descendants that are referenced.**

Operation ID: `GetMediaByIdReferencedDescendants`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedReferenceByIdModel`

---

### `PUT /umbraco/management/api/v1/media/{id}/validate`

**Validates updating a media item.**

Operation ID: `PutMediaByIdValidate`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateMediaRequestModel`


---

### `GET /umbraco/management/api/v1/media/are-referenced`

**Gets a collection of referenced media items.**

Operation ID: `GetMediaAreReferenced`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedReferenceByIdModel`

---

### `GET /umbraco/management/api/v1/media/configuration`

**Gets the media configuration.**

Operation ID: `GetMediaConfiguration`

**Response 200:** `OneOf: → MediaConfigurationResponseModel`

---

### `PUT /umbraco/management/api/v1/media/sort`

**Sorts media items.**

Operation ID: `PutMediaSort`

**Request body:** `OneOf: → SortingRequestModel`


---

### `GET /umbraco/management/api/v1/media/urls`

**Gets URLs for media items.**

Operation ID: `GetMediaUrls`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `POST /umbraco/management/api/v1/media/validate`

**Validates creating a media item.**

Operation ID: `PostMediaValidate`

**Request body:** `OneOf: → CreateMediaRequestModel`


---

### `DELETE /umbraco/management/api/v1/recycle-bin/media`

**Empties the media recycle bin.**

Operation ID: `DeleteRecycleBinMedia`


---

### `DELETE /umbraco/management/api/v1/recycle-bin/media/{id}`

**Deletes a media item from the recycle bin.**

Operation ID: `DeleteRecycleBinMediaById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `GET /umbraco/management/api/v1/recycle-bin/media/{id}/original-parent`

**Gets the original parent of a media item in the recycle bin.**

Operation ID: `GetRecycleBinMediaByIdOriginalParent`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → ReferenceByIdModel`

---

### `PUT /umbraco/management/api/v1/recycle-bin/media/{id}/restore`

**Restores a media item from the recycle bin.**

Operation ID: `PutRecycleBinMediaByIdRestore`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → MoveMediaRequestModel`


---

### `GET /umbraco/management/api/v1/recycle-bin/media/children`

**Gets a collection of media items in the recycle bin.**

Operation ID: `GetRecycleBinMediaChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentId` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedMediaRecycleBinItemResponseModel`

---

### `GET /umbraco/management/api/v1/recycle-bin/media/referenced-by`

**Gets items referencing media in the recycle bin.**

Operation ID: `GetRecycleBinMediaReferencedBy`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedIReferenceResponseModel`

---

### `GET /umbraco/management/api/v1/recycle-bin/media/root`

**Gets media at the root of the recycle bin.**

Operation ID: `GetRecycleBinMediaRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedMediaRecycleBinItemResponseModel`

---

### `GET /umbraco/management/api/v1/recycle-bin/media/siblings`

**Gets sibling media in the recycle bin.**

Operation ID: `GetRecycleBinMediaSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `target` | query | string (uuid) | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |
| `dataTypeId` | query | string (uuid) | No |

**Response 200:** `OneOf: → SubsetMediaRecycleBinItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/media/ancestors`

**Gets a collection of ancestor media items.**

Operation ID: `GetTreeMediaAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantId` | query | string (uuid) | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/media/children`

**Gets a collection of media tree child items.**

Operation ID: `GetTreeMediaChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentId` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `dataTypeId` | query | string (uuid) | No |

**Response 200:** `OneOf: → PagedMediaTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/media/root`

**Gets a collection of media items from the root of the tree.**

Operation ID: `GetTreeMediaRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `dataTypeId` | query | string (uuid) | No |

**Response 200:** `OneOf: → PagedMediaTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/media/siblings`

**Gets a collection of media tree sibling items.**

Operation ID: `GetTreeMediaSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `target` | query | string (uuid) | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |
| `dataTypeId` | query | string (uuid) | No |

**Response 200:** `OneOf: → SubsetMediaTreeItemResponseModel`

---
