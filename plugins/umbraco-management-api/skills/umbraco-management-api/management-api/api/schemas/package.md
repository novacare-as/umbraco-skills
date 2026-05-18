# Package Schemas

## Schemas in this file

- [CreatePackageRequestModel](#createpackagerequestmodel)
- [PackageConfigurationResponseModel](#packageconfigurationresponsemodel)
- [PackageDefinitionResponseModel](#packagedefinitionresponsemodel)
- [PagedPackageDefinitionResponseModel](#pagedpackagedefinitionresponsemodel)
- [PagedPackageMigrationStatusResponseModel](#pagedpackagemigrationstatusresponsemodel)
- [UpdatePackageRequestModel](#updatepackagerequestmodel)

---

## CreatePackageRequestModel

**Fields:**

- `contentLoadChildNodes`: boolean **required**
- `contentNodeId`: string, nullable
- `dataTypes`: List<string> **required**
- `dictionaryItems`: List<string> **required**
- `documentTypes`: List<string> **required**
- `id`: string (uuid), nullable
- `languages`: List<string> **required**
- `mediaIds`: List<string (uuid)> **required**
- `mediaLoadChildNodes`: boolean **required**
- `mediaTypes`: List<string> **required**
- `name`: string **required**
- `partialViews`: List<string> **required**
- `scripts`: List<string> **required**
- `stylesheets`: List<string> **required**
- `templates`: List<string> **required**

---

## PackageConfigurationResponseModel

**Fields:**

- `marketplaceUrl`: string **required**

---

## PackageDefinitionResponseModel

**Fields:**

- `contentLoadChildNodes`: boolean **required**
- `contentNodeId`: string, nullable
- `dataTypes`: List<string> **required**
- `dictionaryItems`: List<string> **required**
- `documentTypes`: List<string> **required**
- `id`: string (uuid) **required**
- `languages`: List<string> **required**
- `mediaIds`: List<string (uuid)> **required**
- `mediaLoadChildNodes`: boolean **required**
- `mediaTypes`: List<string> **required**
- `name`: string **required**
- `packagePath`: string **required**
- `partialViews`: List<string> **required**
- `scripts`: List<string> **required**
- `stylesheets`: List<string> **required**
- `templates`: List<string> **required**

---

## PagedPackageDefinitionResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedPackageMigrationStatusResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## UpdatePackageRequestModel

**Fields:**

- `contentLoadChildNodes`: boolean **required**
- `contentNodeId`: string, nullable
- `dataTypes`: List<string> **required**
- `dictionaryItems`: List<string> **required**
- `documentTypes`: List<string> **required**
- `languages`: List<string> **required**
- `mediaIds`: List<string (uuid)> **required**
- `mediaLoadChildNodes`: boolean **required**
- `mediaTypes`: List<string> **required**
- `name`: string **required**
- `packagePath`: string **required**
- `partialViews`: List<string> **required**
- `scripts`: List<string> **required**
- `stylesheets`: List<string> **required**
- `templates`: List<string> **required**

---
