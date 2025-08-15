# Payment Links Customization

> Learn how to use and customize Payment Links in Creem for no-code, flexible payment flows.

# Payment Links

Payment Links are the fastest way to start accepting payments with Creem—no code, no API, no SDK required. Just create a product, copy the link, and share it with your customers.

## Getting Started

To create your first payment link, follow our <a href="/quickstart">Quickstart</a> guide. You'll learn how to:

* Create a product in your Creem dashboard
* Instantly generate a payment link for that product

<Tip>
  After following the Quickstart, you'll have a product and a payment link ready to use—no coding required!
</Tip>

## Why Use Payment Links?

* **No-code:** Share a link, get paid—no integration work needed
* **Instant setup:** Go live in minutes
* **Customizable:** Add metadata and themes for advanced workflows
* **Perfect for:** Social media, email, chat, or anywhere you can paste a link

<CardGroup cols={2}>
  <Card title="No-Code Simplicity" icon="bolt">
    Start selling instantly by sharing a link. No API keys, SDKs, or developer time required.
  </Card>

  <Card title="Advanced Customization" icon="sliders">
    Pass custom data and themes via URL parameters for powerful, flexible workflows.
  </Card>
</CardGroup>

## Customizing Payment Links

You can extend the power of payment links by passing custom data and appearance options directly in the URL—no backend or API required.

### 1. Add Custom Metadata

Want to track a user, campaign, or any custom info with each payment? Just append metadata as query parameters:

**Example:**

```
https://creem.io/payment/prod_abc123?metadata[reference_user_id]=user1234&metadata[referral]=youtube
```

* This will save `reference_user_id: user1234` and `referral: youtube` as metadata on the payment.
* You can add as many metadata fields as you need, using the `metadata[key]=value` format.

<Tip>
  Metadata is available in your dashboard and webhooks, making it easy to connect payments to users, campaigns, or any workflow—no code required.
</Tip>

### 2. Set the Checkout Theme

You can control the appearance of the checkout by adding a `theme` parameter:

* `?theme=dark` for a dark checkout
* `?theme=light` for a light checkout

**Example:**

```
https://creem.io/payment/prod_abc123?theme=dark
```

You can combine theme and metadata parameters:

```
https://creem.io/pay/prod_abc123?theme=dark&metadata[reference_user_id]=user1234
```

<Frame caption="Dark themed checkout example">
  <img style={{ borderRadius: '0.5rem', maxWidth: 600 }} src="https://nucn5fajkcc6sgrd.public.blob.vercel-storage.com/Screenshot%202025-05-07%20at%2022.54.09-yY6OBPt5K5S0Ek9WmsA3AXk3p06awN.png" alt="Creem checkout page in dark theme" />
</Frame>

## Best Practices

* Use metadata to track users, campaigns, or any custom info
* Choose a theme that matches your brand or context
* Test your payment links before sharing widely
* Share links anywhere: email, chat, social, QR codes, and more

<aside>
  <b>Need help?</b> Our support team is here to help you get the most out of payment links. Reach out for advanced workflows or troubleshooting.
</aside>
