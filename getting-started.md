---
icon: play
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Getting Started with Walver.io

This guide will help you get started with [Walver.io](https://walver.io), from creating an account to implementing your first wallet verification.

## Creating an Account

1. Visit [walver.io](https://walver.io) and click on the "Get started" button
2. Signup with email or connect your wallet (Solana, Ethereum, or other supported chains)
3. Sign a message to verify your wallet ownership if you connected your wallet, or choose a password and verify your email if you signed up with email
4. Your creator dashboard will be ready to use

## Understanding the Dashboard

After logging in, you'll be taken to the creator dashboard where you can:

* Create and manage verification links
* Organize verifications into folders
* View verification statistics
* Generate and manage API keys

## Creating Your First Verification

### Using the [Dashboard](https://walver.io/creator/dashboard)

1. From your dashboard, click on "Create Folder"
2. Fill in the required information:
   * **Name**: The name of your folder
   * **Description**: A description of the folder
3. Add custom fields if needed (email, social media handles, etc.)
4. Click "Create Folder"
5. From the folder, click "Create Verification"
6. Fill in the required information:
   * ### Basic options:
     * **Service Name**: The name of your service
     * **Expiration**: (Optional) The expiration date of the verification
     * **Redirect URL**: (Optional) Where to send users after successful verification
     * **One Time**: (Optional) Enable if the link should only be used once
   * ### Verification options:
     * **Blockchain**: The blockchain your users will connect with
     * **Force Email Verification**: (Optional) Enable if you want to force email verification
     * **Force Telegram Verification**: (Optional) Enable if you want to force telegram verification
     * **Force Twitter Verification**: (Optional) Enable if you want to force twitter verification
     * **Token Gate**: (Optional) Enable if the verification should be token gated
     * **Token Address**: (Optional) The address of the token to gate the verification
     * **Token Amount**: (Optional) The amount of the token to gate the verification
   * ### Advanced options:
     * **Webhook URL**: (Optional) Where verification results should be sent
     * **Internal ID**: (Optional) A unique identifier for the verification
     * **Secret Key**: (Optional) For securing webhook communications
7. Click "Create Verification"
8. Copy the generated verification URL to share with your users

### Using the [API](https://walver.io/api/docs)

You can also create verifications programmatically using the Walver API:

```bash
curl -X POST "https://walver.io/new" \
  -H "X-API-Key: your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "id": "verification_123",
    "service_name": "My Service",
    "chain": "solana",
    "webhook": "https://your-service.com/webhook",
    "secret": "your_webhook_secret",
    "custom_fields": [
      {
        "id": "email",
        "type": "email",
        "name": "Email Address",
        "required": true
      }
    ]
  }'
```

### Using the [Python SDK](https://github.com/Walver-io/walver-sdk/)

For Python applications, you can use our official SDK:

```python
from walver_sdk import Walver

# Initialize the client
walver = Walver(api_key="your-api-key")

# Create a verification
verification = walver.create_verification(
    id="verification_123",
    service_name="My Service",
    chain="solana",
    webhook="https://your-service.com/webhook",
    secret="your_webhook_secret",
    custom_fields=[
        {
            "id": "email",
            "type": "email",
            "name": "Email Address",
            "required": True
        }
    ]
)

# Get the verification URL
verification_url = verification["verification_url"]
print(f"Verification URL: {verification_url}")
```

## Handling Verifications

### Webhook Setup

When a user completes a verification, Walver will send a webhook to your specified URL with the verification data:

```json
{
  "id": "verification_123",
  "wallet_address": "0x1234567890abcdef",
  "verification_time": "2023-05-01T12:34:56Z",
  "custom_fields": {
    "email": "user@example.com"
  },
  "signature": "0x...",
  "message": "...",
  "chain": "solana"
}
```

Your webhook endpoint should:

1. Verify the webhook secret (if configured)
2. Process the verification data
3. Return a 200 OK response

### Security Considerations

* Always verify the webhook signature using your secret key
* Use HTTPS for your webhook endpoint
* Consider implementing rate limiting to prevent abuse
* Store verification data securely

## Next Steps

Now that you've created your first verification, you can:

* Explore [token gating](token-gating.md) to restrict access based on token ownership
* Set up [custom fields](verification-process.md#custom-fields) to collect additional information
* Organize your verifications into [folders](creator-dashboard.md#organizing-with-folders)
* Implement [email verification](verification-process.md#email-verification) for added security
* Integrate with [social media verification](verification-process.md#identity-enhanced-verification)
