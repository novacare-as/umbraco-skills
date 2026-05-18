# Delete Guardrail | AI in Umbraco

Delete an AI guardrail.

Request

```
DELETE /umbraco/ai/management/api/v1/guardrails/{guardrailIdOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `guardrailIdOrAlias` | string | Guardrail GUID or alias |

Response

Success

```
(empty response body)
```

Not Found

```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Guardrail not found",
    "status": 404,
    "detail": "The specified guardrail could not be found."
}
```

Examples

Last updated

Was this helpful?