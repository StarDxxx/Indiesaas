# Update Subscription

## OpenAPI

````yaml post /v1/subscriptions/{id}
paths:
  path: /v1/subscriptions/{id}
  method: post
  servers:
    - url: https://api.creem.io
    - url: https://test-api.creem.io
  request:
    security: []
    parameters:
      path:
        id:
          schema:
            - type: string
              required: true
      query: {}
      header:
        x-api-key:
          schema:
            - type: string
              required: true
      cookie: {}
    body:
      application/json:
        schemaArray:
          - type: object
            properties:
              items:
                allOf:
                  - description: >-
                      List of subscription items to update/create. If no item ID
                      is provided, the item will be created.
                    type: array
                    items:
                      $ref: '#/components/schemas/UpsertSubscriptionItemEntity'
              update_behavior:
                allOf:
                  - type: string
                    description: >-
                      The update behavior for the subscription (defaults to
                      proration)
                    enum:
                      - proration-charge-immediately
                      - proration-charge
                      - proration-none
                    default: proration-charge
            required: true
            refIdentifier: '#/components/schemas/UpdateSubscriptionRequestEntity'
        examples:
          example:
            value:
              items:
                - id: <string>
                  product_id: <string>
                  price_id: <string>
                  units: 123
              update_behavior: proration-charge
  response:
    '200':
      application/json:
        schemaArray:
          - type: object
            properties:
              id:
                allOf:
                  - type: string
                    description: Unique identifier for the object.
              mode:
                allOf:
                  - type: string
                    enum:
                      - test
                      - prod
                      - sandbox
                    description: String representing the environment.
              object:
                allOf:
                  - type: string
                    description: >-
                      String representing the object's type. Objects of the same
                      type share the same value.
                    example: subscription
              product:
                allOf:
                  - description: The product associated with the subscription.
                    oneOf:
                      - $ref: '#/components/schemas/ProductEntity'
                      - type: string
              customer:
                allOf:
                  - description: The customer who owns the subscription.
                    oneOf:
                      - $ref: '#/components/schemas/CustomerEntity'
                      - type: string
              items:
                allOf:
                  - description: Subscription items.
                    type: array
                    items:
                      $ref: '#/components/schemas/SubscriptionItemEntity'
              collection_method:
                allOf:
                  - type: string
                    description: >-
                      The method used for collecting payments for the
                      subscription.
                    example: charge_automatically
              status:
                allOf:
                  - type: string
                    description: The current status of the subscription.
                    enum:
                      - active
                      - canceled
                      - unpaid
                      - paused
                      - trialing
                    example: active
              last_transaction_id:
                allOf:
                  - type: string
                    description: The ID of the last paid transaction.
                    example: tran_3e6Z6TzvHKdsjEgXnGDEp0
              last_transaction:
                allOf:
                  - description: The last paid transaction.
                    allOf:
                      - $ref: '#/components/schemas/TransactionEntity'
              last_transaction_date:
                allOf:
                  - format: date-time
                    type: string
                    description: The date of the last paid transaction.
                    example: '2024-09-12T12:34:56Z'
              next_transaction_date:
                allOf:
                  - format: date-time
                    type: string
                    description: >-
                      The date when the next subscription transaction will be
                      charged.
                    example: '2024-09-12T12:34:56Z'
              current_period_start_date:
                allOf:
                  - format: date-time
                    type: string
                    description: The start date of the current subscription period.
                    example: '2024-09-12T12:34:56Z'
              current_period_end_date:
                allOf:
                  - format: date-time
                    type: string
                    description: The end date of the current subscription period.
                    example: '2024-09-12T12:34:56Z'
              canceled_at:
                allOf:
                  - type: string
                    description: >-
                      The date and time when the subscription was canceled, if
                      applicable.
                    example: '2024-09-12T12:34:56Z'
                    format: date-time
                    nullable: true
              created_at:
                allOf:
                  - format: date-time
                    type: string
                    description: The date and time when the subscription was created.
                    example: '2024-01-01T00:00:00Z'
              updated_at:
                allOf:
                  - type: string
                    description: The date and time when the subscription was last updated.
                    example: '2024-09-12T12:34:56Z'
                    format: date-time
            refIdentifier: '#/components/schemas/SubscriptionEntity'
            requiredProperties:
              - id
              - mode
              - object
              - product
              - customer
              - collection_method
              - status
              - created_at
              - updated_at
        examples:
          example:
            value:
              id: <string>
              mode: test
              object: subscription
              product:
                id: <string>
                mode: test
                object: <string>
                name: <string>
                description: This is a sample product description.
                image_url: https://example.com/image.jpg
                features:
                  - id: <string>
                    type: <string>
                    description: Get access to discord server.
                price: 400
                currency: EUR
                billing_type: recurring
                billing_period: every-month
                status: <string>
                tax_mode: inclusive
                tax_category: saas
                product_url: https://creem.io/product/prod_123123123123
                default_success_url: https://example.com/?status=successful
                created_at: '2023-01-01T00:00:00Z'
                updated_at: '2023-01-01T00:00:00Z'
              customer:
                id: <string>
                mode: test
                object: <string>
                email: user@example.com
                name: John Doe
                country: US
                created_at: '2023-01-01T00:00:00Z'
                updated_at: '2023-01-01T00:00:00Z'
              items:
                - id: <string>
                  mode: test
                  object: <string>
                  product_id: <string>
                  price_id: <string>
                  units: 123
              collection_method: charge_automatically
              status: active
              last_transaction_id: tran_3e6Z6TzvHKdsjEgXnGDEp0
              last_transaction:
                id: <string>
                mode: test
                object: transaction
                amount: 2000
                amount_paid: 2000
                discount_amount: 2000
                currency: EUR
                type: <string>
                tax_country: US
                tax_amount: 2000
                status: <string>
                refunded_amount: 2000
                order: <string>
                subscription: <string>
                customer: <string>
                description: <string>
                period_start: 123
                period_end: 123
                created_at: 123
              last_transaction_date: '2024-09-12T12:34:56Z'
              next_transaction_date: '2024-09-12T12:34:56Z'
              current_period_start_date: '2024-09-12T12:34:56Z'
              current_period_end_date: '2024-09-12T12:34:56Z'
              canceled_at: '2024-09-12T12:34:56Z'
              created_at: '2024-01-01T00:00:00Z'
              updated_at: '2024-09-12T12:34:56Z'
        description: Successfully update a subscription
  deprecated: false
  type: path
