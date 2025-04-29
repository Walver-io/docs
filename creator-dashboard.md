---
icon: grid-horizontal
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

# Creator Dashboard

The [Walver.io](https://walver.io) Creator Dashboard is a powerful interface for managing your wallet verifications, API keys, and folders. This guide explains how to use the dashboard effectively.

## Accessing the Dashboard

To access the Creator Dashboard:

1. Visit [Walver.io](https://walver.io)
2. Click on "Login" in the top-right corner
3. Either connect your wallet (Solana, Ethereum, or other supported chains) and sign a verification message to prove wallet ownership, or log in with email and password
4. You'll be redirected to the dashboard after successful authentication

## Dashboard Overview

The Creator Dashboard is organized into several sections:

* **Home**: Overview of your verification statistics and recent activity
* **Verifications**: Create and manage verification links
* **Folders**: Organize verifications into folders
* **API Keys**: Create and manage API keys
* **Settings**: Configure your creator account



## Organizing with Folders

Folders help you organize verifications by project, purpose, or any other categorization.

### Creating a Folder

To create a new folder:

1. Go to the "Folders" tab in the dashboard
2. Click "Create Folder"
3. Enter a name for the folder
4. Add an optional description
5. Configure default custom fields (optional)
6. Click "Create Folder"

### Using Custom Fields

Folders can have default custom fields that are automatically applied to any verification created in that folder:

1. When creating or editing a folder, scroll to the "Custom Fields" section
2. Click "Add Field" to add a custom field
3. Configure the field properties:
   * **Type**: The type of data (email, text, etc.)
   * **Name**: The display name for the field
   * **Placeholder**: The placeholder text for the field
   * **Required**: Whether the field is mandatory
4. Add as many fields as needed
5. Save the folder

Now, when you create a verification inside of this folder, these custom fields will be pre-populated.

## Managing Verifications

### Creating a New Verification

Refer to [this section](verification-process.md#verification-create-link) to understand how to create a verification

### Viewing Verification Results

To see detailed results for a verification:

1. Click on a verification in the list
2. The details panel will show all completed verifications, including:
   * Wallet addresses
   * Verification timestamps
   * Custom field responses
   * Token verification results (if applicable)

### Editing a Verification (coming soon!)

## Managing API Keys

API keys allow you to interact with the [Walver API](https://walver.io/api/docs) programmatically.

### Creating an API Key

To create a new API key:

1. Go to the "API Keys" tab in the dashboard
2. Click "Create API Key"
3. Enter a name for the API key
4. Add an optional description
5. Click "Create"
6. **Important**: Copy and save the API key that is displayed. It will only be shown once and cannot be retrieved later.

### Viewing API Keys

The API Keys tab displays all your active API keys, including:

* **Name**: The name you gave the key
* **Created**: When the key was created
* **Last Used**: When the key was last used
* **Description**: The optional description you provided

For security reasons, only a masked version of each key is displayed.

### Deleting API Keys

To delete an API key:

1. Find the key in the list
2. Click the "Delete" button (trash icon)
3. Confirm the deletion

**Warning**: Deleting an API key immediately revokes access for any applications using that key. This action cannot be undone.

## Dashboard Statistics (coming soon!)

## User Settings

### - Profile Settings (coming soon!)

### - Notification Settings (coming soon!)

## Advanced Features

### - Webhook Testing (coming soon!)

### - Verification Templates (coming soon!)

## Best Practices

### Organization

* Use descriptive names for verifications and folders
* Create folders for different projects or verification purposes
* Use consistent naming conventions for custom fields across verifications

### Security

* Regularly rotate API keys
* Use strong webhook secrets
* Delete inactive verifications
* Use one-time links for sensitive verifications
* Set appropriate expiration dates

### Performance

* Keep the number of custom fields reasonable
* Archive old or unused verifications
* Use folders to keep the dashboard organized

## Support and Help

If you encounter issues with the dashboard:

1. Check the [FAQ](faq.md) section
2. Look for tooltips and help text within the interface
3. Contact support through the help button in the dashboard
4. Refer to the [API documentation ](https://walver.io/api/docs)for programmatic interactions
