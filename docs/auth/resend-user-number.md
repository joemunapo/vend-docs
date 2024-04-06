# Resend User Number

This endpoint allows users to request a resend of their user number.

**Method:** `POST`

**Endpoint:** `/auth/resend-user-number/{phone}`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |

**Parameters:**

| Name  | Type   | Description             |
|-------|--------|-------------------------|
| phone | string | The user's phone number in E.164 format without leading + |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "User number resent successfully."
  }
  ```

- 404 Not Found:
  ```json
  {
    "success": false,
    "message": "User not found."
  }
  ```
