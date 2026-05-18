# Delete Audit Log | AI in Umbraco

Delete a specific audit log entry.

Request

```
DELETE /umbraco/ai/management/api/v1/audit-logs/{id}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `id` | guid | Audit log unique identifier |

Response

Success

```
(empty response body)
```

Not Found

```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "detail": "Audit log not found"
}
```

Examples

Last updated

Was this helpful?