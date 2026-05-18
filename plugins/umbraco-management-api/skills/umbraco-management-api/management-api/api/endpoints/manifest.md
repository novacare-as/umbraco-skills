# Manifest — API Endpoints

See `schemas/common.md` for field definitions.

## Contents

### Manifest

- `GET /umbraco/management/api/v1/manifest/manifest`
- `GET /umbraco/management/api/v1/manifest/manifest/private`
- `GET /umbraco/management/api/v1/manifest/manifest/public`

---

## Manifest

### `GET /umbraco/management/api/v1/manifest/manifest`

**Gets all manifests.**

Operation ID: `GetManifestManifest`

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/manifest/manifest/private`

**Gets private manifests.**

Operation ID: `GetManifestManifestPrivate`

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/manifest/manifest/public`

**Gets public manifests.**

Operation ID: `GetManifestManifestPublic`

**Response 200:** `List<object>`

---
