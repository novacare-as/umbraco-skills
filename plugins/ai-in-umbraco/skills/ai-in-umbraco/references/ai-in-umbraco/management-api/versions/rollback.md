# Rollback | AI in Umbraco

Rollback an entity to a previous version.

Request

```
POST /umbraco/ai/management/api/v1/versions/{entityType}/{entityId}/{entityVersion}/rollback
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `entityType` | string | Entity type (`connection` , `profile` , `context` , `prompt` , `agent` ) |
| `entityId` | guid | Entity unique identifier |
| `entityVersion` | int | Version number to restore |

Response

Success

```
(empty response body)
```

Not Found

```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Rollback failed",
    "status": 404,
    "detail": "Version not found for this entity."
}
```

Examples

Notes

Last updated

Was this helpful?