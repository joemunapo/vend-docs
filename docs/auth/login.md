# Login

This endpoint allows users to authenticate and obtain a session token.

**Method:** `POST`

**Endpoint:** `/api/v1/auth/login`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |

**Body:**

| Name        | Type    | Description                   |
|-------------|---------|-------------------------------|
| user_number | integer | The user's unique user number |
| password    | string  | The user's password           |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Login successful.",
    "token": "JIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "tokenType": "Bearer"
  }
  ```

- 401 Unauthorized:
  ```json
  {
    "success": false,
    "message": "Invalid credentials."
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
        "The password field is required."
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
