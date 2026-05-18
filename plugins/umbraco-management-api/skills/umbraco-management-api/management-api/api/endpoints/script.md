# Script — API Endpoints

See `schemas/script.md` for field definitions.

## Contents

### Script

- `GET /umbraco/management/api/v1/item/script`
- `POST /umbraco/management/api/v1/script`
- `GET /umbraco/management/api/v1/script/{path}`
- `DELETE /umbraco/management/api/v1/script/{path}`
- `PUT /umbraco/management/api/v1/script/{path}`
- `PUT /umbraco/management/api/v1/script/{path}/rename`
- `POST /umbraco/management/api/v1/script/folder`
- `GET /umbraco/management/api/v1/script/folder/{path}`
- `DELETE /umbraco/management/api/v1/script/folder/{path}`
- `GET /umbraco/management/api/v1/tree/script/ancestors`
- `GET /umbraco/management/api/v1/tree/script/children`
- `GET /umbraco/management/api/v1/tree/script/root`
- `GET /umbraco/management/api/v1/tree/script/siblings`

---

## Script

### `GET /umbraco/management/api/v1/item/script`

**Gets a collection of script items.**

Operation ID: `GetItemScript`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | query | List<string> | No |

**Response 200:** `List<object>`

---

### `POST /umbraco/management/api/v1/script`

**Creates a new script.**

Operation ID: `PostScript`

**Request body:** `OneOf: → CreateScriptRequestModel`


---

### `GET /umbraco/management/api/v1/script/{path}`

**Gets a script by path.**

Operation ID: `GetScriptByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Response 200:** `OneOf: → ScriptResponseModel`

---

### `DELETE /umbraco/management/api/v1/script/{path}`

**Deletes a script.**

Operation ID: `DeleteScriptByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |


---

### `PUT /umbraco/management/api/v1/script/{path}`

**Updates a script.**

Operation ID: `PutScriptByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Request body:** `OneOf: → UpdateScriptRequestModel`


---

### `PUT /umbraco/management/api/v1/script/{path}/rename`

**Renames a script.**

Operation ID: `PutScriptByPathRename`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Request body:** `OneOf: → RenameScriptRequestModel`


---

### `POST /umbraco/management/api/v1/script/folder`

**Creates a script folder.**

Operation ID: `PostScriptFolder`

**Request body:** `OneOf: → CreateScriptFolderRequestModel`


---

### `GET /umbraco/management/api/v1/script/folder/{path}`

**Gets a script folder by path.**

Operation ID: `GetScriptFolderByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |

**Response 200:** `OneOf: → ScriptFolderResponseModel`

---

### `DELETE /umbraco/management/api/v1/script/folder/{path}`

**Deletes a script folder.**

Operation ID: `DeleteScriptFolderByPath`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | path | string | Yes |


---

### `GET /umbraco/management/api/v1/tree/script/ancestors`

**Gets a collection of ancestor script items.**

Operation ID: `GetTreeScriptAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantPath` | query | string | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/script/children`

**Gets a collection of script tree child items.**

Operation ID: `GetTreeScriptChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentPath` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedFileSystemTreeItemPresentationModel`

---

### `GET /umbraco/management/api/v1/tree/script/root`

**Gets a collection of script items from the root of the tree.**

Operation ID: `GetTreeScriptRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedFileSystemTreeItemPresentationModel`

---

### `GET /umbraco/management/api/v1/tree/script/siblings`

**Gets a collection of script tree sibling items.**

Operation ID: `GetTreeScriptSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | query | string | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |

**Response 200:** `OneOf: → SubsetFileSystemTreeItemPresentationModel`

---
