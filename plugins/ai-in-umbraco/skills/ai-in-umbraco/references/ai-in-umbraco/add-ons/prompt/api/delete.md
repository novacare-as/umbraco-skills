# Delete | AI in Umbraco

Delete a prompt.

Request

```
DELETE /umbraco/ai/management/api/v1/prompts/{idOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `idOrAlias` | string | Prompt GUID or alias |

Response

Success

```
(empty response body)
```

Not Found

```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "AIPrompt not found",
    "status": 404,
    "detail": "The specified prompt could not be found."
}
```

Examples

Last updated

Was this helpful?