# User Group Schemas

## Schemas in this file

- [CreateUserGroupRequestModel](#createusergrouprequestmodel)
- [DeleteUserGroupsRequestModel](#deleteusergroupsrequestmodel)
- [PagedUserGroupResponseModel](#pagedusergroupresponsemodel)
- [UpdateUserGroupRequestModel](#updateusergrouprequestmodel)
- [UserGroupResponseModel](#usergroupresponsemodel)

---

## CreateUserGroupRequestModel

**Fields:**

- `alias`: string **required**
- `description`: string, nullable
- `documentRootAccess`: boolean **required**
- `documentStartNode`: object, nullable
- `fallbackPermissions`: List<string> **required**
- `hasAccessToAllLanguages`: boolean **required**
- `icon`: string, nullable
- `id`: string (uuid), nullable
- `languages`: List<string> **required**
- `mediaRootAccess`: boolean **required**
- `mediaStartNode`: object, nullable
- `name`: string **required**
- `permissions`: List<object> **required**
- `sections`: List<string> **required**

---

## DeleteUserGroupsRequestModel

**Fields:**

- `userGroupIds`: List<object> **required**

---

## PagedUserGroupResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## UpdateUserGroupRequestModel

**Fields:**

- `alias`: string **required**
- `description`: string, nullable
- `documentRootAccess`: boolean **required**
- `documentStartNode`: object, nullable
- `fallbackPermissions`: List<string> **required**
- `hasAccessToAllLanguages`: boolean **required**
- `icon`: string, nullable
- `languages`: List<string> **required**
- `mediaRootAccess`: boolean **required**
- `mediaStartNode`: object, nullable
- `name`: string **required**
- `permissions`: List<object> **required**
- `sections`: List<string> **required**

---

## UserGroupResponseModel

**Fields:**

- `alias`: string **required**
- `aliasCanBeChanged`: boolean **required**
- `description`: string, nullable
- `documentRootAccess`: boolean **required**
- `documentStartNode`: object, nullable
- `fallbackPermissions`: List<string> **required**
- `hasAccessToAllLanguages`: boolean **required**
- `icon`: string, nullable
- `id`: string (uuid) **required**
- `isDeletable`: boolean **required**
- `languages`: List<string> **required**
- `mediaRootAccess`: boolean **required**
- `mediaStartNode`: object, nullable
- `name`: string **required**
- `permissions`: List<object> **required**
- `sections`: List<string> **required**

---
