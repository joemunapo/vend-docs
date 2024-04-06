# Create Business

This endpoint allows authenticated users to create a business.

**Method:** `POST`

**Endpoint:** `/auth/create-business`

**Headers:**

| Name          | Value                |
|---------------|----------------------|
| Content-Type  | application/json     |
| Authorization | Bearer {access_token} |

**Body:**

| Name                    | Type   | Description                           | Validation                                 |
|-------------------------|--------|---------------------------------------|-------------------------------------------|
| business_name           | string | The name of the business              | Required, min 2 characters, max 50 characters |
| business_category       | string | The category of the business          | Required                                    |
| bp_number               | string | The business partner number           | Optional                                    |
| address_line_1          | string | The home address line 1               | Required, min 3 characters, max 256 characters |
| address_line_2          | string | The home address line 2               | Optional, min 3 characters, max 256 characters |
| city                    | string | The home address city                 | Required, min 3 characters, max 256 characters |
| business_address_line_1 | string | The business address line 1           | Required, min 3 characters, max 256 characters |
| business_address_line_2 | string | The business address line 2           | Optional, min 3 characters, max 256 characters |
| business_city           | string | The business address city             | Required, min 3 characters, max 256 characters |

**Responses:**

- 201 Created:
  ```json
  {
    "success": true,
    "message": "Business created successfully.",
    "data": {
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
  ```

- 401 Unauthorized:
  ```json
  {
    "success": false,
    "message": "Unauthenticated."
  }
  ```

- 422 Unprocessable Entity:
  ```json
  {
    "success": false,
    "message": "Validation failed.",
    "errors": {
      "business_name": [
        "The business name field is required."
      ],
      "business_category": [
        "The business category field is required."
      ],
      "address_line_1": [
        "The address line 1 must be at least 3 characters."
      ],
      "city": [
        "The city field is required."
      ],
      "business_address_line_1": [
        "The business address line 1 must be at least 3 characters."
      ],
      "business_city": [
        "The business city field is required."
      ]
    }
  }
  ```
