# Models Builder Schemas

## Schemas in this file

- [ModelsBuilderResponseModel](#modelsbuilderresponsemodel)
- [OutOfDateStatusResponseModel](#outofdatestatusresponsemodel)
- [OutOfDateTypeModel](#outofdatetypemodel)

---

## ModelsBuilderResponseModel

**Fields:**

- `canGenerate`: boolean **required**
- `lastError`: string, nullable
- `mode`: string **required**
- `modelsNamespace`: string, nullable
- `outOfDateModels`: boolean **required**
- `trackingOutOfDateModels`: boolean **required**
- `version`: string, nullable

---

## OutOfDateStatusResponseModel

**Fields:**

- `status`: → `OutOfDateTypeModel` **required**

---

## OutOfDateTypeModel

**Enum values:** `OutOfDate`, `Current`, `Unknown`

---
