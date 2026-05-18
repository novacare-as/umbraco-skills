# Segment — API Endpoints

See `schemas/common.md` for field definitions.

## Contents

### Segment

- `GET /umbraco/management/api/v1/segment`

---

## Segment

### `GET /umbraco/management/api/v1/segment`

**Gets a paginated collection of segments.**

Operation ID: `GetSegment`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedSegmentResponseModel`

---
