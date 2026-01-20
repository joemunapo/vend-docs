# Equal Voucher WiFi

This feature lets a user buy Equal WiFi vouchers by selecting a bundle, choosing a quantity, and completing a purchase. The app uses two endpoints: one to list available WiFi bundles and one to purchase vouchers.

## Base URL

The HTTP client is configured with `BASE_URL` from environment config, and all endpoints below are relative to that base.

## Authentication

Requests include the bearer token set by the request interceptor.

**Headers**

| Name | Value |
| --- | --- |
| Accept | application/json |
| Content-Type | application/json |
| Authorization | Bearer {token} |

## API Endpoints

### 1) List WiFi bundles

**Method:** GET
**Endpoint:** `/api/v1/wifi/vouchers`

**Response (200)**
The API returns a list of bundles in `data`.

```json
{
  "data": [
    {
      "amount": "10.00",
      "currency": "USD",
      "duration": 24,
      "data_limit": "1GB",
      "duration_in": "hours"
    }
  ]
}
```

**Fields**

| Name | Type | Description |
| --- | --- | --- |
| amount | string | Price for one voucher |
| currency | string | Currency code |
| duration | integer | Voucher duration (number) |
| data_limit | string | Data limit for the voucher |
| duration_in | string | Duration unit (e.g., hours, days) |

### 2) Buy WiFi vouchers

**Method:** POST
**Endpoint:** `/api/v1/wifi/vouchers/buy`

**Body**

| Name | Type | Description | Required |
| --- | --- | --- | --- |
| amount | string | Bundle price for one voucher | yes |
| currency | string | Currency code | yes |
| quantity | string | Number of vouchers to buy (UI allows 1-20) | yes |
| duration | integer | Bundle duration | yes |
| data_limit | string | Bundle data limit | yes |
| duration_in | string | Bundle duration unit | yes |

**Example request**

```json
{
  "amount": "10.00",
  "currency": "USD",
  "quantity": "2",
  "duration": 24,
  "data_limit": "1GB",
  "duration_in": "hours"
}
```

**Response (200)**
The API returns the purchase details in `data`.

```json
{
  "data": {
    "name": "Equal WiFi",
    "amount": "20.00",
    "currency": "USD",
    "commission": "0.50",
    "id": "txn_123",
    "balance": {
      "balance": "100.00",
      "currency": "USD",
      "profit_on_hold": "0.00"
    },
    "reference": "EQW-ABC123",
    "voucher_value": "10.00",
    "recharge_instructions": "Connect to Equal WiFi and enter the voucher PIN.",
    "receipt_footer": "Thank you for using Xash.",
    "created_at": "2024-01-03T12:34:56Z",
    "vouchers": [
      {
        "pin": "1234-5678-9012",
        "duration": 24,
        "amount": "10.00",
        "data_limit": "1GB",
        "duration_in": "hours"
      }
    ]
  }
}
```

**Response fields**

| Name | Type | Description |
| --- | --- | --- |
| name | string | Product name shown on receipt |
| amount | string | Total amount paid |
| currency | string | Currency code |
| commission | string | Commission for the transaction |
| id | string | Transaction ID |
| balance.balance | string | Updated wallet balance |
| balance.currency | string | Balance currency |
| balance.profit_on_hold | string | Profit on hold after transaction |
| reference | string | Purchase reference |
| voucher_value | string | Value for one voucher |
| recharge_instructions | string | Instructions for redeeming the voucher |
| receipt_footer | string | Footer text printed on receipt |
| created_at | string | Timestamp for purchase |
| vouchers | array | List of voucher objects |
| vouchers[].pin | string | Voucher PIN |
| vouchers[].duration | integer | Voucher duration |
| vouchers[].amount | string | Voucher amount |
| vouchers[].data_limit | string | Voucher data limit |
| vouchers[].duration_in | string | Voucher duration unit |

## Notes

- Transaction type in reporting is `equal_voucher`.
