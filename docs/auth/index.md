# Introduction

Welcome to the documentation for the Authentication API. This API provides endpoints for user registration, authentication, and account management.

The API follows RESTful principles and uses JSON for data serialization. It provides a secure and efficient way to authenticate users and manage their accounts.

## Base URL

The base URL for all API endpoints is:

```
https://xv.xash.co.zw/api/v1 # Live Server
https://xvdev.xash.co.zw/api/v1 # Development Server
```

## Authentication

To access protected endpoints, you need to include an access token in the `Authorization` header of your requests. The access token should be prefixed with `Bearer`. For example:

```
Authorization: Bearer {access_token}
```

Access tokens are obtained through the [Login](login.md) endpoint and have an expiration time of 1 hour.

## Endpoints

The following endpoints are available in the Authentication API:

- [Registration](registration.md)
- [Set Password](set-password.md)
- [Resend User Number](resend-user-number.md)
- [Login](login.md)
- [Logout](login.md#logout)
- [Create Business](create-business.md)
- [Fetch Profile](fetch-profile.md)

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