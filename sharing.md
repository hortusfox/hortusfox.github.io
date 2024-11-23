## Custom Sharing Backend

This document describes the requirements to implement your own photo sharing backend. Implementing your own photo sharing backend is only required if you want to provide your own web service for letting your users share workspace photos instead of the official hortusfox.com backend.

Your backend needs to provide two API routes. After you have successfully set up your own backend, you can then set the URL of your backend via the admin dashboard.

## Share photo

This endpoint is used to share a photo.

```
POST /api/photo/share
```

Arguments:
- **title**: Title of photo (String)
- **workspace**: Name of workspace (String)
- **public**: Whether a photo is public or private (Boolean)
- **description**: Description of the photo (String, optional)
- **keywords**: Keywords of the photo for categorization (String, optional, separated by spaces)
- **hortusfox_photo**: The actual sent image file (File resource)

Successful response:

```json
{
    "code": 200,
    "data": {
        "ident": "Item identifier",
        "url": "URL to photo (prettified)",
        "asset": "Full URL to image asset",
        "public": "Flag to indicate if public or private"
    }
}
```

Error response:

```json
{
    "code": 500,
    "msg": "String with further information"
}
```

## Remove photo

This endpoint is used to remove a photo upon request

```
ANY /api/photo/remove
```

Arguments:
- **ident**: Identifier of the photo (String, previously retrieved via `ident` property)
- **ret**: Identifier of how to respond (String). Typical behaviour in this context is to return JSON

Successful response:

```json
{
    "code": 200
}
```

Error response:

```json
{
    "code": 500,
    "msg": "String with further information"
}
```

<p><hr/></p>

[Go back](index.md)