# User Group — API Endpoints

See `schemas/user-group.md` for field definitions.

## Contents

### User Group

- `GET /umbraco/management/api/v1/filter/user-group`
- `GET /umbraco/management/api/v1/item/user-group`
- `DELETE /umbraco/management/api/v1/user-group`
- `POST /umbraco/management/api/v1/user-group`
- `GET /umbraco/management/api/v1/user-group`
- `GET /umbraco/management/api/v1/user-group/{id}`
- `DELETE /umbraco/management/api/v1/user-group/{id}`
- `PUT /umbraco/management/api/v1/user-group/{id}`
- `DELETE /umbraco/management/api/v1/user-group/{id}/users`
- `POST /umbraco/management/api/v1/user-group/{id}/users`

---

## User Group

### `GET /umbraco/management/api/v1/filter/user-group`

**Gets a filtered collection of user groups.**

Operation ID: `GetFilterUserGroup`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `filter` | query | string | No |

**Response 200:** `OneOf: → PagedUserGroupResponseModel`

---

### `GET /umbraco/management/api/v1/item/user-group`

**Gets a collection of user group items.**

Operation ID: `GetItemUserGroup`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `DELETE /umbraco/management/api/v1/user-group`

**Deletes multiple user groups.**

Operation ID: `DeleteUserGroup`

**Request body:** `OneOf: → DeleteUserGroupsRequestModel`


---

### `POST /umbraco/management/api/v1/user-group`

**Creates a new user group.**

Operation ID: `PostUserGroup`

**Request body:** `OneOf: → CreateUserGroupRequestModel`


---

### `GET /umbraco/management/api/v1/user-group`

**Gets a paginated collection of user groups.**

Operation ID: `GetUserGroup`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedUserGroupResponseModel`

---

### `GET /umbraco/management/api/v1/user-group/{id}`

**Gets a user group.**

Operation ID: `GetUserGroupById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → UserGroupResponseModel`

---

### `DELETE /umbraco/management/api/v1/user-group/{id}`

**Deletes a user group.**

Operation ID: `DeleteUserGroupById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/user-group/{id}`

**Updates a user group.**

Operation ID: `PutUserGroupById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateUserGroupRequestModel`


---

### `DELETE /umbraco/management/api/v1/user-group/{id}/users`

**Removes users from a user group.**

Operation ID: `DeleteUserGroupByIdUsers`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `List<object>`


---

### `POST /umbraco/management/api/v1/user-group/{id}/users`

**Adds users to a user group.**

Operation ID: `PostUserGroupByIdUsers`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `List<object>`


---
