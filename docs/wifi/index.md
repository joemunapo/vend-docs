# Wifi Voucher

The Wifi Voucher API allows users to retrieve available wifi voucher, and buy wifi vouchers. It provides endpoints for browsing wifi voucher, applying wifi voucher to mobile numbers, and generating vouchers for later use.

## Available Endpoints

- [Available Wifi Vouchers](/wifi/available-vouchers.md)
  - `GET /api/v1/wifi/vouchers` - Retrieve a list of wifi vouchers grouped by camount, duration and data limit.

- [Buy Wifi Voucher](/wifi/buy-voucher.md)
  - `POST /api/v1/wifi/vouchers/buy` - Purchase a specified quantity of wifi vouchers.

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
- Attempting to purchase an invalid wifi voucher or quantity

Refer to the individual endpoint documentation for specific error responses.

## Wallet and Commissions

Purchasing wifi vouchers requires sufficient balance in the user's wallet. Upon successful purchases, the wallet balance will be updated accordingly.

The API also calculates and returns the earned commission for each purchase. Commissions are based on the configured rates for each wifi voucher.

## Getting Started

To get started with the wifi voucher API, follow these steps:

1. Obtain an authentication token by logging in or registering a user account.
2. Browse the available wifi vouchers using the [Available Wifi Voucher](/wifi/available-vouchers.md) endpoint.
3. Buy vouchers using the [Buy Wifi Voucher](/wifi/buy-voucher.md) endpoint.
4. Monitor the user's wallet balance and earned commissions after each successful purchase.

For detailed information on each endpoint, request parameters, and response formats, refer to the respective endpoint documentation.