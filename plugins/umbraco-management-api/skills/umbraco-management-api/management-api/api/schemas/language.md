# Language Schemas

## Schemas in this file

- [CreateLanguageRequestModel](#createlanguagerequestmodel)
- [LanguageItemResponseModel](#languageitemresponsemodel)
- [LanguageResponseModel](#languageresponsemodel)
- [PagedLanguageResponseModel](#pagedlanguageresponsemodel)
- [UpdateLanguageRequestModel](#updatelanguagerequestmodel)

---

## CreateLanguageRequestModel

**Fields:**

- `fallbackIsoCode`: string, nullable
- `isDefault`: boolean **required**
- `isMandatory`: boolean **required**
- `isoCode`: string **required**
- `name`: string **required**

---

## LanguageItemResponseModel

**Fields:**

- `isoCode`: string **required**
- `name`: string **required**

---

## LanguageResponseModel

**Fields:**

- `fallbackIsoCode`: string, nullable
- `isDefault`: boolean **required**
- `isMandatory`: boolean **required**
- `isoCode`: string **required**
- `name`: string **required**

---

## PagedLanguageResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## UpdateLanguageRequestModel

**Fields:**

- `fallbackIsoCode`: string, nullable
- `isDefault`: boolean **required**
- `isMandatory`: boolean **required**
- `name`: string **required**

---
