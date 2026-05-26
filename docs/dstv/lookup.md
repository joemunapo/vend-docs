# Lookup DStv Account

This endpoint verifies a DStv smartcard number before payment.

**Method:** POST

**Endpoint:** `/api/v1/dstv/lookup`

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

### Example Request

```json
{
  "smart_card_number": "5550001234",
  "package_slug": "compact"
}
```

### Responses

#### Success Response:
```json
{
  "success": true,
  "message": "DStv account verified successfully.",
  "data": {
    "name": "Sample Customer",
    "smartcard": "5550001234",
    "services": [
      "DStv Compact Bouquet IS20"
    ],
    "package": {
      "name": "Compact",
      "slug": "compact",
      "amount": 35
    }
  }
}
```

`package.amount` is the USD amount the customer pays for the selected package, including the service fee.

#### Error Response:
```json
{
  "success": false,
  "message": "Unable to verify DStv account.",
  "data": {
    "error_code": "DSTV_LOOKUP_FAILED"
  }
}
```

[Previous](/dstv/packages.md) | [Next](/dstv/purchase.md)
