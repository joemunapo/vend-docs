Based on the provided code and the log output, here's the updated documentation for the "Get All Banks" endpoint:

# Get All Banks

Retrieves a list of all active banks.

**Method:** GET

**Endpoint:** `/api/v1/banks`

**Description:** This endpoint allows you to retrieve a list of all active banks in the system.

**Headers:**

| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |
| Accept        | application/json |

**Example Response:**

```json
{
  "success": true,
  "message": "Banks retrieved successfully",
  "data": [
    {
      "name": "Stanbic Bank",
      "logo": "https://xash.co.zw/banks/stanbic.png",
      "account_name": "Xash Solutions",
      "account_number": "1234567890",
      "branch": "MUTARE"
    },
    {
      "name": "ZB Bank",
      "logo": "https://xash.co.zw/banks/zb.png",
      "account_name": "Xash Solutions",
      "account_number": "1234567890",
      "branch": "MUTARE"
    },
    {
      "name": "Steward Bank",
      "logo": "https://xash.co.zw/banks/steward.png",
      "account_name": "Xash Solutions",
      "account_number": "1234567890",
      "branch": "MUTARE"
    }
  ]
}
```