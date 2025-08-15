# Get Customer

## OpenAPI

````yaml get /v1/customers
paths:
  path: /v1/customers
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
              description: The unique identifier of the customer
        email:
          schema:
            - type: string
              required: false
              description: The unique email of the customer
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
                      String representing the object’s type. Objects of the same
                      type share the same value.
              email:
                allOf:
                  - type: string
                    description: Customer email address.
                    example: user@example.com
              name:
                allOf:
                  - type: string
                    description: Customer name.
                    example: John Doe
              country:
                allOf:
                  - type: string
                    description: The ISO alpha-2 country code for the customer.
                    example: US
                    pattern: ^[A-Z]{2}$
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
            refIdentifier: '#/components/schemas/CustomerEntity'
            requiredProperties:
              - id
              - mode
              - object
              - email
              - country
              - created_at
              - updated_at
        examples:
          example:
            value:
              id: <string>
              mode: test
              object: <string>
              email: user@example.com
              name: John Doe
              country: US
              created_at: '2023-01-01T00:00:00Z'
              updated_at: '2023-01-01T00:00:00Z'
        description: Successfully retrieved the customer
  deprecated: false
  type: path
components:
  schemas: {}

````