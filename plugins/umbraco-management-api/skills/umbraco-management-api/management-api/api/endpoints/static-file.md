# Static File — API Endpoints

See `schemas/common.md` for field definitions.

## Contents

### Static File

- `GET /umbraco/management/api/v1/item/static-file`
- `GET /umbraco/management/api/v1/tree/static-file/ancestors`
- `GET /umbraco/management/api/v1/tree/static-file/children`
- `GET /umbraco/management/api/v1/tree/static-file/root`

---

## Static File

### `GET /umbraco/management/api/v1/item/static-file`

**Gets a collection of static file items.**

Operation ID: `GetItemStaticFile`

| Param | In | Type | Required |
|-------|----|------|----------|
| `path` | query | List<string> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/static-file/ancestors`

**Gets a collection of ancestor static file items.**

Operation ID: `GetTreeStaticFileAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantPath` | query | string | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/static-file/children`

**Gets a collection of static file tree child items.**

Operation ID: `GetTreeStaticFileChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentPath` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedFileSystemTreeItemPresentationModel`

---

### `GET /umbraco/management/api/v1/tree/static-file/root`

**Gets a collection of static file items from the root of the tree.**

Operation ID: `GetTreeStaticFileRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedFileSystemTreeItemPresentationModel`

---
