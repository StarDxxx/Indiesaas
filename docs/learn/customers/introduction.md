# Introduction

> Customers can be queried by your application to refresh statuses and can do actions by themselves using the Customer Portal.

## Customer Actions

Customers have access to a separated portal where they can manage their subscriptions, payment methods, and personal information. This portal is called the Customer Portal.
Get more information about the Customer Portal [here](/learn/customers/customer-portal).

On the following page, you can also read more about customer receipts, refunds, and how Users access that information.

<Card title="Customer Portal" icon="users" href="/learn/customers/customer-portal">
  Understand how customers can manage their subscriptions and information.
</Card>

Customer objects can also be queried independently by your application so that you can synchronize specific customer data with their subscription statuses and transaction history.

For example, you can query a customer by their email address to refresh their subscription statuses and update your application's UI accordingly.

```bash
curl -X 'GET' \
  'http://api.creem.io/v1/customers?email=alecerasmus@gmail.com' \
  -H 'accept: application/json' \
  -H 'x-api-key: creem_123456789'
```

<AccordionGroup>
  <Accordion title="Sample Response Body">
    ```json
      {
          "id": "cust_3biFPNt4Cz5YRDSdIqs7kc",
          "object": "customer",
          "email": "alecerasmus2@gmail.com",
          "name": "Alec Erasmus",
          "country": "SE",
          "created_at": "2024-09-16T16:13:39.265Z",
          "updated_at": "2024-09-16T16:13:39.265Z",
          "mode": "local"
      }
    ```
  </Accordion>
</AccordionGroup>
