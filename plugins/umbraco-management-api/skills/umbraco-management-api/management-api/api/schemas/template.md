# Template Schemas

## Schemas in this file

- [CreateTemplateRequestModel](#createtemplaterequestmodel)
- [PagedModelTemplateItemResponseModel](#pagedmodeltemplateitemresponsemodel)
- [SubsetNamedEntityTreeItemResponseModel](#subsetnamedentitytreeitemresponsemodel)
- [TemplateConfigurationResponseModel](#templateconfigurationresponsemodel)
- [TemplateQueryExecuteModel](#templatequeryexecutemodel)
- [TemplateQueryResultResponseModel](#templatequeryresultresponsemodel)
- [TemplateQuerySettingsResponseModel](#templatequerysettingsresponsemodel)
- [TemplateResponseModel](#templateresponsemodel)
- [UpdateTemplateRequestModel](#updatetemplaterequestmodel)

---

## CreateTemplateRequestModel

**Fields:**

- `alias`: string **required**
- `content`: string, nullable
- `id`: string (uuid), nullable
- `name`: string **required**

---

## PagedModelTemplateItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## SubsetNamedEntityTreeItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `totalAfter`: integer (int64) **required**
- `totalBefore`: integer (int64) **required**

---

## TemplateConfigurationResponseModel

**Fields:**

- `disabled`: boolean **required**

---

## TemplateQueryExecuteModel

**Fields:**

- `documentTypeAlias`: string, nullable
- `filters`: List<object>, nullable
- `rootDocument`: object, nullable
- `sort`: object, nullable
- `take`: integer (int32) **required**

---

## TemplateQueryResultResponseModel

**Fields:**

- `executionTime`: integer (int64) **required**
- `queryExpression`: string **required**
- `resultCount`: integer (int32) **required**
- `sampleResults`: List<object> **required**

---

## TemplateQuerySettingsResponseModel

**Fields:**

- `documentTypeAliases`: List<string> **required**
- `operators`: List<object> **required**
- `properties`: List<object> **required**

---

## TemplateResponseModel

**Fields:**

- `alias`: string **required**
- `content`: string, nullable
- `id`: string (uuid) **required**
- `masterTemplate`: object, nullable
- `name`: string **required**

---

## UpdateTemplateRequestModel

**Fields:**

- `alias`: string **required**
- `content`: string, nullable
- `name`: string **required**

---
