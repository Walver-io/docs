---
icon: hexagon-vertical-nft
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

# Token Gating

Token gating is a powerful feature of [Walver.io](https://walver.io) that allows you to restrict access to your content or services based on token ownership. This guide explains how to implement token gating in your verification flows.

## What is Token Gating?

Token gating is a mechanism that verifies whether a user owns a specific amount of tokens or NFTs before granting them access to exclusive content, services, or features. This allows you to create exclusive experiences for token holders or community members.

With [Walver.io](https://walver.io), you can implement token gating without writing complex blockchain code. The platform handles the verification process, checking token balances on-chain before completing the verification.

## Supported Blockchains

[Walver.io](https://walver.io) supports token gating on multiple blockchains:

* Solana
* Ethereum
* Polygon
* Binance Smart Chain (BSC)
* Base
* Arbitrum
* Optimism
* Avalanche

## Types of Token Gating

### Fungible Token Gating

Verify that users own a minimum amount of a specific fungible token (e.g., USDC, SOL, ETH, etc.).

Example use cases:

* Governance access for token holders
* Premium features for users holding a service token
* Early access to products for investors

### NFT Gating

Verify that users own at least one specific NFT or a required number of NFTs from a collection.

Example use cases:

* Exclusive access for NFT holders
* Special features for NFT community members
* Verification of ownership for NFT-based memberships

## Setting Up Token Gating

### Using the Dashboard

1. Go to the [Creator Dashboard at walver.io](https://walver.io/creator/dashboard)
2. Click "Create Verification" or edit an existing verification
3. Enable the "Token Gate" option
4. Fill in the required token information:
   * **Token Address**: The contract address of the token
   * **Token Amount**: The minimum amount required
   * **Is NFT**: Toggle this if checking for NFT ownership
5. Complete the rest of the verification setup
6. Save your changes

### Using the API

```json
{
  "id": "token_gated_verification",
  "service_name": "Premium Content",
  "chain": "ethereum",
  "token_gate": true,
  "token_address": "0x1234567890abcdef1234567890abcdef12345678",
  "token_amount": 100.0,
  "is_nft": false
}
```

### Using the Python SDK

```python
from walver_sdk import Walver

walver = Walver(api_key="your-api-key")

verification = walver.create_verification(
    id="token_gated_verification",
    service_name="Premium Content",
    chain="ethereum",
    token_gate=True,
    token_address="0x1234567890abcdef1234567890abcdef12345678",
    token_amount=100.0,
    is_nft=False
)
```

## Token Addresses

### Finding Token Addresses

The token address is the contract address of the token or NFT collection you want to verify. Here's how to find it for different chains:

#### Solana

For Solana, you'll need the token mint address, which you can find by:

1. Looking up the token on [Solscan](https://solscan.io) or [Explorer](https://explorer.solana.com)
2. Finding the "Mint Address" field
3. Copying the address (e.g., `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` for USDC)

#### Ethereum and EVM Chains

For Ethereum and other EVM chains:

1. Look up the token on [Etherscan](https://etherscan.io) or the relevant block explorer
2. Find the "Contract Address" field
3. Copy the address (e.g., `0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48` for USDC on Ethereum)

### Common Token Addresses

Here are some common token addresses for reference:

#### Solana

* **SOL (Native Token)**: `So11111111111111111111111111111111111111112`
* **USDC**: `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v`
* **BONK**: `DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263`

#### Ethereum

* **ETH (Native Token)**: For native ETH, use `0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE`
* **USDC**: `0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48`
* **USDT**: `0xdAC17F958D2ee523a2206206994597C13D831ec7`

## Token Amounts

The token amount specifies the minimum amount of tokens a user must own to pass verification.

### Decimal Precision

Different tokens have different decimal precision:

* Most ERC-20 tokens use 18 decimals (1.0 = 10^18 wei)
* USDC uses 6 decimals (1.0 = 10^6)
* USDT uses 6 decimals (1.0 = 10^6)
* SOL uses 9 decimals (1.0 = 10^9 lamports)

When setting token amounts, use the human-readable amount (e.g., 5.0 for 5 tokens), not the raw amount with all decimals.

### NFTs

For NFTs (when `is_nft` is set to `true`):

* Set `token_amount` to 1.0 to verify ownership of at least one NFT
* Set higher amounts if requiring multiple NFTs from the same collection

## User Experience

When a user goes through a token-gated verification:

1. They connect their wallet
2. They sign a message to prove ownership
3. Walver.io checks their token balance on-chain
4. If they meet the token requirement, the verification proceeds
5. If they don't meet the requirement, they see an error message

## Webhook Responses

When using webhooks with token-gated verifications, the webhook payload will include a `token_verification` field:

```json
{
  "id": "token_gated_verification",
  "wallet_address": "0x1234567890abcdef",
  "verification_time": "2023-05-01T12:34:56Z",
  "custom_fields": {},
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

## Token Gating Best Practices

1. **Choose the Right Token**: Select a token that aligns with your community or service
2. **Set Appropriate Thresholds**: Consider token price and accessibility when setting amounts
3. **Consider Staked Tokens**: Be aware that tokens staked in DeFi protocols might not be counted
4. **Test Thoroughly**: Always test your token gating with different wallet balances
5. **Provide Clear Instructions**: Explain to users which token and amount they need
6. **Offer Alternatives**: Consider providing alternative paths for users who don't have the required tokens
7. **Update Requirements**: Periodically review and adjust token requirements as token values change

## Example: NFT Community Access

This example creates a verification that requires ownership of at least one NFT from a specific collection:

```python
from walver_sdk import Walver

walver = Walver(api_key="your-api-key")

verification = walver.create_verification(
    id="nft_community_access",
    service_name="Exclusive NFT Community",
    chain="ethereum",
    webhook="https://your-service.com/webhook",
    secret="your_webhook_secret",
    token_gate=True,
    token_address="0x57f1887a8bf19b14fc0df6fd9b2acc9af147ea85",  # Example NFT collection
    token_amount=1.0,
    is_nft=True,
    custom_fields=[
        {
            "id": "email",
            "type": "email",
            "name": "Email Address",
            "required": True
        },
        {
            "id": "discord",
            "type": "discord",
            "name": "Discord Username",
            "required": True
        }
    ]
)
```

## Advanced: Combining Token Gating with Other Requirements

You can combine token gating with other verification requirements:

### Token Gating + Email Verification

```python
verification = walver.create_verification(
    id="premium_access",
    service_name="Premium Service",
    chain="solana",
    token_gate=True,
    token_address="EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
    token_amount=100.0,
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

### Token Gating + Social Verification

```python
verification = walver.create_verification(
    id="community_access",
    service_name="Community Access",
    chain="ethereum",
    token_gate=True,
    token_address="0x1234567890abcdef1234567890abcdef12345678",
    token_amount=5.0,
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
