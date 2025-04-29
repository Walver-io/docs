# Walver SDK Documentation

The Walver SDK provides a convenient way to interact with the Walver API from your Python applications. It offers both synchronous and asynchronous clients for creating and managing wallet verification links.

## Installation

Install the SDK using pip:

```bash
pip install walver-sdk
```

## Configuration

### API Key

You can provide your API key in two ways:

1. Pass it directly when initializing the client:
   ```python
   from walver_sdk import Walver
   
   walver = Walver(api_key="your-api-key")
   ```

2. Set it as an environment variable in your `.env` file:
   ```env
   WALVER_API_KEY=your-api-key
   ```
   ```python
   from walver_sdk import Walver
   
   walver = Walver()  # Will use the API key from .env
   ```

### Base URL

By default, the client uses `https://walver.io/api/`. You can change this by passing the `base_url` parameter:

```python
walver = Walver(
    api_key="your-api-key",
    base_url="https://your-custom-url.com"
)
```

### Timeout

The default timeout is 10 seconds. You can change this by passing the `timeout` parameter:

```python
walver = Walver(
    api_key="your-api-key",
    timeout=30  # 30 seconds timeout
)
```

## Synchronous Client

The `Walver` class provides synchronous methods for interacting with the API.

### Creating a Verification

```python
verification = walver.create_verification(
    id="verification_123",
    service_name="My Service",
    chain="solana",
    webhook="https://your-webhook-url.com/webhook",
    secret="your-webhook-secret",
    redirect_url="https://your-redirect-url.com",
    one_time=True,
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

verification_url = verification["verification_url"]
```

#### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| id | string | Yes | A unique identifier for the verification |
| service_name | string | Yes | The name of your service (shown to users) |
| chain | string | Yes | The blockchain to use (e.g., "solana", "ethereum") |
| internal_id | string | No | An optional internal ID for your reference |
| webhook | string | No | URL to call when verification is complete |
| expiration | string/datetime | No | When the verification link expires |
| secret | string | No | A secret key for webhook security |
| redirect_url | string | No | URL to redirect after verification |
| one_time | boolean | No | If true, the link can only be used once |
| folder_id | string | No | ID of a folder to associate with |
| custom_fields | list | No | List of custom fields to collect |
| token_gate | boolean | No | Enable token gating |
| token_address | string | No | Token address for gating (required if token_gate=True) |
| token_amount | number | No | Minimum token amount (required if token_gate=True) |
| is_nft | boolean | No | Whether the token is an NFT |
| force_email_verification | boolean | No | Require email verification via OTP |
| force_telegram_verification | boolean | No | Require Telegram verification |
| force_twitter_verification | boolean | No | Require Twitter verification |

### Managing Folders

#### Creating a Folder

```python
folder = walver.create_folder(
    name="My Folder",
    description="A folder for organizing verifications",
    custom_fields=[
        {
            "id": "discord",
            "type": "discord",
            "name": "Discord Username",
            "required": True
        }
    ]
)
```

#### Getting All Folders

```python
folders = walver.get_folders()
```

#### Getting a Specific Folder

```python
folder = walver.get_folder(folder_id="folder_123")
```

#### Getting Verifications in a Folder

```python
verifications = walver.get_folder_verifications(folder_id="folder_123")
```

### Managing API Keys

#### Creating an API Key

```python
api_key = walver.create_api_key(
    name="My API Key",
    description="API key for production use"
)
```

#### Getting All API Keys

```python
api_keys = walver.get_api_keys()
```

#### Deleting an API Key

```python
walver.delete_api_key(api_key="key_123")
```

## Asynchronous Client

The `AsyncWalver` class provides asynchronous methods for interacting with the API.

```python
import asyncio
from walver_sdk import AsyncWalver

async def main():
    # Initialize the client
    walver = AsyncWalver(api_key="your-api-key")
    
    # Create a verification
    verification = await walver.create_verification(
        id="verification_123",
        service_name="My Service",
        chain="solana"
    )
    
    print(verification)

# Run the async code
asyncio.run(main())
```

The async client provides the same methods as the synchronous client, but with async/await syntax.

## Error Handling

The SDK raises exceptions for various error conditions:

```python
try:
    verification = walver.create_verification(
        id="verification_123",
        service_name="My Service",
        chain="solana",
        token_gate=True  # Missing token_address and token_amount
    )
except ValueError as e:
    print(f"Validation error: {e}")
except requests.HTTPError as e:
    print(f"HTTP error: {e}")
```

Common exceptions:
- `ValueError`: Raised for client-side validation errors
- `requests.HTTPError`: Raised for server-side errors
- `requests.Timeout`: Raised when the request times out

## Custom Field Types

When creating verifications, you can specify various types of custom fields:

| Type | Description |
|------|-------------|
| text | Simple text input |
| email | Email address with validation |
| url | URL with validation |
| twitter | Twitter handle |
| telegram | Telegram username |
| discord | Discord username |
| number | Numeric input with validation |
| date | Date input with validation |
| wallet | Wallet address with validation |

Example:
```python
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
        "required": False
    }
]
```

## Token Gating

You can create token-gated verifications by setting the `token_gate` parameter to `True` and providing the required token information:

```python
verification = walver.create_verification(
    id="verification_123",
    service_name="My Service",
    chain="solana",
    token_gate=True,
    token_address="So11111111111111111111111111111111111111112",
    token_amount=1.0,
    is_nft=False  # Set to True for NFT verification
)
```

## Complete Examples

### Basic Verification

```python
from walver_sdk import Walver

# Initialize the client
walver = Walver(api_key="your-api-key")

# Create a basic verification
verification = walver.create_verification(
    id="basic_verification",
    service_name="My Service",
    chain="solana",
    webhook="https://example.com/webhook",
    secret="your_webhook_secret"
)

print(f"Verification URL: {verification['verification_url']}")
```

### Token-Gated Verification with Email

```python
from walver_sdk import Walver

# Initialize the client
walver = Walver(api_key="your-api-key")

# Create a token-gated verification with email requirement
verification = walver.create_verification(
    id="token_gated_verification",
    service_name="Premium Service",
    chain="ethereum",
    webhook="https://example.com/webhook",
    secret="your_webhook_secret",
    token_gate=True,
    token_address="0x1234567890abcdef1234567890abcdef12345678",
    token_amount=10.0,
    force_email_verification=True,
    custom_fields=[
        {
            "id": "email",
            "type": "email",
            "name": "Email Address",
            "required": True
        },
        {
            "id": "name",
            "type": "text",
            "name": "Full Name",
            "required": True
        }
    ]
)

print(f"Verification URL: {verification['verification_url']}")
```

### Folder Management

```python
from walver_sdk import Walver

# Initialize the client
walver = Walver(api_key="your-api-key")

# Create a folder
folder = walver.create_folder(
    name="My Project",
    description="Verifications for my project"
)

# Create a verification in the folder
verification = walver.create_verification(
    id="folder_verification",
    service_name="My Service",
    chain="solana",
    folder_id=folder["id"]
)

# Get all verifications in the folder
verifications = walver.get_folder_verifications(folder_id=folder["id"])
``` 