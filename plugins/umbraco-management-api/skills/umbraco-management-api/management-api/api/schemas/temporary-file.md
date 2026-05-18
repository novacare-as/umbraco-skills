# Temporary File Schemas

## Schemas in this file

- [TemporaryFileConfigurationResponseModel](#temporaryfileconfigurationresponsemodel)
- [TemporaryFileResponseModel](#temporaryfileresponsemodel)

---

## TemporaryFileConfigurationResponseModel

**Fields:**

- `allowedUploadedFileExtensions`: List<string> **required**
- `disallowedUploadedFilesExtensions`: List<string> **required**
- `imageFileTypes`: List<string> **required**
- `maxFileSize`: integer (int64), nullable

---

## TemporaryFileResponseModel

**Fields:**

- `availableUntil`: string (date-time), nullable
- `fileName`: string **required**
- `id`: string (uuid) **required**

---