components:
  schemas:
    FeatureEntity:
      type: object
      properties:
        id:
          type: string
          description: Unique identifier for the feature.
        type:
          type: string
          description: The feature type.
        description:
          type: string
          description: A brief description of the feature
          example: Get access to discord server.
      required:
        - id
        - type
        - description
    ProductEntity:
      type: object
      properties:
        id:
          type: string
          description: Unique identifier for the object.
        mode:
          type: string
          enum:
            - test
            - prod
            - sandbox
          description: String representing the environment.
        object:
          type: string
          description: >-
            String representing the object's type. Objects of the same type
            share the same value.
        name:
          type: string
          description: The name of the product
        description:
          type: string
          description: A brief description of the product
          example: This is a sample product description.
        image_url:
          type: string
          description: URL of the product image. Only png as jpg are supported
          example: https://example.com/image.jpg
        features:
          description: Features of the product.
          type: array
          items:
            $ref: '#/components/schemas/FeatureEntity'
        price:
          type: number
          description: The price of the product in cents. 1000 = $10.00
          example: 400
        currency:
          type: string
          description: >-
            Three-letter ISO currency code, in uppercase. Must be a supported
            currency.
          example: EUR
        billing_type:
          type: string
          description: >-
            Indicates the billing method for the customer. It can either be a
            `recurring` billing cycle or a `onetime` payment.
          example: recurring
        billing_period:
          type: string
          description: Billing period
          example: every-month
        status:
          type: string
          description: Status of the product
        tax_mode:
          type: string
          description: >-
            Specifies the tax calculation mode for the transaction. If set to
            "inclusive," the tax is included in the price. If set to
            "exclusive," the tax is added on top of the price.
          example: inclusive
        tax_category:
          type: string
          description: >-
            Categorizes the type of product or service for tax purposes. This
            helps determine the applicable tax rules based on the nature of the
            item or service.
          example: saas
        product_url:
          type: string
          description: >-
            The product page you can redirect your customers to for express
            checkout.
          example: https://creem.io/product/prod_123123123123
        default_success_url:
          type: string
          description: >-
            The URL to which the user will be redirected after successfull
            payment.
          example: https://example.com/?status=successful
          nullable: true
        created_at:
          format: date-time
          type: string
          description: Creation date of the product
          example: '2023-01-01T00:00:00Z'
        updated_at:
          format: date-time
          type: string
          description: Last updated date of the product
          example: '2023-01-01T00:00:00Z'
      required:
        - id
        - mode
        - object
        - name
        - description
        - price
        - currency
        - billing_type
        - billing_period
        - status
        - tax_mode
        - tax_category
        - created_at
        - updated_at
    CustomerEntity:
      type: object
      properties:
        id:
          type: string
          description: Unique identifier for the object.
        mode:
          type: string
          enum:
            - test
            - prod
            - sandbox
          description: String representing the environment.
        object:
          type: string
          description: >-
            String representing the object’s type. Objects of the same type
            share the same value.
        email:
          type: string
          description: Customer email address.
          example: user@example.com
        name:
          type: string
          description: Customer name.
          example: John Doe
        country:
          type: string
          description: The ISO alpha-2 country code for the customer.
          example: US
          pattern: ^[A-Z]{2}$
        created_at:
          format: date-time
          type: string
          description: Creation date of the product
          example: '2023-01-01T00:00:00Z'
        updated_at:
          format: date-time
          type: string
          description: Last updated date of the product
          example: '2023-01-01T00:00:00Z'
      required:
        - id
        - mode
        - object
        - email
        - country
        - created_at
        - updated_at
    SubscriptionItemEntity:
      type: object
      properties:
        id:
          type: string
          description: Unique identifier for the object.
        mode:
          type: string
          enum:
            - test
            - prod
            - sandbox
          description: String representing the environment.
        object:
          type: string
          description: >-
            String representing the object’s type. Objects of the same type
            share the same value.
        product_id:
          type: string
          description: The ID of the product associated with the subscription item.
        price_id:
          type: string
          description: The ID of the price associated with the subscription item.
        units:
          type: number
          description: The number of units for the subscription item.
      required:
        - id
        - mode
        - object
    TransactionEntity:
      type: object
      properties:
        id:
          type: string
          description: Unique identifier for the object.
        mode:
          type: string
          enum:
            - test
            - prod
            - sandbox
          description: String representing the environment.
        object:
          type: string
          description: >-
            String representing the object's type. Objects of the same type
            share the same value.
          example: transaction
        amount:
          type: number
          description: The transaction amount in cents. 1000 = $10.00
          example: 2000
        amount_paid:
          type: number
          description: The amount the customer paid in cents. 1000 = $10.00
          example: 2000
        discount_amount:
          type: number
          description: The discount amount in cents. 1000 = $10.00
          example: 2000
        currency:
          type: string
          description: >-
            Three-letter ISO currency code, in uppercase. Must be a supported
            currency.
          example: EUR
        type:
          type: string
          description: >-
            The type of transaction. payment(one time payments) and
            invoice(subscription)
        tax_country:
          type: string
          description: The ISO alpha-2 country code where tax is collected.
          example: US
          pattern: ^[A-Z]{2}$
        tax_amount:
          type: number
          description: The sale tax amount in cents. 1000 = $10.00
          example: 2000
        status:
          type: string
          description: Status of the transaction.
        refunded_amount:
          type: number
          description: The amount that has been refunded in cents. 1000 = $10.00
          example: 2000
          nullable: true
        order:
          type: string
          description: The order associated with the transaction.
          nullable: true
        subscription:
          type: string
          description: The subscription associated with the transaction.
          nullable: true
        customer:
          type: string
          description: The customer associated with the transaction.
          nullable: true
        description:
          type: string
          description: The description of the transaction.
        period_start:
          type: number
          description: Start period for the invoice as timestamp
        period_end:
          type: number
          description: End period for the invoice as timestamp
        created_at:
          type: number
          description: Creation date of the order as timestamp
      required:
        - id
        - mode
        - object
        - amount
        - currency
        - type
        - status
        - created_at
    UpsertSubscriptionItemEntity:
      type: object
      properties:
        id:
          type: string
          description: The id of the item to update.
        product_id:
          type: string
          description: The ID of the product associated with the subscription item.
        price_id:
          type: string
          description: The ID of the price associated with the subscription item.
        units:
          type: number
          description: The number of units for the subscription item.

````