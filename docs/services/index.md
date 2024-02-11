### Services API

#### Description
The Services API provides a list of all active services available for transactions, such as utility payments for electricity, television subscriptions, and more. Each service comes with a unique identifier, name, commission rate, and a slug that can be used to reference the service in further API calls.

#### Route
- **Method:** GET
- **URL:** `/v1/services`

#### Headers
- **Content-Type:** application/json
- **Authorization:** Bearer \<User's Access Token\>

#### Response
The response enumerates the services that are active and available for use, detailing their names, the commission rate applicable to transactions involving the service, and a slug for identifying the service type.

#### Response Status Codes
- **200 OK**: Successfully retrieved the list of services.
- **401 Unauthorized**: The request lacks valid authentication credentials or the token is expired/invalid.

#### Example Response
```json
{
  "message": "Available services",
  "data": [
    {
      "id": 1,
      "name": "ZESA",
      "commission": "2.50",
      "slug": "electricity"
    }
    // ... other services
  ]
}
```

#### Notes
- The `slug` field in each service object is particularly useful for making targeted API calls for specific services.
- The `commission` rate included in the response indicates the percentage of the transaction amount that will be taken as a commission.
- Active services are those that are currently available for transactions, and their availability may change over time.
- Developers should periodically query this endpoint to fetch the latest list of services available for transactions within their applications.