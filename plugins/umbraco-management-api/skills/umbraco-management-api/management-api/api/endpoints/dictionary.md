# Dictionary — API Endpoints

See `schemas/dictionary.md` for field definitions.

## Contents

### Dictionary

- `GET /umbraco/management/api/v1/dictionary`
- `POST /umbraco/management/api/v1/dictionary`
- `GET /umbraco/management/api/v1/dictionary/{id}`
- `DELETE /umbraco/management/api/v1/dictionary/{id}`
- `PUT /umbraco/management/api/v1/dictionary/{id}`
- `GET /umbraco/management/api/v1/dictionary/{id}/export`
- `PUT /umbraco/management/api/v1/dictionary/{id}/move`
- `POST /umbraco/management/api/v1/dictionary/import`
- `GET /umbraco/management/api/v1/item/dictionary`
- `GET /umbraco/management/api/v1/tree/dictionary/ancestors`
- `GET /umbraco/management/api/v1/tree/dictionary/children`
- `GET /umbraco/management/api/v1/tree/dictionary/root`

---

## Dictionary

### `GET /umbraco/management/api/v1/dictionary`

**Gets a paginated collection of dictionary items.**

Operation ID: `GetDictionary`

| Param | In | Type | Required |
|-------|----|------|----------|
| `filter` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedDictionaryOverviewResponseModel`

---

### `POST /umbraco/management/api/v1/dictionary`

**Creates a new dictionary.**

Operation ID: `PostDictionary`

**Request body:** `OneOf: → CreateDictionaryItemRequestModel`


---

### `GET /umbraco/management/api/v1/dictionary/{id}`

**Gets a dictionary.**

Operation ID: `GetDictionaryById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → DictionaryItemResponseModel`

---

### `DELETE /umbraco/management/api/v1/dictionary/{id}`

**Deletes a dictionary.**

Operation ID: `DeleteDictionaryById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/dictionary/{id}`

**Updates a dictionary.**

Operation ID: `PutDictionaryById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateDictionaryItemRequestModel`


---

### `GET /umbraco/management/api/v1/dictionary/{id}/export`

**Exports a dictionary.**

Operation ID: `GetDictionaryByIdExport`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `includeChildren` | query | boolean | No |

**Response 200:** `OneOf: string (binary)`

---

### `PUT /umbraco/management/api/v1/dictionary/{id}/move`

**Moves a dictionary.**

Operation ID: `PutDictionaryByIdMove`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → MoveDictionaryRequestModel`


---

### `POST /umbraco/management/api/v1/dictionary/import`

**Imports a dictionary.**

Operation ID: `PostDictionaryImport`

**Request body:** `OneOf: → ImportDictionaryRequestModel`


---

### `GET /umbraco/management/api/v1/item/dictionary`

**Gets a collection of dictionary items.**

Operation ID: `GetItemDictionary`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/dictionary/ancestors`

**Gets a collection of ancestor dictionary items.**

Operation ID: `GetTreeDictionaryAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantId` | query | string (uuid) | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/dictionary/children`

**Gets a collection of dictionary tree child items.**

Operation ID: `GetTreeDictionaryChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentId` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedNamedEntityTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/dictionary/root`

**Gets a collection of dictionary items from the root of the tree.**

Operation ID: `GetTreeDictionaryRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedNamedEntityTreeItemResponseModel`

---
