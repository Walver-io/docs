# API Reference

This document provides detailed information about the Walver.io API endpoints.

## Authentication

The API supports two authentication methods:

### 1. Session-based Authentication

Used primarily for browser-based interactions:

1. Call the `/creator/login` endpoint with a valid wallet signature
2. The response will include a session cookie that should be included in subsequent requests

### 2. API Key Authentication

Recommended for server-to-server integrations:

1. Create an API key in the creator dashboard (under the "API Keys" tab)
2. Include the API key in the `X-API-Key` header for all requests that require authentication

Example:
```
X-API-Key: wvs_your_api_key_here
```

## Base URL

All API endpoints are relative to the base URL of your deployed instance, typically:

```
https://walver.io
```

## Rate Limiting

The API implements rate limiting to prevent abuse. Most endpoints are limited to 10 requests per minute per IP address. Some sensitive endpoints have stricter limits.

If you exceed the rate limit, you'll receive a `429 Too Many Requests` response.

## API Endpoints

### Verification Endpoints

#### Create Verification Link

Creates a new verification link that can be shared with users.

- **URL**: `/new`
- **Method**: `POST`
- **Authentication**: Required
- **Rate Limit**: 10 requests per minute
- **Request Body**:
  ```json
  {
    "id": "string",
    "service_name": "string",
    "webhook": "string",
    "chain": "string",
    "expiration": "string",
    "secret": "string",
    "redirect_url": "string",
    "one_time": false,
    "folder_id": "string",
    "custom_fields": [
      {
        "id": "string",
        "name": "string",
        "type": "string",
        "required": true,
        "description": "string"
      }
    ],
    "token_gate": false,
    "token_address": "string",
    "token_amount": 0,
    "is_nft": false,
    "force_email_verification": false,
    "force_telegram_verification": false,
    "force_twitter_verification": false
  }
  ```
- **Required Fields**:
  - `id`: A unique identifier for the verification
  - `service_name`: The name of your service
  - `chain`: One of the supported blockchains (solana, ethereum, polygon, etc.)
- **Optional Fields**:
  - `webhook`: URL to call when verification is complete
  - `expiration`: ISO format date when the verification link expires
  - `secret`: A secret key included in webhook calls for verification
  - `redirect_url`: URL to redirect users after successful verification
  - `one_time`: If true, the link can only be used once
  - `folder_id`: ID of a folder to associate this verification with
  - `custom_fields`: Array of custom fields to collect during verification
  - `token_gate`: Whether to enable token gating for this verification
  - `token_address`: The token address to check for token gating
  - `token_amount`: The minimum token amount required for successful verification
  - `is_nft`: Whether the token is an NFT
  - `force_email_verification`: Whether to require email verification using OTP
  - `force_telegram_verification`: Whether to require Telegram verification
  - `force_twitter_verification`: Whether to require Twitter verification
- **Response**:
  ```json
  {
    "verification_url": "string"
  }
  ```

#### Verify Signature

Verifies a wallet signature without creating a verification link.

- **URL**: `/api/verify-signature`
- **Method**: `POST`
- **Authentication**: Optional
- **Rate Limit**: 60 requests per minute
- **Request Body**:
  ```json
  {
    "wallet_address": "string",
    "message": "string",
    "signature": "string",
    "chain": "string"
  }
  ```
- **Required Fields**:
  - `wallet_address`: The wallet address being verified
  - `message`: The message that was signed
  - `signature`: The signature as a string (usually hex-encoded)
  - `chain`: The blockchain to use for verification
- **Response**:
  ```json
  {
    "valid": true
  }
  ```

#### Generate Authentication Message

Generates a message for wallet authentication.

- **URL**: `/api/generate-auth-message`
- **Method**: `POST`
- **Authentication**: No
- **Rate Limit**: 20 requests per minute
- **Request Body**:
  ```json
  {
    "wallet_address": "string",
    "chain": "string",
    "application_name": "string"
  }
  ```
- **Required Fields**:
  - `wallet_address`: The wallet address requesting authentication
  - `chain`: The blockchain to use
  - `application_name`: The name of your application
- **Response**:
  ```json
  {
    "message": "string"
  }
  ```

### Folder Endpoints

#### Create Folder

Creates a new folder for organizing verifications.

