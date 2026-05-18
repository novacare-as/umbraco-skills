# Security Schemas

## Schemas in this file

- [ResetPasswordRequestModel](#resetpasswordrequestmodel)
- [ResetPasswordTokenRequestModel](#resetpasswordtokenrequestmodel)
- [SecurityConfigurationResponseModel](#securityconfigurationresponsemodel)
- [VerifyResetPasswordResponseModel](#verifyresetpasswordresponsemodel)
- [VerifyResetPasswordTokenRequestModel](#verifyresetpasswordtokenrequestmodel)

---

## ResetPasswordRequestModel

**Fields:**

- `email`: string **required**

---

## ResetPasswordTokenRequestModel

**Fields:**

- `password`: string **required**
- `resetCode`: string **required**
- `user`: object **required**

---

## SecurityConfigurationResponseModel

**Fields:**

- `passwordConfiguration`: object **required**

---

## VerifyResetPasswordResponseModel

**Fields:**

- `passwordConfiguration`: object **required**

---

## VerifyResetPasswordTokenRequestModel

**Fields:**

- `resetCode`: string **required**
- `user`: object **required**

---
