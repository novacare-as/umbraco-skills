# Document Blueprint — API Endpoints

See `schemas/document-blueprint.md` for field definitions.

## Contents

### Document Blueprint

- `POST /umbraco/management/api/v1/document-blueprint`
- `GET /umbraco/management/api/v1/document-blueprint/{id}`
- `DELETE /umbraco/management/api/v1/document-blueprint/{id}`
- `PUT /umbraco/management/api/v1/document-blueprint/{id}`
- `PUT /umbraco/management/api/v1/document-blueprint/{id}/move`
- `GET /umbraco/management/api/v1/document-blueprint/{id}/scaffold`
- `POST /umbraco/management/api/v1/document-blueprint/folder`
- `GET /umbraco/management/api/v1/document-blueprint/folder/{id}`
- `DELETE /umbraco/management/api/v1/document-blueprint/folder/{id}`
- `PUT /umbraco/management/api/v1/document-blueprint/folder/{id}`
- `POST /umbraco/management/api/v1/document-blueprint/from-document`
- `GET /umbraco/management/api/v1/item/document-blueprint`
- `GET /umbraco/management/api/v1/tree/document-blueprint/ancestors`
- `GET /umbraco/management/api/v1/tree/document-blueprint/children`
- `GET /umbraco/management/api/v1/tree/document-blueprint/root`
- `GET /umbraco/management/api/v1/tree/document-blueprint/siblings`

---

## Document Blueprint

### `POST /umbraco/management/api/v1/document-blueprint`

**Creates a new document blueprint.**

Operation ID: `PostDocumentBlueprint`

**Request body:** `OneOf: → CreateDocumentBlueprintRequestModel`


---

### `GET /umbraco/management/api/v1/document-blueprint/{id}`

**Gets a document blueprint.**

Operation ID: `GetDocumentBlueprintById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → DocumentBlueprintResponseModel`

---

### `DELETE /umbraco/management/api/v1/document-blueprint/{id}`

**Deletes a document blueprint.**

Operation ID: `DeleteDocumentBlueprintById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/document-blueprint/{id}`

**Updates a document blueprint.**

Operation ID: `PutDocumentBlueprintById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateDocumentBlueprintRequestModel`


---

### `PUT /umbraco/management/api/v1/document-blueprint/{id}/move`

**Moves a document blueprint.**

Operation ID: `PutDocumentBlueprintByIdMove`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → MoveDocumentBlueprintRequestModel`


---

### `GET /umbraco/management/api/v1/document-blueprint/{id}/scaffold`

**Scaffolds a document blueprint.**

Operation ID: `GetDocumentBlueprintByIdScaffold`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → DocumentBlueprintResponseModel`

---

### `POST /umbraco/management/api/v1/document-blueprint/folder`

**Creates a document blueprint folder.**

Operation ID: `PostDocumentBlueprintFolder`

**Request body:** `OneOf: → CreateFolderRequestModel`


---

### `GET /umbraco/management/api/v1/document-blueprint/folder/{id}`

**Gets a document blueprint folder.**

Operation ID: `GetDocumentBlueprintFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → FolderResponseModel`

---

### `DELETE /umbraco/management/api/v1/document-blueprint/folder/{id}`

**Deletes a document blueprint folder.**

Operation ID: `DeleteDocumentBlueprintFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/document-blueprint/folder/{id}`

**Updates a document blueprint folder.**

Operation ID: `PutDocumentBlueprintFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateFolderResponseModel`


---

### `POST /umbraco/management/api/v1/document-blueprint/from-document`

**Creates a document blueprint from an existing document.**

Operation ID: `PostDocumentBlueprintFromDocument`

**Request body:** `OneOf: → CreateDocumentBlueprintFromDocumentRequestModel`


---

### `GET /umbraco/management/api/v1/item/document-blueprint`

**Gets a collection of document blueprint items.**

Operation ID: `GetItemDocumentBlueprint`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/document-blueprint/ancestors`

**Gets a collection of ancestor document blueprint items.**

Operation ID: `GetTreeDocumentBlueprintAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantId` | query | string (uuid) | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/document-blueprint/children`

**Gets a collection of document blueprint tree child items.**

Operation ID: `GetTreeDocumentBlueprintChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentId` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → PagedDocumentBlueprintTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/document-blueprint/root`

**Gets a collection of document blueprint items from the root of the tree.**

Operation ID: `GetTreeDocumentBlueprintRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → PagedDocumentBlueprintTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/document-blueprint/siblings`

**Gets a collection of document blueprint tree sibling items.**

Operation ID: `GetTreeDocumentBlueprintSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `target` | query | string (uuid) | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → SubsetDocumentBlueprintTreeItemResponseModel`

---
