### Available Airtime Carriers API

#### Description
This endpoint lists all mobile carriers available on the platform that support direct airtime purchases. It is designed to provide end users with the necessary information to select a carrier for direct airtime recharge.

#### Route
- **Method:** GET
- **URL:** `/v1/airtime/direct/carriers`

#### Headers
- **Content-Type:** application/json

#### Response
The response includes an array of carriers that are available for direct airtime purchases, with each entry providing details about the carrier. For each carrier, the following information is included:
- **name**: String. The official name of the carrier.
- **commission**: Numeric. The commission percentage associated with airtime purchases from this carrier. (This field is for internal use and may not be displayed to the end user if not relevant.)

#### Response Status Codes
- **200 OK**: Successfully retrieved the list of available carriers for direct airtime purchases.

#### Example Response
```json
[
  {
    "name": "Econet",
    "commission": 2.5
  },
  {
    "name": "Telecel",
    "commission": 3.0
  },
  {
    "name": "NetOne",
    "commission": 2.0
  }
]
```

#### Notes
- This API call returns only carriers that support direct airtime purchases, simplifying the selection process for users looking to recharge airtime directly.
- The list provided to the end user focuses on the carriers' names, ensuring a straightforward selection process without overwhelming them with unnecessary details such as vouchers and bundles availability.
- The inclusion of the commission rate is optional and may be omitted in the user-facing documentation if it does not directly affect the end user's experience or decision-making process.