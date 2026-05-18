# Member Group — API Endpoints

See `schemas/member-group.md` for field definitions.

## Contents

### Member Group

- `GET /umbraco/management/api/v1/item/member-group`
- `GET /umbraco/management/api/v1/member-group`
- `POST /umbraco/management/api/v1/member-group`
- `GET /umbraco/management/api/v1/member-group/{id}`
- `DELETE /umbraco/management/api/v1/member-group/{id}`
- `PUT /umbraco/management/api/v1/member-group/{id}`
- `GET /umbraco/management/api/v1/tree/member-group/root`

---

## Member Group

### `GET /umbraco/management/api/v1/item/member-group`

**Gets a collection of member group items.**

Operation ID: `GetItemMemberGroup`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/member-group`

**Gets a paginated collection of member groups.**

Operation ID: `GetMemberGroup`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedMemberGroupResponseModel`

---

### `POST /umbraco/management/api/v1/member-group`

**Creates a new member group.**

Operation ID: `PostMemberGroup`

**Request body:** `OneOf: → CreateMemberGroupRequestModel`


---

### `GET /umbraco/management/api/v1/member-group/{id}`

**Gets a member group.**

Operation ID: `GetMemberGroupById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → MemberGroupResponseModel`

---

### `DELETE /umbraco/management/api/v1/member-group/{id}`

**Deletes a member group.**

Operation ID: `DeleteMemberGroupById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/member-group/{id}`

**Updates a member group.**

Operation ID: `PutMemberGroupById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateMemberGroupRequestModel`


---

### `GET /umbraco/management/api/v1/tree/member-group/root`

**Gets a collection of member group items from the root of the tree.**

Operation ID: `GetTreeMemberGroupRoot`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedNamedEntityTreeItemResponseModel`

---
