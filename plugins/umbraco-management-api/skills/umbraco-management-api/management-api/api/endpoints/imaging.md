# Imaging — API Endpoints

See `schemas/imaging.md` for field definitions.

## Contents

### Imaging

- `GET /umbraco/management/api/v1/imaging/resize/urls`

---

## Imaging

### `GET /umbraco/management/api/v1/imaging/resize/urls`

**Gets URLs for image resizing.**

Operation ID: `GetImagingResizeUrls`

| Param | In | Type | Required |
|-------|----|------|----------|
| `id` | query | List<string (uuid)> | No |
| `height` | query | integer (int32) | No |
| `width` | query | integer (int32) | No |
| `mode` | query | → ImageCropModeModel | No |
| `format` | query | string | No |

**Response 200:** `List<object>`

---
