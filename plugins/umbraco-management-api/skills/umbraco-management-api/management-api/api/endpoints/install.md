# Install — API Endpoints

See `schemas/install.md` for field definitions.

## Contents

### Install

- `GET /umbraco/management/api/v1/install/settings`
- `POST /umbraco/management/api/v1/install/setup`
- `POST /umbraco/management/api/v1/install/validate-database`

---

## Install

### `GET /umbraco/management/api/v1/install/settings`

**Gets install settings.**

Operation ID: `GetInstallSettings`

**Response 200:** `OneOf: → InstallSettingsResponseModel`

---

### `POST /umbraco/management/api/v1/install/setup`

**Performs installation setup.**

Operation ID: `PostInstallSetup`

**Request body:** `OneOf: → InstallRequestModel`


---

### `POST /umbraco/management/api/v1/install/validate-database`

**Validates database connection.**

Operation ID: `PostInstallValidateDatabase`

**Request body:** `OneOf: → DatabaseInstallRequestModel`


---
