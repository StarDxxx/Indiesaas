# Customer Portal

> Customers can cancel and refund subscriptions by themselves.

## What is a Customer Portal?

After every successful payment, your customers will receive an email with a link to their Customer Portal. This portal allows them to manage their subscriptions, payment methods, and personal information.

This email contains a magic link, to a completely different authentication mechanism, in which they are able to access their account which allows them to execute the aforementioned actions.

<AccordionGroup>
  <Accordion icon="receipt" title="Receipt Example">
    <img style={{ borderRadius: '0.5rem' }} src="https://nucn5fajkcc6sgrd.public.blob.vercel-storage.com/Screenshot%202024-12-17%20at%2023.26.24-zus6vfFFS6vdT5GSwjjXSbinB5KWZp.png" />
  </Accordion>

  <Accordion icon="right-to-bracket" title="Magic Link Login Example">
    <img style={{ borderRadius: '0.5rem' }} src="https://nucn5fajkcc6sgrd.public.blob.vercel-storage.com/magic-link-nq675ngtIqI95c6EeGiHPa8id6D1x1.png" />
  </Accordion>
</AccordionGroup>

## What can customers do in the Customer Portal?

### 1. Cancel a subscription

Upon entering the Customer Portal, customers can cancel their subscriptions by selecting an active subscription, and clicking on the **Manage Subscription** button.
This will open a details sheet on the right side of the screen, where a **Cancel Subscription** button is available.

This will immediately cancel their subscription and they will no longer be charged for it.

<img style={{ borderRadius: '0.5rem' }} src="https://nucn5fajkcc6sgrd.public.blob.vercel-storage.com/cancel-subscription-e7svTi3ym0foZze7gG8SOa6arqIj78.png" />

### 2. Request Invoice or Support

Customers using the customer portal, can copy all details of a specific payment, including order\_ID and request support from Creem team directly without contacting the merchant.

<img style={{ borderRadius: '0.5rem' }} src="https://nucn5fajkcc6sgrd.public.blob.vercel-storage.com/customer-portal-Klxod6wVtoF6JFJdeEDPOPPxDMJ31q.png" />

### 3. Request Customer Portal Login through the API

Merchants can generate a customer portal login for their users, using the API, providing the `customer_id`.
The API responds a URL, that the merchant can then use to redirect their customer to the customer portal.

<AccordionGroup>
  <Accordion title="Response">
    ```json
    {
      "customer_portal_link": "https://creem.io/my-orders/login/xxxxxxxxxx"
    }
    ```
  </Accordion>
</AccordionGroup>

<CodeGroup>
  ```javascript getCustomerPortalUrl.js
      const redirectUrl = await axios.post(
        `https://api.creem.io/v1/customers/billing`,
          {
            "customer_id": "cust_xxxxxxx",
          },
          {
            headers: { "x-api-key": `creem_123456789` },
          },
      );
  ```

  ```bash getCustomerPortalUrl.sh
  curl -X 'POST' \
    'https://api.creem.io/v1/customers/billing' \
    -H 'accept: application/json' \
    -H 'x-api-key: creem_123456789' \
    -H 'Content-Type: application/json' \
    -d '{
    "customer_id": "cust_xxxxxxx"
  }'

  ```
</CodeGroup>
