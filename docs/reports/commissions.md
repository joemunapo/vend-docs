# Commissions

This endpoint allows users to retrieve commission summaries for an account within a specified currency and date range.

**Method:** `GET`

**Endpoint:** `/reports/commission/{currency}/{range?}`

**Example:** `/reports/commission/usd/august?per_page=15`

**Headers:**

| Name         | Value            |
|--------------|------------------|
| Content-Type | application/json |

**Body:**

| Name       | Type   | Description                   | Validation                                             |
|------------|--------|-------------------------------|--------------------------------------------------------|
| currency | string | The currency for which the commissions are being retrieved. USD or Zig         | Required                                               |
| range  | string | 	(Optional) The time period for the report. Options include 'today', 'yesterday', 'this_month', 'last_month', or specific month names like 'april'. Defaults to the last 3 months if not provided.          | Required                                               |
                   

**Responses:**

- 201 Created:
  ```json
  {
    "success": true,
    "message": "Transactions retrieved successfully",
    "data": [
    "transaction_id": "TX12345",
      "date": "2024-08-30",
      "user": "John Doe",
      "amount": 100.00,
      "currency": "USD",
      "status": "Success",
      "type": "Commission",
      "related_transaction_id": "TX67890"
    ],
     "meta": {
        "total": 0,
        "per_page": 15,
        "current_page": 1,
        "last_page": 1,
        "from": null,
        "to": null
    }
    
  }
  ```

- 422 Unprocessable Entity:
  ```json
  {
    "success": false,
    "message": "Invalid period provided", 
  }
  ```
