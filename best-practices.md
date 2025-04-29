# Best Practices

This guide provides recommendations for getting the most out of Walver.io while maintaining security and a good user experience.

## Verification Design

### Naming and Organization

- **Use Clear Identifiers**: Choose descriptive, readable IDs for your verifications (e.g., `event_registration_2023` rather than `er23`)
- **Organize with Folders**: Group related verifications into folders based on project, purpose, or time period
- **Consistent Naming**: Use consistent naming conventions across your verifications and custom fields

### Custom Fields

- **Collect Only Necessary Data**: Only ask for information you actually need
- **Clear Field Labels**: Use descriptive labels that clearly indicate what information is being requested
- **Helpful Descriptions**: Add descriptions to fields to provide context or instructions
- **Logical Ordering**: Arrange fields in a logical order (e.g., name before email)
- **Reasonable Field Count**: Limit the number of fields to avoid overwhelming users

### Expiration Settings

- **Set Appropriate Expirations**: Define expiration dates based on the verification's purpose:
  - Event registrations should expire after the event
  - Member applications might expire after a few weeks
  - Long-term verifications might have longer expiration periods
- **Time Buffer**: Add a buffer before time-sensitive verifications expire
- **Regular Cleanup**: Delete or archive expired verifications that are no longer needed

### One-Time vs. Reusable Links

- **One-Time Links for Sensitive Verifications**: Use one-time links for:
  - Exclusive access grants
  - Token airdrops
  - Official certifications
- **Reusable Links for Ongoing Programs**: Use reusable links for:
  - Community registrations
  - Event check-ins
  - General verifications

## Security Practices

### API Keys

- **Dedicated Keys for Different Services**: Create separate API keys for different applications or services
- **Regular Rotation**: Rotate API keys every 90 days for enhanced security
- **Least Privilege**: Use API keys only where needed
- **Secure Storage**: Store API keys securely in environment variables or secret management systems
- **Monitor Usage**: Regularly check API key usage in the dashboard

### Webhook Security

- **Strong Webhook Secrets**: Use a secure random generator to create long, complex webhook secrets
- **Always Verify Signatures**: Verify the signature of every webhook before processing
- **HTTPS Only**: Only use HTTPS URLs for webhooks
- **Error Handling**: Implement proper error handling for webhook failures
- **Idempotent Processing**: Design webhook handlers to safely process duplicate deliveries

### Token Gating

- **Test Token Requirements**: Ensure token requirements are reasonable and testable
- **Clear Instructions**: Provide clear instructions about what tokens are required
- **Balance Security and Accessibility**: Set token thresholds that are secure but accessible
- **Consider Price Volatility**: For volatile tokens, consider using NFTs or adjusting thresholds periodically
- **Alternative Paths**: When possible, provide alternative verification methods for users without tokens

## User Experience

### Communication

- **Provide Context**: Give users context about why they're being asked to verify their wallet
- **Set Expectations**: Clearly communicate what information will be collected and how it will be used
- **Success Messages**: Provide clear success messages after verification is complete
- **Error Handling**: Give helpful error messages when verifications fail

### Verification Flow

- **Minimize Steps**: Keep the verification process as simple as possible
- **Mobile Optimization**: Ensure the verification flow works well on mobile devices
- **Browser Compatibility**: Test on different browsers and devices
- **Guided Experience**: Provide guidance for users unfamiliar with wallet signing
- **Progress Indicators**: Show progress in multi-step verifications

### Redirect Strategy

- **Seamless Returns**: Redirect users back to your application after verification
- **Contextual Redirects**: Customize redirects based on the verification purpose
- **Fallback URLs**: Provide a default redirect URL for successful verifications
- **Error Handling**: Handle failed verifications gracefully with appropriate redirects

## Implementation Strategies

### Integration Approaches

- **Direct API Integration**: Use direct API calls for deep integration with your application
- **SDK Usage**: Leverage the Python SDK for simplified integration in Python applications
- **Webhook-Driven Architecture**: Design your system to act on webhook events
- **Iframe Integration**: Consider iframe integration for seamless in-app verification experiences

### Testing

- **Test with Different Wallets**: Test verifications with various wallet types
- **Test Token Gating**: Test token-gated verifications with different token balances
- **Webhook Testing**: Use the webhook testing tool to verify your endpoint integration
- **Security Testing**: Regularly test your webhook security implementation

### Monitoring and Maintenance

- **Check Webhook Delivery Status**: Regularly check webhook delivery status in the dashboard
- **Monitor Verification Rates**: Track how many users complete vs. abandon verifications
- **Update Expired Verifications**: Renew or replace expired verifications
- **Regular Security Reviews**: Periodically review your security practices

## Use Case Specific Recommendations

### Event Check-ins

- **QR Codes**: Generate QR codes linking to verification URLs for easy in-person scanning
- **Expiration Timing**: Set expiration to shortly after the event ends
- **Collect Relevant Info**: Gather information relevant to the event (e.g., dietary preferences, t-shirt size)
- **One-Time Use**: Use one-time links for exclusive events

### Community Registration

- **Folder Organization**: Create separate folders for different community segments
- **Standardized Fields**: Standardize custom fields across related registrations
- **Social Verification**: Use social media verification for community building
- **Token Thresholds**: Set appropriate token thresholds for community tiers

### Token Airdrops

- **Security Focus**: Implement strict security measures for airdrops
- **One-Time Links**: Always use one-time links for token airdrops
- **Short Expirations**: Set relatively short expiration periods
- **Required Fields**: Collect necessary information for compliance and distribution

### Membership Verification

- **Tiered Access**: Create different verifications for different membership tiers
- **Token-Based Tiers**: Use token gating with different thresholds for each tier
- **Renewal Process**: Plan for membership renewal and verification updates
- **Member Dashboard**: Integrate with a member dashboard for a seamless experience

## Scaling and Performance

### High-Volume Scenarios

- **Rate Limit Awareness**: Be aware of API rate limits for high-volume scenarios
- **Batched Processing**: Process webhook data in batches when possible
- **Caching**: Implement caching for frequently accessed verification data
- **Asynchronous Processing**: Use asynchronous processing for webhook handling

### Enterprise Considerations

- **Multiple Admin Access**: Plan for multiple administrators with separate access
- **Audit Trails**: Maintain audit logs of all verification activities
- **Data Retention**: Define and implement appropriate data retention policies
- **Backup Strategy**: Implement regular backups of verification data 