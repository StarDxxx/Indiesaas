# Seat Based Billing

> Seat Based Billing in Creem enables you to charge customers based on the number of seats or users they need, supporting both one-time payments and subscription models. This documentation explains how to implement and manage seat-based billing for your products.

## Understanding Seat Based Billing

Seat Based Billing allows you to set a per-seat price for your product and let customers purchase multiple seats. This is particularly useful for team-based products, enterprise software, or any service where pricing scales with the number of users.

Seat Based Billing in Creem works for both One Time Payments and Subscriptions seamlessly without any special setup.

## Key Concepts

### Per-Seat Pricing

In Seat Based Billing:

* **Base Price:** Set in the Creem dashboard as the price per individual seat
* **Units:** Represents the number of seats being purchased
* **Total Price:** Automatically calculated as (Base Price × Units)

## Implementation

To implement Seat Based Billing, you'll need to:

1. Create a product in your Creem dashboard where the price is the base seat price
2. Generate a checkout session with the desired number of seats
3. Direct your customer to the checkout URL

### Code Example

```javascript
const seatBasedCheckout = await axios.post(
  `https://api.creem.io/v1/checkouts`,
  {
    product_id: 'prod_your-product-id',
    units: 5, // Number of seats to purchase
  },
  {
    headers: { "x-api-key": `creem_123456789` },
  }
);
```

## Managing Seat Changes

You can manage seat quantities for your customers in subscriptions by:

* **Adding seats:** Modify the subscription through the dashboard or update subscription API
* **Reducing seats:** Modify the subscription through the dashboard or update subscription API

### Update Subscription API

If you wish to add or reduce the amount of seats in a given subscription, you can use the subscription API to make changes.
Usually, it is great practice for your system to store the subscription ID of a given customer. With the subscription ID, we can then query Creem API to get all information needed to update a subscription.

1. Querying subscription details
   * With the subscription ID, call the [GET Subscription Creem API](https://docs.creem.io/api-reference/endpoint/get-subscription).
   * Retrieve the Item ID from the subscription item.

<AccordionGroup>
  <Accordion icon="table-tree" title="Retrieve subscription details">
    Query the GET Subscription Creem API with the subscription ID

    ```javascript
    const subscriptionDetails = await axios.get(
      `https://api.creem.io/v1/subscriptions?subscription_id=sub_12312312312'`,
      {
        headers: { "x-api-key": `creem_123456789` },
      }
    );

    ```
  </Accordion>

  <Accordion icon="location-crosshairs" title="Parse the response">
    Parse, locate and store the Item ID of the subscription item, located under the items array.

    ```json
    {
      "id": "sub_2O4LbygGkNJJ6VrStIZz21",
      "object": "subscription",
      "product": {
        "id": "prod_6PyZn18alhCSGwhJXHBdQ4",
        "name": "This is a product",
        "description": "This is a product",
        "image_url": null,
        "price": 1000,
        "currency": "EUR",
        "billing_type": "recurring",
        "billing_period": "every-month",
        "status": "active",
        "tax_mode": "exclusive",
        "tax_category": "saas",
        "default_success_url": "",
        "created_at": "2025-01-10T06:18:31.583Z",
        "updated_at": "2025-01-10T06:18:31.583Z",
        "mode": "local"
      },
      "customer": {
        "id": "cust_3y4k2CELGsw7n9Eeeiw2hm",
        "object": "customer",
        "email": "alec@creem.io",
        "name": "Alec Erasmus",
        "country": "NL",
        "created_at": "2024-12-09T16:09:20.709Z",
        "updated_at": "2024-12-09T16:09:20.709Z",
        "mode": "local"
      },
      "items": [
        {
          "object": "subscription_item",
          "id": "sitem_3l8jhRR2jWWhIBbJrKLwPT",
          "product_id": "prod_6PyZn18alhCSGwhJXHBdQ4",
          "price_id": "pprice_3WBdYmRIFBgaXRM3Adcdpp",
          "units": 10,
          "created_at": "2025-01-10T08:49:13.790Z",
          "updated_at": "2025-01-10T08:49:13.790Z",
          "mode": "local"
        }
      ],
      "collection_method": "charge_automatically",
      "status": "active",
      "last_transaction_id": "tran_5jcJjZ1xEczUjqYiOjPSyd",
      "last_transaction_date": "2025-01-10T08:49:22.301Z",
      "next_transaction_date": "2025-02-10T08:49:10.000Z",
      "current_period_start_date": "2025-01-10T08:49:10.000Z",
      "current_period_end_date": "2025-02-10T08:49:10.000Z",
      "canceled_at": null,
      "created_at": "2025-01-10T08:49:13.777Z",
      "updated_at": "2025-01-10T08:49:19.991Z",
      "mode": "local"
    }
    ```
  </Accordion>
</AccordionGroup>

2. Make the subscription change
   * With the Item Id and Subscription ID, call the [UPDATE subscription API](https://docs.creem.io/api-reference/endpoint/get-subscription).
   * Use the `units` field to the desired amount of seats changed.

<Accordion icon="table-tree" title="Update Subscription">
  Update the Subscription with the desired units amount

  ```javascript
  const subscriptionDetails = await axios.post(
    `https://api.creem.io/v1/subscriptions/sub_123123`,
    {
      "items": [
        {
          "id": "sitem_123213123",
          "units": 2
        }
      ]
    },
    {
      headers: { "x-api-key": `creem_123456789` },
    }
  );

  ```
</Accordion>

### Manual subscription changes through the Creem Dashboard

You can also modify subscription seats through your Creem Dashboard as a merchant.
Simply click on a subscription, and upon the details sheet opening, click on the "Modify Subscription" button

<Frame>
  <img style={{ borderRadius: '0.5rem' }} src="https://nucn5fajkcc6sgrd.public.blob.vercel-storage.com/Screenshot%202025-01-10%20at%2015.56.28-aOLgNWFNoWZLLpytZ5Y5H94HMl8rxb.png" />
</Frame>

### Billing after subscription updates

The new amount will be charged upon subscription renewal. If you need pro-rata charges or different use cases, contact the Creem team.

<Warning>
  Remember to validate and track seat usage in your application to ensure customers don't exceed their purchased seat limit.
</Warning>
