# Upgrade — API Endpoints

See `schemas/upgrade.md` for field definitions.

## Contents

### Upgrade

- `POST /umbraco/management/api/v1/upgrade/authorize`
- `GET /umbraco/management/api/v1/upgrade/settings`

---

## Upgrade

### `POST /umbraco/management/api/v1/upgrade/authorize`

**Authorizes the upgrade.**

Operation ID: `PostUpgradeAuthorize`


---

### `GET /umbraco/management/api/v1/upgrade/settings`

**Gets upgrade settings.**

Operation ID: `GetUpgradeSettings`

**Response 200:** `OneOf: → UpgradeSettingsResponseModel`

---
