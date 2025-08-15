# Create Product

## OpenAPI

````yaml post /v1/products
paths:
  path: /v1/products
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
              name:
                allOf:
                  - type: string
                    description: Name of the product
              description:
                allOf:
                  - type: string
                    description: Description of the product
              image_url:
                allOf:
                  - type: string
                    description: URL of the product image
                    example: https://picsum.photos/200/300
              price:
                allOf:
                  - type: integer
                    description: 'The price of the product in cents '
                    example: 400
                    minimum: 100
              currency:
                allOf:
                  - type: string
                    description: >-
                      Three-letter ISO currency code, in uppercase. Must be a
                      supported currency.
                    example: EUR
              billing_type:
                allOf:
                  - type: string
                    description: >-
                      Indicates the billing method for the customer. It can
                      either be a `recurring` billing cycle or a `onetime`
                      payment.
                    example: recurring
              billing_period:
                allOf:
                  - type: string
                    description: Billing period, required if billing_type is recurring
                    example: every-month
              tax_mode:
                allOf:
                  - type: string
                    description: >-
                      Specifies the tax calculation mode for the transaction. If
                      set to "inclusive," the tax is included in the price. If
                      set to "exclusive," the tax is added on top of the price.
                    example: inclusive
              tax_category:
                allOf:
                  - type: string
                    description: >-
                      Categorizes the type of product or service for tax
                      purposes. This helps determine the applicable tax rules
                      based on the nature of the item or service.
                    example: saas
              default_success_url:
                allOf:
                  - type: string
                    description: >-
                      The URL to which the user will be redirected after
                      successfull payment.
                    example: https://example.com/?status=successful
              custom_field:
                allOf:
                  - description: >-
                      Collect additional information from your customer using
                      custom fields during checkout. Up to 3 fields are
                      supported.
                    type: array
                    items:
                      $ref: '#/components/schemas/CustomFieldRequestEntity'
            required: true
            refIdentifier: '#/components/schemas/CreateProductRequestEntity'
            requiredProperties:
              - name
              - price
              - currency
              - billing_type
        examples:
          example:
            value:
              name: <string>
              description: <string>
              image_url: https://picsum.photos/200/300
              price: 400
              currency: EUR
              billing_type: recurring
              billing_period: every-month
              tax_mode: inclusive
              tax_category: saas
              default_success_url: https://example.com/?status=successful
              custom_field:
                - type: text
                  key: <string>
                  label: <string>
                  optional: true
                  text:
                    max_length: 123
                    min_length: 123
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
              name:
                allOf:
                  - type: string
                    description: The name of the product
              description:
                allOf:
                  - type: string
                    description: A brief description of the product
                    example: This is a sample product description.
              image_url:
                allOf:
                  - type: string
                    description: URL of the product image. Only png as jpg are supported
                    example: https://example.com/image.jpg
              features:
                allOf:
                  - description: Features of the product.
                    type: array
                    items:
                      $ref: '#/components/schemas/FeatureEntity'
              price:
                allOf:
                  - type: number
                    description: The price of the product in cents. 1000 = $10.00
                    example: 400
              currency:
                allOf:
                  - type: string
                    description: >-
                      Three-letter ISO currency code, in uppercase. Must be a
                      supported currency.
                    example: EUR
              billing_type:
                allOf:
                  - type: string
                    description: >-
                      Indicates the billing method for the customer. It can
                      either be a `recurring` billing cycle or a `onetime`
                      payment.
                    example: recurring
              billing_period:
                allOf:
                  - type: string
                    description: Billing period
                    example: every-month
              status:
                allOf:
                  - type: string
                    description: Status of the product
              tax_mode:
                allOf:
                  - type: string
                    description: >-
                      Specifies the tax calculation mode for the transaction. If
                      set to "inclusive," the tax is included in the price. If
                      set to "exclusive," the tax is added on top of the price.
                    example: inclusive
              tax_category:
                allOf:
                  - type: string
                    description: >-
                      Categorizes the type of product or service for tax
                      purposes. This helps determine the applicable tax rules
                      based on the nature of the item or service.
                    example: saas
              product_url:
                allOf:
                  - type: string
                    description: >-
                      The product page you can redirect your customers to for
                      express checkout.
                    example: https://creem.io/product/prod_123123123123
              default_success_url:
                allOf:
                  - type: string
                    description: >-
                      The URL to which the user will be redirected after
                      successfull payment.
                    example: https://example.com/?status=successful
                    nullable: true
              created_at:
                allOf:
                  - format: date-time
                    type: string
                    description: Creation date of the product
                    example: '2023-01-01T00:00:00Z'
              updated_at:
                allOf:
                  - format: date-time
                    type: string
                    description: Last updated date of the product
                    example: '2023-01-01T00:00:00Z'
            refIdentifier: '#/components/schemas/ProductEntity'
            requiredProperties:
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
        examples:
          example:
            value:
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
        description: Successfully created a product
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

````