# Branding Customization

> Customize your checkout and email receipts with your brand logo, colors, and theme for a seamless customer experience.

# Branding Your Checkout & Receipts

Deliver a seamless, on-brand experience from your application to the checkout and beyond. Creem lets you customize your checkout flow and email receipts with your store's logo, colors, and theme—ensuring your customers always feel at home.

<Frame caption="Branded checkout example">
  <img style={{ borderRadius: '0.5rem', maxWidth: 600 }} src="https://nucn5fajkcc6sgrd.public.blob.vercel-storage.com/Screenshot%202025-05-07%20at%2022.54.09-yY6OBPt5K5S0Ek9WmsA3AXk3p06awN.png" alt="Example of a branded checkout with custom logo and colors" />
</Frame>

## Why Customize Branding?

* **Consistent brand experience** from your app to checkout and receipts
* **Build trust** with your customers
* **Increase conversion** by reducing friction and confusion

<Tip>
  Your logo and colors are used on both the checkout page and the email receipt sent after a successful payment.
</Tip>

## How to Update Your Store Branding

<Steps>
  <Step title="Open Account Settings">
    Click your profile icon in the top right corner, then select <b>Settings</b> for your current store.
  </Step>

  <Step title="Choose Branding Menu">
    In the settings sidebar, navigate to <b>Branding</b>.
  </Step>

  <Step title="Customize Your Branding">
    <ul>
      <li><b>Upload your logo</b> (used on checkout and email receipts)</li>
      <li><b>Select your default checkout theme</b> (light or dark)</li>
      <li><b>Pick your accent color</b> (used for buttons, upsells, and field borders)</li>
      <li><b>Set your accent hover color</b> (for button hover states)</li>
      <li><b>Choose your text color</b> (for dynamic buttons and component text)</li>
    </ul>
  </Step>

  <Step title="Save and Preview">
    Save your changes. You can preview your checkout with the new branding instantly.
  </Step>
</Steps>

<Frame caption="Branding settings UI">
  <img style={{ borderRadius: '0.5rem', maxWidth: 600 }} src="https://nucn5fajkcc6sgrd.public.blob.vercel-storage.com/Screenshot%202025-05-07%20at%2022.55.01-7k1fgfuPbZHiOKxelfiAjYJNXZHEXB.png" alt="Creem branding settings UI with logo upload and color pickers" />
</Frame>

## Test Mode vs Live Mode

You can safely experiment with different branding options in <b>test mode</b>—these changes won't affect your live checkout. When you're ready, switch to <b>live mode</b> and apply your final branding for real customers.

<CardGroup cols={2}>
  <Card title="Test Mode" icon="flask">
    Try out new logos, colors, and themes without impacting your live store. Perfect for previewing and iterating.
  </Card>

  <Card title="Live Mode" icon="rocket">
    Confident in your branding? Switch to live mode to update the experience for your customers.
  </Card>
</CardGroup>

## Programmatic Theme Selection

You can override the default checkout theme by appending <code>?theme=light</code> or <code>?theme=dark</code> to your checkout URL before redirecting your customers.

<Tip>
  Example: <code>[https://www.creem.io/payment/prod\_3pcofZ4pTXtuvdDb1j2MMp?theme=dark](https://www.creem.io/payment/prod_3pcofZ4pTXtuvdDb1j2MMp?theme=dark)</code>
</Tip>

## Best Practices

* Use a high-contrast logo with a transparent background for best results
* Choose accessible color combinations for text and buttons
* Preview your checkout and email receipts in both light and dark themes
* Test your branding in both test and live modes before going live

<aside>
  <b>Need help?</b> Reach out to our support team for guidance on branding best practices or troubleshooting.
</aside>
