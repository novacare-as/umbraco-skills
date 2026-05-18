# Health Check Schemas

## Schemas in this file

- [HealthCheckActionRequestModel](#healthcheckactionrequestmodel)
- [HealthCheckGroupPresentationModel](#healthcheckgrouppresentationmodel)
- [HealthCheckGroupWithResultResponseModel](#healthcheckgroupwithresultresponsemodel)
- [HealthCheckResultResponseModel](#healthcheckresultresponsemodel)
- [PagedHealthCheckGroupResponseModel](#pagedhealthcheckgroupresponsemodel)
- [StatusResultTypeModel](#statusresulttypemodel)

---

## HealthCheckActionRequestModel

**Fields:**

- `actionParameters`: object, nullable
- `alias`: string, nullable
- `description`: string, nullable
- `healthCheck`: object **required**
- `name`: string, nullable
- `providedValue`: string, nullable
- `providedValueValidation`: string, nullable
- `providedValueValidationRegex`: string, nullable
- `valueRequired`: boolean **required**

---

## HealthCheckGroupPresentationModel

**Fields:**

- `checks`: List<object> **required**
- `name`: string **required**

---

## HealthCheckGroupWithResultResponseModel

**Fields:**

- `checks`: List<object> **required**

---

## HealthCheckResultResponseModel

**Fields:**

- `actions`: List<object>, nullable
- `message`: string **required**
- `readMoreLink`: string, nullable
- `resultType`: → `StatusResultTypeModel` **required**

---

## PagedHealthCheckGroupResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## StatusResultTypeModel

**Enum values:** `Success`, `Warning`, `Error`, `Info`

---
