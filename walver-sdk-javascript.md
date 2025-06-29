---
icon: javascript
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

# Walver JavaScript SDK Documentation

[The Walver JavaScript SDK](https://github.com/walver-io/walver-sdk-javascript) provides a convenient way to interact with the Walver API from JavaScript and TypeScript applications. It enables developers to create and manage wallet verification links easily.

## Installation

Install the SDK using npm or yarn:

```bash
# Using npm
npm install walver-sdk

# Using yarn
yarn add walver-sdk
```

## Configuration

### API Key

You can provide your API key in two ways:

1.  Pass it directly when initializing the client:

    ```typescript
    import { Walver } from 'walver-sdk';

    const walver = new Walver('your-api-key');
    ```

2.  Set it as an environment variable in your `.env` file:

    ```env
    WALVER_API_KEY=your-api-key
    ```

    ```typescript
    import { Walver } from 'walver-sdk';

    const walver = new Walver(); // Will use the API key from .env
    ```

### Base URL

By default, the client uses `https://walver.io/`. You can change this by passing the `baseUrl` parameter:

```typescript
const walver = new Walver(
  'your-api-key',
  'https://your-custom-url.com'
);
```

### Timeout

The default timeout is 10 seconds (10000ms). You can change this by passing the `timeout` parameter:

```typescript
const walver = new Walver(
  'your-api-key',
  'https://walver.io/',
  30000 // 30 seconds timeout
);
```

## Creating a Verification

```typescript
const verification = await walver.createVerification({
  id: 'verification_123',
  service_name: 'My Service',
  chain: 'ETH', // or 'SOL' for Solana
  webhook: 'https://your-webhook-url.com/webhook',
  secret: 'your-webhook-secret',
  redirect_url: 'https://your-redirect-url.com',
  one_time: true,
  force_email_verification: true,
  custom_fields: [
    {
      type: 'email',
      label: 'Email Address',
      required: true
    }
  ]
});

const verificationUrl = verification.verification_url;
```

### Parameters

| Parameter                    | Type             | Required | Description                                             |
|------------------------------|------------------|----------|---------------------------------------------------------|
| id                           | string           | Yes      | A unique identifier for the verification                |
| service_name                 | string           | Yes      | The name of your service (shown to users)               |
| chain                        | string           | Yes      | The blockchain to use (e.g., "SOL", "ETH")             |
| internal_id                  | string           | No       | An optional internal ID for your reference              |
| webhook                      | string           | No       | URL to call when verification is complete               |
| expiration                   | string/Date      | No       | When the verification link expires                      |
| secret                       | string           | No       | A secret key for webhook security                       |
| redirect_url                 | string           | No       | URL to redirect after verification                      |
| one_time                     | boolean          | No       | If true, the link can only be used once                 |
| folder_id                    | string           | No       | ID of a folder to associate with                        |
| custom_fields                | array            | No       | Array of custom fields to collect                       |
| token_gate                   | boolean          | No       | Enable token gating                                     |
| token_address                | string           | No       | Token address for gating (required if token_gate=true)  |
| token_amount                 | number           | No       | Minimum token amount (required if token_gate=true)      |
| is_nft                       | boolean          | No       | Whether the token is an NFT                             |
| force_email_verification     | boolean          | No       | Require email verification via OTP                      |
| force_telegram_verification  | boolean          | No       | Require Telegram verification                           |
| force_twitter_verification   | boolean          | No       | Require Twitter verification                            |
| force_discord_verification   | boolean          | No       | Require Discord verification                           |

## Managing Folders

### Creating a Folder

```typescript
const folder = await walver.createFolder(
  'My Folder',
  'A folder for organizing verifications',
  [
    {
      type: 'discord',
      label: 'Discord Username',
      required: true
    }
  ]
);
```

### Getting All Folders

```typescript
const folders = await walver.getFolders();
```

### Getting a Specific Folder

```typescript
const folder = await walver.getFolder('folder_123');
```

### Getting Verifications in a Folder

```typescript
const verifications = await walver.getFolderVerifications('folder_123');
```

## Managing API Keys

### Creating an API Key

```typescript
const apiKey = await walver.createApiKey(
  'My API Key',
  'API key for production use'
);
```

### Getting All API Keys

```typescript
const apiKeys = await walver.getApiKeys();
```

### Deleting an API Key

```typescript
await walver.deleteApiKey('key_123');
```

## Error Handling

The SDK throws exceptions for various error conditions:

```typescript
try {
  const verification = await walver.createVerification({
    id: 'verification_123',
    service_name: 'My Service',
    chain: 'ETH',
    token_gate: true // Missing token_address and token_amount
  });
} catch (error) {
  console.error(`Error: ${error.message}`);
}
```

Common exceptions:

* Validation errors: Thrown for client-side validation issues
* HTTP errors: Thrown for server-side errors
* Network errors: Thrown for connectivity issues

## Custom Field Types

When creating verifications, you can specify various types of custom fields:

| Type     | Description                    |
|----------|--------------------------------|
| text     | Simple text input              |
| email    | Email address with validation  |
| url      | URL with validation            |
| twitter  | Twitter handle                 |
| telegram | Telegram username              |
| discord  | Discord username               |

## TypeScript Support

The SDK is written in TypeScript and provides full type definitions. You can leverage your IDE's code completion and type checking for a better development experience.

```typescript
import { Walver } from 'walver-sdk';

// Interface for custom fields
interface CustomField {
  type: string;
  label?: string;
  required?: boolean;
  [key: string]: any;
}

// Custom fields with proper typing
const customFields: CustomField[] = [
  {
    type: 'email',
    label: 'Email Address',
    required: true
  }
];

const walver = new Walver('your-api-key');
const verification = await walver.createVerification({
  id: 'verification_123',
  service_name: 'My Service',
  chain: 'ETH',
  custom_fields: customFields
});
``` 