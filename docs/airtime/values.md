# Get Carriers Values Endpoint

## Overview

Retrieve a list of pre-defined airtime values that are available for purchase for a specific carrier. This information is crucial for presenting users with valid purchase options.

## Endpoint Details

```
GET https://xvdev.xash.co.zw/api/v1/airtime/direct/{carrier}/values
```

Substitute `{carrier}` with the carrier's unique identifier. To obtain a list of valid carriers, refer to the `GET /airtime/direct/carriers` endpoint.

### Authorization

Include a bearer token in the request headers for authentication:

```plaintext
Authorization: Bearer YOUR_ACCESS_TOKEN
```

Replace `YOUR_ACCESS_TOKEN` with the token you received upon authentication.

### Request Example

```javascript
const axios = require("axios").default;

const options = {
  method: 'GET',
  url: 'https://xvdev.xash.co.zw/api/v1/airtime/direct/{carrier}/values',
  headers: { Authorization: 'Bearer YOUR_ACCESS_TOKEN' }
};

axios.request(options).then(response => {
  console.log(response.data);
}).catch(error => {
  console.error(error);
});
```

### Successful Response Example

```json
{
  "status": "success",
  "message": "Airtime values retrieved",
  "allow_custom_amount": false,
  "data": [0.5, 1, 2, 5, 10, 20]
}
```

The `data` array contains the airtime values that users can purchase. The `allow_custom_amount` indicates whether users can specify their own amounts.

## Contact Support

For more detailed integration guidance or to report an issue, contact our API support team