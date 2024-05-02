# Get All Agents

Retrieves a list of all active agents.

**Method:** GET

**Endpoint:** `/api/v1/agents`

**Description:** This endpoint allows you to retrieve a list of all active agents in the system.

**Headers:**

| Name          | Value            |
|---------------|------------------|
| Authorization | Bearer {token}   |
| Accept        | application/json |

**Parameters:** None

**Body:** None

**Example Response:**

```json
{
  "success": true,
  "message": "Agents retrieved successfully",
  "data": [
    {
      "id": 1,
      "name": "John Doe",
      "shop_name": "John Doe Shop",
      "phone": "+263716123456",
      "wa_link": "https://wa.me/1234567890",
      "address": "123, Main Street",
      "city": "Mutare"
    },
    {
      "id": 2,
      "name": "Jane Doe",
      "shop_name": "Jane Doe Shop",
      "phone": "+263775123456",
      "wa_link": "https://wa.me/263775123456",
      "address": "456, Main Street",
      "city": "Gweru"
    }
  ]
}
```