- **URL**: `/creator/folders`
- **Method**: `POST`
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "name": "string",
    "description": "string",
    "custom_fields": [
      {
        "id": "string",
        "name": "string",
        "type": "string",
        "required": true,
        "description": "string"
      }
    ]
  }
  ```
- **Required Fields**:
  - `name`: The name of the folder
- **Optional Fields**:
  - `description`: A description for the folder
  - `custom_fields`: Array of default custom fields for verifications in this folder
- **Response**:
  ```json
  {
    "id": "string",
    "name": "string",
    "description": "string",
    "creator": "string",
    "custom_fields": [],
    "created_at": "string"
  }
  ```

#### List Folders

Returns all folders for the authenticated creator.

- **URL**: `/creator/folders`
- **Method**: `GET`
- **Authentication**: Required
- **Response**:
  ```json
  [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "creator": "string",
      "custom_fields": [],
      "created_at": "string"
    }
  ]
  ```

#### Get Folder

Returns information about a specific folder.

- **URL**: `/creator/folders/{folder_id}`
- **Method**: `GET`
- **Authentication**: Required
- **URL Parameters**:
  - `folder_id`: The ID of the folder
- **Response**:
  ```json
  {
    "id": "string",
    "name": "string",
    "description": "string",
    "creator": "string",
    "custom_fields": [],
    "created_at": "string"
  }
  ```

#### Get Folder Verifications

Returns all verifications in a specific folder.

- **URL**: `/creator/folders/{folder_id}/verifications`
- **Method**: `GET`
- **Authentication**: Required
- **URL Parameters**:
  - `folder_id`: The ID of the folder
- **Response**:
  ```json
  [
    {
      "id": "string",
      "service_name": "string",
      "verification_url": "string",
      "created_at": "string",
      "verified_count": 0
    }
  ]
  ```

### API Key Endpoints

#### Create API Key

Creates a new API key for the authenticated creator.

- **URL**: `/creator/api-keys`
- **Method**: `POST`
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "name": "string",
    "description": "string"
  }
  ```
- **Required Fields**:
  - `name`: A name for the API key
- **Optional Fields**:
  - `description`: A description for the API key
- **Response**:
  ```json
  {
    "key": "string",
    "name": "string",
    "description": "string",
    "created_at": "string",
    "creator": "string"
  }
  ```
- **Note**: The API key is only shown once upon creation. Store it securely.

#### List API Keys

Returns all API keys for the authenticated creator.

- **URL**: `/creator/api-keys`
- **Method**: `GET`
- **Authentication**: Required
- **Response**:
  ```json
  [
    {
      "key": "string",
      "name": "string",
      "description": "string",
      "created_at": "string",
      "creator": "string"
    }
  ]
  ```

#### Delete API Key

Deletes an API key.

- **URL**: `/creator/api-keys/{api_key}`
- **Method**: `DELETE`
- **Authentication**: Required
- **URL Parameters**:
  - `api_key`: The API key to delete
- **Response**:
  ```json
  {
    "success": true,
    "message": "string"
  }
  ```

### Authentication Endpoints

#### Creator Login

Authenticates a creator using their wallet signature.

- **URL**: `/creator/login`
- **Method**: `POST`
- **Authentication**: No
- **Request Body**:
  ```json
  {
    "wallet_address": "string",
    "message": "string",
    "signature": "string",
    "chain": "string"
  }
  ```
- **Required Fields**:
  - `wallet_address`: The creator's wallet address
  - `message`: The message that was signed
  - `signature`: The signature
  - `chain`: The blockchain used for signing
- **Response**:
  ```json
  {
    "success": true,
    "wallet_address": "string"
  }
  ```
- **Note**: Sets a session cookie for authentication

#### Creator Logout

Logs out the currently authenticated creator.

- **URL**: `/creator/logout`
- **Method**: `POST`
- **Authentication**: Required
- **Response**:
  ```json
  {
    "success": true
  }
  ```
- **Note**: Clears the session cookie

## Error Handling

The API returns appropriate HTTP status codes and error messages for different scenarios:

- `400 Bad Request`: Invalid request parameters
- `401 Unauthorized`: Authentication failed
- `403 Forbidden`: Insufficient permissions
- `404 Not Found`: Resource not found
- `409 Conflict`: Resource already exists (e.g., duplicate verification ID)
- `422 Unprocessable Entity`: Validation error in request body
- `429 Too Many Requests`: Rate limit exceeded
- `500 Internal Server Error`: Server-side error

Error responses include a JSON body with details:

```json
{
  "detail": "Error description"
}
```

## Webhooks

When a verification is completed, Walver.io sends a webhook to the URL specified in the verification configuration. The webhook includes:

- **Headers**:
  - `Content-Type`: `application/json`
  - `X-Webhook-Signature`: HMAC-SHA256 signature (if secret is configured)
- **Body**:
  ```json
  {
    "id": "string",
    "wallet_address": "string",
    "verification_time": "string",
    "custom_fields": {},
    "signature": "string",
    "message": "string",
    "chain": "string"
  }
  ```

To verify the webhook signature:

```python
import hmac
import hashlib

def verify_webhook_signature(payload, signature, secret):
    expected = hmac.new(
        secret.encode(), 
        payload.encode(), 
        hashlib.sha256
    ).hexdigest()
    return hmac.compare_digest(expected, signature)
```

Your webhook endpoint should return a `200 OK` response to acknowledge receipt of the verification. 