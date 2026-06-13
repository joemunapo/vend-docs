# Registration

This endpoint allows users to register for an account.

After a successful registration, Xash sends the user number by SMS. The same SMS may also include a short-lived PIN setup OTP. Existing integrations can continue with [Set Password](/auth/set-password.md). New integrations can use the OTP with [Set PIN](/auth/pin.md#set-pin) so the user can log in later with a 5-digit PIN.

**Method:** `POST`

**Endpoint:** `/api/v1/auth/register`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |

**Body:**

| Name       | Type   | Description                   | Validation                                             |
|------------|--------|-------------------------------|--------------------------------------------------------|
| first_name | string | The user's first name         | Required                                               |
| last_name  | string | The user's last name          | Required                                               |
| dob        | string | The user's date of birth      | Required, format: "YYYY-MM-DD", must be at least 11 years old |
| phone      | string | The user's phone number       | Required, valid Zimbabwe phone number, unique among completed profiles |
| email      | string | The user's email address      | Optional, valid email                                 |
| id_number  | string | The user's identification number | Required, unique among completed profiles          |

**Responses:**

- 201 Created:
  ```json
  {
    "success": true,
    "message": "Registration successful.",
    "data": {
      "first_name": "John",
      "last_name": "Doe",
      "dob": "2000-01-01",
      "phone": "263775123456",
      "id_number": "71-123456X55"
    }
  }
  ```

  The PIN setup OTP is delivered by SMS only and is not returned in this response.

- 422 Unprocessable Entity:
  ```json
  {
    "success": false,
    "message": "Validation failed.",
    "errors": {
      "phone": [
        "The phone has already been taken."
      ],
      "id_number": [
        "The id number has already been taken."
      ]
    }
  }
  ```
