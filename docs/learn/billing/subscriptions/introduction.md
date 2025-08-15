# Introduction

> Subscriptions in Creem allow you to create recurring payment plans for your products and services. This documentation will guide you through the key concepts and implementation details of the subscription system.

## Understanding Subscriptions

A subscription represents a recurring payment agreement between you and your customer. When a customer subscribes to your product, they agree to be billed periodically (monthly, yearly, etc.) until they cancel their subscription.

## Key Concepts

### Subscription Status

A subscription can be in different states throughout its lifecycle:

* **Active:** The subscription is current and payments are being processed normally
* **Past Due:** A payment attempt has failed but the subscription is still active and retrying.
* **Canceled:** The subscription has been terminated
* **Trialing:** The subscription is in a trial period before the first payment
* **Incomplete:** The subscription and checkout session was created but not paid

### Billing Cycles

Subscriptions operate on billing cycles that determine when payments are collected. You can set up various billing intervals:

* Monthly billing
* Yearly billing
* Custom intervals (quarterly, 6 months, etc.)

## Creating a Subscription

To create a subscription, you'll need to:

1. Set up a subscription product in your Creem dashboard
2. Generate a checkout session for the subscription
3. Direct your customer to the checkout URL

### Code Example

```jsx
const subscriptionCheckout = await axios.post(
  `https://api.creem.io/v1/checkouts`,
  {
    product_id: 'prod_your-subscription-id',
  },
  {
    headers: { "x-api-key": `creem_123456789` },
  }
);
```

For more details on checkout session options, navigate to our [Checkout Session Introduction](https://docs.creem.io/learn/checkout-session/introduction)

## Managing Subscriptions

Creem provides several ways to manage active subscriptions:

* **Update billing information:** Customers can update their payment method through the customer portal
* **Cancel subscriptions:** Customers or merchants can cancel at any time, through the Dashboard, customer portal or APIs
* **Change prices:** Merchants can update the price of a subscription, that takes into effect in the next billing cycle
* **Seat Based Billing:** Merchants can update the usage of a specific subscription based on seats or units through the Dashboard or API
