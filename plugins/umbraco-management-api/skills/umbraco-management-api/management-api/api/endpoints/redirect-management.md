# Redirect Management — API Endpoints

See `schemas/redirect-management.md` for field definitions.

## Contents

### Redirect Management

- `GET /umbraco/management/api/v1/redirect-management`
- `GET /umbraco/management/api/v1/redirect-management/{id}`
- `DELETE /umbraco/management/api/v1/redirect-management/{id}`
- `GET /umbraco/management/api/v1/redirect-management/status`
- `POST /umbraco/management/api/v1/redirect-management/status`

---

## Redirect Management

### `GET /umbraco/management/api/v1/redirect-management`

**Gets a paginated collection of redirect URLs.**

Operation ID: `GetRedirectManagement`

| Param | In | Type | Required |
|-------|----|------|----------|
| `filter` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedRedirectUrlResponseModel`

---

### `GET /umbraco/management/api/v1/redirect-management/{id}`

**Gets a redirect URL.**

Operation ID: `GetRedirectManagementById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedRedirectUrlResponseModel`

---

### `DELETE /umbraco/management/api/v1/redirect-management/{id}`

**Deletes a redirect URL.**

Operation ID: `DeleteRedirectManagementById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `GET /umbraco/management/api/v1/redirect-management/status`

**Gets the current redirect URL management status.**

Operation ID: `GetRedirectManagementStatus`

**Response 200:** `OneOf: → RedirectUrlStatusResponseModel`

---

### `POST /umbraco/management/api/v1/redirect-management/status`

**Sets the redirect URL tracking status.**

Operation ID: `PostRedirectManagementStatus`

| Param | In | Type | Required |
|-------|----|------|----------|
| `status` | query | → RedirectStatusModel | No |


---
