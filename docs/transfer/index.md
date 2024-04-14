# Transfer Credit

The Transfer Credit API allows users to securely transfer funds from their account to another user's account within the system. The process involves two steps: initiating the transfer and confirming the transfer.

## Overview

To transfer funds to another user, follow these steps:

1. **Initiate Transfer**: The sender initiates the transfer by providing the recipient's user number, the amount to transfer, the currency, and an optional reference. The system validates the request, checks the recipient's existence, and verifies the sender's balance. If successful, a pending transfer record is created.

2. **Confirm Transfer**: The sender confirms the transfer by providing the transfer ID received in the initiate step. The system checks the sender's balance again and, if sufficient, transfers the funds to the recipient's account. The transfer record is then deleted, and the updated balance and transaction details are returned.

By separating the process into two steps, the API ensures secure and validated transfers between user accounts.

## API Endpoints

- [Initiate Transfer](/transfer/initiate-transfer.md): `POST /api/v1/transfer`
  - Initiates a transfer request by validating the recipient and sender's balance.

- [Confirm Transfer](/transfer/confirm-transfer.md): `POST /api/v1/transfer/confirm/{transfer}`
  - Confirms and completes a previously initiated transfer.

## Transfer Flow

1. The sender initiates a transfer by making a POST request to the [Initiate Transfer](/transfer/initiate-transfer.md) endpoint with the required parameters.

2. If the validation passes, a pending transfer record is created, and the transfer details are returned in the response.

3. The sender confirms the transfer by making a POST request to the [Confirm Transfer](/transfer/confirm-transfer.md) endpoint, providing the transfer ID received in the initiate step.

4. If the sender's balance is sufficient, the funds are transferred to the recipient's account, the transfer record is deleted, and the updated balance and transaction details are returned.

By following this flow, users can securely transfer funds between accounts while ensuring proper validation and balance checks.

For detailed information on each endpoint, request parameters, and response formats, please refer to the respective endpoint documentation:

- [Initiate Transfer](/transfer/initiate-transfer.md)
- [Confirm Transfer](/transfer/confirm-transfer.md)