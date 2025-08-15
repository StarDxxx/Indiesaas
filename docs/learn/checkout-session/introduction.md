# Introduction

> Create checkout sessions for each payment and user independently.

<Frame>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/3eTSRXz9OdA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen />
</Frame>

## Why use a checkout session?

With checkout sessions generated dynamically instead of just using a product payment link, you are able to pass a `request_id` to the session.

This allows you to track the payment status and the user that made the payment in your system in a more organized way, and gives you the flexibility to track that payment with any ID you choose instead of relying on Creem IDs.

## Create a checkout session

You can create a checkout session with a product ID

<Tip>
  You can find a product ID by going to the products tab and clicking on the product options and selecting "Copy ID".
</Tip>

Additionally, you can pass a `request_id` to the session to track the payment in your system.
You will also need the API key to authenticate the request.

<CodeGroup>
  ```javascript getCheckout.js
      const redirectUrl = await axios.post(
        `https://api.creem.io/v1/checkouts`,
          {
            product_id: 'prod_6tW66i0oZM7w1qXReHJrwg',
            request_id: 'your-request-id',
          },
          {
            headers: { "x-api-key": `creem_123456789` },
          },
      );
  ```

  ```bash getCheckout.sh
  curl -X POST https://api.creem.io/v1/checkouts \
    -H "x-api-key: creem_123456789"
    -D '{
      "product_id": "prod_6tW66i0oZM7w1qXReHJrwg",
      "request_id": "your-request-id"
      }'
  ```
</CodeGroup>

The above request will return a checkout session object with a `checkout_url` that you can use to redirect the user to the payment page.

Any payments made with this checkout session will have the `request_id` you provided on the Redirect URL, as well as the webhook event.

## Metadata

The `request_id` is only returned in the `checkout.completed` webhook (which is very useful for one-time payments), but it’s not sent with every new subscription transaction.

To make things easier, we also allow you to pass `metadata` in a checkoutSession with or without the `request_id`. This metadata will be saved in the Subscription object and returned with every subsequent webhook.

<CodeGroup>
  ```javascript getCheckout.js
      const redirectUrl = await axios.post(
        `https://api.creem.io/v1/checkouts`,
          {
            "request_id": "your-request-id",
            "product_id": "prod_your-product-id",
            "metadata": {
              "userId": "my_internal_customer_id",
              "any_key": "any_value"
            }
          },
          {
            headers: { "x-api-key": `creem_123456789` },
          },
      );
  ```

  ```bash getCheckout.sh
  curl -X 'POST' \
    'https://test-api.creem.io/v1/checkouts' \
      -H 'accept: application/json' \
      -H 'x-api-key: creem_123456789' \
      -H 'Content-Type: application/json' \
      -d '{
        "request_id": "your-request-id",
        "product_id": "prod_your-product-id",
        "metadata": {
          "userId": "my_internal_customer_id",
          "any_key": "any_value"
          }
      }'
  ```
</CodeGroup>

## Success URL

You can pass a custom `success_url` for each checkout\_session, which will override the `success_url` set on the product.

This allows you to dynamically redirect users to custom pages after each payment (useful for directing users to their specific account resources after payment).

<CodeGroup>
  ```javascript getCheckout.js
      const redirectUrl = await axios.post(
        `https://api.creem.io/v1/checkouts`,
          {
            "success_url": "https://example.com",
            "product_id": "prod_your-product-id",
          },
          {
            headers: { "x-api-key": `creem_123456789` },
          },
      );
  ```

  ```bash getCheckout.sh
  curl -X 'POST' \
    'https://test-api.creem.io/v1/checkouts' \
      -H 'accept: application/json' \
      -H 'x-api-key: creem_123456789' \
      -H 'Content-Type: application/json' \
      -d '{
        "product_id": "prod_your-product-id",
        "success_url": "https://example.com",
      }'
  ```
</CodeGroup>

## Customer Email

You can pass a `customer.email` directly in the checkout session.
This email will be pre-filled for the user on the checkout session page and cannot be changed.

This is useful if you want to ensure that the user completes the payment using the email they registered on your platform.

<CodeGroup>
  ```javascript getCheckout.js
      const redirectUrl = await axios.post(
        `https://api.creem.io/v1/checkouts`,
          {
            "customer": {
              "email": "yourUserEmail@gmail.com"
            },
            "product_id": "prod_your-product-id",
          },
          {
            headers: { "x-api-key": `creem_123456789` },
          },
      );
  ```

  ```bash getCheckout.sh
  curl -X 'POST' \
    'https://test-api.creem.io/v1/checkouts' \
      -H 'accept: application/json' \
      -H 'x-api-key: creem_123456789' \
      -H 'Content-Type: application/json' \
      -d '{
        "product_id": "prod_your-product-id",
        "customer": {
          "email": "yourUserEmail@gmail.com"
        },
      }'
  ```
</CodeGroup>

## Discount Codes

You can pass a `discount_code` directly in the checkout session.
This discount code will be pre-filled for the user on the checkout session page.

<CodeGroup>
  ```javascript getCheckout.js
      const redirectUrl = await axios.post(
        `https://api.creem.io/v1/checkouts`,
          {
            "product_id": "prod_your-product-id",
            "discount_code": "BF200XX",
          },
          {
            headers: { "x-api-key": `creem_123456789` },
          },
      );
  ```

  ```bash getCheckout.sh
  curl -X 'POST' \
    'https://test-api.creem.io/v1/checkouts' \
      -H 'accept: application/json' \
      -H 'x-api-key: creem_123456789' \
      -H 'Content-Type: application/json' \
      -d '{
        "product_id": "prod_your-product-id",
        "discount_code": "BF200XX",
      }'
  ```
</CodeGroup>

## Seat Based Billing

You can pass a `units` amount directly in the checkout session.
The product price will be used as the base price for one seat/unit of the product and the checkout session will reflect the (base price x units) to be charged.

<CodeGroup>
  ```javascript getCheckout.js
      const redirectUrl = await axios.post(
        `https://api.creem.io/v1/checkouts`,
          {
            "product_id": "prod_your-product-id",
            "units": 2,
          },
          {
            headers: { "x-api-key": `creem_123456789` },
          },
      );
  ```

  ```bash getCheckout.sh
  curl -X 'POST' \
    'https://test-api.creem.io/v1/checkouts' \
      -H 'accept: application/json' \
      -H 'x-api-key: creem_123456789' \
      -H 'Content-Type: application/json' \
      -d '{
        "product_id": "prod_your-product-id",
        "units": 2,
      }'
  ```
</CodeGroup>
