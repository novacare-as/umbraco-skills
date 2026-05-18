# Partial View — API Endpoints

See `schemas/partial-view.md` for field definitions.

## Contents

### Partial View

- `GET /umbraco/management/api/v1/item/partial-view`
- `POST /umbraco/management/api/v1/partial-view`
- `GET /umbraco/management/api/v1/partial-view/{path}`
- `DELETE /umbraco/management/api/v1/partial-view/{path}`
- `PUT /umbraco/management/api/v1/partial-view/{path}`
- `PUT /umbraco/management/api/v1/partial-view/{path}/rename`
- `POST /umbraco/management/api/v1/partial-view/folder`
- `GET /umbraco/management/api/v1/partial-view/folder/{path}`
- `DELETE /umbraco/management/api/v1/partial-view/folder/{path}`
- `GET /umbraco/management/api/v1/partial-view/snippet`
- `GET /umbraco/management/api/v1/partial-view/snippet/{id}`
- `GET /umbraco/management/api/v1/tree/partial-view/ancestors`
- `GET /umbraco/management/api/v1/tree/partial-view/children`
- `GET /umbraco/management/api/v1/tree/partial-view/root`
- `GET /umbraco/management/api/v1/tree/partial-view/siblings`

---

## Partial View

### `GET /umbraco/management/api/v1/item/partial-view`

**Gets a collection of partial view items.**

Operation ID: `GetItemPartialView`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | query | List<string> | No |

**Response 200:** `List<object>`

---

### `POST /umbraco/management/api/v1/partial-view`

**Creates a new partial view.**

Operation ID: `PostPartialView`

**Request body:** `OneOf: → CreatePartialViewRequestModel`


---

### `GET /umbraco/management/api/v1/partial-view/{path}`

**Gets a partial view by path.**

Operation ID: `GetPartialViewByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Response 200:** `OneOf: → PartialViewResponseModel`

---

### `DELETE /umbraco/management/api/v1/partial-view/{path}`

**Deletes a partial view.**

Operation ID: `DeletePartialViewByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |


---

### `PUT /umbraco/management/api/v1/partial-view/{path}`

**Updates a partial view.**

Operation ID: `PutPartialViewByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Request body:** `OneOf: → UpdatePartialViewRequestModel`


---

### `PUT /umbraco/management/api/v1/partial-view/{path}/rename`

**Renames a partial view.**

Operation ID: `PutPartialViewByPathRename`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Request body:** `OneOf: → RenamePartialViewRequestModel`


---

### `POST /umbraco/management/api/v1/partial-view/folder`

**Creates a partial view folder.**

Operation ID: `PostPartialViewFolder`

**Request body:** `OneOf: → CreatePartialViewFolderRequestModel`


---

### `GET /umbraco/management/api/v1/partial-view/folder/{path}`

**Gets a partial view folder by path.**

Operation ID: `GetPartialViewFolderByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Response 200:** `OneOf: → PartialViewFolderResponseModel`

---

### `DELETE /umbraco/management/api/v1/partial-view/folder/{path}`

**Deletes a partial view folder.**

Operation ID: `DeletePartialViewFolderByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |


---

### `GET /umbraco/management/api/v1/partial-view/snippet`

**Gets a paginated collection of partial view snippets.**

Operation ID: `GetPartialViewSnippet`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedPartialViewSnippetItemResponseModel`

---

### `GET /umbraco/management/api/v1/partial-view/snippet/{id}`

**Gets a partial view snippet.**

Operation ID: `GetPartialViewSnippetById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string | Yes |

**Response 200:** `OneOf: → PartialViewSnippetResponseModel`

---

### `GET /umbraco/management/api/v1/tree/partial-view/ancestors`

**Gets a collection of ancestor partial view items.**

Operation ID: `GetTreePartialViewAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantPath` | query | string | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/partial-view/children`

**Gets a collection of partial view tree child items.**

Operation ID: `GetTreePartialViewChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentPath` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedFileSystemTreeItemPresentationModel`

---

### `GET /umbraco/management/api/v1/tree/partial-view/root`

**Gets a collection of partial view items from the root of the tree.**

Operation ID: `GetTreePartialViewRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedFileSystemTreeItemPresentationModel`

---

### `GET /umbraco/management/api/v1/tree/partial-view/siblings`

**Gets a collection of partial view tree sibling items.**

Operation ID: `GetTreePartialViewSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | query | string | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |

**Response 200:** `OneOf: → SubsetFileSystemTreeItemPresentationModel`

---
