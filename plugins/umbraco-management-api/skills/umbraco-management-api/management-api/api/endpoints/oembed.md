# oEmbed — API Endpoints

See `schemas/oembed.md` for field definitions.

## Contents

### oEmbed

- `GET /umbraco/management/api/v1/oembed/query`

---

## oEmbed

### `GET /umbraco/management/api/v1/oembed/query`

**Queries OEmbed information.**

Operation ID: `GetOembedQuery`

| Param | In | Type | Required |
|-------|----|------|----------|
| `url` | query | string (uri) | No |
| `maxWidth` | query | integer (int32) | No |
| `maxHeight` | query | integer (int32) | No |

**Response 200:** `OneOf: → OEmbedResponseModel`

---
