# Media Type — API Endpoints

See `schemas/media-type.md` for field definitions.

## Contents

### Media Type

- `GET /umbraco/management/api/v1/item/media-type`
- `GET /umbraco/management/api/v1/item/media-type/allowed`
- `GET /umbraco/management/api/v1/item/media-type/ancestors`
- `GET /umbraco/management/api/v1/item/media-type/folders`
- `GET /umbraco/management/api/v1/item/media-type/search`
- `POST /umbraco/management/api/v1/media-type`
- `GET /umbraco/management/api/v1/media-type/{id}`
- `DELETE /umbraco/management/api/v1/media-type/{id}`
- `PUT /umbraco/management/api/v1/media-type/{id}`
- `GET /umbraco/management/api/v1/media-type/{id}/allowed-children`
- `GET /umbraco/management/api/v1/media-type/{id}/allowed-parents`
- `GET /umbraco/management/api/v1/media-type/{id}/composition-references`
- `POST /umbraco/management/api/v1/media-type/{id}/copy`
- `GET /umbraco/management/api/v1/media-type/{id}/export`
- `PUT /umbraco/management/api/v1/media-type/{id}/import`
- `PUT /umbraco/management/api/v1/media-type/{id}/move`
- `GET /umbraco/management/api/v1/media-type/allowed-at-root`
- `POST /umbraco/management/api/v1/media-type/available-compositions`
- `GET /umbraco/management/api/v1/media-type/batch`
- `GET /umbraco/management/api/v1/media-type/configuration`
- `POST /umbraco/management/api/v1/media-type/folder`
- `GET /umbraco/management/api/v1/media-type/folder/{id}`
- `DELETE /umbraco/management/api/v1/media-type/folder/{id}`
- `PUT /umbraco/management/api/v1/media-type/folder/{id}`
- `POST /umbraco/management/api/v1/media-type/import`
- `GET /umbraco/management/api/v1/tree/media-type/ancestors`
- `GET /umbraco/management/api/v1/tree/media-type/children`
- `GET /umbraco/management/api/v1/tree/media-type/root`
- `GET /umbraco/management/api/v1/tree/media-type/siblings`

---

## Media Type

### `GET /umbraco/management/api/v1/item/media-type`

**Gets a collection of media type items.**

Operation ID: `GetItemMediaType`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/media-type/allowed`

**Gets a collection of media type items.**

Operation ID: `GetItemMediaTypeAllowed`

| Param | In | Type | Required |
|-------|----|------|----------|
| `fileExtension` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedModelAllowedMediaTypeItemResponseModel`

---

### `GET /umbraco/management/api/v1/item/media-type/ancestors`

**Gets ancestors for a collection of media type items.**

Operation ID: `GetItemMediaTypeAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/media-type/folders`

**Gets a collection of media type folder items.**

Operation ID: `GetItemMediaTypeFolders`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedModelMediaTypeItemResponseModel`

---

### `GET /umbraco/management/api/v1/item/media-type/search`

**Searches media type items.**

Operation ID: `GetItemMediaTypeSearch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `query` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedModelMediaTypeItemResponseModel`

---

### `POST /umbraco/management/api/v1/media-type`

**Creates a new media type.**

Operation ID: `PostMediaType`

**Request body:** `OneOf: → CreateMediaTypeRequestModel`


---

### `GET /umbraco/management/api/v1/media-type/{id}`

**Gets a media type.**

Operation ID: `GetMediaTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → MediaTypeResponseModel`

---

### `DELETE /umbraco/management/api/v1/media-type/{id}`

**Deletes a media type.**

Operation ID: `DeleteMediaTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/media-type/{id}`

**Updates a media type.**

Operation ID: `PutMediaTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateMediaTypeRequestModel`


---

### `GET /umbraco/management/api/v1/media-type/{id}/allowed-children`

**Gets allowed child media types.**

Operation ID: `GetMediaTypeByIdAllowedChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `parentContentKey` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedAllowedMediaTypeModel`

---

### `GET /umbraco/management/api/v1/media-type/{id}/allowed-parents`

**Gets allowed parent media types.**

Operation ID: `GetMediaTypeByIdAllowedParents`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → MediaTypeAllowedParentsResponseModel`

---

### `GET /umbraco/management/api/v1/media-type/{id}/composition-references`

**Gets composition references.**

Operation ID: `GetMediaTypeByIdCompositionReferences`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `List<object>`

---

### `POST /umbraco/management/api/v1/media-type/{id}/copy`

**Copies a media type.**

Operation ID: `PostMediaTypeByIdCopy`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → CopyMediaTypeRequestModel`


---

### `GET /umbraco/management/api/v1/media-type/{id}/export`

**Exports a media type.**

Operation ID: `GetMediaTypeByIdExport`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: string (binary)`

---

### `PUT /umbraco/management/api/v1/media-type/{id}/import`

**Imports a media type.**

Operation ID: `PutMediaTypeByIdImport`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → ImportMediaTypeRequestModel`


---

### `PUT /umbraco/management/api/v1/media-type/{id}/move`

**Moves a media type.**

Operation ID: `PutMediaTypeByIdMove`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → MoveMediaTypeRequestModel`


---

### `GET /umbraco/management/api/v1/media-type/allowed-at-root`

**Gets media types allowed at root.**

Operation ID: `GetMediaTypeAllowedAtRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedAllowedMediaTypeModel`

---

### `POST /umbraco/management/api/v1/media-type/available-compositions`

**Gets available compositions.**

Operation ID: `PostMediaTypeAvailableCompositions`

**Request body:** `OneOf: → MediaTypeCompositionRequestModel`

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/media-type/batch`

**Gets multiple media types.**

Operation ID: `GetMediaTypeBatch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `OneOf: → BatchResponseModelMediaTypeResponseModel`

---

### `GET /umbraco/management/api/v1/media-type/configuration`

**Gets the media type configuration.**

Operation ID: `GetMediaTypeConfiguration`

**Response 200:** `OneOf: → MediaTypeConfigurationResponseModel`

---

### `POST /umbraco/management/api/v1/media-type/folder`

**Creates a media type folder.**

Operation ID: `PostMediaTypeFolder`

**Request body:** `OneOf: → CreateFolderRequestModel`


---

### `GET /umbraco/management/api/v1/media-type/folder/{id}`

**Gets a media type folder.**

Operation ID: `GetMediaTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → FolderResponseModel`

---

### `DELETE /umbraco/management/api/v1/media-type/folder/{id}`

**Deletes a media type folder.**

Operation ID: `DeleteMediaTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/media-type/folder/{id}`

**Updates a media type folder.**

Operation ID: `PutMediaTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateFolderResponseModel`


---

### `POST /umbraco/management/api/v1/media-type/import`

**Imports a media type.**

Operation ID: `PostMediaTypeImport`

**Request body:** `OneOf: → ImportMediaTypeRequestModel`


---

### `GET /umbraco/management/api/v1/tree/media-type/ancestors`

**Gets a collection of ancestor media type items.**

Operation ID: `GetTreeMediaTypeAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantId` | query | string (uuid) | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/media-type/children`

**Gets a collection of media type tree child items.**

Operation ID: `GetTreeMediaTypeChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentId` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → PagedMediaTypeTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/media-type/root`

**Gets a collection of media type items from the root of the tree.**

Operation ID: `GetTreeMediaTypeRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → PagedMediaTypeTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/media-type/siblings`

**Gets a collection of media type tree sibling items.**

Operation ID: `GetTreeMediaTypeSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `target` | query | string (uuid) | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → SubsetMediaTypeTreeItemResponseModel`

---
