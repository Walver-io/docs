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

# Walver.io JavaScript Widget

The [Walver.io Authentication Widget](https://walver.io/iframe/demo) provides an easy way to integrate blockchain wallet-based authentication into your web application. This widget handles the entire authentication flow, including wallet connection, message signing, and signature verification through our infrastructure.

## Installation

Add the [Walver.io](https://walver.io) Authentication Widget script to your HTML page:

```html
<script src="https://walver.io/static/js/walver-auth.js"></script>
```

## Initialization

Initialize the widget with your configuration options:

```javascript
// Optional: Set the base URL (useful for development environments)
window.walverBaseUrl = 'https://walver.io'; // Default value if not specified

// Initialize the authentication widget
WalverAuth.init({
    buttonText: 'Login with Walver.io', // Optional: Custom button text
    buttonClass: 'walver-auth-button', // Optional: Custom button class
    width: '360px', // Optional: Width of the iframe
    height: '480px', // Optional: Height of the iframe
    serviceName: 'Your Application Name', // Recommended: Your service name
    container: '#my-auth-container', // Required: Container element or selector
    onSuccess: function(data) {
        // Handle successful authentication
        console.log('Authentication successful:', data);
        // data contains: walletAddress, signature, message, chain, nonce, verifiedDomain
    },
    onError: function(error) {
        // Handle authentication error
        console.error('Authentication error:', error);
    },
    onCancel: function() {
        // Handle authentication cancellation
        console.log('Authentication cancelled');
    }
});
```

## Configuration Options

| Option | Type | Required | Default | Description |
|--------|------|----------|---------|-------------|
| `container` | String \| Element | Yes | - | The container element or selector where the widget will be rendered |
| `serviceName` | String | Recommended | "Walver.io" | Your application's name (appears in the signing message) |
| `buttonText` | String | No | "Login with Walver.io" | Custom text for the authentication button |
| `buttonClass` | String | No | "walver-auth-button" | Custom CSS class for the button |
| `width` | String | No | "360px" | Width of the authentication iframe |
| `height` | String | No | "480px" | Height of the authentication iframe |
| `onSuccess` | Function | No | - | Callback function called after successful authentication |
| `onError` | Function | No | - | Callback function called when an error occurs |
| `onCancel` | Function | No | - | Callback function called when the user cancels authentication |

## Authentication Response

When authentication is successful, the `onSuccess` callback will receive an object with the following properties:

```javascript
{
    walletAddress: "The user's blockchain wallet address",
    signature: "The signature proving wallet ownership",
    message: "The message that was signed",
    chain: "The blockchain used (e.g., 'solana', 'ethereum')",
    nonce: "The nonce used for the authentication",
    verifiedDomain: "The domain that the user authenticated from"
}
```

## Security Features

The Walver.io Authentication Widget implements several security measures:

- **Server-side Signature Verification**: All signatures are verified on the server, never in the browser.
- **Service-specific Messages**: Each message includes your service name to prevent phishing.
- **Domain Binding**: Authentication is bound to your domain to prevent cross-site abuse.
- **Time-limited Signatures**: Messages expire after 5 minutes for security.
- **Nonce Protection**: Each authentication attempt uses a unique nonce that can only be used once.
- **Origin Validation**: Messages are only accepted from authorized origins.
- **Content Security Policy**: Strict CSP headers protect against XSS attacks.
- **IP Monitoring**: Rate limiting and suspicious activity detection are implemented.

## Example Integration

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Walver.io Authentication Example</title>
</head>
<body>
    <h1>Login with Wallet</h1>
    <div id="auth-container"></div>
    
    <script src="https://walver.io/static/js/walver-auth.js"></script>
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            WalverAuth.init({
                container: '#auth-container',
                serviceName: 'My Example App',
                onSuccess: function(data) {
                    console.log('Authenticated!', data);
                    // Here you would typically:
                    // 1. Verify the authentication with your backend
                    // 2. Create a session for the user
                    // 3. Redirect to a logged-in page
                },
                onError: function(error) {
                    console.error('Authentication error:', error);
                    alert('Authentication failed: ' + error);
                }
            });
        });
    </script>
</body>
</html>
```

## Advanced Usage

### Custom Button Styling

You can customize the appearance of the authentication button by providing a custom CSS class:

```javascript
WalverAuth.init({
    container: '#auth-container',
    buttonClass: 'my-custom-button-class',
    // other options...
});
```

### Server-side Verification

For complete security, you should verify the authentication data on your server:

1. Send the authentication data (wallet address, signature, message, chain, nonce) to your server
2. Your server should verify the signature using [Walver.io's](https://walver.io) verification API or your own verification logic
3. Only after server-side verification should you create a session for the user

## Troubleshooting

### Widget Not Appearing
- Make sure the container element exists in the DOM before initializing the widget
- Check browser console for any JavaScript errors

### Authentication Failures
- Ensure the user has a compatible wallet installed and configured
- Check that the user is connected to the correct blockchain network
- Verify that your application is properly configured with Walver.io 