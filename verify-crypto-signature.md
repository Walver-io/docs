# Verify Crypto Signature

The Verify Crypto Signature package is a Python library for verifying and working with cryptographic signatures from various blockchain networks. It currently supports EVM (Ethereum Virtual Machine) and Solana blockchain signatures.

## Installation

```bash
pip install verify-crypto-signature
```

## Features

- Verify message signatures from EVM and Solana addresses
- Sign messages using private keys
- Recover wallet addresses from signatures (EVM only)
- Validate EVM and Solana addresses

## EVM Signature Verification

### Verifying an EVM Signature

```python
from verify_crypto_signature.evm import VerifyEVM

# Verify if a message was signed by a specific address
wallet_address = "0x..."  # Example address
message = "Hello, world!"
signature = "0x..."  # Signature obtained from the wallet

# Verify the signature
is_valid = VerifyEVM.verify_signature(wallet_address, message, signature)
if is_valid:
    print("Signature is valid")
else:
    print("Signature is invalid")
```

### Signing a Message with EVM

```python
from verify_crypto_signature.evm import VerifyEVM

# Sign a message with a private key
private_key = "0x..."  # Your private key (keep this secret!)
message = "Hello, world!"

# Sign the message
signed_message = VerifyEVM.sign_message(message, private_key)
signature = signed_message.signature.hex()
print(f"Signature: {signature}")
```

### Recovering an Address from an EVM Signature

```python
from verify_crypto_signature.evm import VerifyEVM

# Recover the signer's address
message = "Hello, world!"
signature = "0x..."  # The signature

address = VerifyEVM.get_address_from_message(message, signature=signature)
print(f"Signer address: {address}")
```

## Solana Signature Verification

### Verifying a Solana Signature

```python
from verify_crypto_signature.sol import VerifySOL

# Verify if a message was signed by a specific address
wallet_address = "5yQ6...."  # Example Solana address
message = "Hello, world!"
signature = "4K2...."  # Signature obtained from the wallet

# Verify the signature
is_valid = VerifySOL.verify_signature(wallet_address, message, signature)
```

### Signing a Message with Solana

```python
from verify_crypto_signature.sol import VerifySOL

# Sign a message with a private key
private_key = "4K2...."  # Your private key (keep this secret!)
message = "Hello, world!"

# Sign the message
signed_message = VerifySOL.sign_message(message, private_key)
```

## Integration with Walver.io

The Verify Crypto Signature package can be used together with Walver.io for enhanced crypto verification workflows. This package enables:

1. **Secure verification** of user wallet ownership
2. **Seamless integration** with your authentication systems
3. **Multi-chain support** covering both EVM and Solana ecosystems
4. **Signature creation** for both EVM and Solana

## Dependencies

The package requires the following key dependencies:
- eth_account
- eth_utils
- eth_keys
- solders

These are automatically installed when you install the package using pip.

## Source Code

The source code for this package is available on GitHub: [https://github.com/walver-io/verify-crypto-signature](https://github.com/walver-io/verify-crypto-signature) 