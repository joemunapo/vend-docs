# Airtime

The Airtime API allows you to manage and process airtime purchases for various carriers. You can retrieve available carriers, purchase direct airtime, and manage voucher airtime.

## Overview

The Airtime API provides the following functionality:

- Retrieve a list of carriers that support direct airtime recharge.
- Purchase direct airtime for a mobile phone number.
- Retrieve a list of carriers that support voucher airtime.
- Retrieve available voucher values for a specific carrier.
- Purchase voucher airtime for a specific carrier.

## Authentication

To access the Airtime API endpoints, you need to include the `Authorization` header in your requests. The header should contain a valid token obtained through the authentication process. The token should be prefixed with `Bearer`. For example:

```
Authorization: Bearer {token}
```

## Endpoints

The following endpoints are available in the Airtime API:

- [Carriers](./carriers.md): Retrieve a list of carriers that support direct airtime recharge.
- [Buy Direct Airtime](./buy-direct-airtime.md): Purchase direct airtime for a mobile phone number.
- [Voucher Values](./voucher-values.md): Retrieve available voucher values for a specific carrier.
- [Buy Voucher Airtime](./buy-voucher-airtime.md): Purchase voucher airtime for a specific carrier.

## Error Handling

The Airtime API returns appropriate HTTP status codes and error messages in case of any errors. The error responses follow a consistent format:

```json
{
  "success": false,
  "message": "Error message"
}
```

## Feedback and Support

If you have any questions, feedback, or need assistance with the Airtime API, please contact our support team at support@xash.co.zw. We appreciate your feedback and are committed to improving the API based on your suggestions.

Happy coding!