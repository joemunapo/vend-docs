### Create Business API

#### Description
This endpoint is designed for users to add business information to their profile. It allows for the registration of a business name, category, BP number (optional), and both home and business addresses. This endpoint is only accessible to users who have not already registered a business or address with their profile.

#### Route
- **Method:** POST
- **URL:** `/v1/auth/create-business`

#### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<Your Access Token\>

#### Parameters
- **address_line_1** (required): String. The primary line of the user's home address.
- **address_line_2** (optional): String. The secondary line of the user's home address.
- **city** (required): String. The city of the user's home address.
- **business_name** (required): String. The name of the business.
- **business_category** (required): String. The category of the business.
- **bp_number** (optional): String. The business's BP number.
- **business_address_line_1** (required): String. The primary line of the business address.
- **business_address_line_2** (optional): String. The secondary line of the business address.
- **business_city** (required): String. The city of the business address.

#### Response Status Codes
- **200 OK**: Business information successfully added. The response includes a success message.
- **400 Bad Request**: Indicates that the profile already has a business or address registered.
- **500 Internal Server Error**: An error occurred during the process. The response includes an error message detailing the issue.

#### Example Response
```json
{
  "success": true,
  "message": "Business created successfully."
}
```

#### Notes
- This endpoint checks if the user already has an address or business registered to prevent duplicates.
- Detailed validation rules are applied to ensure that all provided information meets the required formats and lengths.
- The user must be authenticated with a valid access token to access this endpoint.