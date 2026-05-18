# User — API Endpoints

See `schemas/user.md` for field definitions.

## Contents

### User

- `GET /umbraco/management/api/v1/filter/user`
- `GET /umbraco/management/api/v1/item/user`
- `POST /umbraco/management/api/v1/user`
- `DELETE /umbraco/management/api/v1/user`
- `GET /umbraco/management/api/v1/user`
- `GET /umbraco/management/api/v1/user/{id}`
- `DELETE /umbraco/management/api/v1/user/{id}`
- `PUT /umbraco/management/api/v1/user/{id}`
- `GET /umbraco/management/api/v1/user/{id}/2fa`
- `DELETE /umbraco/management/api/v1/user/{id}/2fa/{providerName}`
- `GET /umbraco/management/api/v1/user/{id}/calculate-start-nodes`
- `POST /umbraco/management/api/v1/user/{id}/change-password`
- `POST /umbraco/management/api/v1/user/{id}/client-credentials`
- `GET /umbraco/management/api/v1/user/{id}/client-credentials`
- `DELETE /umbraco/management/api/v1/user/{id}/client-credentials/{clientId}`
- `POST /umbraco/management/api/v1/user/{id}/reset-password`
- `DELETE /umbraco/management/api/v1/user/avatar/{id}`
- `POST /umbraco/management/api/v1/user/avatar/{id}`
- `GET /umbraco/management/api/v1/user/configuration`
- `GET /umbraco/management/api/v1/user/current`
- `GET /umbraco/management/api/v1/user/current/2fa`
- `DELETE /umbraco/management/api/v1/user/current/2fa/{providerName}`
- `POST /umbraco/management/api/v1/user/current/2fa/{providerName}`
- `GET /umbraco/management/api/v1/user/current/2fa/{providerName}`
- `POST /umbraco/management/api/v1/user/current/avatar`
- `POST /umbraco/management/api/v1/user/current/change-password`
- `GET /umbraco/management/api/v1/user/current/configuration`
- `GET /umbraco/management/api/v1/user/current/login-providers`
- `GET /umbraco/management/api/v1/user/current/permissions`
- `GET /umbraco/management/api/v1/user/current/permissions/document`
- `GET /umbraco/management/api/v1/user/current/permissions/media`
- `POST /umbraco/management/api/v1/user/disable`
- `POST /umbraco/management/api/v1/user/enable`
- `POST /umbraco/management/api/v1/user/invite`
- `POST /umbraco/management/api/v1/user/invite/create-password`
- `POST /umbraco/management/api/v1/user/invite/resend`
- `POST /umbraco/management/api/v1/user/invite/verify`
- `POST /umbraco/management/api/v1/user/set-user-groups`
- `POST /umbraco/management/api/v1/user/unlock`

---

## User

### `GET /umbraco/management/api/v1/filter/user`

**Gets a filtered collection of users.**

Operation ID: `GetFilterUser`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `orderBy` | query | → UserOrderModel | No |
| `orderDirection` | query | → DirectionModel | No |
| `userGroupIds` | query | List<string (uuid)> | No |
| `userStates` | query | List<`UserStateModel`> | No |
| `filter` | query | string | No |

**Response 200:** `OneOf: → PagedUserResponseModel`

---

### `GET /umbraco/management/api/v1/item/user`

**Gets a collection of user items.**

Operation ID: `GetItemUser`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `POST /umbraco/management/api/v1/user`

**Creates a new user.**

Operation ID: `PostUser`

**Request body:** `OneOf: → CreateUserRequestModel`


---

### `DELETE /umbraco/management/api/v1/user`

**Deletes multiple users.**

Operation ID: `DeleteUser`

**Request body:** `OneOf: → DeleteUsersRequestModel`


---

### `GET /umbraco/management/api/v1/user`

**Gets a paginated collection of users.**

Operation ID: `GetUser`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedUserResponseModel`

---

### `GET /umbraco/management/api/v1/user/{id}`

**Gets a user.**

Operation ID: `GetUserById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → UserResponseModel`

---

### `DELETE /umbraco/management/api/v1/user/{id}`

**Deletes a user.**

Operation ID: `DeleteUserById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `PUT /umbraco/management/api/v1/user/{id}`

**Updates a user.**

Operation ID: `PutUserById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → UpdateUserRequestModel`


---

### `GET /umbraco/management/api/v1/user/{id}/2fa`

**Lists two-factor providers for a user.**

Operation ID: `GetUserById2fa`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `List<object>`

---

### `DELETE /umbraco/management/api/v1/user/{id}/2fa/{providerName}`

**Disables two-factor authentication for a user.**

Operation ID: `DeleteUserById2faByProviderName`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `providerName` | path | string | Yes |


---

### `GET /umbraco/management/api/v1/user/{id}/calculate-start-nodes`

**Calculates start nodes for users.**

Operation ID: `GetUserByIdCalculateStartNodes`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → CalculatedUserStartNodesResponseModel`

---

### `POST /umbraco/management/api/v1/user/{id}/change-password`

**Changes a user's password.**

Operation ID: `PostUserByIdChangePassword`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → ChangePasswordUserRequestModel`


---

### `POST /umbraco/management/api/v1/user/{id}/client-credentials`

**Creates client credentials for a user.**

