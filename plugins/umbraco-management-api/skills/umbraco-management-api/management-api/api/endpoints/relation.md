# Relation — API Endpoints

See `schemas/relation.md` for field definitions.

## Contents

### Relation

- `GET /umbraco/management/api/v1/relation/type/{id}`

---

## Relation

### `GET /umbraco/management/api/v1/relation/type/{id}`

**Gets relations by relation type.**

Operation ID: `GetRelationByRelationTypeId`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedRelationResponseModel`

---
