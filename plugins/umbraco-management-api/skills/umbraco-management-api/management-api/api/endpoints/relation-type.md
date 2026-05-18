# Relation Type — API Endpoints

See `schemas/relation-type.md` for field definitions.

## Contents

### Relation Type

- `GET /umbraco/management/api/v1/item/relation-type`
- `GET /umbraco/management/api/v1/relation-type`
- `GET /umbraco/management/api/v1/relation-type/{id}`

---

## Relation Type

### `GET /umbraco/management/api/v1/item/relation-type`

**Gets a collection of relation type items.**

Operation ID: `GetItemRelationType`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/relation-type`

**Gets a paginated collection of relation types.**

Operation ID: `GetRelationType`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedRelationTypeResponseModel`

---

### `GET /umbraco/management/api/v1/relation-type/{id}`

**Gets a relation type.**

Operation ID: `GetRelationTypeById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → RelationTypeResponseModel`

---
