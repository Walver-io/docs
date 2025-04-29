# Creator Dashboard

The Walver.io Creator Dashboard is a powerful interface for managing your wallet verifications, API keys, and folders. This guide explains how to use the dashboard effectively.

## Accessing the Dashboard

To access the Creator Dashboard:

1. Visit [walver.io](https://walver.io)
2. Click on "Login" in the top-right corner
3. Connect your wallet (Solana, Ethereum, or other supported chains) and sign a verification message to prove wallet ownership, or log in with email and password
4. You'll be redirected to the dashboard after successful authentication

## Dashboard Overview

The Creator Dashboard is organized into several sections:

- **Home**: Overview of your verification statistics and recent activity
- **Verifications**: Create and manage verification links
- **Folders**: Organize verifications into folders
- **API Keys**: Create and manage API keys
- **Settings**: Configure your creator account

## Managing Verifications

### Creating a New Verification

To create a new verification link:

1. Click on "Create Verification" in the sidebar or the "+" button in the Verifications tab
2. Fill in the required information:
   - **ID**: A unique identifier for this verification
   - **Service Name**: The name of your service (shown to users)
   - **Blockchain**: Select the blockchain your users will connect with
3. Configure optional settings:
   - **Webhook URL**: Where verification results should be sent
   - **Secret Key**: For securing webhook communications
   - **Redirect URL**: Where to send users after successful verification
   - **One-time Use**: Enable if the link should only be used once
   - **Expiration Date**: When the verification link should expire
   - **Folder**: Select a folder to organize this verification
4. Add custom fields if needed (email, social media handles, etc.)
5. Configure token gating (optional)
6. Click "Create Verification"
7. Copy the generated verification URL to share with your users

### Viewing Verification Details

For each verification, you can view:

- **Verification URL**: The link to share with users
- **Created At**: When the verification was created
- **Status**: Active, Expired, or Completed (if one-time)
- **Verified Count**: How many users have completed the verification
- **Last Verified**: When the verification was last completed

### Viewing Verification Results

To see detailed results for a verification:

1. Click on a verification in the list
2. The details panel will show all completed verifications, including:
   - Wallet addresses
   - Verification timestamps
   - Custom field responses
   - Token verification results (if applicable)

### Editing a Verification

Some verification properties can be edited after creation:

1. Select the verification from the list
2. Click the "Edit" button
3. Update the allowed fields (note that some core properties cannot be changed)
4. Click "Save Changes"

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

### Using Default Custom Fields

Folders can have default custom fields that are automatically applied to any verification created in that folder:

1. When creating or editing a folder, scroll to the "Default Custom Fields" section
2. Click "Add Field" to add a custom field
3. Configure the field properties:
   - **Type**: The type of data (email, text, etc.)
   - **Name**: The display name for the field
   - **Placeholder**: The placeholder text for the field
   - **Required**: Whether the field is mandatory
4. Add as many fields as needed
5. Save the folder

Now, when you create a verification and select this folder, these custom fields will be pre-populated.

### Moving Verifications Between Folders

To move a verification to a different folder:

1. Select the verification from the list
2. Click "Edit"
3. Change the folder in the dropdown menu
4. Save your changes

## Managing API Keys

API keys allow you to interact with the Walver API programmatically.

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

- **Name**: The name you gave the key
- **Created**: When the key was created
- **Last Used**: When the key was last used
- **Description**: The optional description you provided

For security reasons, only a masked version of each key is displayed.

### Deleting API Keys

To delete an API key:

1. Find the key in the list
2. Click the "Delete" button (trash icon)
3. Confirm the deletion

**Warning**: Deleting an API key immediately revokes access for any applications using that key. This action cannot be undone.

## Dashboard Statistics

The dashboard home page provides useful statistics about your verifications:

- **Total Verifications**: The number of verification links you've created
- **Completed Verifications**: How many verifications have been successfully completed
- **Active Verifications**: The number of verification links currently active
- **Expired Verifications**: The number of verification links that have expired

You can also see charts showing:

- Verification completion trends over time
- Distribution of verifications by blockchain
- Most active verification links
- Recent activity log

## User Settings

The Settings tab allows you to configure your creator account:

### Profile Settings

- **Username**: Set a username for your creator profile
- **Email**: Add an email for notifications (optional)
- **Profile Picture**: Upload a profile picture

### Notification Settings

Configure how you receive notifications:

- **Email Notifications**: Toggle email notifications for completed verifications
- **Webhook Failures**: Get notified of webhook delivery failures
- **Security Alerts**: Receive notifications about security events

## Advanced Features

### Webhook Testing

To test your webhook integration:

1. Go to the "API Keys" tab
2. Click "Test Webhook"
3. Enter your webhook URL
4. Configure the test payload
5. Send the test request
6. View the response

### Verification Templates

Save commonly used verification configurations as templates:

1. Create a new verification with your desired settings
2. Before saving, check "Save as Template"
3. Give the template a name
4. When creating a new verification, you can select from your saved templates

### Bulk Operations

For managing multiple verifications:

1. In the Verifications tab, select multiple verifications using the checkboxes
2. Use the "Bulk Actions" dropdown to:
   - Move to a folder
   - Deactivate verifications
   - Delete verifications

## Best Practices

### Organization

- Use descriptive names for verifications and folders
- Create folders for different projects or verification purposes
- Use consistent naming conventions for custom fields across verifications

### Security

- Regularly rotate API keys
- Use strong webhook secrets
- Delete inactive verifications
- Use one-time links for sensitive verifications
- Set appropriate expiration dates

### Performance

- Keep the number of custom fields reasonable
- Archive old or unused verifications
- Use folders to keep the dashboard organized

## Support and Help

If you encounter issues with the dashboard:

1. Check the FAQ section
2. Look for tooltips and help text within the interface
3. Contact support through the help button in the dashboard
4. Refer to the API documentation for programmatic interactions 