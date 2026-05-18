# User Data — API Endpoints

See `schemas/user-data.md` for field definitions.

## Contents

### User Data

- `POST /umbraco/management/api/v1/user-data`
- `GET /umbraco/management/api/v1/user-data`
- `PUT /umbraco/management/api/v1/user-data`
- `GET /umbraco/management/api/v1/user-data/{id}`
- `DELETE /umbraco/management/api/v1/user-data/{id}`

---

## User Data

### `POST /umbraco/management/api/v1/user-data`

**Creates user data.**

Operation ID: `PostUserData`

**Request body:** `OneOf: → CreateUserDataRequestModel`


---

### `GET /umbraco/management/api/v1/user-data`

**Gets user data.**

Operation ID: `GetUserData`

| Param | In | Type | Required |
|-------|----|------|----------|
| `groups` | query | List<string> | No |
| `identifiers` | query | List<string> | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedUserDataResponseModel`

---

### `PUT /umbraco/management/api/v1/user-data`

**Updates user data.**

Operation ID: `PutUserData`

**Request body:** `OneOf: → UpdateUserDataRequestModel`


---

### `GET /umbraco/management/api/v1/user-data/{id}`

**Gets user data.**

Operation ID: `GetUserDataById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → UserDataModel`

---

### `DELETE /umbraco/management/api/v1/user-data/{id}`

**Deletes user data.**

Operation ID: `DeleteUserDataById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---
