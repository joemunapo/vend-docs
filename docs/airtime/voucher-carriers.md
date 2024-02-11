### Available Voucher Carriers API

#### Description
This endpoint lists all mobile carriers available on the platform that offer airtime vouchers. It provides end users with essential information to select a carrier from which they wish to purchase airtime vouchers.

#### Route
- **Method:** GET
- **URL:** `/v1/airtime/direct/voucher/carriers`

#### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<Your Access Token\>

#### Response
The response includes an array of carriers that offer airtime vouchers. For each carrier listed, the response provides the following details to aid in the selection process:
- **id**: Integer. The unique identifier of the carrier.
- **name**: String. The official name of the carrier.
- **commission**: Numeric. The commission percentage associated with voucher purchases from this carrier. (This information might be utilized internally and could be excluded from end-user documentation if it does not directly impact the user.)

#### Response Status Codes
- **200 OK**: Successfully retrieved the list of carriers offering airtime vouchers.

#### Example Response
```json
{
  "message": "Voucher airtime carriers",
  "data": [
    {
      "id": 1,
      "name": "Econet",
      "commission": 2.5
    },
    {
      "id": 2,
      "name": "Telecel",
      "commission": 3.0
    },
    {
      "id": 3,
      "name": "NetOne",
      "commission": 2.0
    }
  ]
}
```

#### Notes
- This API call specifically returns carriers that provide airtime vouchers, making it easier for users to identify their options for voucher purchases.
- The list is designed to be user-friendly, focusing on the carriers' names and including the unique identifier (id) for each carrier, which may be required for subsequent voucher purchase requests.