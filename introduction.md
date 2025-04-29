---
icon: hand-wave
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

# Introduction to Walver.io

[Walver.io](https://walver.io) is a modern wallet verification service designed for blockchain applications. It provides a secure and user-friendly way to verify wallet ownership, collect custom information from users, and manage verifications through an intuitive dashboard.

## What is [Walver.io](https://walver.io)?

[Walver.io](https://walver.io) is a service that helps blockchain applications verify that users actually own the wallets they claim to own. It does this by creating secure verification links that users can access to prove their ownership through cryptographic signatures. The service supports multiple blockchains including Solana, Ethereum, Polygon, BSC, Base, Arbitrum, Optimism, and Avalanche.

## Key Features

### Wallet Verification

* **Secure Signature Verification**: [Walver.io](https://walver.io) uses cryptographic signatures to verify wallet ownership, ensuring that only the true wallet owner can complete the verification process.
* **Multi-Chain Support**: Verify wallets across multiple blockchains including Solana, Ethereum, Polygon, and more.
* **Custom Verification Forms**: Collect additional information from users during the verification process with customizable fields.

### Token Gating

* **Access Control Based on Token Ownership**: Verify that users own a specific amount of tokens before granting access.
* **NFT Verification**: Verify ownership of specific NFTs for exclusive access.
* **Configurable Token Requirements**: Set minimum token amounts needed for verification.

### Data Collection

* **Custom Fields**: Collect and validate various types of information such as email, social media handles, and more.
* **Identity Verification**: Optionally require email or social media verification for additional security.
* **Structured Data Collection**: Organize collected information in a standardized format.

### Creator Dashboard

* **Intuitive Management Interface**: Easily manage all your verifications in one place.
* **Folder Organization**: Group verifications by project or purpose.
* **API Key Management**: Create and manage API keys for programmatic access.
* **Verification Statistics**: Track verification completion rates and other metrics.

### Security Features

* **Cryptographic Message Signing**: Users prove wallet ownership by signing unique messages.
* **Backend Verification**: All signatures are verified on the backend for enhanced security.
* **Tamper-Proof Design**: Prevents spoofing and other attacks.
* **Webhook Secret Keys**: Add an additional layer of security to webhook communications.

### Developer Tools

* **Comprehensive API**: [Full-featured API](https://walver.io/api/docs) for creating and managing verifications.
* **Python SDK**: [Official Python SDK](https://github.com/Walver-io/walver-sdk/) for easy integration.
* **Webhook Integration**: Receive real-time notifications when verifications are completed.
* **Customizable Experience**: Tailor the verification flow to match your application's needs.

## Use Cases

* **User Registration**: Securely register users in web3 applications while verifying wallet ownership.
* **Token-Gated Access**: Control access to content or features based on token ownership.
* **Event Check-in**: Verify attendees at blockchain events by confirming wallet ownership.
* **Community Verification**: Verify community members before granting access to exclusive channels.
* **NFT Holder Benefits**: Provide special benefits to users who own specific NFTs.
* **Airdrop Qualification**: Verify wallet ownership before airdrops to prevent fraud.
* **Governance Participation**: Ensure only legitimate wallet owners can participate in governance.

## How it Works

1. **Create a Verification**: Developers create verification links through the [API](https://walver.io/api/docs) or [dashboard](https://walver.io/creator/dashboard).
2. **Share the Link**: The verification link is shared with users who need to verify their wallet.
3. **User Verification**: Users visit the link, connect their wallet, and sign a message to prove ownership.
4. **Data Collection**: Optional custom fields collect additional information from users.
5. **Webhook Notification**: Upon successful verification, a webhook notifies the application.
6. **Access Granted**: The application grants appropriate access based on the verification result.

In the following sections, we'll dive deeper into how to get started with [Walver.io](https://walver.io) and explore its features in detail.
