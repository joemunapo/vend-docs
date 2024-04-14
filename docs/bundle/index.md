# Bundles

The Bundles API allows users to retrieve available bundles, purchase bundles directly, and buy bundle vouchers. It provides endpoints for browsing bundles, applying bundles to mobile numbers, and generating vouchers for later use.

## Available Endpoints

- [Available Bundles](/bundle/available-bundles.md)
  - `GET /api/v1/bundles` - Retrieve a list of available bundles filtered by currency and network.

- [Buy Direct Bundle](/bundle/buy-direct.md)
  - `POST /api/v1/bundles/buy/{bundle}` - Purchase a bundle and apply it directly to a mobile number.

- [Buy Bundle Voucher](/bundle/buy-voucher.md)
  - `POST /api/v1/bundles/voucher/buy/{bundle}` - Purchase a specified quantity of bundle vouchers.

## Authentication

All endpoints require authentication using a Bearer token. Include the token in the `Authorization` header of each request.

```
Authorization: Bearer {token}
```

## Error Handling

In case of an error, the API will respond with an appropriate HTTP status code and an error object in the following format:

```json
{
  "success": false,
  "message": "Error message"
}
```

Common error scenarios include:
- Insufficient funds in the user's wallet
- Invalid or missing parameters
- Attempting to purchase an invalid bundle or quantity

Refer to the individual endpoint documentation for specific error responses.

## Wallet and Commissions

Purchasing bundles and vouchers requires sufficient balance in the user's wallet. Upon successful purchases, the wallet balance will be updated accordingly.

The API also calculates and returns the earned commission for each purchase. Commissions are based on the configured rates for each carrier and bundle.

## Getting Started

To get started with the Bundles API, follow these steps:

1. Obtain an authentication token by logging in or registering a user account.
2. Browse the available bundles using the [Available Bundles](/bundle/available-bundles.md) endpoint.
3. Purchase bundles directly using the [Buy Direct Bundle](/bundle/buy-direct.md) endpoint, or buy vouchers using the [Buy Bundle Voucher](/bundle/buy-voucher.md) endpoint.
4. Monitor the user's wallet balance and earned commissions after each successful purchase.

For detailed information on each endpoint, request parameters, and response formats, refer to the respective endpoint documentation.