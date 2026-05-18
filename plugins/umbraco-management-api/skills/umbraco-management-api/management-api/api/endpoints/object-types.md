# Object Types — API Endpoints

See `schemas/object-types.md` for field definitions.

## Contents

### Object Types

- `GET /umbraco/management/api/v1/object-types`

---

## Object Types

### `GET /umbraco/management/api/v1/object-types`

**Gets a paginated collection of allowed object types.**

Operation ID: `GetObjectTypes`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedObjectTypeResponseModel`

---
