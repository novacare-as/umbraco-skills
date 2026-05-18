# Server Schemas

## Schemas in this file

- [RuntimeLevelModel](#runtimelevelmodel)
- [RuntimeModeModel](#runtimemodemodel)
- [ServerConfigurationResponseModel](#serverconfigurationresponsemodel)
- [ServerInformationResponseModel](#serverinformationresponsemodel)
- [ServerStatusResponseModel](#serverstatusresponsemodel)
- [ServerTroubleshootingResponseModel](#servertroubleshootingresponsemodel)
- [UpgradeCheckResponseModel](#upgradecheckresponsemodel)

---

## RuntimeLevelModel

**Enum values:** `Unknown`, `Boot`, `Install`, `Upgrade`, `Upgrading`, `Run`, `BootFailed`

---

## RuntimeModeModel

**Enum values:** `BackofficeDevelopment`, `Development`, `Production`

---

## ServerConfigurationResponseModel

**Fields:**

- `allowLocalLogin`: boolean **required**
- `allowPasswordReset`: boolean **required**
- `umbracoCssPath`: string **required**
- `versionCheckPeriod`: integer (int32) **required**

---

## ServerInformationResponseModel

**Fields:**

- `assemblyVersion`: string **required**
- `baseUtcOffset`: string **required**
- `runtimeMode`: → `RuntimeModeModel` **required**
- `version`: string **required**

---

## ServerStatusResponseModel

**Fields:**

- `serverStatus`: → `RuntimeLevelModel` **required**

---

## ServerTroubleshootingResponseModel

**Fields:**

- `items`: List<object> **required**

---

## UpgradeCheckResponseModel

**Fields:**

- `comment`: string **required**
- `type`: string **required**
- `url`: string **required**

---
