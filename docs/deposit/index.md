# Receive Funds

Welcome to the Receive Funds section. This module outlines the available methods for adding funds to a user's wallet.

Select a payment provider below to view the specific API implementation details.

## Available Methods

### [EcoCash](/deposit/eco.md)
**Direct Mobile Payment**
Initiate a real-time transaction that triggers a USSD push notification to the user's Econet mobile device. The user simply enters their PIN on their phone to authorize the fund transfer instantly.

### [InnBucks](/deposit/innbucks.md)
**Reference Code Payment**
Generate a unique payment reference code (token). Users can use this code to pay for the deposit at any InnBucks counter or complete the transaction directly within the InnBucks mobile app.

### [OMari](/deposit/omari.md)
**Mobile Wallet Payment**
Initiate a deposit request specifically for the OMari payment gateway.

### [Card](/deposit/card.md)
**Visa / Mastercard Payment**
Initiate a card checkout and handle any returned 3D Secure challenge HTML. Card deposits currently charge and credit USD.

### [Crypto](/deposit/crypto.md)
**USDT BEP20 Payment**
Create a CryptoPay deposit address and return the payment instructions your customer should use to send USDT on BEP20. Crypto deposits credit the USD wallet after the payment is confirmed on-chain.

### ZWG Mobile-Money Deposits

EcoCash, OMari, and InnBucks can bill the customer in ZWG while crediting the user's USD wallet. Send `charge_currency: "ZWG"` with the normal deposit request. The `amount` remains the USD wallet credit amount, and the response includes `charge_amount`, `charge_currency`, and `exchange_rate`.

You can also use the generic receive endpoint:

**Method:** POST

**Endpoint:** `/api/v1/payments/receive`

Send the same fields as the provider-specific endpoint, plus `method`.

```json
{
  "method": "ecocash",
  "amount": 10.00,
  "charge_currency": "ZWG",
  "ecocash_phone": "0771234567",
  "callback_url": "https://client.example.com/webhooks/xash/deposit?reference=ORDER_12345"
}
```

Allowed `method` values are `ecocash`, `innbucks`, `omari`, `card`, and `crypto`.

---

## Transaction Status

### [Check Status (Poll)](/deposit/poll.md)
**Verify Payment**
Since deposits are asynchronous, use this endpoint to poll the status of a transaction (e.g., check if the user has entered their PIN, if the counter payment is complete, or if a crypto payment is confirmed).
