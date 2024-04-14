## Available Bundles

This endpoint retrieves a list of available bundles.

**Method:** GET

**Endpoint:** `/api/v1/bundles`

Retrieves a list of available bundles grouped by network and currency. The response includes bundle details such as id, name, description, price, currency, network, and validity period.

### Parameters

| Name     | Type   | Description                                     | Validation |
|----------|--------|-------------------------------------------------|------------|
| currency | string | Filter bundles by currency (optional)           |            |
| network  | string | Filter bundles by mobile network name (optional)|            |

### Responses

#### Success Response:
```json
{
  "success": true,
  "message": "Available bundles",
  "data": [
    {
      "id": 1,
      "name": "Daily Bundle",
      "description": "500MB valid for 1 day",
      "price": 1,
      "currency": "USD",
      "network": "Carrier1",
      "valid_for": 1
    },
    ...
  ]
}
```

#### Error Response:
```json
{
  "success": false,
  "message": "Error message"
}
```

[Previous](/bundle/index.md) | [Next](/bundle/buy-direct.md)
