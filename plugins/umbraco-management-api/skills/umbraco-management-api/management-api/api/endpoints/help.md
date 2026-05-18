# Help — API Endpoints

See `schemas/help.md` for field definitions.

## Contents

### Help

- `GET /umbraco/management/api/v1/help`

---

## Help

### `GET /umbraco/management/api/v1/help`

**Gets help information.**

Operation ID: `GetHelp`

| Param | In | Type | Required |
|-------|----|------|----------|
| `section` | query | string | No |
| `tree` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `baseUrl` | query | string | No |

**Response 200:** `OneOf: → PagedHelpPageResponseModel`

---
