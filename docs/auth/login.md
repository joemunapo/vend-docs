### User Login API

#### Description
The User Login API endpoint authenticates users by their unique user number and password. Upon successful authentication, it issues a new token, ensuring that all previous tokens are invalidated. This endpoint is essential for maintaining secure user sessions within your application.

#### Route
- **Method:** POST
- **URL:** `/v1/auth/login`

#### Headers
- **Content-Type:** application/json

#### Body Parameters
- **user_number** (required): String. The user's unique identifier number.
- **password** (required): String. The user's password.

#### Response Status Codes
- **200 OK**: Login was successful. A new access token is provided in the response.
- **401 Unauthorized**: The login attempt failed due to invalid user number or password.

#### Example Response
```json
{
  "success": true,
  "accessToken": "newly_generated_access_token",
  "tokenType": "Bearer",
  "has_address": true,
  "has_business": true,
  "message": "Login successful."
}
```

#### Notes
- Upon login, the API returns a Bearer token which must be used in the Authorization header for subsequent requests that require authentication.
- The response also indicates whether the user has completed their address and business profile setup, which can be useful for directing the user flow post-login.
- It is important to handle the login credentials securely and prompt the user to re-enter their login details if a 401 status code is received.
- The API ensures that each successful login generates a new token and invalidates all others to maintain the security of the user session.