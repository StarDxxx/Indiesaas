# List Transactions

## OpenAPI

````yaml get /v1/transactions/search
paths:
  path: /v1/transactions/search
  method: get
  servers:
    - url: https://api.creem.io
    - url: https://test-api.creem.io
  request:
    security: []
    parameters:
      path: {}
      query:
        customer_id:
          schema:
            - type: string
              required: false
              description: The customer id
        order_id:
          schema:
            - type: string
              required: false
              description: The order id
        product_id:
          schema:
            - type: string
              required: false
              description: The product id
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
                  - description: List of transactions items
                    items:
                      $ref: '#/components/schemas/TransactionEntity'
                    type: array
              pagination:
                allOf:
                  - description: Pagination details for the list
                    allOf:
                      - $ref: '#/components/schemas/PaginationEntity'
            refIdentifier: '#/components/schemas/TransactionListEntity'
            requiredProperties:
              - items
              - pagination
        examples:
          example:
            value:
              items:
                - id: <string>
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
              pagination:
                total_records: 0
                total_pages: 0
                current_page: 1
                next_page: 2
                prev_page: null
        description: Successfully retrieved transactions
  deprecated: false
  type: path
components:
  schemas:
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

````