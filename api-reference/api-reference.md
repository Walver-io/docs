---
description: This section provides detailed information about the Walver.io API endpoints.
icon: flag-checkered
---

# Getting started

## Authentication

The API supports two authentication methods:

### 1. Session-based Authentication

Used primarily for browser-based interactions:

1. Call the GET `/api/generate-login-message?wallet_address=your-wallet?selected_chain=chain`
2. You will receive an object containing a message to be signed, a nonce, and an expiration time for the message
3. You should sign the message with your wallet address and then call the POST `/api/login`with the request body like this:

```python
{
    "wallet_address": str
    "selected_chain": str
    "nonce": str
    "message": str
    "signature": list[int] OR str
}
```

* The response will include a session\_id that should be included in subsequent requests

### 2. API Key Authentication (most convenient)

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
