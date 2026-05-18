# Delete Connection | AI in Umbraco

Delete an AI provider connection.

Endpoint

```
DELETE /umbraco/ai/management/api/v1/connections/{id}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `id` | guid | Connection ID (GUID only, not alias) |

Response

Success (200 OK)

404 Not Found

```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "detail": "Connection with ID '3fa85f64-5717-4562-b3fc-2c963f66afa6' not found"
}
```

Considerations

Examples

cURL

JavaScript

Safe Delete Pattern

Last updated

Was this helpful?