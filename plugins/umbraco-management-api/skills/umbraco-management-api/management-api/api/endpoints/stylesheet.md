# Stylesheet — API Endpoints

See `schemas/stylesheet.md` for field definitions.

## Contents

### Stylesheet

- `GET /umbraco/management/api/v1/item/stylesheet`
- `POST /umbraco/management/api/v1/stylesheet`
- `GET /umbraco/management/api/v1/stylesheet/{path}`
- `DELETE /umbraco/management/api/v1/stylesheet/{path}`
- `PUT /umbraco/management/api/v1/stylesheet/{path}`
- `PUT /umbraco/management/api/v1/stylesheet/{path}/rename`
- `POST /umbraco/management/api/v1/stylesheet/folder`
- `GET /umbraco/management/api/v1/stylesheet/folder/{path}`
- `DELETE /umbraco/management/api/v1/stylesheet/folder/{path}`
- `GET /umbraco/management/api/v1/tree/stylesheet/ancestors`
- `GET /umbraco/management/api/v1/tree/stylesheet/children`
- `GET /umbraco/management/api/v1/tree/stylesheet/root`
- `GET /umbraco/management/api/v1/tree/stylesheet/siblings`

---

## Stylesheet

### `GET /umbraco/management/api/v1/item/stylesheet`

**Gets a collection of stylesheet items.**

Operation ID: `GetItemStylesheet`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | query | List<string> | No |

**Response 200:** `List<object>`

---

### `POST /umbraco/management/api/v1/stylesheet`

**Creates a new stylesheet.**

Operation ID: `PostStylesheet`

**Request body:** `OneOf: → CreateStylesheetRequestModel`


---

### `GET /umbraco/management/api/v1/stylesheet/{path}`

**Gets a stylesheet by path.**

Operation ID: `GetStylesheetByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Response 200:** `OneOf: → StylesheetResponseModel`

---

### `DELETE /umbraco/management/api/v1/stylesheet/{path}`

**Deletes a stylesheet.**

Operation ID: `DeleteStylesheetByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |


---

### `PUT /umbraco/management/api/v1/stylesheet/{path}`

**Updates a stylesheet.**

Operation ID: `PutStylesheetByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Request body:** `OneOf: → UpdateStylesheetRequestModel`


---

### `PUT /umbraco/management/api/v1/stylesheet/{path}/rename`

**Renames a stylesheet.**

Operation ID: `PutStylesheetByPathRename`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Request body:** `OneOf: → RenameStylesheetRequestModel`


---

### `POST /umbraco/management/api/v1/stylesheet/folder`

**Creates a stylesheet folder.**

Operation ID: `PostStylesheetFolder`

**Request body:** `OneOf: → CreateStylesheetFolderRequestModel`


---

### `GET /umbraco/management/api/v1/stylesheet/folder/{path}`

**Gets a stylesheet folder by path.**

Operation ID: `GetStylesheetFolderByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Response 200:** `OneOf: → StylesheetFolderResponseModel`

---

### `DELETE /umbraco/management/api/v1/stylesheet/folder/{path}`

**Deletes a stylesheet folder.**

Operation ID: `DeleteStylesheetFolderByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |


---

### `GET /umbraco/management/api/v1/tree/stylesheet/ancestors`

**Gets a collection of ancestor stylesheet items.**

Operation ID: `GetTreeStylesheetAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantPath` | query | string | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/stylesheet/children`

**Gets a collection of stylesheet tree child items.**

Operation ID: `GetTreeStylesheetChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentPath` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedFileSystemTreeItemPresentationModel`

---

### `GET /umbraco/management/api/v1/tree/stylesheet/root`

**Gets a collection of stylesheet items from the root of the tree.**

Operation ID: `GetTreeStylesheetRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedFileSystemTreeItemPresentationModel`

---

### `GET /umbraco/management/api/v1/tree/stylesheet/siblings`

**Gets a collection of stylesheet tree sibling items.**

Operation ID: `GetTreeStylesheetSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | query | string | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |

**Response 200:** `OneOf: → SubsetFileSystemTreeItemPresentationModel`

---
