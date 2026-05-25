# DStv Packages

This endpoint returns active DStv packages and their current customer-facing pricing.

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
      "package": {
        "name": "Compact",
        "slug": "compact",
        "type": "bouquet",
        "amount": 32,
        "fee": 3,
        "total": 35
      },
      "amount": 32,
      "fee": 3,
      "total": 35
    }
  ]
}
```

The response includes:
- `package.name`: The package name to display to the user
- `package.slug`: The value to send as `package_slug` on lookup and payment requests
- `package.type`: The package type
- `amount`: The package amount in USD
- `fee`: The service fee in USD
- `total`: The total amount to charge in USD

#### Error Response:
```json
{
  "success": false,
  "message": "Unauthenticated."
}
```

[Previous](/dstv/index.md) | [Next](/dstv/lookup.md)
