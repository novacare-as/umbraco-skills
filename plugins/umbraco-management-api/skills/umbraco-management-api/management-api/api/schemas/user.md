# User Schemas

## Schemas in this file

- [CalculatedUserStartNodesResponseModel](#calculateduserstartnodesresponsemodel)
- [ChangePasswordCurrentUserRequestModel](#changepasswordcurrentuserrequestmodel)
- [ChangePasswordUserRequestModel](#changepassworduserrequestmodel)
- [CreateInitialPasswordUserRequestModel](#createinitialpassworduserrequestmodel)
- [CreateUserClientCredentialsRequestModel](#createuserclientcredentialsrequestmodel)
- [CreateUserRequestModel](#createuserrequestmodel)
- [CurrentUserConfigurationResponseModel](#currentuserconfigurationresponsemodel)
- [CurrentUserResponseModel](#currentuserresponsemodel)
- [DeleteUsersRequestModel](#deleteusersrequestmodel)
- [DisableUserRequestModel](#disableuserrequestmodel)
- [EnableTwoFactorRequestModel](#enabletwofactorrequestmodel)
- [EnableUserRequestModel](#enableuserrequestmodel)
- [InviteUserRequestModel](#inviteuserrequestmodel)
- [NoopSetupTwoFactorModel](#noopsetuptwofactormodel)
- [PagedUserResponseModel](#pageduserresponsemodel)
- [ResendInviteUserRequestModel](#resendinviteuserrequestmodel)
- [ResetPasswordUserResponseModel](#resetpassworduserresponsemodel)
- [SetAvatarRequestModel](#setavatarrequestmodel)
- [UnlockUsersRequestModel](#unlockusersrequestmodel)
- [UpdateUserGroupsOnUserRequestModel](#updateusergroupsonuserrequestmodel)
- [UpdateUserRequestModel](#updateuserrequestmodel)
- [UserConfigurationResponseModel](#userconfigurationresponsemodel)
- [UserKindModel](#userkindmodel)
- [UserOrderModel](#userordermodel)
- [UserPermissionsResponseModel](#userpermissionsresponsemodel)
- [UserResponseModel](#userresponsemodel)
- [UserStateModel](#userstatemodel)
- [VerifyInviteUserRequestModel](#verifyinviteuserrequestmodel)
- [VerifyInviteUserResponseModel](#verifyinviteuserresponsemodel)

---

## CalculatedUserStartNodesResponseModel

**Fields:**

- `documentStartNodeIds`: List<object> **required**
- `hasDocumentRootAccess`: boolean **required**
- `hasMediaRootAccess`: boolean **required**
- `id`: string (uuid) **required**
- `mediaStartNodeIds`: List<object> **required**

---

## ChangePasswordCurrentUserRequestModel

**Fields:**

- `newPassword`: string **required**
- `oldPassword`: string, nullable

---

## ChangePasswordUserRequestModel

**Fields:**

- `newPassword`: string **required**

---

## CreateInitialPasswordUserRequestModel

**Fields:**

- `password`: string **required**
- `token`: string **required**
- `user`: object **required**

---

## CreateUserClientCredentialsRequestModel

**Fields:**

- `clientId`: string **required**
- `clientSecret`: string **required**

---

## CreateUserRequestModel

**Fields:**

- `email`: string **required**
- `id`: string (uuid), nullable
- `kind`: → `UserKindModel` **required**
- `name`: string **required**
- `userGroupIds`: List<object> **required**
- `userName`: string **required**

---

## CurrentUserConfigurationResponseModel

**Fields:**

- `allowChangePassword`: boolean **required**
- `allowTwoFactor`: boolean **required**
- `keepUserLoggedIn`: boolean **required**
- `passwordConfiguration`: object **required**

---

## CurrentUserResponseModel

**Fields:**

- `allowedSections`: List<string> **required**
- `avatarUrls`: List<string> **required**
- `documentStartNodeIds`: List<object> **required**
- `email`: string **required**
- `fallbackPermissions`: List<string> **required**
- `hasAccessToAllLanguages`: boolean **required**
- `hasAccessToSensitiveData`: boolean **required**
- `hasDocumentRootAccess`: boolean **required**
- `hasMediaRootAccess`: boolean **required**
- `id`: string (uuid) **required**
- `isAdmin`: boolean **required**
- `languageIsoCode`: string, nullable **required**
- `languages`: List<string> **required**
- `mediaStartNodeIds`: List<object> **required**
- `name`: string **required**
- `permissions`: List<object> **required**
- `userGroupIds`: List<object> **required**
- `userName`: string **required**

---

## DeleteUsersRequestModel

**Fields:**

- `userIds`: List<object> **required**

---

## DisableUserRequestModel

**Fields:**

- `userIds`: List<object> **required**

---

## EnableTwoFactorRequestModel

**Fields:**

- `code`: string **required**
- `secret`: string **required**

---

## EnableUserRequestModel

**Fields:**

- `userIds`: List<object> **required**

---

## InviteUserRequestModel

**Fields:**

- `email`: string **required**
- `id`: string (uuid), nullable
- `message`: string, nullable
- `name`: string **required**
- `userGroupIds`: List<object> **required**
- `userName`: string **required**

---

## NoopSetupTwoFactorModel

---

## PagedUserResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## ResendInviteUserRequestModel

**Fields:**

- `message`: string, nullable
- `user`: object **required**

---

## ResetPasswordUserResponseModel

**Fields:**

- `resetPassword`: string, nullable

---

## SetAvatarRequestModel

**Fields:**

- `file`: object **required**

---

## UnlockUsersRequestModel

**Fields:**

- `userIds`: List<object> **required**

---

## UpdateUserGroupsOnUserRequestModel

**Fields:**

- `userGroupIds`: List<object> **required**
- `userIds`: List<object> **required**

---

## UpdateUserRequestModel

**Fields:**

- `documentStartNodeIds`: List<object> **required**
- `email`: string **required**
- `hasDocumentRootAccess`: boolean **required**
- `hasMediaRootAccess`: boolean **required**
- `languageIsoCode`: string **required**
- `mediaStartNodeIds`: List<object> **required**
- `name`: string **required**
- `userGroupIds`: List<object> **required**
- `userName`: string **required**

---

## UserConfigurationResponseModel

**Fields:**

- `allowChangePassword`: boolean **required**
- `allowTwoFactor`: boolean **required**
- `canInviteUsers`: boolean **required**
- `passwordConfiguration`: object **required**
- `usernameIsEmail`: boolean **required**

---

## UserKindModel

**Enum values:** `Default`, `Api`

---

## UserOrderModel

**Enum values:** `UserName`, `Language`, `Name`, `Email`, `Id`, `CreateDate`, `UpdateDate`, `IsApproved`, `IsLockedOut`, `LastLoginDate`

---

## UserPermissionsResponseModel

**Fields:**

- `permissions`: List<object> **required**

---

## UserResponseModel

**Fields:**

- `avatarUrls`: List<string> **required**
- `createDate`: string (date-time) **required**
- `documentStartNodeIds`: List<object> **required**
- `email`: string **required**
- `failedLoginAttempts`: integer (int32) **required**
- `hasDocumentRootAccess`: boolean **required**
- `hasMediaRootAccess`: boolean **required**
- `id`: string (uuid) **required**
- `isAdmin`: boolean **required**
- `kind`: → `UserKindModel` **required**
- `languageIsoCode`: string, nullable
- `lastLockoutDate`: string (date-time), nullable
- `lastLoginDate`: string (date-time), nullable
- `lastPasswordChangeDate`: string (date-time), nullable
- `mediaStartNodeIds`: List<object> **required**
- `name`: string **required**
- `state`: → `UserStateModel` **required**
- `updateDate`: string (date-time) **required**
- `userGroupIds`: List<object> **required**
- `userName`: string **required**

---

## UserStateModel

**Enum values:** `Active`, `Disabled`, `LockedOut`, `Invited`, `Inactive`, `All`

---

## VerifyInviteUserRequestModel

**Fields:**

- `token`: string **required**
- `user`: object **required**

---

## VerifyInviteUserResponseModel

**Fields:**

- `passwordConfiguration`: object **required**

---
