# Purchase DStv Package

This endpoint pays the selected DStv package amount to a smartcard.

**Method:** POST

**Endpoint:** `/api/v1/dstv/purchase`

Before calling this endpoint, call the lookup endpoint to confirm the smartcard details.

### Headers

| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |
| Content-Type  | application/json |

### Parameters

| Name              | Type   | Description                                      | Validation |
|-------------------|--------|--------------------------------------------------|------------|
| smart_card_number | string | The customer's DStv smartcard number             | Required, 5 to 20 digits |
| package_slug      | string | The selected package slug from the packages list | Required, active package |
| currency          | string | Payment currency                                 | Optional, must be USD when supplied |
| reference         | string | Your optional client reference                   | Optional, max 100 characters |

### Example Request

```json
{
  "smart_card_number": "5550001234",
  "package_slug": "compact",
  "reference": "APP-ORDER-1001"
}
```

### Responses

#### Success Response:
```json
{
  "success": true,
  "message": "DStv payment completed successfully.",
  "data": {
    "name": "Sample Customer",
    "smartcard": "5550001234",
    "services": [
      "DStv Compact Bouquet IS20"
    ],
    "package": {
      "name": "Compact",
      "slug": "compact",
      "amount": 35,
      "fee": 3
    },
    "reference": "TXN-REFERENCE"
  }
}
```

The response includes:
- `package.amount`: The USD amount charged to the customer, including the service fee
- `package.fee`: The service fee included in `package.amount`
- `reference`: The Xash transaction reference

#### Error Response:
```json
{
  "success": false,
  "message": "You do not have enough balance to make this transaction."
}
```

[Previous](/dstv/lookup.md)
