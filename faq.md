---
icon: comment-question
cover: .gitbook/assets/Captura de pantalla 2025-04-29 194438.png
coverY: 0
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

# Frequently Asked Questions (FAQ)

## General Questions <a href="#faq-general-questions" id="faq-general-questions"></a>

### What is [Walver.io](https://walver.io)? <a href="#faq-what-is-walver-io" id="faq-what-is-walver-io"></a>

[Walver.io](https://walver.io) is a service that helps blockchain applications verify wallet ownership. It creates secure verification links that users can access to prove their ownership through cryptographic signatures. The service supports multiple blockchains including Solana, Ethereum, Polygon, and others.

### Which blockchains are supported? <a href="#faq-blockchains-supported" id="faq-blockchains-supported"></a>

[Walver.io](https://walver.io) currently supports:

* Solana
* Ethereum
* Polygon
* Binance Smart Chain (BSC)
* Base
* Arbitrum
* Optimism
* Avalanche

### Does using [Walver.io](https://walver.io) require coding? <a href="#faq-does-walver-require-coding" id="faq-does-walver-require-coding"></a>

No, [Walver.io](https://walver.io) provides a user-friendly dashboard for creating and managing verifications without coding. However, for more advanced integrations, you can use the API or Python SDK.

### Is [Walver.io](https://walver.io) free to use? <a href="#faq-is-walver-free" id="faq-is-walver-free"></a>

Right now, [Walver.io](https://walver.io) is in **beta** and **free to use**. This will change in the future.

## Verification Process <a href="#faq-verification-process" id="faq-verification-process"></a>

### How does wallet verification work? <a href="#faq-how-does-verification-work" id="faq-how-does-verification-work"></a>

Wallet verification works by asking users to sign a cryptographic message with their wallet's private key. This proves that they own the wallet without revealing the private key. [Walver.io](https://walver.io) handles this process securely and can also collect additional information from users.

### Can I collect information from users during verification? <a href="#faq-can-i-collect-data" id="faq-can-i-collect-data"></a>

Yes, you can configure custom fields to collect various types of information such as email addresses, social media handles, and more. Each field can be marked as required or optional.

### What happens after a user completes verification? <a href="#faq-what-happens-after-verification" id="faq-what-happens-after-verification"></a>

When a user completes verification, [Walver.io](https://walver.io):

1. Sends the verification data to your webhook endpoint (if configured)
2. Redirects the user to a success page or your custom redirect URL
3. Marks the verification as completed in the dashboard

### Can verifications expire? <a href="#faq-can-verifications-expire" id="faq-can-verifications-expire"></a>

Yes, you can set an expiration date when creating a verification. After this date, the verification link will no longer be valid.

### Can I limit a verification link to one-time use? <a href="#faq-can-i-limit-one-time" id="faq-can-i-limit-one-time"></a>

Yes, you can configure a verification to be one-time use only. After a successful verification, the link will no longer be usable.

## Token Gating <a href="#faq-token-gating" id="faq-token-gating"></a>

### What is token gating? <a href="#faq-what-is-token-gating" id="faq-what-is-token-gating"></a>

Token gating is a feature that restricts access based on token ownership. It verifies that users own a specific amount of tokens or NFTs before granting access to content or services.

### How does token gating work in [Walver.io](https://walver.io)? <a href="#faq-how-does-token-gating-work" id="faq-how-does-token-gating-work"></a>

When creating a verification, you can enable token gating and specify:

1. The token address (contract address)
2. The minimum amount required
3. Whether it's an NFT

During verification, [Walver.io ](https://walver.io)checks the user's wallet balance against these requirements.

### Can I gate access based on NFT ownership? <a href="#faq-can-i-gate-based-on-nft" id="faq-can-i-gate-based-on-nft"></a>

Yes, you can create verifications that require ownership of specific NFTs by setting the `is_nft` flag to `true` and specifying the NFT contract address.

### Does [Walver.io](https://walver.io) support multiple token conditions? <a href="#faq-does-support-multiple-token-conditions" id="faq-does-support-multiple-token-conditions"></a>

Currently, each verification can have one token condition. For more complex requirements, you can create multiple verifications or handle the logic in your application after receiving the webhook.

## Webhooks and Integration <a href="#faq-webhooks-and-integration" id="faq-webhooks-and-integration"></a>

### What is a webhook in the context of [Walver.io](https://walver.io)? <a href="#faq-what-is-a-webhook" id="faq-what-is-a-webhook"></a>

A webhook is an HTTP callback that [Walver.io](https://walver.io) sends to your application when a user completes a verification. It contains all the verification data, allowing your application to process verifications automatically.

### How secure are the webhooks? <a href="#faq-how-secure-are-webhooks" id="faq-how-secure-are-webhooks"></a>

Webhooks include a "secret" that you configure when setting it up and can verify to ensure the webhook came from Walver.io. This prevents tampering and spoofing.

### What if my webhook endpoint is temporarily unavailable? <a href="#faq-whaat-if-webhook-unavailable" id="faq-whaat-if-webhook-unavailable"></a>

Walver.io uses an exponential backoff retry strategy, attempting to deliver the webhook multiple times over a 24-hour period if your endpoint is unavailable.

### Can I test webhooks in a development environment? <a href="#faq-can-i-test-webhooks-in-development" id="faq-can-i-test-webhooks-in-development"></a>

Yes, you can set up verifications with your development webhook URL to test the integration before going to production.

## [API](https://walver.io/api/docs) and [SDK](https://github.com/Walver-io/walver-sdk/) <a href="#faq-api-and-sdk" id="faq-api-and-sdk"></a>

### Does [Walver.io](https://walver.io) provide an [API](https://walver.io/api/docs)? <a href="#faq-does-walver-provide-api" id="faq-does-walver-provide-api"></a>

Yes, [Walver.io](https://walver.io) offers a [comprehensive API](https://walver.io/api/docs) for creating and managing verifications programmatically.

### Is there an [SDK](https://github.com/Walver-io/walver-sdk/) available? <a href="#faq-is-there-an-sdk" id="faq-is-there-an-sdk"></a>

Yes, there is an [official Python SDK](https://github.com/Walver-io/walver-sdk/) ([walver-sdk on PyPI](https://pypi.org/project/walver-sdk/)) that provides both synchronous and asynchronous clients for easy integration.

### How do I authenticate API requests? <a href="#faq-how-do-i-authenticate-api" id="faq-how-do-i-authenticate-api"></a>

API requests can be authenticated using API keys, which you can create and manage in the creator dashboard.

### Is there a rate limit on API calls? <a href="#faq-is-there-rate-limit" id="faq-is-there-rate-limit"></a>

Yes, most API endpoints are limited to 10 requests per minute per IP address, with some endpoints having different limits.

## Security <a href="#faq-security" id="faq-security"></a>

### How secure is the wallet verification process? <a href="#faq-how-secure-is-verification" id="faq-how-secure-is-verification"></a>

The verification process uses cryptographic signatures to securely verify wallet ownership without exposing private keys. All communications are encrypted using HTTPS.

### How should I secure my webhook endpoint? <a href="#faq-how-should-i-secure-my-webhook" id="faq-how-should-i-secure-my-webhook"></a>

You should:

1. Use HTTPS for your endpoint
2. Verify webhook signatures using your secret
3. Implement rate limiting
4. Follow security best practices for handling webhook data

### Can verifications be tampered with? <a href="#faq-can-verification-be-tampered" id="faq-can-verification-be-tampered"></a>

No, each verification includes cryptographic signatures that cannot be forged. Additionally, webhook payloads are signed with your secret key to prevent tampering.

### Is user data encrypted? <a href="#faq-is-user-data-encrypted" id="faq-is-user-data-encrypted"></a>

Yes, all data is transmitted over HTTPS. For specific details about data storage and encryption, please refer to the privacy policy.

## Custom Solutions <a href="#faq-custom-solutions" id="faq-custom-solutions"></a>

### Can I customize the verification page? <a href="#faq-can-i-customize" id="faq-can-i-customize"></a>

The verification page maintains a consistent design to ensure security and user trust. However, you can customize the service name and add your logo through the dashboard.

### Can [Walver.io](https://walver.io) integrate with my existing user system? <a href="#faq-can-walver-integrate-with-my-system" id="faq-can-walver-integrate-with-my-system"></a>

Yes, using webhooks, you can integrate [Walver.io](https://walver.io) verifications with your existing user management system.

### Can I use [Walver.io](https://walver.io) for events or in-person verifications? <a href="#faq-can-i-use-for-events-or-inperson" id="faq-can-i-use-for-events-or-inperson"></a>

Yes, [Walver.io](https://walver.io) is suitable for event check-ins, conference registrations, and other in-person verification needs.

### Is there support for enterprise or custom solutions? <a href="#faq-is-there-enterprise-or-custom" id="faq-is-there-enterprise-or-custom"></a>

For enterprise needs or custom solutions, please contact the [Walver.io](https://walver.io) team through the official website.

## Troubleshooting <a href="#faq-troubleshooting" id="faq-troubleshooting"></a>

### What should I do if a verification fails? <a href="#faq-what-if-verification-fails" id="faq-what-if-verification-fails"></a>

If a verification fails, check:

1. The wallet is connected to the correct blockchain network
2. The user has the required tokens (if token gating is enabled)
3. The verification link hasn't expired or been used (if one-time use)

### Why am I receiving a rate limit error? <a href="#faq-why-rate-limit-error" id="faq-why-rate-limit-error"></a>

API and webhook endpoints have rate limits to prevent abuse. If you're receiving rate limit errors, you might be making too many requests in a short period.

### How can I get help with integration issues? <a href="#faq-how-get-help-with-integration" id="faq-how-get-help-with-integration"></a>

For integration assistance:

1. Check the API documentation
2. Review the SDK examples
3. Contact support through the official website
