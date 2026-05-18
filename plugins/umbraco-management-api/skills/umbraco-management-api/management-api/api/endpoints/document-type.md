# Document Type — API Endpoints

See `schemas/document-type.md` for field definitions.

## Contents

### Document Type

- `POST /umbraco/management/api/v1/document-type`
- `GET /umbraco/management/api/v1/document-type/{id}`
- `DELETE /umbraco/management/api/v1/document-type/{id}`
- `PUT /umbraco/management/api/v1/document-type/{id}`
- `GET /umbraco/management/api/v1/document-type/{id}/allowed-children`
- `GET /umbraco/management/api/v1/document-type/{id}/allowed-parents`
- `GET /umbraco/management/api/v1/document-type/{id}/blueprint`
- `GET /umbraco/management/api/v1/document-type/{id}/composition-references`
- `POST /umbraco/management/api/v1/document-type/{id}/copy`
- `GET /umbraco/management/api/v1/document-type/{id}/export`
- `PUT /umbraco/management/api/v1/document-type/{id}/import`
- `PUT /umbraco/management/api/v1/document-type/{id}/move`
- `POST /umbraco/management/api/v1/document-type/{id}/template`
- `GET /umbraco/management/api/v1/document-type/allowed-at-root`
- `POST /umbraco/management/api/v1/document-type/available-compositions`
- `GET /umbraco/management/api/v1/document-type/batch`
- `GET /umbraco/management/api/v1/document-type/configuration`
- `POST /umbraco/management/api/v1/document-type/folder`
- `GET /umbraco/management/api/v1/document-type/folder/{id}`
- `DELETE /umbraco/management/api/v1/document-type/folder/{id}`
- `PUT /umbraco/management/api/v1/document-type/folder/{id}`
- `POST /umbraco/management/api/v1/document-type/import`
- `GET /umbraco/management/api/v1/item/document-type`
- `GET /umbraco/management/api/v1/item/document-type/ancestors`
- `GET /umbraco/management/api/v1/item/document-type/search`
- `GET /umbraco/management/api/v1/tree/document-type/ancestors`
- `GET /umbraco/management/api/v1/tree/document-type/children`
- `GET /umbraco/management/api/v1/tree/document-type/root`
- `GET /umbraco/management/api/v1/tree/document-type/search`
- `GET /umbraco/management/api/v1/tree/document-type/siblings`

---

## Document Type

### `POST /umbraco/management/api/v1/document-type`

**Creates a new document type.**

Operation ID: `PostDocumentType`

**Request body:** `OneOf: → CreateDocumentTypeRequestModel`


---

### `GET /umbraco/management/api/v1/document-type/{id}`

**Gets a document type.**

Operation ID: `GetDocumentTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → DocumentTypeResponseModel`

---

### `DELETE /umbraco/management/api/v1/document-type/{id}`

**Deletes a document type.**

Operation ID: `DeleteDocumentTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/document-type/{id}`

**Updates a document type.**

Operation ID: `PutDocumentTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateDocumentTypeRequestModel`


---

### `GET /umbraco/management/api/v1/document-type/{id}/allowed-children`

**Gets allowed child document types.**

Operation ID: `GetDocumentTypeByIdAllowedChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `parentContentKey` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedAllowedDocumentTypeModel`

---

### `GET /umbraco/management/api/v1/document-type/{id}/allowed-parents`

**Gets allowed parent document types.**

Operation ID: `GetDocumentTypeByIdAllowedParents`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → DocumentTypeAllowedParentsResponseModel`

---

### `GET /umbraco/management/api/v1/document-type/{id}/blueprint`

**Gets document blueprints for a document type.**

Operation ID: `GetDocumentTypeByIdBlueprint`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedDocumentTypeBlueprintItemResponseModel`

---

### `GET /umbraco/management/api/v1/document-type/{id}/composition-references`

**Gets composition references.**

Operation ID: `GetDocumentTypeByIdCompositionReferences`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `List<object>`

---

### `POST /umbraco/management/api/v1/document-type/{id}/copy`

**Copies a document type.**

