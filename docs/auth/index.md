# Introduction

Welcome to the documentation for the Authentication API. This API provides endpoints for user registration, authentication, and account management.

The API follows RESTful principles and uses JSON for data serialization. It provides a secure and efficient way to authenticate users and manage their accounts.

## Base URL

The base URL for all API endpoints is:

```
https://app.xash.co.zw # Live Server
https://dev.xash.co.zw # Development Server
```

All endpoints below are prefixed with `/api/v1`.

## Authentication

To access protected endpoints, include a session token in the `Authorization` header of your requests. The token should be prefixed with `Bearer`. For example:

```
Authorization: Bearer {token}
```

Session tokens are obtained through the [Login](/auth/login.md) and [Set Password](/auth/set-password.md) endpoints. The API returns `tokenType: "Bearer"`.

## Token Types

- **Session tokens** are for portal login only and may rotate.
- **Server tokens** are for long-lived server integrations. They can be revoked individually without logging out of the portal.

## Endpoints

The following endpoints are available in the Authentication API:

- [Registration](/auth/registration.md)
- [Set Password](/auth/set-password.md)
- [Resend User Number](/auth/resend-user-number.md)
- [Login](/auth/login.md)
- [Logout](/auth/login.md#logout)
- [Change Password](/auth/change-password.md)
- [Create Business](/auth/create-business.md)
- [Fetch Profile](/auth/fetch-profile.md)
- [Server Tokens](/auth/server-tokens.md)

Click on the links above to navigate to the detailed documentation for each endpoint.

## Error Handling

The API returns appropriate HTTP status codes and error messages in case of any errors. The error responses follow a consistent format:

```json
{
  "success": false,
  "message": "Error message",
  "errors": {
    "field1": [
      "Error detail 1",
      "Error detail 2"
    ],
    "field2": [
      "Error detail"
    ]
  }
}
```

## Feedback and Support

If you have any questions, feedback, or need assistance, please contact our support team at support@xash.co.zw We appreciate your feedback and are committed to continuously improving the API.

Happy coding!
