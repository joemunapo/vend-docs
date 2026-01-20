# Change Password

This endpoint allows authenticated users to change their password. It revokes session tokens only; server tokens stay active.

**Method:** `POST`

**Endpoint:** `/api/v1/auth/change-password`

**Headers:**

| Name | Value |
| --- | --- |
| Content-Type | application/json |
| Authorization | Bearer {token} |

**Body:**

| Name | Type | Description |
| --- | --- | --- |
| current_password | string | The user's current password |
| password | string | The new password |
| password_confirmation | string | Must match `password` |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Password changed successfully."
  }
  ```

- 422 Unprocessable Entity:
  ```json
  {
    "success": false,
    "message": "Validation failed.",
    "errors": {
      "current_password": [
        "The current password is incorrect."
      ],
      "password": [
        "The password must be at least 8 characters."
      ]
    }
  }
  ```
