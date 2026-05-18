# Member Group Schemas

## Schemas in this file

- [CreateMemberGroupRequestModel](#createmembergrouprequestmodel)
- [MemberGroupResponseModel](#membergroupresponsemodel)
- [PagedMemberGroupResponseModel](#pagedmembergroupresponsemodel)
- [UpdateMemberGroupRequestModel](#updatemembergrouprequestmodel)

---

## CreateMemberGroupRequestModel

**Fields:**

- `id`: string (uuid), nullable
- `name`: string **required**

---

## MemberGroupResponseModel

**Fields:**

- `id`: string (uuid) **required**
- `name`: string **required**

---

## PagedMemberGroupResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## UpdateMemberGroupRequestModel

**Fields:**

- `name`: string **required**

---
