# Log Viewer Schemas

## Schemas in this file

- [LogLevelCountsReponseModel](#loglevelcountsreponsemodel)
- [LogLevelModel](#loglevelmodel)
- [PagedLogMessageResponseModel](#pagedlogmessageresponsemodel)
- [PagedLogTemplateResponseModel](#pagedlogtemplateresponsemodel)
- [PagedLoggerResponseModel](#pagedloggerresponsemodel)
- [PagedSavedLogSearchResponseModel](#pagedsavedlogsearchresponsemodel)
- [SavedLogSearchRequestModel](#savedlogsearchrequestmodel)
- [SavedLogSearchResponseModel](#savedlogsearchresponsemodel)

---

## LogLevelCountsReponseModel

**Fields:**

- `debug`: integer (int32) **required**
- `error`: integer (int32) **required**
- `fatal`: integer (int32) **required**
- `information`: integer (int32) **required**
- `warning`: integer (int32) **required**

---

## LogLevelModel

**Enum values:** `Verbose`, `Debug`, `Information`, `Warning`, `Error`, `Fatal`

---

## PagedLogMessageResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedLogTemplateResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedLoggerResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedSavedLogSearchResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## SavedLogSearchRequestModel

**Fields:**

- `name`: string **required**
- `query`: string **required**

---

## SavedLogSearchResponseModel

**Fields:**

- `name`: string **required**
- `query`: string **required**

---
