# Return URLs

> Understand how to redirect users back to your website after a successful payment.

## What is a Return/Redirect URL?

Return and Redirect URLs, are urls that your customer will be redirected to, after a successful payment.
They contain important information signed by creem, that you can use to verify the payment and the user.

Using these URLs, you can create a seamless experience for your users, by redirecting them back to your website after a successful payment.

<Tip>
  You have the optionality to use the information in the URL query parameters, or to use webhooks to receive updates on your application automatically, or both.
</Tip>

## How to set a Return/Redirect URL

<AccordionGroup>
  <Accordion icon="table-tree" title="Option 1: Set a success URL on the product creation.">
    When creating a product, you can optionally add a Return URL.
    This URL will be used as a default to every payment done to this product, in case you don't provide other URLs when creating a checkout session or using a payment link.

    <img style={{ borderRadius: '0.5rem' }} src="https://nucn5fajkcc6sgrd.public.blob.vercel-storage.com/product-return-url-Wx2o0b0XfQ2mWdcue6wXAh7LZywYal.png" />
  </Accordion>

  <Accordion icon="location-crosshairs" title="Option 2: Set a success URL when creating a checkout session">
    You can bypass the product Return URL by setting a success URL on the checkout session request by adding the `success_url` parameter.
  </Accordion>
</AccordionGroup>

## What is included on the Return URL?

A return URL will always contain the following query parameters, and will look like the following:

<Tip>
  `https://yourwebsite.com?checkout_id=ch_1QyIQDw9cbFWdA1ry5Qc6I&order_id=ord_4ucZ7Ts3r7EhSrl5yQE4G6&customer_id=cust_2KaCAtu6l3tpjIr8Nr9XOp&subscription_id=sub_ILWMTY6uBim4EB0uxK6WE&product_id=prod_6tW66i0oZM7w1qXReHJrwg&signature=044bd1691d254c4ad4b31b7f246330adf09a9f07781cd639979a288623f4394c?`
</Tip>

| Query parameter  | Description                                                                    |
| ---------------- | ------------------------------------------------------------------------------ |
| checkout\_id     | The ID of the checkout session created for this payment.                       |
| order\_id        | The ID of the order created after successful payment.                          |
| customer\_id     | The customer ID, based on the email that executed the successful payment.      |
| subscription\_id | The subscription ID of the product.                                            |
| product\_id      | The product ID that the payment is related to.                                 |
| request\_id      | **Optional** The request ID you provided when creating this checkout session.  |
| signature        | All previous parameters signed by creem using your API-key, verifiable by you. |

## How to verify Creem signature?

To verify the signature, you can use the following code snippet:

```javascript
export interface RedirectParams {
  request_id?: string | null;
  checkout_id?: string | null;
  order_id?: string | null;
  customer_id?: string | null;
  subscription_id?: string | null;
  product_id?: string | null;
}

  private generateSignature(params: RedirectParams, apiKey: string): string {
    const data = Object.entries(params)
      .map(([key, value]) => `${key}=${value}`)
      .concat(`salt=${apiKey}`)
      .join('|');
    return crypto.createHash('sha256').update(data).digest('hex');
  }
```

In summary, concatenate all parameters and the salt (your API-key) with a `|` separator, and hash it using SHA256. This will generate a signature that you can compare with the signature provided in the URL.
