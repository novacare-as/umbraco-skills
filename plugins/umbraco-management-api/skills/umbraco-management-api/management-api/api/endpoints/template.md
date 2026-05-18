# Template — API Endpoints

See `schemas/template.md` for field definitions.

## Contents

### Template

- `GET /umbraco/management/api/v1/item/template`
- `GET /umbraco/management/api/v1/item/template/ancestors`
- `GET /umbraco/management/api/v1/item/template/search`
- `POST /umbraco/management/api/v1/template`
- `GET /umbraco/management/api/v1/template/{id}`
- `DELETE /umbraco/management/api/v1/template/{id}`
- `PUT /umbraco/management/api/v1/template/{id}`
- `GET /umbraco/management/api/v1/template/configuration`
- `POST /umbraco/management/api/v1/template/query/execute`
- `GET /umbraco/management/api/v1/template/query/settings`
- `GET /umbraco/management/api/v1/tree/template/ancestors`
- `GET /umbraco/management/api/v1/tree/template/children`
- `GET /umbraco/management/api/v1/tree/template/root`
- `GET /umbraco/management/api/v1/tree/template/siblings`

---

## Template

### `GET /umbraco/management/api/v1/item/template`

**Gets a collection of template items.**

Operation ID: `GetItemTemplate`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/template/ancestors`

**Gets ancestors for a collection of template items.**

Operation ID: `GetItemTemplateAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/template/search`

**Searches template items.**

Operation ID: `GetItemTemplateSearch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `query` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedModelTemplateItemResponseModel`

---

### `POST /umbraco/management/api/v1/template`

**Creates a new template.**

Operation ID: `PostTemplate`

**Request body:** `OneOf: → CreateTemplateRequestModel`


---

### `GET /umbraco/management/api/v1/template/{id}`

**Gets a template.**

Operation ID: `GetTemplateById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → TemplateResponseModel`

---

### `DELETE /umbraco/management/api/v1/template/{id}`

**Deletes a template.**

Operation ID: `DeleteTemplateById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/template/{id}`

**Updates a template.**

Operation ID: `PutTemplateById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateTemplateRequestModel`


---

### `GET /umbraco/management/api/v1/template/configuration`

**Gets the template configuration.**

Operation ID: `GetTemplateConfiguration`

**Response 200:** `OneOf: → TemplateConfigurationResponseModel`

---

### `POST /umbraco/management/api/v1/template/query/execute`

**Executes a template query.**

Operation ID: `PostTemplateQueryExecute`

**Request body:** `OneOf: → TemplateQueryExecuteModel`

**Response 200:** `OneOf: → TemplateQueryResultResponseModel`

---

### `GET /umbraco/management/api/v1/template/query/settings`

**Gets template query settings.**

Operation ID: `GetTemplateQuerySettings`

**Response 200:** `OneOf: → TemplateQuerySettingsResponseModel`

---

### `GET /umbraco/management/api/v1/tree/template/ancestors`

**Gets a collection of ancestor template items.**

Operation ID: `GetTreeTemplateAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `descendantId` | query | string (uuid) | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/tree/template/children`

**Gets a collection of template tree child items.**

Operation ID: `GetTreeTemplateChildren`

| Param | In | Type | Required |
|-------|----|------|----------|
| `parentId` | query | string (uuid) | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedNamedEntityTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/template/root`

**Gets a collection of template items from the root of the tree.**

Operation ID: `GetTreeTemplateRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedNamedEntityTreeItemResponseModel`

---

### `GET /umbraco/management/api/v1/tree/template/siblings`

**Gets a collection of template tree sibling items.**

Operation ID: `GetTreeTemplateSiblings`

| Param | In | Type | Required |
|-------|----|------|----------|
| `target` | query | string (uuid) | No |
| `before` | query | integer (int32) | No |
| `after` | query | integer (int32) | No |

**Response 200:** `OneOf: → SubsetNamedEntityTreeItemResponseModel`

---
