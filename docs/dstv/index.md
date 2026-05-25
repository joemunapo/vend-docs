# DStv

The DStv API allows you to integrate Zimbabwe DStv subscription payments into your application. It supports package selection, customer lookup, payment, and package change flows.

## Overview

To process a DStv subscription, follow these steps:

1. **Get Packages**: Retrieve the current package list and pricing that should be shown to the user.

2. **Lookup Account**: Verify the smartcard number against the selected package. The lookup confirms the customer name and indicates whether the smartcard is already on the selected package.

3. **Purchase Package**: If the lookup confirms the smartcard is already on the selected package, submit the payment.

4. **Change Package**: If the lookup indicates that the selected package does not match the smartcard's current package, use the change package endpoint instead of the purchase endpoint.

## API Endpoints

- [Packages](/dstv/packages.md): `GET /api/v1/dstv/packages`
  - Retrieve active DStv packages with amount, fee, and total.

- [Lookup Account](/dstv/lookup.md): `POST /api/v1/dstv/lookup`
  - Verify a smartcard number before payment.

- [Purchase Package](/dstv/purchase.md): `POST /api/v1/dstv/purchase`
  - Pay for a smartcard that is already on the selected package.

- [Change Package](/dstv/change-package.md): `POST /api/v1/dstv/change-package`
  - Change the smartcard to the selected package and pay for that package.

## Payment Flow

1. Call the packages endpoint and let the user choose a package.

2. Call the lookup endpoint with the smartcard number and selected `package_slug`.

3. If `requires_change_package` is `false`, call the purchase endpoint.

4. If `requires_change_package` is `true`, call the change package endpoint.

5. Use the returned `amount`, `fee`, `total`, `reference`, and `transaction_reference` fields on the receipt.

All DStv amounts are in USD.

[Next](/dstv/packages.md)
