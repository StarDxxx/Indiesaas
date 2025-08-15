# Create Checkout Session

## OpenAPI

````yaml post /v1/checkouts
paths:
  path: /v1/checkouts
  method: post
  servers:
    - url: https://api.creem.io
    - url: https://test-api.creem.io
  request:
    security: []
    parameters:
      path: {}
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
              request_id:
                allOf:
                  - type: string
                    description: Identify and track each checkout request.
              product_id:
                allOf:
                  - type: string
                    description: >-
                      The ID of the product associated with the checkout
                      session.
                    example: prod_1234567890
              units:
                allOf:
                  - type: number
                    description: The number of units for the order.
                    example: 1
              discount_code:
                allOf:
                  - type: string
                    description: Prefill the checkout session with a discount code.
                    example: SUMMER2024
              customer:
                allOf:
                  - description: >-
                      Customer data for checkout session. This will prefill the
                      customer info on the checkout page
                    allOf:
                      - $ref: '#/components/schemas/CustomerRequestEntity'
              custom_field:
                allOf:
                  - description: >-
                      Collect additional information from your customer using
                      custom fields. Up to 3 fields are supported.
                    type: array
                    items:
                      $ref: '#/components/schemas/CustomFieldRequestEntity'
              success_url:
                allOf:
                  - type: string
                    description: >-
                      The URL to which the user will be redirected after the
                      checkout process is completed.
              metadata:
                allOf:
                  - type: object
                    description: Metadata for the checkout in the form of key-value pairs
                    example:
                      userId: user_123
                      visitCount: 42
                      lastVisit: '2023-04-01'
                    additionalProperties: true
            required: true
            refIdentifier: '#/components/schemas/CreateCheckoutRequest'
            requiredProperties:
              - product_id
        examples:
          example:
            value:
              request_id: <string>
              product_id: prod_1234567890
              units: 1
              discount_code: SUMMER2024
              customer:
                id: cust_1234567890
                email: user@example.com
              custom_field:
                - type: text
                  key: <string>
                  label: <string>
                  optional: true
                  text:
                    max_length: 123
                    min_length: 123
              success_url: <string>
              metadata:
                userId: user_123
                visitCount: 42
                lastVisit: '2023-04-01'
        description: Create checkout request payload
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
              status:
                allOf:
                  - type: string
                    description: Status of the checkout.
              request_id:
                allOf:
                  - type: string
                    description: Identify and track each checkout request.
              product:
                allOf:
                  - description: The product associated with the checkout session.
                    oneOf:
                      - type: string
                      - $ref: '#/components/schemas/ProductEntity'
              units:
                allOf:
                  - type: number
                    description: The number of units for the of the product.
                    default: 1
              order:
                allOf:
                  - description: The order associated with the checkout session.
                    allOf:
                      - $ref: '#/components/schemas/OrderEntity'
              subscription:
                allOf:
                  - description: The subscription associated with the checkout session.
                    oneOf:
                      - type: string
                      - $ref: '#/components/schemas/SubscriptionEntity'
              customer:
                allOf:
                  - description: The customer associated with the checkout session.
                    oneOf:
                      - type: string
                      - $ref: '#/components/schemas/CustomerEntity'
              custom_fields:
                allOf:
                  - description: >-
                      Additional information collected from your customer during
                      the checkout process.
                    type: array
                    items:
                      $ref: '#/components/schemas/CustomField'
              checkout_url:
                allOf:
                  - type: string
                    description: >-
                      The URL to which the customer will be redirected to
                      complete the payment.
              success_url:
                allOf:
                  - type: string
                    description: >-
                      The URL to which the user will be redirected after the
                      checkout process is completed.
                    example: https://example.com/return
                    nullable: true
              feature:
                allOf:
                  - description: Features issued for the order.
                    type: array
                    items:
                      $ref: '#/components/schemas/ProductFeatureEntity'
              metadata:
                allOf:
                  - type: object
                    description: Metadata for the checkout in the form of key-value pairs
                    example:
                      userId: user_123
                      visitCount: 42
                      lastVisit: '2023-04-01'
                    additionalProperties: true
            refIdentifier: '#/components/schemas/CheckoutEntity'
            requiredProperties:
              - id
              - mode
              - object
              - status
              - product
        examples:
          example:
            value:
              id: <string>
              mode: test
              object: <string>
              status: <string>
              request_id: <string>
              product: <string>
              units: 1
              order:
                id: <string>
                mode: test
                object: <string>
                customer: <string>
                product: <string>
                transaction: tx_1234567890
                discount: dis_1234567890
                amount: 2000
                sub_total: 1800
                tax_amount: 200
                discount_amount: 100
                amount_due: 1900
                amount_paid: 1900
                currency: EUR
                fx_amount: 15
                fx_currency: EUR
                fx_rate: 1.2
                status: pending
                type: recurring
                affiliate: <string>
                created_at: '2023-09-13T00:00:00Z'
                updated_at: '2023-09-13T00:00:00Z'
              subscription: <string>
              customer: <string>
              custom_fields:
                - type: <string>
                  key: <string>
                  label: <string>
                  optional: true
                  text:
                    max_length: 123
                    min_length: 123
              checkout_url: <string>
              success_url: https://example.com/return
              feature:
                - license:
                    id: <string>
                    mode: test
                    object: <string>
                    status: active
                    key: ABC123-XYZ456-XYZ456-XYZ456
                    activation: 5
                    activation_limit: 1
                    expires_at: '2023-09-13T00:00:00Z'
                    created_at: '2023-09-13T00:00:00Z'
                    instance:
                      id: <string>
                      mode: test
                      object: license-instance
                      name: My Customer License Instance
                      status: active
                      created_at: '2023-09-13T00:00:00Z'
              metadata:
                userId: user_123
                visitCount: 42
                lastVisit: '2023-04-01'
        description: Successfully created a checkout session
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
    Text:
      type: object
      properties:
        max_length:
          type: number
          description: Maximum character length constraint for the input.
        min_length:
          type: number
          description: Minimum character length requirement for the input.
    CustomFieldRequestEntity:
      type: object
      properties:
        type:
          type: string
          description: The type of the field.
          enum:
            - text
          example: text
        key:
          type: string
          description: >-
            Unique key for custom field. Must be unique to this field,
            alphanumeric, and up to 200 characters.
          maxLength: 200
        label:
          type: string
          description: >-
            The label for the field, displayed to the customer, up to 50
            characters
          maxLength: 200
        optional:
          type: boolean
          description: >-
            Whether the customer is required to complete the field. Defaults to
            `false`
        text:
          description: Configuration for type of text field.
          allOf:
            - $ref: '#/components/schemas/Text'
      required:
        - type
        - key
        - label
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
    SubscriptionEntity:
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
          example: subscription
        product:
          description: The product associated with the subscription.
          oneOf:
            - $ref: '#/components/schemas/ProductEntity'
            - type: string
        customer:
          description: The customer who owns the subscription.
          oneOf:
            - $ref: '#/components/schemas/CustomerEntity'
            - type: string
        items:
          description: Subscription items.
          type: array
          items:
            $ref: '#/components/schemas/SubscriptionItemEntity'
        collection_method:
          type: string
          description: The method used for collecting payments for the subscription.
          example: charge_automatically
        status:
          type: string
          description: The current status of the subscription.
          enum:
            - active
            - canceled
            - unpaid
            - paused
            - trialing
          example: active
        last_transaction_id:
          type: string
          description: The ID of the last paid transaction.
          example: tran_3e6Z6TzvHKdsjEgXnGDEp0
        last_transaction:
          description: The last paid transaction.
          allOf:
            - $ref: '#/components/schemas/TransactionEntity'
        last_transaction_date:
          format: date-time
          type: string
          description: The date of the last paid transaction.
          example: '2024-09-12T12:34:56Z'
        next_transaction_date:
          format: date-time
          type: string
          description: The date when the next subscription transaction will be charged.
          example: '2024-09-12T12:34:56Z'
        current_period_start_date:
          format: date-time
          type: string
          description: The start date of the current subscription period.
          example: '2024-09-12T12:34:56Z'
        current_period_end_date:
          format: date-time
          type: string
          description: The end date of the current subscription period.
          example: '2024-09-12T12:34:56Z'
        canceled_at:
          type: string
          description: The date and time when the subscription was canceled, if applicable.
          example: '2024-09-12T12:34:56Z'
          format: date-time
          nullable: true
        created_at:
          format: date-time
          type: string
          description: The date and time when the subscription was created.
          example: '2024-01-01T00:00:00Z'
        updated_at:
          type: string
          description: The date and time when the subscription was last updated.
          example: '2024-09-12T12:34:56Z'
          format: date-time
      required:
        - id
        - mode
        - object
        - product
        - customer
        - collection_method
        - status
        - created_at
        - updated_at
    OrderEntity:
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
        customer:
          type: string
          description: The customer who placed the order.
        product:
          type: string
          description: The product associated with the order.
        transaction:
          type: string
          description: The transaction ID of the order
          example: tx_1234567890
        discount:
          type: string
          description: The discount ID of the order
          example: dis_1234567890
        amount:
          type: number
          description: The total amount of the order in cents. 1000 = $10.00
          example: 2000
        sub_total:
          type: number
          description: The subtotal of the order in cents. 1000 = $10.00
          example: 1800
        tax_amount:
          type: number
          description: The tax amount of the order in cents. 1000 = $10.00
          example: 200
        discount_amount:
          type: number
          description: The discount amount of the order in cents. 1000 = $10.00
          example: 100
        amount_due:
          type: number
          description: The amount due for the order in cents. 1000 = $10.00
          example: 1900
        amount_paid:
          type: number
          description: The amount paid for the order in cents. 1000 = $10.00
          example: 1900
        currency:
          type: string
          description: >-
            Three-letter ISO currency code, in uppercase. Must be a supported
            currency.
          example: EUR
        fx_amount:
          type: number
          description: The amount in the foreign currency, if applicable.
          example: 15
        fx_currency:
          type: string
          description: Three-letter ISO code of the foreign currency, if applicable.
          example: EUR
        fx_rate:
          type: number
          description: >-
            The exchange rate used for converting between currencies, if
            applicable.
          example: 1.2
        status:
          type: string
          description: Current status of the order.
          enum:
            - pending
            - paid
          example: pending
        type:
          type: string
          description: >-
            The type of order. This can specify whether it's a regular purchase,
            subscription, etc.
          example: recurring
          enum:
            - recurring
            - onetime
        affiliate:
          type: string
          description: The affiliate associated with the order, if applicable.
        created_at:
          format: date-time
          type: string
          description: Creation date of the order
          example: '2023-09-13T00:00:00Z'
        updated_at:
          format: date-time
          type: string
          description: Last updated date of the order
          example: '2023-09-13T00:00:00Z'
      required:
        - id
        - mode
        - object
        - product
        - amount
        - currency
        - status
        - type
        - created_at
        - updated_at
    CustomField:
      type: object
      properties:
        type:
          type: string
          description: The type of the field.
        key:
          type: string
          description: >-
            Unique key for custom field. Must be unique to this field,
            alphanumeric, and up to 200 characters.
          maxLength: 200
        label:
          type: string
          description: >-
            The label for the field, displayed to the customer, up to 50
            characters
          maxLength: 200
        optional:
          type: boolean
          description: >-
            Whether the customer is required to complete the field. Defaults to
            `false`.
        text:
          description: >-
            Whether the customer is required to complete the field. Defaults to
            `false`.
          allOf:
            - $ref: '#/components/schemas/Text'
      required:
        - type
        - key
        - label
    LicenseInstanceEntity:
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
            A string representing the object’s type. Objects of the same type
            share the same value.
          example: license-instance
        name:
          type: string
          description: The name of the license instance.
          example: My Customer License Instance
        status:
          type: string
          description: The status of the license instance.
          enum:
            - active
            - deactivated
          example: active
        created_at:
          format: date-time
          type: string
          description: The creation date of the license instance.
          example: '2023-09-13T00:00:00Z'
      required:
        - id
        - mode
        - object
        - name
        - status
        - created_at
    LicenseEntity:
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
            A string representing the object’s type. Objects of the same type
            share the same value.
        status:
          type: string
          description: The current status of the license key.
          enum:
            - inactive
            - active
            - expired
            - disabled
          example: active
        key:
          type: string
          description: The license key.
          example: ABC123-XYZ456-XYZ456-XYZ456
        activation:
          type: number
          description: The number of instances that this license key was activated.
          example: 5
        activation_limit:
          type: object
          description: The activation limit. Null if activations are unlimited.
          example: 1
          nullable: true
        expires_at:
          type: object
          description: >-
            The date the license key expires. Null if it does not have an
            expiration date.
          example: '2023-09-13T00:00:00Z'
          nullable: true
        created_at:
          format: date-time
          type: string
          description: The creation date of the license key.
          example: '2023-09-13T00:00:00Z'
        instance:
          description: Associated license instances.
          nullable: true
          allOf:
            - $ref: '#/components/schemas/LicenseInstanceEntity'
      required:
        - id
        - mode
        - object
        - status
        - key
        - activation
        - created_at
    ProductFeatureEntity:
      type: object
      properties:
        license:
          description: License key issued for the order.
          allOf:
            - $ref: '#/components/schemas/LicenseEntity'
      required:
        - license
    CustomerRequestEntity:
      type: object
      properties:
        id:
          type: string
          description: >-
            Unique identifier of the customer. You may specify only one of these
            parameters: id or email.
          example: cust_1234567890
        email:
          type: string
          description: >-
            Customer email address. You may only specify one of these
            parameters: id, email.
          example: user@example.com

````