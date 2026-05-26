# DStv

The DStv API allows you to integrate Zimbabwe DStv subscription payments into your application. It supports package selection, customer lookup, and payment flows.

## Overview

To process a DStv subscription, follow these steps:

1. **Get Packages**: Retrieve the current package list and pricing that should be shown to the user.

2. **Lookup Account**: Verify the smartcard number before payment. The lookup confirms the customer name and current services.

3. **Purchase Package**: Submit the payment for the selected package.

## API Endpoints

- [Packages](/dstv/packages.md): `GET /api/v1/dstv/packages`
  - Retrieve active DStv packages with the customer-pay USD amount.

- [Lookup Account](/dstv/lookup.md): `POST /api/v1/dstv/lookup`
  - Verify a smartcard number before payment.

- [Purchase Package](/dstv/purchase.md): `POST /api/v1/dstv/purchase`
  - Pay the selected package amount to the smartcard.

## Payment Flow

1. Call the packages endpoint and let the user choose a package.

2. Call the lookup endpoint with the smartcard number and selected `package_slug`.

3. Call the purchase endpoint with the same smartcard number and selected `package_slug`.

4. Use the returned `package.amount`, `package.fee`, and `reference` fields from the purchase response on the receipt.

All DStv amounts are in USD.

[Next](/dstv/packages.md)
