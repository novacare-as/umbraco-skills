# Webhook Schemas

## Schemas in this file

- [CreateWebhookRequestModel](#createwebhookrequestmodel)
- [PagedWebhookEventModel](#pagedwebhookeventmodel)
- [PagedWebhookLogResponseModel](#pagedwebhooklogresponsemodel)
- [PagedWebhookResponseModel](#pagedwebhookresponsemodel)
- [UpdateWebhookRequestModel](#updatewebhookrequestmodel)
- [WebhookResponseModel](#webhookresponsemodel)

---

## CreateWebhookRequestModel

**Fields:**

- `contentTypeKeys`: List<string (uuid)> **required**
- `description`: string, nullable
- `enabled`: boolean **required**
- `events`: List<string> **required**
- `headers`: object **required**
- `id`: string (uuid), nullable
- `name`: string, nullable
- `url`: string **required**

---

## PagedWebhookEventModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedWebhookLogResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedWebhookResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## UpdateWebhookRequestModel

**Fields:**

- `contentTypeKeys`: List<string (uuid)> **required**
- `description`: string, nullable
- `enabled`: boolean **required**
- `events`: List<string> **required**
- `headers`: object **required**
- `name`: string, nullable
- `url`: string **required**

---

## WebhookResponseModel

**Fields:**

- `contentTypeKeys`: List<string (uuid)> **required**
- `description`: string, nullable
- `enabled`: boolean **required**
- `events`: List<object> **required**
- `headers`: object **required**
- `id`: string (uuid) **required**
- `name`: string, nullable
- `url`: string **required**

---
