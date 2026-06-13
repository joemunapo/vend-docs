# Login

This endpoint allows users to authenticate and obtain a session token. Users can log in with either their password or their 5-digit PIN.

**Method:** `POST`

**Endpoint:** `/api/v1/auth/login`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |

**Body:**

| Name        | Type    | Description                   | Validation |
|-------------|---------|-------------------------------|------------|
| user_number | integer | The user's unique user number | Required |
| password    | string  | The user's password           | Required when `pin` is not provided |
| pin         | string  | The user's 5-digit PIN        | Required when `password` is not provided, exactly 5 digits |

Use one of the following request shapes:

Password login:

```json
{
  "user_number": 123456,
  "password": "Password123!"
}
```

PIN login:

```json
{
  "user_number": 123456,
  "pin": "12345"
}
```

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Login successful.",
    "token": "JIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "tokenType": "Bearer",
    "has_address": true,
    "has_business": true
  }
  ```

- 401 Unauthorized:
  ```json
  {
    "success": false,
    "message": "Invalid user number, password or PIN"
  }
  ```

- 422 Unprocessable Entity:
  ```json
  {
    "success": false,
    "message": "Validation failed.",
    "errors": {
      "user_number": [
        "The user number field is required."
      ],
      "password": [
        "The password field is required when pin is not present."
      ],
      "pin": [
        "The pin field is required when password is not present."
      ]
    }
  }
  ```


# Logout

This endpoint allows authenticated users to logout and invalidate their session token.

**Method:** `POST`

**Endpoint:** `/api/v1/auth/logout`

**Headers:**

| Name          | Value                |
|---------------|----------------------|
| Authorization | Bearer {token} |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Logout successful."
  }
  ```

- 401 Unauthorized:
  ```json
  {
    "success": false,
    "message": "Unauthenticated."
  }
  ```
