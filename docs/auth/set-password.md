### Set User Password API

#### Description
This endpoint is designed for newly registered users to set their password. It requires the user's unique number, provided during registration via WatsApp, and the new password. The password must meet specific security criteria, including a minimum length and the inclusion of uppercase and lowercase letters, numbers, and special characters. Once set, the user's phone is marked as registered, and an access token is generated for immediate use.

#### Route
- **Method:** POST
- **URL:** `/v1/auth/set-password`

#### Headers
- **Content-Type:** application/json

#### Parameters
- **user_number** (required): Integer. The unique user number assigned to the user upon registration.
- **password** (required): String. The new password for the user's account. Must be at least 8 characters long, include uppercase and lowercase letters, at least one digit, and one special character. The password must also be confirmed in the request.

#### Response Status Codes
- **200 OK**: Password set successfully. The response includes an access token for authentication and flags indicating whether the user has set up an address and a business.
- **419 Custom Status**: Indicates that the password has already been set, and the user should be directed to use the login page instead.

#### Example Response
```json
{
  "success": true,
  "accessToken": "your_access_token_here",
  "tokenType": "Bearer",
  "has_address": false,
  "has_business": false,
  "message": "Password has been set successfully."
}
```

#### Notes
- The `password` parameter must be confirmed in the request. This means that the request should include both the password and a password confirmation field that matches the password.
- The API response includes an `accessToken` which is a bearer token, to be used for authenticated requests to the API.
- Additional response fields `has_address` and `has_business` indicate whether the user has completed these parts of their profile setup, facilitating a smoother onboarding flow.