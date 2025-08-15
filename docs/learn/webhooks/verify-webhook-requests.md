# Verify Webhook Requests

> How to verify Creem signature on webhook objects.

## How to verify Creem signature?

Creem signature is sent in the `creem-signature` header of the webhook request. The signature is generated using the HMAC-SHA256 algorithm with the webhook secret as the key, and the request payload as the message.

<AccordionGroup>
  <Accordion title="Sample Webhook Header">
    ```json
    {
    'creem-signature': 'dd7bdd2cf1f6bac6e171c6c508c157b7cd3cc1fd196394277fb59ba0bdd9b87b'
    }
    ```
  </Accordion>
</AccordionGroup>

To verify the signature, you need to generate the signature using the same algorithm and compare it with the signature sent in the header. If the two signatures match, the request is authentic.

<Tip>
  You can find your webhook secret on the Developers>Webhook page.
</Tip>

<img style={{ borderRadius: '0.5rem' }} src="https://nucn5fajkcc6sgrd.public.blob.vercel-storage.com/Screenshot%202024-10-03%20at%2014.26.39-MtSMvooQi4OrZoh9eMyFZngfc0CrQn.png" />

To generate the signature, you can use the following code snippet:

```typescript
import * as crypto from 'crypto';

  generateSignature(payload: string, secret: string): string {
    const computedSignature = crypto
      .createHmac('sha256', secret)
      .update(payload)
      .digest('hex');
    return computedSignature;
  }
```

In the code snippet above, the `payload` is the request body, and the `secret` is the webhook secret.
Simply compare the generated Signature with the one received on the header to complete the verification process.
