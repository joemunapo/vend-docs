# PIN Setup and Reset

The PIN flow lets users authenticate with a 5-digit PIN instead of typing a password every time. Password login remains supported for existing users.

PIN setup and reset use a short-lived OTP sent by SMS. The OTP expires after 10 minutes.

## Request PIN OTP

Use this endpoint when a user needs a PIN setup code after registration.

**Method:** `POST`

**Endpoint:** `/api/v1/auth/request-pin-otp`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |

**Body:**

Provide either `user_number` or `phone`.

| Name        | Type    | Description                   | Validation |
|-------------|---------|-------------------------------|------------|
| user_number | integer | The user's unique user number | Required when `phone` is not provided |
| phone       | string  | The user's phone number       | Required when `user_number` is not provided |

**Response:**

```json
{
  "success": true,
  "message": "PIN verification code sent.",
  "data": {
    "expires_in_minutes": 10
  }
}
```

## Set PIN

Use this endpoint to create a PIN with the OTP sent to the user.

**Method:** `POST`

**Endpoint:** `/api/v1/auth/set-pin`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |

**Body:**

Provide either `user_number` or `phone`.

| Name             | Type    | Description                   | Validation |
|------------------|---------|-------------------------------|------------|
| user_number      | integer | The user's unique user number | Required when `phone` is not provided |
| phone            | string  | The user's phone number       | Required when `user_number` is not provided |
| otp              | string  | OTP sent by SMS               | Required, exactly 5 digits |
| pin              | string  | New login PIN                 | Required, exactly 5 digits |
| pin_confirmation | string  | Confirmation of the new PIN   | Required, must match `pin` |

**Response:**

```json
{
  "success": true,
  "message": "PIN set successfully.",
  "token": "JIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "tokenType": "Bearer",
  "has_address": false,
  "has_business": false
}
```

## Forgot PIN

Use this endpoint when a user has forgotten their PIN. It sends a reset OTP by SMS.

**Method:** `POST`

**Endpoint:** `/api/v1/auth/forgot-pin`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |

**Body:**

Provide either `user_number` or `phone`.

| Name        | Type    | Description                   | Validation |
|-------------|---------|-------------------------------|------------|
| user_number | integer | The user's unique user number | Required when `phone` is not provided |
| phone       | string  | The user's phone number       | Required when `user_number` is not provided |

**Response:**

```json
{
  "success": true,
  "message": "PIN reset code sent.",
  "data": {
    "expires_in_minutes": 10
  }
}
```

## Reset PIN

Use this endpoint to set a new PIN with the forgot-PIN OTP.

**Method:** `POST`

**Endpoint:** `/api/v1/auth/reset-pin`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |

**Body:**

Provide either `user_number` or `phone`.

| Name             | Type    | Description                   | Validation |
|------------------|---------|-------------------------------|------------|
| user_number      | integer | The user's unique user number | Required when `phone` is not provided |
| phone            | string  | The user's phone number       | Required when `user_number` is not provided |
| otp              | string  | OTP sent by SMS               | Required, exactly 5 digits |
| pin              | string  | New login PIN                 | Required, exactly 5 digits |
| pin_confirmation | string  | Confirmation of the new PIN   | Required, must match `pin` |

**Response:**

```json
{
  "success": true,
  "message": "PIN reset successfully.",
  "token": "JIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "tokenType": "Bearer",
  "has_address": true,
  "has_business": true
}
```

## Errors

- `401 Unauthorized` means the login credentials are invalid.
- `422 Unprocessable Entity` means the OTP is invalid, expired, or the request validation failed.
- `429 Too Many Requests` means the login or OTP flow is being throttled. Wait before trying again.

Example expired OTP response:

```json
{
  "success": false,
  "message": "Invalid or expired PIN verification code."
}
```
