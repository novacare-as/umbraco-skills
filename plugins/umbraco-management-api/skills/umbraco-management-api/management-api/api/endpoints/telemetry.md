# Telemetry — API Endpoints

See `schemas/telemetry.md` for field definitions.

## Contents

### Telemetry

- `GET /umbraco/management/api/v1/telemetry`
- `GET /umbraco/management/api/v1/telemetry/level`
- `POST /umbraco/management/api/v1/telemetry/level`

---

## Telemetry

### `GET /umbraco/management/api/v1/telemetry`

**Gets telemetry data.**

Operation ID: `GetTelemetry`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedTelemetryResponseModel`

---

### `GET /umbraco/management/api/v1/telemetry/level`

**Gets telemetry information.**

Operation ID: `GetTelemetryLevel`

**Response 200:** `OneOf: → TelemetryResponseModel`

---

### `POST /umbraco/management/api/v1/telemetry/level`

**Sets telemetry consent level.**

Operation ID: `PostTelemetryLevel`

**Request body:** `OneOf: → TelemetryRequestModel`


---
