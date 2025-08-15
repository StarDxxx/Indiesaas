# Delete Discount Code

## OpenAPI

````yaml delete /v1/discounts/{id}/delete
paths:
  path: /v1/discounts/{id}/delete
  method: delete
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
    body: {}
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
                      A string representing the object’s type. Objects of the
                      same type share the same value.
                    example: discount
              status:
                allOf:
                  - type: string
                    description: The status of the discount (e.g., active, inactive).
                    enum:
                      - active
                      - draft
                      - expired
                      - scheduled
                    example: active
              name:
                allOf:
                  - type: string
                    description: The name of the discount.
                    example: Holiday Sale
              code:
                allOf:
                  - type: string
                    description: The discount code. A unique identifier for the discount.
                    example: HOLIDAY2024
              type:
                allOf:
                  - type: string
                    description: The type of the discount, either "percentage" or "fixed".
                    enum:
                      - percentage
                      - fixed
                    example: percentage
              amount:
                allOf:
                  - type: number
                    description: >-
                      The amount of the discount. Can be a percentage or a fixed
                      amount.
                    example: 20
              currency:
                allOf:
                  - type: string
                    description: >-
                      The currency of the discount. Only required if type is
                      "fixed".
                    example: USD
              percentage:
                allOf:
                  - type: number
                    description: >-
                      The percentage of the discount. Only applicable if type is
                      "percentage".
                    example: 15
              expiry_date:
                allOf:
                  - format: date-time
                    type: string
                    description: The expiry date of the discount.
                    example: '2024-12-31T23:59:59Z'
              max_redemptions:
                allOf:
                  - type: number
                    description: >-
                      The maximum number of redemptions allowed for the
                      discount.
                    example: 100
              duration:
                allOf:
                  - type: string
                    description: The duration type for the discount.
                    enum:
                      - forever
                      - once
                      - repeating
                    example: repeating
              duration_in_months:
                allOf:
                  - type: number
                    description: >-
                      The number of months the discount is valid for. Only
                      applicable if the duration is "repeating" and the product
                      is a subscription.
                    example: 6
              applies_to_products:
                allOf:
                  - description: The list of product IDs to which this discount applies.
                    example:
                      - prod_123
                      - prod_456
                    type: array
                    items:
                      type: string
            refIdentifier: '#/components/schemas/DiscountEntity'
            requiredProperties:
              - id
              - mode
              - object
              - status
              - name
              - code
              - type
        examples:
          example:
            value:
              id: <string>
              mode: test
              object: discount
              status: active
              name: Holiday Sale
              code: HOLIDAY2024
              type: percentage
              amount: 20
              currency: USD
              percentage: 15
              expiry_date: '2024-12-31T23:59:59Z'
              max_redemptions: 100
              duration: repeating
              duration_in_months: 6
              applies_to_products:
                - prod_123
                - prod_456
        description: Successfully deleted a discount
  deprecated: false
  type: path
components:
  schemas: {}

````