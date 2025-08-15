# List Products

## OpenAPI

````yaml get /v1/products/search
paths:
  path: /v1/products/search
  method: get
  servers:
    - url: https://api.creem.io
    - url: https://test-api.creem.io
  request:
    security: []
    parameters:
      path: {}
      query:
        page_number:
          schema:
            - type: number
              required: false
              description: The page number
        page_size:
          schema:
            - type: number
              required: false
              description: The the page size
      header:
        x-api-key:
          schema:
            - type: string
              required: true
      cookie: {}
    body: {}
  response:
    '200':
      application/json:
        schemaArray:
          - type: object
            properties:
              items:
                allOf:
                  - description: List of product items
                    items:
                      $ref: '#/components/schemas/ProductEntity'
                    type: array
              pagination:
                allOf:
                  - description: Pagination details for the list
                    allOf:
                      - $ref: '#/components/schemas/PaginationEntity'
            refIdentifier: '#/components/schemas/ProductListEntity'
            requiredProperties:
              - items
              - pagination
        examples:
          example:
            value:
              items:
                - id: <string>
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
              pagination:
                total_records: 0
                total_pages: 0
                current_page: 1
                next_page: 2
                prev_page: null
        description: Successfully retrieved products
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
    PaginationEntity:
      type: object
      properties:
        total_records:
          type: number
          description: Total number of records in the list
          example: 0
        total_pages:
          type: number
          description: Total number of pages available
          example: 0
        current_page:
          type: number
          description: The current page number
          example: 1
        next_page:
          type: number
          description: The next page number, or null if there is no next page
          example: 2
          nullable: true
        prev_page:
          type: number
          description: The previous page number, or null if there is no previous page
          example: null
          nullable: true
      required:
        - total_records
        - total_pages
        - current_page
        - next_page
        - prev_page

````