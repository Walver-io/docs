# Frequently Asked Questions (FAQ)

## General Questions

### What is Walver.io?
Walver.io is a service that helps blockchain applications verify wallet ownership. It creates secure verification links that users can access to prove their ownership through cryptographic signatures. The service supports multiple blockchains including Solana, Ethereum, Polygon, and others.

### Which blockchains are supported?
Walver.io currently supports:
- Solana
- Ethereum
- Polygon
- Binance Smart Chain (BSC)
- Base
- Arbitrum
- Optimism
- Avalanche

### Does using Walver.io require coding?
No, Walver.io provides a user-friendly dashboard for creating and managing verifications without coding. However, for more advanced integrations, you can use the API or Python SDK.

### Is Walver.io free to use?
Right now, Walver.io is in beta and free to use. This will change in the future.

## Verification Process

### How does wallet verification work?
Wallet verification works by asking users to sign a cryptographic message with their wallet's private key. This proves that they own the wallet without revealing the private key. Walver.io handles this process securely and can also collect additional information from users.

### Can I collect information from users during verification?
Yes, you can configure custom fields to collect various types of information such as email addresses, social media handles, and more. Each field can be marked as required or optional.

### What happens after a user completes verification?
When a user completes verification, Walver.io:
1. Sends the verification data to your webhook endpoint (if configured)
2. Redirects the user to a success page or your custom redirect URL
3. Marks the verification as completed in the dashboard

### Can verifications expire?
Yes, you can set an expiration date when creating a verification. After this date, the verification link will no longer be valid.

### Can I limit a verification link to one-time use?
Yes, you can configure a verification to be one-time use only. After a successful verification, the link will no longer be usable.

## Token Gating

### What is token gating?
Token gating is a feature that restricts access based on token ownership. It verifies that users own a specific amount of tokens or NFTs before granting access to content or services.

### How does token gating work in Walver.io?
When creating a verification, you can enable token gating and specify:
1. The token address (contract address)
2. The minimum amount required
3. Whether it's an NFT

During verification, Walver.io checks the user's wallet balance against these requirements.

### Can I gate access based on NFT ownership?
Yes, you can create verifications that require ownership of specific NFTs by setting the `is_nft` flag to `true` and specifying the NFT contract address.

### Does Walver.io support multiple token conditions?
Currently, each verification can have one token condition. For more complex requirements, you can create multiple verifications or handle the logic in your application after receiving the webhook.

## Webhooks and Integration

### What is a webhook in the context of Walver.io?
A webhook is an HTTP callback that Walver.io sends to your application when a user completes a verification. It contains all the verification data, allowing your application to process verifications automatically.

### How secure are the webhooks?
Webhooks include a signature header that you can verify using your secret key to ensure the webhook came from Walver.io. This prevents tampering and spoofing.

### What if my webhook endpoint is temporarily unavailable?
Walver.io uses an exponential backoff retry strategy, attempting to deliver the webhook multiple times over a 24-hour period if your endpoint is unavailable.

### Can I test webhooks in a development environment?
Yes, you can set up verifications with your development webhook URL to test the integration before going to production.

## API and SDK

### Does Walver.io provide an API?
Yes, Walver.io offers a comprehensive API for creating and managing verifications programmatically.

### Is there an SDK available?
Yes, there is an official Python SDK (walver-sdk) that provides both synchronous and asynchronous clients for easy integration.

### How do I authenticate API requests?
API requests can be authenticated using API keys, which you can create and manage in the creator dashboard.

### Is there a rate limit on API calls?
Yes, most API endpoints are limited to 10 requests per minute per IP address, with some endpoints having different limits.

## Security

### How secure is the wallet verification process?
The verification process uses cryptographic signatures to securely verify wallet ownership without exposing private keys. All communications are encrypted using HTTPS.

### How should I secure my webhook endpoint?
You should:
1. Use HTTPS for your endpoint
2. Verify webhook signatures using your secret
3. Implement rate limiting
4. Follow security best practices for handling webhook data

### Can verifications be tampered with?
No, each verification includes cryptographic signatures that cannot be forged. Additionally, webhook payloads are signed with your secret key to prevent tampering.

### Is user data encrypted?
Yes, all data is transmitted over HTTPS. For specific details about data storage and encryption, please refer to the privacy policy.

## Custom Solutions

### Can I customize the verification page?
The verification page maintains a consistent design to ensure security and user trust. However, you can customize the service name and add your logo through the dashboard.

### Can Walver.io integrate with my existing user system?
Yes, using webhooks, you can integrate Walver.io verifications with your existing user management system.

### Can I use Walver.io for events or in-person verifications?
Yes, Walver.io is suitable for event check-ins, conference registrations, and other in-person verification needs.

### Is there support for enterprise or custom solutions?
For enterprise needs or custom solutions, please contact the Walver.io team through the official website.

## Troubleshooting

### What should I do if a verification fails?
If a verification fails, check:
1. The wallet is connected to the correct blockchain network
2. The user has the required tokens (if token gating is enabled)
3. The verification link hasn't expired or been used (if one-time use)

### How can I check if a webhook was delivered?
You can see webhook delivery status in the creator dashboard under the verification details.

### Why am I receiving a rate limit error?
API and webhook endpoints have rate limits to prevent abuse. If you're receiving rate limit errors, you might be making too many requests in a short period.

### How can I get help with integration issues?
For integration assistance:
1. Check the API documentation
2. Review the SDK examples
3. Contact support through the official website 