# Script Schemas

## Schemas in this file

- [CreateScriptFolderRequestModel](#createscriptfolderrequestmodel)
- [CreateScriptRequestModel](#createscriptrequestmodel)
- [RenameScriptRequestModel](#renamescriptrequestmodel)
- [ScriptFolderResponseModel](#scriptfolderresponsemodel)
- [ScriptResponseModel](#scriptresponsemodel)
- [UpdateScriptRequestModel](#updatescriptrequestmodel)

---

## CreateScriptFolderRequestModel

**Fields:**

- `name`: string **required**
- `parent`: object, nullable

---

## CreateScriptRequestModel

**Fields:**

- `content`: string **required**
- `name`: string **required**
- `parent`: object, nullable

---

## RenameScriptRequestModel

**Fields:**

- `name`: string **required**

---

## ScriptFolderResponseModel

**Fields:**

- `name`: string **required**
- `parent`: object, nullable
- `path`: string **required**

---

## ScriptResponseModel

**Fields:**

- `content`: string **required**
- `name`: string **required**
- `parent`: object, nullable
- `path`: string **required**

---

## UpdateScriptRequestModel

**Fields:**

- `content`: string **required**

---
