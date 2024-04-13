# Electricity

The Electricity API allows you to integrate electricity token purchasing functionality into your application. With this API, you can provide a seamless token buying experience for your users while handling all the necessary interactions with the electricity provider.

## Overview

To purchase electricity tokens, you need to follow these steps:

1. **Check User Account**: Verify the user's electricity account details by providing their meter number and the currency they wish to use for the purchase. This step ensures that the account is valid and retrieves essential information like the customer's name, address, and the meter's currency.

2. **Buy Tokens**: Once the account is verified, you can proceed with the token purchase. Provide the amount of electricity to buy, the currency to use for the transaction, and the user's meter number. Upon successful payment, the API will return the token details, including the token numbers, units, and other relevant information.

## API Endpoints

- [Check User Account](/electricity/verify-account.md): `POST /api/v1/electricity/check-account`
  - Verify the user's electricity account details before proceeding with the token purchase.

- [Buy Tokens](/electricity/buy-tokens.md): `POST /api/v1/electricity/buy-tokens`
  - Purchase electricity tokens for a verified account.

## Token Purchase Flow

To ensure a smooth token purchasing experience, follow these steps:

1. Call the "Check User Account" endpoint to verify the user's account details and retrieve the meter's currency.

2. Display the customer information to the user and allow them to enter the amount of electricity they want to purchase and the currency they wish to use for the transaction.

3. Call the "Buy Tokens" endpoint with the necessary parameters to initiate the token purchase. Ensure that the currency used for the transaction matches the meter's currency.

4. If the purchase is successful, display the token details to the user, including the token numbers, units, and any key change tokens (KCTs) if applicable. Clearly instruct the user to load the tokens into their meter in the strict order provided, especially if KCTs are present.

5. Update the user's balance and display the transaction summary, including the energy cost breakdown, tendered amount, and any earned commissions.

By following these steps and leveraging the Electricity API endpoints, you can seamlessly integrate electricity token purchasing into your application, providing a convenient and reliable service to your users.

For detailed information on each endpoint, request parameters, and response formats, please refer to the respective endpoint documentation:

- [Check User Account](/electricity/verify-account.md)
- [Buy Tokens](/electricity/buy-tokens.md)