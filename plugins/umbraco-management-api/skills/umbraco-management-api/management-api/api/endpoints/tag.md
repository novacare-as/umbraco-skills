# Tag — API Endpoints

See `schemas/tag.md` for field definitions.

## Contents

### Tag

- `GET /umbraco/management/api/v1/tag`

---

## Tag

### `GET /umbraco/management/api/v1/tag`

**Gets a collection of tags.**

Operation ID: `GetTag`

| Param | In | Type | Required |
|-------|----|------|----------|
| `query` | query | string | No |
| `tagGroup` | query | string | No |
| `culture` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedTagResponseModel`

---
