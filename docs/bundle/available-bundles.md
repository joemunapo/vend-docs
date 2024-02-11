### Available Bundles API

#### Description
This endpoint provides a list of available data and SMS bundles for purchase. Users can filter the bundles by currency and network to find the options best suited to their needs. Each bundle includes details such as the name, value (cost), network, validity period, and currency.

#### Route
- **Method:** GET
- **URL:** `/v1/bundles`

#### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<Your Access Token\>

#### Query Parameters
- **currency** (optional): String. Filters the bundles by the specified currency (e.g., "USD").
- **network** (optional): String. Filters the bundles by the specified mobile network (e.g., "Econet").

#### Response
The response includes an array of bundle options, each with the following details:
- **name**: String. The name of the bundle.
- **value**: Numeric. The cost of the bundle.
- **description**: String. A brief description of the bundle (this example shows an empty string, indicating that a description might not always be provided).
- **network**: String. The mobile network the bundle is available for.
- **valid_for**: Integer. The number of days the bundle is valid for.
- **currency**: String. The currency in which the bundle's value is expressed.

#### Response Status Codes
- **200 OK**: Successfully retrieved the list of available bundles.

#### Example Response
```json
{
  "bundles": [
    {
      "name": "SMS Daily Bundle 50SMS",
      "value": 0.15,
      "description": "",
      "network": "Econet",
      "valid_for": 7,
      "currency": "USD"
    },
    {
      "name": "SMS Daily Bundle 130SMS",
      "value": 0.35,
      "description": "",
      "network": "Econet",
      "valid_for": 7,
      "currency": "USD"
    }
  ]
}
```

#### Notes
- This API is useful for users looking to purchase data or SMS bundles, offering a variety of choices tailored to different needs and preferences.
- The inclusion of the `currency` and `network` filters in the request allows for a more customized user experience, ensuring that users can easily find bundles relevant to their specific requirements.
- The `valid_for` field provides users with information on how long the bundle will last, assisting them in making informed decisions based on their usage patterns.