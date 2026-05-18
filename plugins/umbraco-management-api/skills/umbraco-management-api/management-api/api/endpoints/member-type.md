# Member Type — API Endpoints

See `schemas/member-type.md` for field definitions.

## Contents

### Member Type

- `GET /umbraco/management/api/v1/item/member-type`
- `GET /umbraco/management/api/v1/item/member-type/ancestors`
- `GET /umbraco/management/api/v1/item/member-type/search`
- `POST /umbraco/management/api/v1/member-type`
- `GET /umbraco/management/api/v1/member-type/{id}`
- `DELETE /umbraco/management/api/v1/member-type/{id}`
- `PUT /umbraco/management/api/v1/member-type/{id}`
- `GET /umbraco/management/api/v1/member-type/{id}/composition-references`
- `POST /umbraco/management/api/v1/member-type/{id}/copy`
- `GET /umbraco/management/api/v1/member-type/{id}/export`
- `PUT /umbraco/management/api/v1/member-type/{id}/import`
- `PUT /umbraco/management/api/v1/member-type/{id}/move`
- `POST /umbraco/management/api/v1/member-type/available-compositions`
- `GET /umbraco/management/api/v1/member-type/batch`
- `GET /umbraco/management/api/v1/member-type/configuration`
- `POST /umbraco/management/api/v1/member-type/folder`
- `GET /umbraco/management/api/v1/member-type/folder/{id}`
- `DELETE /umbraco/management/api/v1/member-type/folder/{id}`
- `PUT /umbraco/management/api/v1/member-type/folder/{id}`
- `POST /umbraco/management/api/v1/member-type/import`
- `GET /umbraco/management/api/v1/tree/member-type/ancestors`
- `GET /umbraco/management/api/v1/tree/member-type/children`
- `GET /umbraco/management/api/v1/tree/member-type/root`
- `GET /umbraco/management/api/v1/tree/member-type/siblings`

---

## Member Type

### `GET /umbraco/management/api/v1/item/member-type`

**Gets a collection of member type items.**

Operation ID: `GetItemMemberType`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/member-type/ancestors`

**Gets ancestors for a collection of member type items.**

Operation ID: `GetItemMemberTypeAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/member-type/search`

**Searches member type items.**

Operation ID: `GetItemMemberTypeSearch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `query` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedModelMemberTypeItemResponseModel`

---

### `POST /umbraco/management/api/v1/member-type`

**Creates a new member type.**

Operation ID: `PostMemberType`

**Request body:** `OneOf: → CreateMemberTypeRequestModel`


---

### `GET /umbraco/management/api/v1/member-type/{id}`

**Gets a member type.**

Operation ID: `GetMemberTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → MemberTypeResponseModel`

---

### `DELETE /umbraco/management/api/v1/member-type/{id}`

**Deletes a member type.**

Operation ID: `DeleteMemberTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/member-type/{id}`

**Updates a member type.**

Operation ID: `PutMemberTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateMemberTypeRequestModel`


---

### `GET /umbraco/management/api/v1/member-type/{id}/composition-references`

**Gets composition references.**

Operation ID: `GetMemberTypeByIdCompositionReferences`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `List<object>`

---

### `POST /umbraco/management/api/v1/member-type/{id}/copy`

**Copies a member type.**

Operation ID: `PostMemberTypeByIdCopy`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → CopyMemberTypeRequestModel`


---

### `GET /umbraco/management/api/v1/member-type/{id}/export`

**Exports a member type.**

Operation ID: `GetMemberTypeByIdExport`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: string (binary)`

---

### `PUT /umbraco/management/api/v1/member-type/{id}/import`

**Imports a member type.**

Operation ID: `PutMemberTypeByIdImport`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → ImportMemberTypeRequestModel`


---

### `PUT /umbraco/management/api/v1/member-type/{id}/move`

**Moves a member type.**

Operation ID: `PutMemberTypeByIdMove`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → MoveMemberTypeRequestModel`


---

### `POST /umbraco/management/api/v1/member-type/available-compositions`

**Gets available compositions.**

Operation ID: `PostMemberTypeAvailableCompositions`

**Request body:** `OneOf: → MemberTypeCompositionRequestModel`

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/member-type/batch`

**Gets multiple member types.**

Operation ID: `GetMemberTypeBatch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `OneOf: → BatchResponseModelMemberTypeResponseModel`

---

### `GET /umbraco/management/api/v1/member-type/configuration`

**Gets the member type configuration.**

Operation ID: `GetMemberTypeConfiguration`

**Response 200:** `OneOf: → MemberTypeConfigurationResponseModel`

---

### `POST /umbraco/management/api/v1/member-type/folder`

**Creates a member type folder.**

Operation ID: `PostMemberTypeFolder`

**Request body:** `OneOf: → CreateFolderRequestModel`


---

### `GET /umbraco/management/api/v1/member-type/folder/{id}`

**Gets a member type folder.**

Operation ID: `GetMemberTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → FolderResponseModel`

---

### `DELETE /umbraco/management/api/v1/member-type/folder/{id}`

**Deletes a member type folder.**

Operation ID: `DeleteMemberTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/member-type/folder/{id}`

**Updates a member type folder.**

Operation ID: `PutMemberTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateFolderResponseModel`


---

### `POST /umbraco/management/api/v1/member-type/import`

**Imports a member type.**

Operation ID: `PostMemberTypeImport`

**Request body:** `OneOf: → ImportMemberTypeRequestModel`


---

### `GET /umbraco/management/api/v1/tree/member-type/ancestors`

**Gets a collection of ancestor member type items.**

Operation ID: `GetTreeMemberTypeAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantId` | query | string (uuid) | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/member-type/children`

**Gets a collection of member type tree child items.**

Operation ID: `GetTreeMemberTypeChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentId` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → PagedMemberTypeTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/member-type/root`

**Gets a collection of member type items from the root of the tree.**

Operation ID: `GetTreeMemberTypeRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → PagedMemberTypeTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/member-type/siblings`

**Gets sibling member types in the tree.**

Operation ID: `GetTreeMemberTypeSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `target` | query | string (uuid) | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → SubsetMemberTypeTreeItemResponseModel`

---
