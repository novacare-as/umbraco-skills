# Published Cache — API Endpoints

See `schemas/published-cache.md` for field definitions.

## Contents

### Published Cache

- `POST /umbraco/management/api/v1/published-cache/rebuild`
- `GET /umbraco/management/api/v1/published-cache/rebuild/status`
- `POST /umbraco/management/api/v1/published-cache/reload`

---

## Published Cache

### `POST /umbraco/management/api/v1/published-cache/rebuild`

**Rebuilds the published content cache.**

Operation ID: `PostPublishedCacheRebuild`


---

### `GET /umbraco/management/api/v1/published-cache/rebuild/status`

**Gets the rebuild cache status.**

Operation ID: `GetPublishedCacheRebuildStatus`

**Response 200:** `OneOf: → RebuildStatusModel`

---

### `POST /umbraco/management/api/v1/published-cache/reload`

**Reloads the published content cache.**

Operation ID: `PostPublishedCacheReload`


---
