# Redirect Management Schemas

## Schemas in this file

- [PagedRedirectUrlResponseModel](#pagedredirecturlresponsemodel)
- [RedirectStatusModel](#redirectstatusmodel)
- [RedirectUrlStatusResponseModel](#redirecturlstatusresponsemodel)

---

## PagedRedirectUrlResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## RedirectStatusModel

**Enum values:** `Enabled`, `Disabled`

---

## RedirectUrlStatusResponseModel

**Fields:**

- `status`: → `RedirectStatusModel` **required**
- `userIsAdmin`: boolean **required**

---
