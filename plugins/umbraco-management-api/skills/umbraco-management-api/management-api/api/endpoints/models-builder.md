# Models Builder — API Endpoints

See `schemas/models-builder.md` for field definitions.

## Contents

### Models Builder

- `POST /umbraco/management/api/v1/models-builder/build`
- `GET /umbraco/management/api/v1/models-builder/dashboard`
- `GET /umbraco/management/api/v1/models-builder/status`

---

## Models Builder

### `POST /umbraco/management/api/v1/models-builder/build`

**Builds models.**

Operation ID: `PostModelsBuilderBuild`


---

### `GET /umbraco/management/api/v1/models-builder/dashboard`

**Gets models builder dashboard data.**

Operation ID: `GetModelsBuilderDashboard`

**Response 200:** `OneOf: → ModelsBuilderResponseModel`

---

### `GET /umbraco/management/api/v1/models-builder/status`

**Gets models builder status.**

Operation ID: `GetModelsBuilderStatus`

**Response 200:** `OneOf: → OutOfDateStatusResponseModel`

---
