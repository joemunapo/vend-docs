### Wallet Query API

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
  "data": {
    "profile_phone": "+263771234567",
    "is_active": true,
    "balances": [
      {
        "ticker": "USD",
        "name": "US Dollar",
        "balance": 1.00
      },
      {
        "ticker": "ZWL",
        "name": "Zimbabwean Dollar",
        "balance": 0
      },
      {
        "ticker": "USDCOM",
        "name": "USD Commission",
        "balance": 1.00
      },
      {
        "ticker": "ZWLCOM",
        "name": "ZWL Commission",
        "balance": 0
      }
    ]
  }
}
```

#### Notes
- The `profile_phone` field represents the user's contact number linked to the wallet. In the response, it is shown with the international dialing code for clarity.
- The `is_active` boolean flag indicates whether the wallet is currently enabled for transactions.
- The balances are categorized by currency, with each entry showing the currency's ticker symbol, its full name, and the user's current balance.
- This endpoint is pivotal for maintaining user trust and providing them with the necessary tools to manage their finances within the app.