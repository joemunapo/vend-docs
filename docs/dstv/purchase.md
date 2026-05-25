# Purchase DStv Package

This endpoint pays for a DStv smartcard that is already on the selected package.

**Method:** POST

**Endpoint:** `/api/v1/dstv/purchase`

Before calling this endpoint, call the lookup endpoint. Only use this endpoint when `requires_change_package` is `false`.

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
      "amount": 32,
      "fee": 3,
      "total": 35
    },
    "reference": "TXN-REFERENCE",
    "transaction_reference": "DSTV-REFERENCE"
  }
}
```

The response includes:
- `package.amount`: The package amount in USD
- `package.fee`: The service fee in USD
- `package.total`: The total charged in USD
- `reference`: The Xash transaction reference
- `transaction_reference`: The payment reference to print on the receipt

#### Package Change Required:
```json
{
  "success": false,
  "message": "This smartcard is not currently on the selected package. Use change package instead.",
  "data": {
    "name": "Sample Customer",
    "smartcard": "5550001234",
    "services": [
      "DStv Access Bouquet IS20"
    ],
    "requires_change_package": true,
    "package": {
      "name": "Compact",
      "slug": "compact",
      "amount": 32,
      "fee": 3,
      "total": 35
    }
  }
}
```

#### Error Response:
```json
{
  "success": false,
  "message": "You do not have enough balance to make this transaction."
}
```

[Previous](/dstv/lookup.md) | [Next](/dstv/change-package.md)
