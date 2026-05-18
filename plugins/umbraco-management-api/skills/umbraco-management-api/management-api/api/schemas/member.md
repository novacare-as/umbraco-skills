# Member Schemas

## Schemas in this file

- [CreateMemberRequestModel](#creatememberrequestmodel)
- [MemberConfigurationResponseModel](#memberconfigurationresponsemodel)
- [MemberKindModel](#memberkindmodel)
- [MemberResponseModel](#memberresponsemodel)
- [PagedMemberResponseModel](#pagedmemberresponsemodel)
- [PagedModelMemberItemResponseModel](#pagedmodelmemberitemresponsemodel)
- [UpdateMemberRequestModel](#updatememberrequestmodel)

---

## CreateMemberRequestModel

**Fields:**

- `email`: string **required**
- `groups`: List<string (uuid)>, nullable
- `id`: string (uuid), nullable
- `isApproved`: boolean **required**
- `memberType`: object **required**
- `password`: string **required**
- `username`: string **required**
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

## MemberConfigurationResponseModel

---

## MemberKindModel

**Enum values:** `Default`, `Api`

---

## MemberResponseModel

**Fields:**

- `email`: string **required**
- `failedPasswordAttempts`: integer (int32) **required**
- `flags`: List<object> **required**
- `groups`: List<string (uuid)> **required**
- `id`: string (uuid) **required**
- `isApproved`: boolean **required**
- `isLockedOut`: boolean **required**
- `isTwoFactorEnabled`: boolean **required**
- `kind`: → `MemberKindModel` **required**
- `lastLockoutDate`: string (date-time), nullable
- `lastLoginDate`: string (date-time), nullable
- `lastPasswordChangeDate`: string (date-time), nullable
- `memberType`: object **required**
- `username`: string **required**
- `values`: List<object> **required**
- `variants`: List<object> **required**

---

## PagedMemberResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## PagedModelMemberItemResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## UpdateMemberRequestModel

**Fields:**

- `email`: string **required**
- `groups`: List<string (uuid)>, nullable
- `isApproved`: boolean **required**
- `isLockedOut`: boolean **required**
- `isTwoFactorEnabled`: boolean **required**
- `newPassword`: string, nullable
- `oldPassword`: string, nullable
- `username`: string **required**
- `values`: List<object> **required**
- `variants`: List<object> **required**

---
