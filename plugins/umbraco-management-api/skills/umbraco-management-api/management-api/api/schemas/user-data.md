# User Data Schemas

## Schemas in this file

- [CreateUserDataRequestModel](#createuserdatarequestmodel)
- [PagedUserDataResponseModel](#pageduserdataresponsemodel)
- [UpdateUserDataRequestModel](#updateuserdatarequestmodel)
- [UserDataModel](#userdatamodel)

---

## CreateUserDataRequestModel

**Fields:**

- `group`: string **required**
- `identifier`: string **required**
- `key`: string (uuid), nullable
- `value`: string **required**

---

## PagedUserDataResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## UpdateUserDataRequestModel

**Fields:**

- `group`: string **required**
- `identifier`: string **required**
- `key`: string (uuid) **required**
- `value`: string **required**

---

## UserDataModel

**Fields:**

- `group`: string **required**
- `identifier`: string **required**
- `value`: string **required**

---
