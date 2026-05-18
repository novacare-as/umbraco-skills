# Data Type — API Endpoints

See `schemas/data-type.md` for field definitions.

## Contents

### Data Type

- `POST /umbraco/management/api/v1/data-type`
- `GET /umbraco/management/api/v1/data-type/{id}`
- `DELETE /umbraco/management/api/v1/data-type/{id}`
- `PUT /umbraco/management/api/v1/data-type/{id}`
- `POST /umbraco/management/api/v1/data-type/{id}/copy`
- `GET /umbraco/management/api/v1/data-type/{id}/is-used`
- `PUT /umbraco/management/api/v1/data-type/{id}/move`
- `GET /umbraco/management/api/v1/data-type/{id}/referenced-by`
- `GET /umbraco/management/api/v1/data-type/batch`
- `GET /umbraco/management/api/v1/data-type/configuration`
- `POST /umbraco/management/api/v1/data-type/folder`
- `GET /umbraco/management/api/v1/data-type/folder/{id}`
- `DELETE /umbraco/management/api/v1/data-type/folder/{id}`
- `PUT /umbraco/management/api/v1/data-type/folder/{id}`
- `GET /umbraco/management/api/v1/filter/data-type`
- `GET /umbraco/management/api/v1/item/data-type`
- `GET /umbraco/management/api/v1/item/data-type/ancestors`
- `GET /umbraco/management/api/v1/item/data-type/search`
- `GET /umbraco/management/api/v1/tree/data-type/ancestors`
- `GET /umbraco/management/api/v1/tree/data-type/children`
- `GET /umbraco/management/api/v1/tree/data-type/root`
- `GET /umbraco/management/api/v1/tree/data-type/search`
- `GET /umbraco/management/api/v1/tree/data-type/siblings`

---

## Data Type

### `POST /umbraco/management/api/v1/data-type`

**Creates a new data type.**

Operation ID: `PostDataType`

**Request body:** `OneOf: → CreateDataTypeRequestModel`


---

### `GET /umbraco/management/api/v1/data-type/{id}`

**Gets a data type.**

Operation ID: `GetDataTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → DataTypeResponseModel`

---

### `DELETE /umbraco/management/api/v1/data-type/{id}`

**Deletes a data type.**

Operation ID: `DeleteDataTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/data-type/{id}`

**Updates a data type.**

Operation ID: `PutDataTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateDataTypeRequestModel`


---

### `POST /umbraco/management/api/v1/data-type/{id}/copy`

**Copies a data type.**

Operation ID: `PostDataTypeByIdCopy`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → CopyDataTypeRequestModel`


---

### `GET /umbraco/management/api/v1/data-type/{id}/is-used`

**Checks if a data type is used.**

Operation ID: `GetDataTypeByIdIsUsed`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `boolean`

---

### `PUT /umbraco/management/api/v1/data-type/{id}/move`

**Moves a data type.**

Operation ID: `PutDataTypeByIdMove`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → MoveDataTypeRequestModel`


---

### `GET /umbraco/management/api/v1/data-type/{id}/referenced-by`

**Gets a paged collection of entities that are referenced by a data type.**

Operation ID: `GetDataTypeByIdReferencedBy`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedIReferenceResponseModel`

---

### `GET /umbraco/management/api/v1/data-type/batch`

**Gets multiple data types.**

Operation ID: `GetDataTypeBatch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `OneOf: → BatchResponseModelDataTypeResponseModel`

---

### `GET /umbraco/management/api/v1/data-type/configuration`

**Gets the data type configuration.**

Operation ID: `GetDataTypeConfiguration`

**Response 200:** `OneOf: → DatatypeConfigurationResponseModel`

---

### `POST /umbraco/management/api/v1/data-type/folder`

**Creates a data type folder.**

Operation ID: `PostDataTypeFolder`

**Request body:** `OneOf: → CreateFolderRequestModel`


---

### `GET /umbraco/management/api/v1/data-type/folder/{id}`

**Gets a data type folder.**

Operation ID: `GetDataTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → FolderResponseModel`

---

### `DELETE /umbraco/management/api/v1/data-type/folder/{id}`

**Deletes a data type folder.**

Operation ID: `DeleteDataTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/data-type/folder/{id}`

**Updates a data type folder.**

Operation ID: `PutDataTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateFolderResponseModel`


---

### `GET /umbraco/management/api/v1/filter/data-type`

**Gets a filtered collection of data types.**

Operation ID: `GetFilterDataType`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `name` | query | string | No |
| `editorUiAlias` | query | string | No |
| `editorAlias` | query | string | No |

**Response 200:** `OneOf: → PagedDataTypeItemResponseModel`

---

### `GET /umbraco/management/api/v1/item/data-type`

**Gets a collection of data type items.**

Operation ID: `GetItemDataType`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/data-type/ancestors`

**Gets ancestors for a collection of data type items.**

Operation ID: `GetItemDataTypeAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/data-type/search`

**Searches data type items.**

Operation ID: `GetItemDataTypeSearch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `query` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedModelDataTypeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/data-type/ancestors`

**Gets a collection of ancestor data type folders.**

Operation ID: `GetTreeDataTypeAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantId` | query | string (uuid) | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/data-type/children`

**Gets a collection of data type tree child items.**

Operation ID: `GetTreeDataTypeChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentId` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → PagedDataTypeTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/data-type/root`

**Gets a collection of data type items from the root of the tree.**

Operation ID: `GetTreeDataTypeRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → PagedDataTypeTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/data-type/search`

Operation ID: `GetTreeDataTypeSearch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `query` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `itemKind` | query | → TreeItemKindModel | No |

**Response 200:** `OneOf: → PagedDataTypeTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/data-type/siblings`

**Gets a collection of data type tree sibling items.**

Operation ID: `GetTreeDataTypeSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `target` | query | string (uuid) | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → SubsetDataTypeTreeItemResponseModel`

---
