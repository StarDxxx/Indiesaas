# Typescript SDK

> Type-safe SDK for the Creem API – manage SaaS subscriptions, products, and revenue in TypeScript/Node.js environments.

<Tip>
  The Creem TypeScript SDK is available as an [npm package](https://www.npmjs.com/package/creem) for seamless integration with your TypeScript and Node.js projects.
  The SDK is also available on [GitHub](https://github.com/armitage-labs/creem-sdk) for those who prefer to explore the source code directly.
</Tip>

## Installation

Install with your preferred package manager:

```bash
npm install creem
# or
yarn add creem zod
# or
pnpm add creem
# or
bun add creem
```

> **Note:** If using Yarn, install `zod` as a peer dependency.

***

## Quick Start

```ts
import { Creem } from "creem";

const creem = new Creem();

async function main() {
  const product = await creem.retrieveProduct({
    productId: "<id>",
    xApiKey: "<api-key>",
  });
  console.log(product);
}

main();
```

***

## Functions Overview

The SDK exposes all major Creem API resources and operations:

* **Products:** `retrieveProduct`, `createProduct`, `searchProducts`
* **Customers:** `retrieveCustomer`, `generateCustomerLinks`
* **Subscriptions:** `retrieveSubscription`, `cancelSubscription`, `updateSubscription`, `upgradeSubscription`
* **Checkout:** `retrieveCheckout`, `createCheckout`
* **Licenses:** `activateLicense`, `deactivateLicense`, `validateLicense`
* **Discounts:** `retrieveDiscount`, `createDiscount`, `deleteDiscount`
* **Transactions:** `searchTransactions`

You can find a detailed documentation of all functions and their parameters in the [SDK README](https://github.com/armitage-labs/creem-sdk?tab=readme-ov-file#creem-sdk)

***

### Server Selection (Test Mode)

Use a specific server by index or URL, by default the SDK will use the production server:

```ts
const creem = new Creem({ serverIdx: 1 }); // 0: production, 1: test-mode
// or
const creem = new Creem({ serverURL: "https://api.creem.io" });
// or
const creem = new Creem({ serverURL: "https://test-api.creem.io" });
```

## Example: Deleting a Discount

<Tabs>
  <Tab title="Instance Method">
    ```ts
    import { Creem } from "creem";

    const creem = new Creem();

    async function run() {
      const result = await creem.deleteDiscount({
        id: "<discount-id>",
        xApiKey: "<api-key>",
      });

      // Handle the result
      console.log(result);
    }

    run();
    ```
  </Tab>

  <Tab title="Standalone Function">
    ```ts
    import { CreemCore } from "creem/core.js";
    import { deleteDiscount } from "creem/funcs/deleteDiscount.js";

    // Use `CreemCore` for best tree-shaking performance.
    // You can create one instance of it to use across an application.
    const creem = new CreemCore();

    async function run() {
      const res = await deleteDiscount(creem, {
        id: "<discount-id>",
        xApiKey: "<api-key>",
      });

      if (!res.ok) {
        throw res.error;
      }

      const { value: result } = res;

      // Handle the result
      console.log(result);
    }

    run();
    ```
  </Tab>
</Tabs>

***

### Retry Strategy

Override retry behavior per call or globally:

```ts
const creem = new Creem({
  retryConfig: {
    strategy: "backoff",
    backoff: { initialInterval: 1, maxInterval: 50, exponent: 1.1, maxElapsedTime: 100 },
    retryConnectionErrors: false,
  },
});
```

***

## Standalone Functions

All SDK methods are also available as named imports for minimal bundle size:

```ts
import { retrieveProduct } from "creem/funcs/retrieveProduct.js";

const product = await retrieveProduct({ productId: "<id>", xApiKey: "<api-key>" });
```

***

## References

* [Creem SDK on npm](https://www.npmjs.com/package/creem)
* [Creem API Docs](https://docs.creem.io/api-reference/introduction)
* [GitHub Releases](https://github.com/armitage-labs/creem-sdk)

***

> For feedback or issues, open a PR or issue on the [Creem SDK GitHub](https://github.com/creem-io/creem-sdk).