Operation ID: `PostDocumentTypeByIdCopy`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → CopyDocumentTypeRequestModel`


---

### `GET /umbraco/management/api/v1/document-type/{id}/export`

**Exports a document type.**

Operation ID: `GetDocumentTypeByIdExport`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: string (binary)`

---

### `PUT /umbraco/management/api/v1/document-type/{id}/import`

**Imports a document type.**

Operation ID: `PutDocumentTypeByIdImport`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → ImportDocumentTypeRequestModel`


---

### `PUT /umbraco/management/api/v1/document-type/{id}/move`

**Moves a document type.**

Operation ID: `PutDocumentTypeByIdMove`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → MoveDocumentTypeRequestModel`


---

### `POST /umbraco/management/api/v1/document-type/{id}/template`

**Creates a template for a document type.**

Operation ID: `PostDocumentTypeByIdTemplate`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → CreateDocumentTypeTemplateRequestModel`


---

### `GET /umbraco/management/api/v1/document-type/allowed-at-root`

**Gets document types allowed at root.**

Operation ID: `GetDocumentTypeAllowedAtRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedAllowedDocumentTypeModel`

---

### `POST /umbraco/management/api/v1/document-type/available-compositions`

**Gets available compositions.**

Operation ID: `PostDocumentTypeAvailableCompositions`

**Request body:** `OneOf: → DocumentTypeCompositionRequestModel`

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/document-type/batch`

**Gets multiple document types.**

Operation ID: `GetDocumentTypeBatch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `OneOf: → BatchResponseModelDocumentTypeResponseModel`

---

### `GET /umbraco/management/api/v1/document-type/configuration`

**Gets the document type configuration.**

Operation ID: `GetDocumentTypeConfiguration`

**Response 200:** `OneOf: → DocumentTypeConfigurationResponseModel`

---

### `POST /umbraco/management/api/v1/document-type/folder`

**Creates a document type folder.**

Operation ID: `PostDocumentTypeFolder`

**Request body:** `OneOf: → CreateFolderRequestModel`


---

### `GET /umbraco/management/api/v1/document-type/folder/{id}`

**Gets a document type folder.**

Operation ID: `GetDocumentTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → FolderResponseModel`

---

### `DELETE /umbraco/management/api/v1/document-type/folder/{id}`

**Deletes a document type folder.**

Operation ID: `DeleteDocumentTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/document-type/folder/{id}`

**Updates a document type folder.**

Operation ID: `PutDocumentTypeFolderById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateFolderResponseModel`


---

### `POST /umbraco/management/api/v1/document-type/import`

**Imports a document type.**

Operation ID: `PostDocumentTypeImport`

**Request body:** `OneOf: → ImportDocumentTypeRequestModel`


---

### `GET /umbraco/management/api/v1/item/document-type`

**Gets a collection of document type items.**

Operation ID: `GetItemDocumentType`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/document-type/ancestors`

**Gets ancestors for a collection of document type items.**

Operation ID: `GetItemDocumentTypeAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/document-type/search`

**Searches document type items.**

Operation ID: `GetItemDocumentTypeSearch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `query` | query | string | No |
| `isElement` | query | boolean | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedModelDocumentTypeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/document-type/ancestors`

**Gets a collection of ancestor document type items.**

Operation ID: `GetTreeDocumentTypeAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantId` | query | string (uuid) | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/document-type/children`

**Gets a collection of document type tree child items.**

Operation ID: `GetTreeDocumentTypeChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentId` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → PagedDocumentTypeTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/document-type/root`

**Gets a collection of document type items from the root of the tree.**

Operation ID: `GetTreeDocumentTypeRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → PagedDocumentTypeTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/document-type/search`

Operation ID: `GetTreeDocumentTypeSearch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `query` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `itemKind` | query | → TreeItemKindModel | No |

**Response 200:** `OneOf: → PagedDocumentTypeTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/document-type/siblings`

**Gets a collection of document type tree sibling items.**

Operation ID: `GetTreeDocumentTypeSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `target` | query | string (uuid) | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |
| `foldersOnly` | query | boolean | No |

**Response 200:** `OneOf: → SubsetDocumentTypeTreeItemResponseModel`

---
