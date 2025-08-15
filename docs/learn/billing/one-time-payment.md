# One Time Payments

> One Time Payments in Creem allow you to accept single, non-recurring payments for your products and services. This documentation will guide you through the key concepts and implementation details of the one-time payment system.

## Understanding One Time Payments

A one time payment represents a single transaction between you and your customer. When a customer makes a one time payment, they are charged once for the full amount of the purchase.

## Key Concepts

### Payment Status

A payment can be in different states throughout its lifecycle:

* **Pending:** The payment has been initiated but not yet completed
* **Paid:** The payment has been successfully processed
* **Refunded:** The payment has been refunded to the customer
* **Partially Refunded:** The payment has been partially refunded to the customer

## Creating a One Time Payment

To create a one time payment, you'll need to:

1. Set up a product in your Creem dashboard
2. Generate a checkout session for the payment
3. Direct your customer to the checkout URL

### Code Example

```jsx
const paymentCheckout = await axios.post(
  `https://api.creem.io/v1/checkouts`,
  {
    product_id: 'prod_your-product-id',
    request_id: 'your-request-id',
    metadata: {
      customerId: 'your-customer-id'
    }
  },
  {
    headers: { "x-api-key": `creem_123456789` },
  }
);
```

## Managing Payments

Creem provides several payment management features:

* **Refund payments:** Process full or partial refunds directly throught the Creem Dashboard
* **Payment history:** View detailed transaction history
* **Payment metadata:** Add custom data to payments for tracking
* **Payment Custom Fields:** Add custom input fields on your checkout session that your users can fill
