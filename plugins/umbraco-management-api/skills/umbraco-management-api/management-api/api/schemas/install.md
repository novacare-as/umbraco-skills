# Install Schemas

## Schemas in this file

- [DatabaseInstallRequestModel](#databaseinstallrequestmodel)
- [InstallRequestModel](#installrequestmodel)
- [InstallSettingsResponseModel](#installsettingsresponsemodel)

---

## DatabaseInstallRequestModel

**Fields:**

- `connectionString`: string, nullable
- `id`: string (uuid) **required**
- `name`: string, nullable
- `password`: string, nullable
- `providerName`: string **required**
- `server`: string, nullable
- `trustServerCertificate`: boolean **required**
- `useIntegratedAuthentication`: boolean **required**
- `username`: string, nullable

---

## InstallRequestModel

**Fields:**

- `database`: object **required**
- `telemetryLevel`: → `TelemetryLevelModel` **required**
- `user`: object **required**

---

## InstallSettingsResponseModel

**Fields:**

- `databases`: List<object> **required**
- `user`: object **required**

---
