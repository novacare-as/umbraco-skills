# Document Version — API Endpoints

See `schemas/document-version.md` for field definitions.

## Contents

### Document Version

- `GET /umbraco/management/api/v1/document-version`
- `GET /umbraco/management/api/v1/document-version/{id}`
- `PUT /umbraco/management/api/v1/document-version/{id}/prevent-cleanup`
- `POST /umbraco/management/api/v1/document-version/{id}/rollback`

---

## Document Version

### `GET /umbraco/management/api/v1/document-version`

**Gets a paginated collection of versions for a specific document.**

Operation ID: `GetDocumentVersion`

| Param | In | Type | Required |
|-------|----|------|----------|
| `documentId` | query | string (uuid) | Yes |
| `culture` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedDocumentVersionItemResponseModel`

---

### `GET /umbraco/management/api/v1/document-version/{id}`

**Gets a specific document version.**

Operation ID: `GetDocumentVersionById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → DocumentVersionResponseModel`

---

### `PUT /umbraco/management/api/v1/document-version/{id}/prevent-cleanup`

**Sets the prevent clean up status for a document version.**

Operation ID: `PutDocumentVersionByIdPreventCleanup`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `preventCleanup` | query | boolean | No |


---

### `POST /umbraco/management/api/v1/document-version/{id}/rollback`

**Rolls back a document to a specific version.**

Operation ID: `PostDocumentVersionByIdRollback`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `culture` | query | string | No |


---
