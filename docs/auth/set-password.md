# Set Password

This endpoint allows users to set their password after registration.

**Method:** `POST`

**Endpoint:** `/auth/set-password`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |

**Body:**

| Name                  | Type   | Description                   | Validation                                             |
|-----------------------|--------|-------------------------------|--------------------------------------------------------|
| user_number           | integer | The user's unique user number that was sent via WhatsApp | Required                                              |
| password              | string | The new password              | Required, min 8 characters, must include letters (mixed case), numbers, and symbols |
| password_confirmation | string | The confirmation of the new password | Required, must match the password field         |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Password set successfully.",
    "accessToken": "JIUzI1NiIsInR5cCI6IkpXVCJ9...", // DO NOT Use this key - to be Deprecated in favor of token for consistency
    "token": "JIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
  ```

- 422 Unprocessable Entity:
  ```json
  {
    "success": false,
    "message": "Validation failed.",
    "errors": {
      "password": [
        "The password must be at least 8 characters.",
        "The password must contain at least one uppercase and one lowercase letter.",
        "The password must contain at least one number.",
        "The password must contain at least one symbol."
      ],
      "password_confirmation": [
        "The password confirmation does not match."
      ]
    }
  }
  ```
