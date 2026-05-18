# Dynamic Root — API Endpoints

See `schemas/dynamic-root.md` for field definitions.

## Contents

### Dynamic Root

- `POST /umbraco/management/api/v1/dynamic-root/query`
- `GET /umbraco/management/api/v1/dynamic-root/steps`

---

## Dynamic Root

### `POST /umbraco/management/api/v1/dynamic-root/query`

**Gets dynamic roots.**

Operation ID: `PostDynamicRootQuery`

**Request body:** `OneOf: → DynamicRootRequestModel`

**Response 200:** `OneOf: → DynamicRootResponseModel`

---

### `GET /umbraco/management/api/v1/dynamic-root/steps`

**Gets dynamic root query steps.**

Operation ID: `GetDynamicRootSteps`

**Response 200:** `List<string>`

---
