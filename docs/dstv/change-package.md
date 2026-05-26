# Change DStv Package

This endpoint changes a DStv smartcard to the selected package and collects payment for that package.

**Method:** POST

**Endpoint:** `/api/v1/dstv/change-package`

Use this endpoint when the lookup response returns `requires_change_package: true`.

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
  "reference": "APP-ORDER-1002"
}
```

### Responses

#### Success Response:
```json
{
  "success": true,
  "message": "DStv package changed successfully.",
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

The response includes the same receipt fields as a standard purchase: `package.amount`, `package.fee`, and `reference`.

#### Error Response:
```json
{
  "success": false,
  "message": "DStv package change requires review.",
  "data": {
    "reference": "TXN-REFERENCE",
    "requires_review": true,
    "refund_status": "held_for_review"
  }
}
```

[Previous](/dstv/purchase.md)
