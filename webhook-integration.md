---
icon: webhook
---

# Webhook Integration

[Walver.io](https://walver.io) uses webhooks to notify your application when verifications are completed. This guide explains how to set up and handle webhook notifications securely.

## What are Webhooks?

Webhooks are HTTP callbacks that are triggered by specific events in [Walver.io](https://walver.io). When a user completes a verification, [Walver.io](https://walver.io) can send a POST request to a URL you specify, containing information about the verification.

This allows your application to:

* Receive real-time notifications of completed verifications
* Process verification data automatically
* Update user permissions based on verification results
* Trigger other actions in your application

## Setting Up Webhooks

### 1. Create a Webhook Endpoint

First, you need to create an endpoint in your application that can receive webhook notifications. This should be a public URL that [Walver.io](https://walver.io) can reach.

### 2. Configure the Webhook in [Walver.io](https://walver.io)

When creating a verification, specify your webhook URL and (optionally) a secret key:

Using the dashboard:

1. Go to the "Create Verification" page
2. Enter your webhook URL in the "Webhook URL" field
3. Enter a secure secret key in the "Webhook Secret" field
4. Complete the rest of the verification setup
5. Save your changes

Using the Python SDK:

```python
from walver_sdk import Walver

walver = Walver(api_key="your-api-key")

verification = walver.create_verification(
    id="verification_123",
    service_name="My Service",
    chain="solana",
    webhook="https://your-service.com/webhook",
    secret="your_webhook_secret"
)
```

### 3. Test Your Webhook

To test your webhook integration:

1. Create a verification with your webhook URL
2. Complete the verification process
3. Check your webhook endpoint logs to ensure the notification was received
4. Verify that your application processed the webhook correctly

## Webhook Payload

When a verification is completed, [Walver.io](https://walver.io) sends a JSON payload to your webhook endpoint containing the verification details:

```json
{
  "id": "verification_123",
  "wallet_address": "0x1234567890abcdef",
  "verification_time": "2023-05-01T12:34:56Z",
  "custom_fields": {
    "email": "user@example.com",
    "discord": "username#1234"
  },
  "signature": "0x...",
  "message": "...",
  "chain": "solana"
}
```

For token-gated verifications, the payload includes additional token information:

```json
{
  "id": "verification_123",
  "wallet_address": "0x1234567890abcdef",
  "verification_time": "2023-05-01T12:34:56Z",
  "custom_fields": {
    "email": "user@example.com"
  },
  "token_verification": {
    "token_address": "0x1234567890abcdef1234567890abcdef12345678",
    "required_amount": 100.0,
    "actual_amount": 250.0,
    "passed": true
  },
  "signature": "0x...",
  "message": "...",
  "chain": "ethereum"
}
```

## Securing Webhooks

### Using a Webhook Secret

To secure your webhook integration, you should always use a webhook secret. This is a shared secret key known only to your application and [Walver.io](https://walver.io). When a webhook is sent, [Walver.io](https://walver.io) includes the secret key in the request body.

### Best Practices for Webhook Security

1. **Always Use HTTPS**: Ensure your webhook endpoint uses HTTPS to encrypt data in transit
2. **Use a Strong Secret**: Generate a strong, random secret key for each webhook
3. **Verify Signatures**: Always verify the signature of incoming webhooks
4. **Implement Rate Limiting**: Protect your endpoint from excessive requests
5. **Log Verification Attempts**: Keep logs of webhook verification attempts
6. **Store Webhook Data Securely**: Handle and store webhook data securely
7. **Implement Idempotency**: Handle duplicate webhook deliveries gracefully

## Handling Webhook Failures

[Walver.io](https://walver.io) will attempt to deliver webhooks immediately after a verification is completed. However, if your endpoint is unavailable or returns an error, [Walver.io](https://walver.io) will retry the delivery using an exponential backoff strategy:

* First retry: 30 seconds after the initial attempt
* Second retry: 30 seconds after the first retry
* Third retry: 30 seconds after the second retry

After all retry attempts have failed, the webhook will be marked as failed.
