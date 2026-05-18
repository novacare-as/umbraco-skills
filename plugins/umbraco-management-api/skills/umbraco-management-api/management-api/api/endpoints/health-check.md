# Health Check — API Endpoints

See `schemas/health-check.md` for field definitions.

## Contents

### Health Check

- `GET /umbraco/management/api/v1/health-check-group`
- `GET /umbraco/management/api/v1/health-check-group/{name}`
- `POST /umbraco/management/api/v1/health-check-group/{name}/check`
- `POST /umbraco/management/api/v1/health-check/execute-action`

---

## Health Check

### `GET /umbraco/management/api/v1/health-check-group`

**Gets a collection of health check groups.**

Operation ID: `GetHealthCheckGroup`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedHealthCheckGroupResponseModel`

---

### `GET /umbraco/management/api/v1/health-check-group/{name}`

**Gets a health check group by name.**

Operation ID: `GetHealthCheckGroupByName`

| Param | In | Type | Required |
|-------|----|------|----------|
| `name` | path | string | Yes |

**Response 200:** `OneOf: → HealthCheckGroupPresentationModel`

---

### `POST /umbraco/management/api/v1/health-check-group/{name}/check`

**Executes all health checks in a group.**

Operation ID: `PostHealthCheckGroupByNameCheck`

| Param | In | Type | Required |
|-------|----|------|----------|
| `name` | path | string | Yes |

**Response 200:** `OneOf: → HealthCheckGroupWithResultResponseModel`

---

### `POST /umbraco/management/api/v1/health-check/execute-action`

**Executes a health check action.**

Operation ID: `PostHealthCheckExecuteAction`

**Request body:** `OneOf: → HealthCheckActionRequestModel`

**Response 200:** `OneOf: → HealthCheckResultResponseModel`

---
