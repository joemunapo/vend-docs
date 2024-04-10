### Wallet

#### Description
The Wallet Query API provides a real-time snapshot of a user's financial status within the application. It delivers crucial information about the availability and amounts of various currencies stored in the user's wallet, including any commission balances. It's a critical tool for users to manage and monitor their funds effectively.

#### Route
- **Method:** GET
- **URL:** `/v1/wallet`

#### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<User's Access Token\>

#### Response
Upon a successful request, the response includes detailed wallet information, such as the wallet's active status and the available balances in different currencies.

#### Response Status Codes
- **200 OK**: The request was successful, and the wallet information has been retrieved.
- **401 Unauthorized**: The request failed authentication due to an invalid or expired access token.

#### Example Response
```json
{
  "message": "Wallet retrieved successfully",
  "data":[
      {
        "currency": "USD",
        "name": "US Dollar",
        "balance": 1.00,
        "profit_on_hold": 0
      },
      {
        "currency": "ZiG",
        "name": "Zimbabwe Gold",
        "balance": 0,
        "profit_on_hold": 0
      },
  ]
}
```

#### Notes
- The balances are categorized by currency, with each entry showing the currency's symbol, its full name, and the user's current balance.