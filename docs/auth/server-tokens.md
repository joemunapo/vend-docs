# Server Tokens

Use **server tokens** for long-lived server integrations. Session `token` is for portal login only and may rotate.

Server tokens can be revoked individually without logging out of the portal.

## List server tokens

**Method:** `GET`

**Endpoint:** `/api/v1/auth/server-tokens`

### Headers

| Name | Value |
| :--- | :--- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

### Response

```json
{
  "success": true,
  "message": "Server tokens retrieved.",
  "data": [
    {
      "id": 12,
      "name": "My VPS",
      "last_used_at": "2025-01-12T10:20:30.000000Z",
      "created_at": "2025-01-10T09:05:00.000000Z"
    }
  ]
}
```

## Create server token

**Method:** `POST`

**Endpoint:** `/api/v1/auth/server-tokens`

### Headers

| Name | Value |
| :--- | :--- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

### Body

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `name` | string | No | Optional label for the token. |

### Example request

```json
{
  "name": "My VPS"
}
```

### Response

The `token` value is returned **once**. Store it securely.

```json
{
  "success": true,
  "message": "Server token created.",
  "data": {
    "id": 13,
    "name": "My VPS",
    "token": "svt_************************"
  }
}
```

## Revoke server token

**Method:** `DELETE`

**Endpoint:** `/api/v1/auth/server-tokens/{id}`

### Headers

| Name | Value |
| :--- | :--- |
| Authorization | Bearer {token} |
| Content-Type | application/json |

### Response

```json
{
  "success": true,
  "message": "Server token revoked."
}
```
