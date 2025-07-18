---
icon: lock-keyhole
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

# Security Features

[Walver.io](https://walver.io) is designed with security as a top priority. This document outlines the security features and best practices implemented in the service.

## Cryptographic Message Signing

At the core of [Walver.io](https://walver.io)'s security model is cryptographic message signing, which ensures that only the true owner of a wallet can complete the verification process.

### How It Works

1. When a user connects their wallet to a verification page, [Walver.io](https://walver.io) generates a unique message containing:
   * A verification identifier
   * A timestamp
   * The wallet address being verified
   * A unique session identifier
2. The user signs this message using their wallet's private key, which never leaves their device.
3. The signature and message are sent to [Walver.io](https://walver.io)'s servers, where:
   * The signature is verified against the user's public key
   * The message contents are validated to ensure they haven't been tampered with
   * The timestamp is checked to prevent replay attacks

This process guarantees that the person completing the verification actually controls the wallet's private key, without ever exposing that key.

## Backend Verification

All cryptographic verification happens on the backend, which provides several security advantages:

1. **Tamper Resistance**: Client-side verification can be bypassed by modifying browser code or using developer tools. Backend verification prevents this.
2. **Consistent Validation**: The same validation logic is applied to all verifications, regardless of the client used.
3. **Protection Against MITM Attacks**: Malicious actors cannot intercept and modify the verification process.

## Secure Webhook Communications

Webhooks are secured using a user-defined secret key

1. When creating a verification, you can specify a secret key.
2. When Walver.io sends a webhook notification, it includes the secret key in the request body.
3. Your application can verify this secret key to ensure the webhook comes from Walver.io and hasn't been tampered with.

## API Key Management

[Walver.io](https://walver.io) implements secure API key management:

1. **Fine-grained Permissions**: API keys can be created with specific permissions (coming soon).
2. **Usage Tracking**: All API key usage is logged for security auditing.
3. **Key Rotation**: API keys can be easily created and deleted, facilitating regular key rotation.
4. **Single-View**: Full API keys are only shown once upon creation, requiring users to save them securely.

## Rate Limiting

To prevent abuse and brute force attacks, [Walver.io](https://walver.io) implements rate limiting:

1. Most API endpoints are limited to 10 requests per minute per IP address.
2. Sensitive endpoints, like those for signature verification, have more strict limits.
3. Rate limit information is included in response headers:
   * `X-RateLimit-Limit`: The maximum number of requests allowed per time period
   * `X-RateLimit-Remaining`: The number of requests remaining in the current time period
   * `X-RateLimit-Reset`: The time when the rate limit will reset

When rate limits are exceeded, the API returns a `429 Too Many Requests` response.

## Data Protection

[Walver.io](https://walver.io) implements multiple layers of data protection:

1. **HTTPS Everywhere**: All API endpoints and the web interface use HTTPS to encrypt data in transit.
2. **Data Minimization**: Only required data is collected and stored.
3. **Database Security**: Production data is stored in a secure database with access controls and encryption.
4. **Regular Backups**: Data is backed up regularly with a 7-day rotation to prevent data loss.

## Unique Message Generation

Each verification generates a unique message for signing, which includes:

1. A verification identifier
2. The service name requiring the verification
3. A timestamp
4. The wallet address
5. A session identifier

This prevents replay attacks where a signature from one verification could be reused for another.

## One-Time Verification Links

For sensitive verifications,[ Walver.io](https://walver.io) supports one-time use links:

1. Once a verification is successfully completed, the link becomes invalid.
2. This prevents the same link from being shared or reused by multiple people.
3. Ideal for sensitive verifications like token airdrops or exclusive access grants.

## Email and Social Media Verification

For enhanced identity verification, [Walver.io](https://walver.io) offers additional verification methods:

### Email Verification

1. Users provide their email address
2. [Walver.io](https://walver.io) sends a one-time verification code to the email
3. Users must enter this code to complete verification
4. This adds an additional layer of identity verification beyond wallet ownership

### Telegram Verification

1. Users provide their Telegram username
2. They are directed to start a conversation with the Walver bot with a specific payload
3. The bot verifies the payload and confirms the user owns the specified Telegram account
4. This confirms the user owns the specified Telegram account

### Twitter/X Verification

1. Users provide their Twitter/X username
2. They are instructed to follow a link to a verification page
3. They are instructed to click a button to verify their account
4. This confirms the user controls the Twitter account

### Discord Verification

1. Users provide their Discord username
2. They are instructed to follow a link to a verification page
3. They are instructed to click a button to verify their account
4. This confirms the user controls the Discord account

## Secure Deployment

The production environment uses Docker containers with:

1. **Minimal Base Images**: Reduces attack surface
2. **Non-Root Users**: Containers run as non-root users
3. **Read-Only Filesystems**: Where possible
4. **Resource Limitations**: Prevents DoS attacks
5. **Automatic Updates**: Security patches are applied regularly

## Security Monitoring

[Walver.io](https://walver.io) implements continuous security monitoring:

1. **Application Logging**: All significant actions are logged
2. **Error Tracking**: Errors are tracked and analyzed for security implications
3. **Usage Patterns**: Unusual usage patterns trigger alerts

## Security Best Practices for Users

When using [Walver.io](https://walver.io), we recommend these security best practices:

1. **Use Strong Secrets**: Use long, random webhook secrets and API keys
2. **Verify Signatures**: Always verify webhook signatures
3. **Use HTTPS**: Only use HTTPS for webhooks and redirect URLs
4. **Rotate Keys**: Regularly rotate API keys
5. **One-Time Links**: Use one-time links for sensitive verifications
6. **Set Expirations**: Use expiration dates for verification links
7. **Check Domains**: Ensure users are on the genuine walver.io domain

## Reporting Security Issues

If you discover a security vulnerability in [Walver.io](https://walver.io), please report it immediately:

1. Do not disclose the issue publicly
2. Email the security details to [security@walver.io](mailto:security@walver.io)
3. Include steps to reproduce the vulnerability
4. Allow time for the issue to be addressed before disclosure

## Security Roadmap

Walver.io is continuously improving its security features. Upcoming security enhancements include:

1. **Fine-grained API Key Permissions**: Limit what each API key can do
2. **Enhanced MFA**: Additional multi-factor authentication options for creator accounts
3. **Audit Logs**: Detailed logs of all actions for security compliance
4. **IP Restrictions**: Restrict API access by IP address
5. **Enhanced Fraud Detection**: Machine learning-based detection of suspicious activity
