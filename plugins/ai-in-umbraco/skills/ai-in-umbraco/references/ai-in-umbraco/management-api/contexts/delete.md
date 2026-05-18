# Delete Context | AI in Umbraco

Delete an AI context.

Request

```
DELETE /umbraco/ai/management/api/v1/contexts/{contextIdOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `contextIdOrAlias` | string | Context GUID or alias |

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
    "detail": "Context not found"
}
```

Examples

Last updated

Was this helpful?