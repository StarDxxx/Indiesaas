# Subscription Upgrades

> Learn how to manage subscription upgrades and downgrades using Product Bundles in Creem

## Overview

Subscription upgrades and downgrades in Creem provide a seamless experience for both merchants and customers. When paired with Product Bundles, this functionality becomes even more powerful, enabling self-service subscription management and strategic upsell opportunities.

<Frame>
  <img style={{ borderRadius: "0.5rem" }} src="https://nucn5fajkcc6sgrd.public.blob.vercel-storage.com/product-upgrades-IHSx20ijI5xkwzqJVCdOPLhZxNXuT0.png" />
</Frame>

## Enhanced Experience with Product Bundles

Product Bundles significantly improve the subscription management experience by:

* **Self-Service Management**: Customers can upgrade or downgrade their subscriptions independently through the Customer Portal
* **Transparent Tier Comparison**: Clear visualization of features and benefits across different subscription tiers
* **Streamlined Checkout Upsells**: Present upgrade options during the initial checkout process to increase conversion to higher tiers
* **Simplified Product Organization**: Group related subscription tiers logically for easier management

By implementing Product Bundles alongside your subscription offerings, you create a more intuitive experience that empowers customers while maximizing your revenue potential through strategic tier positioning.

<Card href="/learn/billing/subscriptions/bundles" title="Product Bundles" icon="layer-group">
  Discover how Product Bundles can transform your subscription strategy by
  organizing offerings into intuitive tiers, boosting conversions, and creating
  seamless upgrade paths for your customers.
</Card>

## Managing Subscription Changes

### Programmatic Upgrades

To upgrade or downgrade a subscription programmatically, use our [subscription upgrade endpoint](/api-reference/endpoint/upgrade-subscription):

<CodeGroup>
  ```bash upgrade.sh
  curl -X POST https://api.creem.io/v1/subscriptions/sub_123/upgrade \
    -H "x-api-key: creem_123456789" \
    -H "Content-Type: application/json" \
    -d '{
      "product_id": "prod_456",
      "update_behavior": "proration-charge"
    }'
  ```

  ```typescript upgrade.ts
  import axios from "axios";

  async function upgradeSubscription(
    subscriptionId: string,
    productId: string,
    updateBehavior:
      | "proration-charge-immediately"
      | "proration-charge"
      | "proration-none" = "proration-charge",
  ) {
    const response = await axios.post(
      `https://api.creem.io/v1/subscriptions/${subscriptionId}/upgrade`,
      {
        product_id: productId,
        update_behavior: updateBehavior,
      },
      {
        headers: {
          "x-api-key": "creem_123456789",
          "Content-Type": "application/json",
        },
      },
    );

    return response.data;
  }
  ```
</CodeGroup>

<ResponseField name="update_behavior" type="string" required={false}>
  Controls how the upgrade is processed: - `proration-charge-immediately`:
  Charge prorated amount right away. We'll calculate what your customer has used
  so far, charge them immediately for the difference, and start a new billing
  cycle from today. - `proration-charge`: Add prorated amount to next invoice.
  We'll calculate any unused time on the current subscription as credit, apply
  it to the new subscription price, and bill the difference on the next regular
  invoice while maintaining the original billing cycle. - `proration-none`: No
  proration, change takes effect on next billing cycle. No immediate charges
  will occur—when the current billing period ends, we'll simply start charging
  at the new subscription rate.
</ResponseField>

## Best Practices

1. **Upgrade Path**

   * Design clear upgrade paths
   * Highlight additional value at each tier
   * Make downgrades equally accessible

2. **Customer Experience**
   * Provide clear feature comparisons
   * Show pricing differences
   * Explain pro-rata billing
