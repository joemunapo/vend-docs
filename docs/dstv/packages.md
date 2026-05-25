# DStv Packages

This endpoint returns active DStv packages for the user to select.

**Method:** GET

**Endpoint:** `/api/v1/dstv/packages`

### Headers

| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |
| Content-Type  | application/json |

### Responses

#### Success Response:
```json
{
  "success": true,
  "message": "DStv packages retrieved successfully.",
  "data": [
    {
      "name": "Compact",
      "slug": "compact",
      "amount": 32
    },
    {
      "name": "Access",
      "slug": "access",
      "amount": 16
    }
  ]
}
```

The response includes one row per package. Show this list to the user, then send the selected package's `slug` as `package_slug` on lookup, purchase, or change package requests.

The response includes:
- `name`: The package name to display to the user
- `slug`: The value to send as `package_slug` on lookup and payment requests
- `amount`: The package amount in USD

Do not send the package amount back as a custom amount. Send only the selected `package_slug`.

#### Error Response:
```json
{
  "success": false,
  "message": "Unauthenticated."
}
```

[Previous](/dstv/index.md) | [Next](/dstv/lookup.md)
