# Member — API Endpoints

See `schemas/member.md` for field definitions.

## Contents

### Member

- `GET /umbraco/management/api/v1/filter/member`
- `GET /umbraco/management/api/v1/item/member`
- `GET /umbraco/management/api/v1/item/member/ancestors`
- `GET /umbraco/management/api/v1/item/member/search`
- `POST /umbraco/management/api/v1/member`
- `GET /umbraco/management/api/v1/member/{id}`
- `DELETE /umbraco/management/api/v1/member/{id}`
- `PUT /umbraco/management/api/v1/member/{id}`
- `GET /umbraco/management/api/v1/member/{id}/referenced-by`
- `GET /umbraco/management/api/v1/member/{id}/referenced-descendants`
- `PUT /umbraco/management/api/v1/member/{id}/validate`
- `GET /umbraco/management/api/v1/member/are-referenced`
- `GET /umbraco/management/api/v1/member/configuration`
- `POST /umbraco/management/api/v1/member/validate`

---

## Member

### `GET /umbraco/management/api/v1/filter/member`

**Gets a filtered collection of members.**

Operation ID: `GetFilterMember`

| Param | In | Type | Required |
|-------|----|------|----------|
| `memberTypeId` | query | string (uuid) | No |
| `memberGroupName` | query | string | No |
| `isApproved` | query | boolean | No |
| `isLockedOut` | query | boolean | No |
| `orderBy` | query | string | No |
| `orderDirection` | query | → DirectionModel | No |
| `filter` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedMemberResponseModel`

---

### `GET /umbraco/management/api/v1/item/member`

**Gets a collection of member items.**

Operation ID: `GetItemMember`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/member/ancestors`

**Gets ancestors for a collection of member items.**

Operation ID: `GetItemMemberAncestors`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/member/search`

**Searches member items.**

Operation ID: `GetItemMemberSearch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `query` | query | string | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `allowedMemberTypes` | query | List<string (uuid)> | No |

**Response 200:** `OneOf: → PagedModelMemberItemResponseModel`

---

### `POST /umbraco/management/api/v1/member`

**Creates a new member.**

Operation ID: `PostMember`

**Request body:** `OneOf: → CreateMemberRequestModel`


---

### `GET /umbraco/management/api/v1/member/{id}`

**Gets a member.**

Operation ID: `GetMemberById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → MemberResponseModel`

---

### `DELETE /umbraco/management/api/v1/member/{id}`

**Deletes a member.**

Operation ID: `DeleteMemberById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/member/{id}`

**Updates a member.**

Operation ID: `PutMemberById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateMemberRequestModel`


---

### `GET /umbraco/management/api/v1/member/{id}/referenced-by`

**Gets a collection of items that reference members.**

Operation ID: `GetMemberByIdReferencedBy`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedIReferenceResponseModel`

---

### `GET /umbraco/management/api/v1/member/{id}/referenced-descendants`

**Gets a paginated collection of referenced descendant members.**

Operation ID: `GetMemberByIdReferencedDescendants`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedReferenceByIdModel`

---

### `PUT /umbraco/management/api/v1/member/{id}/validate`

**Validates updating a member.**

Operation ID: `PutMemberByIdValidate`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateMemberRequestModel`


---

### `GET /umbraco/management/api/v1/member/are-referenced`

**Gets a collection of items that reference members.**

Operation ID: `GetMemberAreReferenced`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedReferenceByIdModel`

---

### `GET /umbraco/management/api/v1/member/configuration`

**Gets the member configuration.**

Operation ID: `GetMemberConfiguration`

**Response 200:** `OneOf: → MemberConfigurationResponseModel`

---

### `POST /umbraco/management/api/v1/member/validate`

**Validates creating a member.**

Operation ID: `PostMemberValidate`

**Request body:** `OneOf: → CreateMemberRequestModel`


---
