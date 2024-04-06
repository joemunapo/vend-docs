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
| user_number           | integer | The user's unique user number | Required                                              |
| password              | string | The new password              | Required, min 8 characters, must include letters (mixed case), numbers, and symbols |
| password_confirmation | string | The confirmation of the new password | Required, must match the password field         |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Password set successfully.",
    "data": {
      "first_name": "John",
      "last_name": "Doe",
      "dob": "2000-01-01",
      "phone": "263775696233",
      "id_number": "71-123456X55",
      "user_number": 123456
    }
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
