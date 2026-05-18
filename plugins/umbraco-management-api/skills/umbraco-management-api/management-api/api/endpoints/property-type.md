# Property Type — API Endpoints

See `schemas/common.md` for field definitions.

## Contents

### Property Type

- `GET /umbraco/management/api/v1/property-type/is-used`

---

## Property Type

### `GET /umbraco/management/api/v1/property-type/is-used`

**Checks if a property type is used.**

Operation ID: `GetPropertyTypeIsUsed`

| Param | In | Type | Required |
|-------|----|------|----------|
| `contentTypeId` | query | string (uuid) | No |
| `propertyAlias` | query | string | No |

**Response 200:** `boolean`

---
