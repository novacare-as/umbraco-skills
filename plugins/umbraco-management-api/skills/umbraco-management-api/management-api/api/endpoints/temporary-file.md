# Temporary File — API Endpoints

See `schemas/temporary-file.md` for field definitions.

## Contents

### Temporary File

- `POST /umbraco/management/api/v1/temporary-file`
- `GET /umbraco/management/api/v1/temporary-file/{id}`
- `DELETE /umbraco/management/api/v1/temporary-file/{id}`
- `GET /umbraco/management/api/v1/temporary-file/configuration`

---

## Temporary File

### `POST /umbraco/management/api/v1/temporary-file`

**Creates a temporary file.**

Operation ID: `PostTemporaryFile`

**Request body:** `object`


---

### `GET /umbraco/management/api/v1/temporary-file/{id}`

**Gets a temporary file.**

Operation ID: `GetTemporaryFileById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → TemporaryFileResponseModel`

---

### `DELETE /umbraco/management/api/v1/temporary-file/{id}`

**Deletes a temporary file.**

Operation ID: `DeleteTemporaryFileById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `GET /umbraco/management/api/v1/temporary-file/configuration`

**Gets the temporary file configuration.**

Operation ID: `GetTemporaryFileConfiguration`

**Response 200:** `OneOf: → TemporaryFileConfigurationResponseModel`

---
