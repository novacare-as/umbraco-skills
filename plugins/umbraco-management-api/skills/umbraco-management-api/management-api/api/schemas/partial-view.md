# Partial View Schemas

## Schemas in this file

- [CreatePartialViewFolderRequestModel](#createpartialviewfolderrequestmodel)
- [CreatePartialViewRequestModel](#createpartialviewrequestmodel)
- [PagedPartialViewSnippetItemResponseModel](#pagedpartialviewsnippetitemresponsemodel)
- [PartialViewFolderResponseModel](#partialviewfolderresponsemodel)
- [PartialViewResponseModel](#partialviewresponsemodel)
- [PartialViewSnippetResponseModel](#partialviewsnippetresponsemodel)
- [RenamePartialViewRequestModel](#renamepartialviewrequestmodel)
- [UpdatePartialViewRequestModel](#updatepartialviewrequestmodel)

---

## CreatePartialViewFolderRequestModel

**Fields:**

- `name`: string **required**
- `parent`: object, nullable

---

## CreatePartialViewRequestModel

**Fields:**

- `content`: string **required**
- `name`: string **required**
- `parent`: object, nullable

---

## PagedPartialViewSnippetItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PartialViewFolderResponseModel

**Fields:**

- `name`: string **required**
- `parent`: object, nullable
- `path`: string **required**

---

## PartialViewResponseModel

**Fields:**

- `content`: string **required**
- `name`: string **required**
- `parent`: object, nullable
- `path`: string **required**

---

## PartialViewSnippetResponseModel

**Fields:**

- `content`: string **required**
- `id`: string **required**
- `name`: string **required**

---

## RenamePartialViewRequestModel

**Fields:**

- `name`: string **required**

---

## UpdatePartialViewRequestModel

**Fields:**

- `content`: string **required**

---
