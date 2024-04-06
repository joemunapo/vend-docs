# Fetch Profile

This endpoint allows authenticated users to fetch their profile information.

**Method:** `GET`

**Endpoint:** `/profile`

**Headers:**

| Name          | Value                |
|---------------|----------------------|
| Content-Type  | application/json     |
| Authorization | Bearer {access_token} |

**Responses:**

- 200 OK:
  ```json
  {
    "success": true,
    "message": "Profile fetched successfully.",
    "data": {
      "first_name": "John",
      "last_name": "Doe",
      "dob": "2000-01-01",
      "phone": "263775123456",
      "id_number": "71-123456X55",
      "user_number": 123456,
      "business": {
        "id": 1,
        "business_name": "Xash Technologies",
        "business_category": "IT",
        "bp_number": "BP12345678",
        "home_address": {
          "address_line_1": "123 Main St",
          "address_line_2": null,
          "city": "Mutare"
        },
        "business_address": {
          "business_address_line_1": "456 Business Ave",
          "business_address_line_2": null,
          "business_city": "Mutare"
        }
      }
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

Upon successful authentication, the endpoint returns a JSON response with the user's profile information, including their personal details and associated business details (if any).

The response includes the following fields:

- `first_name`: The user's first name.
- `last_name`: The user's last name.
- `dob`: The user's date of birth in the format "YYYY-MM-DD".
- `phone`: The user's phone number in E.164 format without the leading "+".
- `id_number`: The user's identification number.
- `user_number`: The user's unique user number.
- `business` (optional): The user's associated business details, including:
  - `id`: The business ID.
  - `business_name`: The name of the business.
  - `business_category`: The category of the business.
  - `bp_number`: The business partner number.
  - `home_address`: The user's home address details.
  - `business_address`: The business address details.

If the user is not authenticated or the access token is invalid, a 401 Unauthorized response is returned.

Note: The presence of the `business` field in the response depends on whether the user has created a business using the [Create Business](./create-business.md) endpoint.