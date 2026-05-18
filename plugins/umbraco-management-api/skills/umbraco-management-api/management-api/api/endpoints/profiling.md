# Profiling — API Endpoints

See `schemas/profiling.md` for field definitions.

## Contents

### Profiling

- `GET /umbraco/management/api/v1/profiling/status`
- `PUT /umbraco/management/api/v1/profiling/status`

---

## Profiling

### `GET /umbraco/management/api/v1/profiling/status`

**Gets profiling status.**

Operation ID: `GetProfilingStatus`

**Response 200:** `OneOf: → ProfilingStatusResponseModel`

---

### `PUT /umbraco/management/api/v1/profiling/status`

**Updates the web profiling status.**

Operation ID: `PutProfilingStatus`

**Request body:** `OneOf: → ProfilingStatusRequestModel`


---
