# Culture — API Endpoints

See `schemas/culture.md` for field definitions.

## Contents

### Culture

- `GET /umbraco/management/api/v1/culture`

---

## Culture

### `GET /umbraco/management/api/v1/culture`

**Gets a paginated collection of cultures available for creating languages.**

Operation ID: `GetCulture`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedCultureReponseModel`

---
