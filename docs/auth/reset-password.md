# Reset Password

This endpoint allows users to reset their account password. It can be used when a user forgets their password or needs to change it for security reasons.

**Method:** `POST`

**Endpoint:** `/auth/reset-password`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |
| Authorization | Bearer {access_token} |

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
  "message": "Password has been reset successfully."
  }
  ```

- 400 Bad Request:
  ```json
  {
     
    "message": "Failed to reset password."
    
  }
  ```
