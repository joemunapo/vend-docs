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

---

## Transaction Status

### [Check Status (Poll)](/deposit/poll.md)
**Verify Payment**
Since mobile payments are asynchronous, use this endpoint to poll the status of a transaction (e.g., check if the user has entered their PIN or if the counter payment is complete).