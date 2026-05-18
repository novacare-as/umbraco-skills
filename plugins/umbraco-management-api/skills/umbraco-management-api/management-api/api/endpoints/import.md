# Import — API Endpoints

See `schemas/import.md` for field definitions.

## Contents

### Import

- `GET /umbraco/management/api/v1/import/analyze`

---

## Import

### `GET /umbraco/management/api/v1/import/analyze`

**Analyzes an import file.**

Operation ID: `GetImportAnalyze`

| Param | In | Type | Required |
|-------|----|------|----------|
| `temporaryFileId` | query | string (uuid) | No |

**Response 200:** `OneOf: → EntityImportAnalysisResponseModel`

---
