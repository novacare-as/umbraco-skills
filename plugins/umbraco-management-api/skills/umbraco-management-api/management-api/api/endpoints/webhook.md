# Webhook — API Endpoints

See `schemas/webhook.md` for field definitions.

## Contents

### Webhook

- `GET /umbraco/management/api/v1/item/webhook`
- `GET /umbraco/management/api/v1/webhook`
- `POST /umbraco/management/api/v1/webhook`
- `GET /umbraco/management/api/v1/webhook/{id}`
- `DELETE /umbraco/management/api/v1/webhook/{id}`
- `PUT /umbraco/management/api/v1/webhook/{id}`
- `GET /umbraco/management/api/v1/webhook/{id}/logs`
- `GET /umbraco/management/api/v1/webhook/events`
- `GET /umbraco/management/api/v1/webhook/logs`

---

## Webhook

### `GET /umbraco/management/api/v1/item/webhook`

**Gets a collection of webhook items.**

Operation ID: `GetItemWebhook`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/webhook`

**Gets a paginated collection of webhooks.**

Operation ID: `GetWebhook`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedWebhookResponseModel`

---

### `POST /umbraco/management/api/v1/webhook`

**Creates a new webhook.**

Operation ID: `PostWebhook`

**Request body:** `OneOf: → CreateWebhookRequestModel`


---

### `GET /umbraco/management/api/v1/webhook/{id}`

**Gets a webhook.**

Operation ID: `GetWebhookById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → WebhookResponseModel`

---

### `DELETE /umbraco/management/api/v1/webhook/{id}`

**Deletes a webhook.**

Operation ID: `DeleteWebhookById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/webhook/{id}`

**Updates a webhook.**

Operation ID: `PutWebhookById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateWebhookRequestModel`


---

### `GET /umbraco/management/api/v1/webhook/{id}/logs`

**Gets a paginated collection of webhook logs for a specific webhook.**

Operation ID: `GetWebhookByIdLogs`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedWebhookLogResponseModel`

---

### `GET /umbraco/management/api/v1/webhook/events`

**Gets a paginated collection of webhook events.**

Operation ID: `GetWebhookEvents`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedWebhookEventModel`

---

### `GET /umbraco/management/api/v1/webhook/logs`

**Gets a paginated collection of webhook logs.**

Operation ID: `GetWebhookLogs`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedWebhookLogResponseModel`

---
