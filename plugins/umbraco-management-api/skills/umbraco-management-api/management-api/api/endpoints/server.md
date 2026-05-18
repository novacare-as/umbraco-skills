# Server — API Endpoints

See `schemas/server.md` for field definitions.

## Contents

### Server

- `GET /umbraco/management/api/v1/server/configuration`
- `GET /umbraco/management/api/v1/server/information`
- `GET /umbraco/management/api/v1/server/status`
- `GET /umbraco/management/api/v1/server/troubleshooting`
- `GET /umbraco/management/api/v1/server/upgrade-check`

---

## Server

### `GET /umbraco/management/api/v1/server/configuration`

**Gets the server configuration.**

Operation ID: `GetServerConfiguration`

**Response 200:** `OneOf: → ServerConfigurationResponseModel`

---

### `GET /umbraco/management/api/v1/server/information`

**Gets server information.**

Operation ID: `GetServerInformation`

**Response 200:** `OneOf: → ServerInformationResponseModel`

---

### `GET /umbraco/management/api/v1/server/status`

**Gets server status.**

Operation ID: `GetServerStatus`

**Response 200:** `OneOf: → ServerStatusResponseModel`

---

### `GET /umbraco/management/api/v1/server/troubleshooting`

**Gets server troubleshooting information.**

Operation ID: `GetServerTroubleshooting`

**Response 200:** `OneOf: → ServerTroubleshootingResponseModel`

---

### `GET /umbraco/management/api/v1/server/upgrade-check`

**Checks for available upgrades.**

Operation ID: `GetServerUpgradeCheck`

**Response 200:** `OneOf: → UpgradeCheckResponseModel`

---
