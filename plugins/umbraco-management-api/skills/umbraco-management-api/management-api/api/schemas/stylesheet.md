# Stylesheet Schemas

## Schemas in this file

- [CreateStylesheetFolderRequestModel](#createstylesheetfolderrequestmodel)
- [CreateStylesheetRequestModel](#createstylesheetrequestmodel)
- [RenameStylesheetRequestModel](#renamestylesheetrequestmodel)
- [StylesheetFolderResponseModel](#stylesheetfolderresponsemodel)
- [StylesheetResponseModel](#stylesheetresponsemodel)
- [UpdateStylesheetRequestModel](#updatestylesheetrequestmodel)

---

## CreateStylesheetFolderRequestModel

**Fields:**

- `name`: string **required**
- `parent`: object, nullable

---

## CreateStylesheetRequestModel

**Fields:**

- `content`: string **required**
- `name`: string **required**
- `parent`: object, nullable

---

## RenameStylesheetRequestModel

**Fields:**

- `name`: string **required**

---

## StylesheetFolderResponseModel

**Fields:**

- `name`: string **required**
- `parent`: object, nullable
- `path`: string **required**

---

## StylesheetResponseModel

**Fields:**

- `content`: string **required**
- `name`: string **required**
- `parent`: object, nullable
- `path`: string **required**

---

## UpdateStylesheetRequestModel

**Fields:**

- `content`: string **required**

---
