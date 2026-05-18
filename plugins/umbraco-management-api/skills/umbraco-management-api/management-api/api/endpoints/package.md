# Package — API Endpoints

See `schemas/package.md` for field definitions.

## Contents

### Package

- `POST /umbraco/management/api/v1/package/{name}/run-migration`
- `GET /umbraco/management/api/v1/package/configuration`
- `GET /umbraco/management/api/v1/package/created`
- `POST /umbraco/management/api/v1/package/created`
- `GET /umbraco/management/api/v1/package/created/{id}`
- `DELETE /umbraco/management/api/v1/package/created/{id}`
- `PUT /umbraco/management/api/v1/package/created/{id}`
- `GET /umbraco/management/api/v1/package/created/{id}/download`
- `GET /umbraco/management/api/v1/package/migration-status`

---

## Package

### `POST /umbraco/management/api/v1/package/{name}/run-migration`

**Runs pending package migrations.**

Operation ID: `PostPackageByNameRunMigration`

| Param | In | Type | Required |
|-------|----|------|----------|
| `name` | path | string | Yes |


---

### `GET /umbraco/management/api/v1/package/configuration`

**Gets the package configuration.**

Operation ID: `GetPackageConfiguration`

**Response 200:** `OneOf: → PackageConfigurationResponseModel`

---

### `GET /umbraco/management/api/v1/package/created`

**Gets a paginated collection of created packages.**

Operation ID: `GetPackageCreated`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedPackageDefinitionResponseModel`

---

### `POST /umbraco/management/api/v1/package/created`

**Creates a new package.**

Operation ID: `PostPackageCreated`

**Request body:** `OneOf: → CreatePackageRequestModel`


---

### `GET /umbraco/management/api/v1/package/created/{id}`

**Gets a package.**

Operation ID: `GetPackageCreatedById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → PackageDefinitionResponseModel`

---

### `DELETE /umbraco/management/api/v1/package/created/{id}`

**Deletes a package.**

Operation ID: `DeletePackageCreatedById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/package/created/{id}`

**Updates a package.**

Operation ID: `PutPackageCreatedById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdatePackageRequestModel`


---

### `GET /umbraco/management/api/v1/package/created/{id}/download`

**Downloads a created package.**

Operation ID: `GetPackageCreatedByIdDownload`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: string (binary)`

---

### `GET /umbraco/management/api/v1/package/migration-status`

**Gets all package migration statuses.**

Operation ID: `GetPackageMigrationStatus`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedPackageMigrationStatusResponseModel`

---
