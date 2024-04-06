# Registration

This endpoint allows users to register for an account.

**Method:** `POST`

**Endpoint:** `/auth/register`

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
| phone      | string | The user's phone number       | Required, valid phone number in E.164 format without leading +, unique among profiles |
| email      | string | The user's email address      | Optional, valid email, unique among profiles           |
| id_number  | string | The user's identification number | Required, unique among profiles                     |

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
