---
icon: badge-check
---

# The Verification Process

This guide explains the wallet verification process from both the developer and user perspectives.

## Overview <a href="#verification-overview" id="verification-overview"></a>

The [Walver.io](https://walver.io) verification process involves these key steps:

1. **Create a Verification Link**: A developer or creator creates a verification link
2. **Share the Link**: The link is shared with users who need to verify their wallet
3. **User Connects Wallet**: The user visits the link and connects their wallet
4. **Message Signing**: The user signs a cryptographic message to prove ownership
5. **Custom Data Collection**: The user provides any additional required information
6. **Verification Completion**: The system verifies the signature and submits the data
7. **Webhook Notification**: A webhook notifies the application of the verification result
8. **User Redirection**: The user is redirected to the specified redirect URL

## Creating a Verification Link <a href="#verification-create-link" id="verification-create-link"></a>

Verification links can be created through:

* The [Walver.io creator dashboard](https://walver.io/creator/dashboard)
* The [API](https://walver.io/api/docs) (using direct HTTP requests)
* The [Python SDK](http://github.com/Walver-io/walver-sdk)

The minimum required information is:

* A unique identifier for the verification
* The service name (shown to users)
* The blockchain to verify against

Additional options include:

* Webhook URL for receiving verification data
* Secret key for secure webhook communication
* Redirect URL for users after verification
* One-time use flag
* Custom fields to collect from users
* Token gating requirements
* Folder assignment for organization
* Email, Telegram, or Twitter verification requirements

## The User Experience <a href="#verification-user-experience" id="verification-user-experience"></a>

When a user receives a verification link, they experience the following flow:

1. **Landing Page**: The user sees a verification page with your service name and instructions
2. **Custom Fields**: If configured, the user sees forms for additional required information
3. **Email Verification**: If enabled, the user verifies their email using a one-time code
4. **Social Media Verification**: If enabled, the user verifies their social media accounts
5. **Wallet Connection**: The user connects their wallet using a supported wallet adapter
6. **Message Signing**: The user is prompted to sign a unique message
7. **Token Verification**: If token gating is enabled, the system checks token ownership
8. **Completion**: Upon successful verification, the user sees a success message
9. **Redirection**: The user is redirected to the specified redirect URL (if configured)

## Verification Types <a href="#verification-types" id="verification-types"></a>

### Standard Verification

The basic verification confirms wallet ownership through cryptographic signature verification.

### Token-Gated Verification

Token-gated verifications add an additional requirement that the user must own a specific amount of a token or NFT.

Configuration options:

* **Token Address**: The contract address of the token
* **Token Amount**: The minimum amount required
* **Is NFT**: Whether the token is an NFT (defaults to false)

### Identity-Enhanced Verification

These verifications require additional identity verification through:

#### Email Verification

1. User provides their email address
2. System sends a one-time code to the email
3. User enters the code to verify ownership of the email

To enable:

```python
verification = walver.create_verification(
    # ... other parameters ...
    force_email_verification=True,
    custom_fields=[
        {
            "id": "email",
            "type": "email",
            "name": "Email Address",
            "required": True
        }
    ]
)
```

#### Telegram Verification

1. User provides their Telegram username
2. System generates a verification link for Telegram
3. User clicks the link which opens their Telegram app
4. User starts a conversation with the Walver bot
5. Bot verifies the user's Telegram account

To enable:

```python
verification = walver.create_verification(
    # ... other parameters ...
    force_telegram_verification=True,
    custom_fields=[
        {
            "id": "telegram",
            "type": "telegram",
            "name": "Telegram Username",
            "required": True
        }
    ]
)
```

#### Twitter Verification

1. User provides their Twitter username
2. System generates a verification link for Twitter
3. User posts a specific tweet with a verification code
4. System verifies the post to confirm ownership

To enable:

```python
verification = walver.create_verification(
    # ... other parameters ...
    force_twitter_verification=True,
    custom_fields=[
        {
            "id": "twitter",
            "type": "twitter",
            "name": "Twitter Username",
            "required": True
        }
    ]
)
```

## Custom Fields <a href="#custom-fields" id="custom-fields"></a>

Custom fields allow you to collect additional information during the verification process. Each field can be marked as required or optional.

### Available Field Types

| Type     | Description       | Validation                    |
| -------- | ----------------- | ----------------------------- |
| text     | Simple text input | None                          |
| email    | Email address     | Valid email format            |
| url      | URL               | Valid URL format              |
| twitter  | Twitter handle    | Valid Twitter username        |
| telegram | Telegram username | Valid Telegram username       |
| discord  | Discord username  | Valid Discord username format |
| number   | Numeric input     | Valid number                  |
| date     | Date input        | Valid date format             |
| wallet   | Wallet address    | Valid wallet address format   |

### Example Configuration

```python
custom_fields=[
    {
        "id": "email",
        "type": "email",
        "name": "Email Address",
        "required": True,
        "description": "We'll use this to contact you" 
    },
    {
        "id": "twitter",
        "type": "twitter",
        "name": "Twitter Username",
        "required": False,
        "description": "Optional: For social verification"
    },
    {
        "id": "age",
        "type": "number",
        "name": "Age",
        "required": True
    }
]
```

## Webhook Handling

When a verification is completed, [Walver.io](https://walver.io) can send the results to your webhook endpoint. The webhook payload includes:

```json
{
  "id": "verification_123",
  "wallet_address": "0x1234567890abcdef",
  "verification_time": "2023-05-01T12:34:56Z",
  "custom_fields": {
    "email": "user@example.com",
    "twitter": "@username",
    "age": "25"
  },
  "signature": "0x...",
  "message": "...",
  "chain": "solana"
}
```

If you specified a secret key, the request will include the secret key in the request body.

Your webhook should respond with a 200 OK status to acknowledge receipt of the verification.

## One-Time vs. Reusable Links

Verification links can be configured as one-time use or reusable:

* **One-Time**: The link can only be used for a single successful verification. Useful for unique registrations or sensitive verifications.
* **Reusable**: The link can be used multiple times by different users. Useful for ongoing verification programs or event check-ins.

To create a one-time link:

```python
verification = walver.create_verification(
    # ... other parameters ...
    one_time=True
)
```

## Expiration

You can set an expiration date for verification links. After this date, the link will no longer be valid for new verifications.

```python
from datetime import datetime, timedelta

expiration = datetime.utcnow() + timedelta(days=7)  # Expires in 7 days

verification = walver.create_verification(
    # ... other parameters ...
    expiration=expiration
)
```

## Folders and Organization

For easier management, verifications can be organized into folders. Folders can also have default custom fields that are applied to all verifications in that folder.

```python
# Create a folder with default custom fields
folder = walver.create_folder(
    name="Event Registration",
    description="Verifications for our upcoming event",
    custom_fields=[
        {
            "id": "email",
            "type": "email",
            "name": "Email Address",
            "required": True
        }
    ]
)

# Create a verification in the folder
verification = walver.create_verification(
    id="event_registration_001",
    service_name="Event Registration",
    chain="solana",
    folder_id=folder["id"]
)
```

## Security Considerations

To ensure the security of your verification process:

1. **Use HTTPS**: Always use HTTPS for webhooks and redirect URLs
2. **Set a Secret Key**: Use a secure random string as your webhook secret
3. **Verify Signatures**: Always verify webhook signatures using your secret
4. **Set Expirations**: Use expiration dates for time-sensitive verifications
5. **One-Time Links**: Use one-time links for sensitive verifications
6. **Rate Limiting**: Implement rate limiting on your webhook endpoints
7. **Secure Storage**: Store verification data securely and in compliance with privacy regulations
