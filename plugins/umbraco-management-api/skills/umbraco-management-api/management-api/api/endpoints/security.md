# Security — API Endpoints

See `schemas/security.md` for field definitions.

## Contents

### Security

- `GET /umbraco/management/api/v1/security/configuration`
- `POST /umbraco/management/api/v1/security/forgot-password`
- `POST /umbraco/management/api/v1/security/forgot-password/reset`
- `POST /umbraco/management/api/v1/security/forgot-password/verify`

---

## Security

### `GET /umbraco/management/api/v1/security/configuration`

**Gets the security configuration.**

Operation ID: `GetSecurityConfiguration`

**Response 200:** `OneOf: → SecurityConfigurationResponseModel`

---

### `POST /umbraco/management/api/v1/security/forgot-password`

**Requests a password reset.**

Operation ID: `PostSecurityForgotPassword`

**Request body:** `OneOf: → ResetPasswordRequestModel`


---

### `POST /umbraco/management/api/v1/security/forgot-password/reset`

**Initiates password reset.**

Operation ID: `PostSecurityForgotPasswordReset`

**Request body:** `OneOf: → ResetPasswordTokenRequestModel`


---

### `POST /umbraco/management/api/v1/security/forgot-password/verify`

**Verifies a password reset token.**

Operation ID: `PostSecurityForgotPasswordVerify`

**Request body:** `OneOf: → VerifyResetPasswordTokenRequestModel`

**Response 200:** `OneOf: → VerifyResetPasswordResponseModel`

---
