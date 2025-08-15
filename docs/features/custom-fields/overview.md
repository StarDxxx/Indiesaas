# Overview

> Enable custom fields on product checkout sessions.

# Custom Fields with Creem

Welcome to Creem's Custom Fields documentation! This feature allows you to collect additional information from customers during checkout by adding customizable fields to your product purchase flow.

## Getting Started

Setting up custom fields for your product is straightforward and requires minimal configuration:

1. Navigate to Your Product Settings
   * Log into your Creem Dashboard
   * Go to "Products" section
   * Create a new product
   * Enable "Custom Fields" feature
2. Configure Your Custom Fields
   * Choose the field type (text, number, email, etc.)
   * Set the field name and label
   * Configure input validation rules
   * Save your configuration

## How It Works

When custom fields are configured, they automatically appear during the checkout process. The collected information is then:

* **Stored securely:** All custom field data is encrypted and stored securely
* **Accessible via Webhook:** Data is included in the `checkout.completed` webhook event
* **Available in Dashboard:** View responses in your merchant dashboard

## Common Use Cases

* **Integration IDs:** Collect user IDs from other platforms or systems
* **Contact Information:** Gather phone numbers, alternative email addresses, or social media handles
* **Customization Details:** Collect preferences, sizes, or specifications
* **Business Information:** Company names, tax IDs, or registration numbers
* **Event Details:** Dates, attendance information, or dietary preferences

## Best Practices

* Keep required fields to a minimum
* Use clear, descriptive field labels
* Select appropriate validation rules
* Consider mobile user experience

**Pro Tips**

* Use conditional fields when appropriate
* Group related fields together
* Test the checkout flow thoroughly

## Webhook Integration

Custom field data is automatically included in the `checkout.completed` webhook payload, making it easy to integrate with your systems.
[Learn more about the checkout.completed webhook](https://docs.creem.io/learn/webhooks/event-types).

**Need Help?**

Our support team is ready to assist you with setting up custom fields. Contact us at [support@creem.co](mailto:support@creem.co)