# Fetch Profile

This endpoint allows authenticated users to fetch their services.

**Method:** `GET`

**Endpoint:** `/services/{user_number}`

**Headers:**

| Name          | Value                |
|---------------|----------------------|
| Content-Type  | application/json     |
| Authorization | Bearer {access_token} |

**Body:**

| Name        | Type    | Description                   |
|-------------|---------|-------------------------------|
| user_number | integer | The user's unique user number |

**Responses:**

- 200 OK:
  ```json
  {
     "message": "User Services retrieved successfully",
    "data": {
        "success": true,
        "user_number": "123456",
        "phone": "263775123456",
        "services": [
            "direct-airtime",
            "dstv",
            "electricity"
        ]
    }
  }
  ```

- 401 Unauthorized:
  ```json
  {
    "success": false,
    "message": "Unauthenticated."
  }
  ```

This endpoint requires authentication. The access token needs to be included in the `Authorization` header with the `Bearer` prefix.

Upon successful authentication, the endpoint returns a JSON response with the user's servies information.

The response includes the following fields:


- `phone`: The user's phone number in E.164 format without the leading "+".
- `user_number`: The user's unique user number.
- `services`: The user's associated services


If the user is not authenticated or the access token is invalid, a 401 Unauthorized response is returned.

Note: The presence of the `business` field in the response depends on whether the user has created a business using the [Create Business](/auth/create-business.md) endpoint.