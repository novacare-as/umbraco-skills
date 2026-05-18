# Delete Profile | AI in Umbraco

Delete an AI profile.

Request

```
DELETE /umbraco/ai/management/api/v1/profiles/{profileIdOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `profileIdOrAlias` | string | Profile GUID or alias |

Response

Success

```
(empty body)
```

Not Found

```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "detail": "Profile not found"
}
```

Examples

Delete by ID

Delete by Alias

Considerations

Before Deleting

After Deleting

Last updated

Was this helpful?