Operation ID: `PostUserByIdClientCredentials`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → CreateUserClientCredentialsRequestModel`


---

### `GET /umbraco/management/api/v1/user/{id}/client-credentials`

**Gets all client credentials for a user.**

Operation ID: `GetUserByIdClientCredentials`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `List<string>`

---

### `DELETE /umbraco/management/api/v1/user/{id}/client-credentials/{clientId}`

**Deletes client credentials for a user.**

Operation ID: `DeleteUserByIdClientCredentialsByClientId`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |
| `clientId` | path | string | Yes |


---

### `POST /umbraco/management/api/v1/user/{id}/reset-password`

**Resets a user's password.**

Operation ID: `PostUserByIdResetPassword`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Response 200:** `OneOf: → ResetPasswordUserResponseModel`

---

### `DELETE /umbraco/management/api/v1/user/avatar/{id}`

**Clears a user's avatar.**

Operation ID: `DeleteUserAvatarById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |


---

### `POST /umbraco/management/api/v1/user/avatar/{id}`

**Sets a user's avatar.**

Operation ID: `PostUserAvatarById`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | path | string (uuid) | Yes |

**Request body:** `OneOf: → SetAvatarRequestModel`


---

### `GET /umbraco/management/api/v1/user/configuration`

**Gets the user configuration.**

Operation ID: `GetUserConfiguration`

**Response 200:** `OneOf: → UserConfigurationResponseModel`

---

### `GET /umbraco/management/api/v1/user/current`

**Gets the current user.**

Operation ID: `GetUserCurrent`

**Response 200:** `OneOf: → CurrentUserResponseModel`

---

### `GET /umbraco/management/api/v1/user/current/2fa`

**Lists two-factor providers for the current user.**

Operation ID: `GetUserCurrent2fa`

**Response 200:** `List<object>`

---

### `DELETE /umbraco/management/api/v1/user/current/2fa/{providerName}`

**Disables two-factor authentication for the current user.**

Operation ID: `DeleteUserCurrent2faByProviderName`

| Param | In | Type | Required |
|-------|----|------|----------|
| `providerName` | path | string | Yes |
| `code` | query | string | No |


---

### `POST /umbraco/management/api/v1/user/current/2fa/{providerName}`

**Enables two-factor authentication for the current user.**

Operation ID: `PostUserCurrent2faByProviderName`

| Param | In | Type | Required |
|-------|----|------|----------|
| `providerName` | path | string | Yes |

**Request body:** `OneOf: → EnableTwoFactorRequestModel`

**Response 200:** `OneOf: → NoopSetupTwoFactorModel`

---

### `GET /umbraco/management/api/v1/user/current/2fa/{providerName}`

**Gets two-factor setup information.**

Operation ID: `GetUserCurrent2faByProviderName`

| Param | In | Type | Required |
|-------|----|------|----------|
| `providerName` | path | string | Yes |

**Response 200:** `OneOf: → NoopSetupTwoFactorModel`

---

### `POST /umbraco/management/api/v1/user/current/avatar`

**Sets the current user's avatar.**

Operation ID: `PostUserCurrentAvatar`

**Request body:** `OneOf: → SetAvatarRequestModel`


---

### `POST /umbraco/management/api/v1/user/current/change-password`

**Changes the current user's password.**

Operation ID: `PostUserCurrentChangePassword`

**Request body:** `OneOf: → ChangePasswordCurrentUserRequestModel`


---

### `GET /umbraco/management/api/v1/user/current/configuration`

**Gets the current user's configuration.**

Operation ID: `GetUserCurrentConfiguration`

**Response 200:** `OneOf: → CurrentUserConfigurationResponseModel`

---

### `GET /umbraco/management/api/v1/user/current/login-providers`

**Lists external login providers.**

Operation ID: `GetUserCurrentLoginProviders`

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/user/current/permissions`

**Gets permissions for the current user.**

Operation ID: `GetUserCurrentPermissions`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `OneOf: → UserPermissionsResponseModel`

---

### `GET /umbraco/management/api/v1/user/current/permissions/document`

**Gets document permissions for the current user.**

Operation ID: `GetUserCurrentPermissionsDocument`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/user/current/permissions/media`

**Gets media permissions for the current user.**

Operation ID: `GetUserCurrentPermissionsMedia`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |

**Response 200:** `OneOf: → UserPermissionsResponseModel`

---

### `POST /umbraco/management/api/v1/user/disable`

**Disables users.**

Operation ID: `PostUserDisable`

**Request body:** `OneOf: → DisableUserRequestModel`


---

### `POST /umbraco/management/api/v1/user/enable`

**Enables users.**

Operation ID: `PostUserEnable`

**Request body:** `OneOf: → EnableUserRequestModel`


---

### `POST /umbraco/management/api/v1/user/invite`

**Invites new users.**

Operation ID: `PostUserInvite`

**Request body:** `OneOf: → InviteUserRequestModel`


---

### `POST /umbraco/management/api/v1/user/invite/create-password`

**Creates an initial password for a user.**

Operation ID: `PostUserInviteCreatePassword`

**Request body:** `OneOf: → CreateInitialPasswordUserRequestModel`


---

### `POST /umbraco/management/api/v1/user/invite/resend`

**Resends a user invitation.**

Operation ID: `PostUserInviteResend`

**Request body:** `OneOf: → ResendInviteUserRequestModel`


---

### `POST /umbraco/management/api/v1/user/invite/verify`

**Verifies a user invitation.**

Operation ID: `PostUserInviteVerify`

**Request body:** `OneOf: → VerifyInviteUserRequestModel`

**Response 200:** `OneOf: → VerifyInviteUserResponseModel`

---

### `POST /umbraco/management/api/v1/user/set-user-groups`

**Updates user group assignments.**

Operation ID: `PostUserSetUserGroups`

**Request body:** `OneOf: → UpdateUserGroupsOnUserRequestModel`


---

### `POST /umbraco/management/api/v1/user/unlock`

**Unlocks users.**

Operation ID: `PostUserUnlock`

**Request body:** `OneOf: → UnlockUsersRequestModel`


---
