# Set Password

This endpoint allows users to set their password after registration. It still supports the existing password-first flow and can optionally set a 5-digit PIN in the same request.

**Method:** `POST`

**Endpoint:** `/api/v1/auth/set-password`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |

**Body:**

| Name                  | Type   | Description                   | Validation                                             |
|-----------------------|--------|-------------------------------|--------------------------------------------------------|
| user_number           | integer | The user's unique user number that was sent by SMS | Required                                              |
| password              | string | The new password              | Required, min 8 characters |
| password_confirmation | string | The confirmation of the new password | Required, must match the password field         |
| pin                   | string | Optional 5-digit login PIN    | Optional, exactly 5 digits                         |
| pin_confirmation      | string | The confirmation of the PIN   | Required when `pin` is present, must match `pin`    |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Password set successfully.",
    "token": "JIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "tokenType": "Bearer",
    "has_address": false,
    "has_business": false
  }
  ```

- 422 Unprocessable Entity:
  ```json
  {
    "success": false,
    "message": "Validation failed.",
    "errors": {
      "password": [
        "The password must be at least 8 characters."
      ],
      "password_confirmation": [
        "The password confirmation does not match."
      ],
      "pin": [
        "The pin must be 5 digits."
      ]
    }
  }
  ```
