### Check Electricity Account API

#### Description
This endpoint facilitates the verification of electricity account details by utilizing a meter number. It is designed to ascertain the existence of the electricity user and fetch pertinent customer information, including the full name and address. For accessing this endpoint, users are required to supply both the meter number and the currency, alongside a valid bearer token for authorization.

#### Route
- **Method:** POST
- **URL:** `/v1/electricity/check-account`

#### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<Your Access Token\>

#### Body Parameters
- **currency** (required): String. Specifies the currency associated with the meter for transaction purposes. Acceptable values include "USD" or "ZWL".
- **meter_number** (required): String. The electricity meter number that is subject to verification. It should be numeric and satisfy the minimum length criteria stipulated.

#### Response Status Codes
- **200 OK**: Indicates successful account verification, inclusive of details such as customer name, address, meter number, and the currency tied to the meter.
- **400 Bad Request**: Denotes validation errors which might stem from missing or invalid meter numbers, or the use of an unsupported currency.
- **401 Unauthorized**: Emanates when the request lacks a valid authorization token or if the token is expired/invalid.
- **500 Internal Server Error**: Signifies an error in processing the request which could arise from complications with the external service provider or unforeseen server issues.

#### Example Response
```json
{
  "success": true,
  "customer_name": "John Doe",
  "customer_address": "123 Elm Street, Harare",
  "meter_number": "0123456789",
  "meter_currency": "USD"
}
```

#### Notes
- Access to this API necessitates a valid bearer token, underscoring the requirement for user authentication prior to fetching sensitive account details.
- The endpoint interfaces with an external service provider to procure account details. Consequently, the precision and availability of the information are contingent upon the response from the external provider.
- The response payload includes a 'success' indicator that reflects the outcome of the verification alongside the customer's name, address, meter number, and currency.
- In scenarios where the external provider signals an error or if the account verification fails, the API dispenses a failure message advising the user to re-check the meter number and attempt again.
- Make sure to check this api before proceeding to purchase electricity