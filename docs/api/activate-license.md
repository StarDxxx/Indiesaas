# Activate License Key

## OpenAPI

````yaml post /v1/licenses/activate
paths:
  path: /v1/licenses/activate
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
              key:
                allOf:
                  - type: string
                    description: The license key to activate.
              instance_name:
                allOf:
                  - type: string
                    description: A label for the new instance to identify it in Creem.
            required: true
            refIdentifier: '#/components/schemas/ActivateLicenseRequestEntity'
            requiredProperties:
              - key
              - instance_name
        examples:
          example:
            value:
              key: <string>
              instance_name: <string>
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
              status:
                allOf:
                  - type: string
                    description: The current status of the license key.
                    enum:
                      - inactive
                      - active
                      - expired
                      - disabled
                    example: active
              key:
                allOf:
                  - type: string
                    description: The license key.
                    example: ABC123-XYZ456-XYZ456-XYZ456
              activation:
                allOf:
                  - type: number
                    description: >-
                      The number of instances that this license key was
                      activated.
                    example: 5
              activation_limit:
                allOf:
                  - type: object
                    description: The activation limit. Null if activations are unlimited.
                    example: 1
                    nullable: true
              expires_at:
                allOf:
                  - type: object
                    description: >-
                      The date the license key expires. Null if it does not have
                      an expiration date.
                    example: '2023-09-13T00:00:00Z'
                    nullable: true
              created_at:
                allOf:
                  - format: date-time
                    type: string
                    description: The creation date of the license key.
                    example: '2023-09-13T00:00:00Z'
              instance:
                allOf:
                  - description: Associated license instances.
                    nullable: true
                    allOf:
                      - $ref: '#/components/schemas/LicenseInstanceEntity'
            refIdentifier: '#/components/schemas/LicenseEntity'
            requiredProperties:
              - id
              - mode
              - object
              - status
              - key
              - activation
              - created_at
        examples:
          example:
            value:
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
        description: Successfully activated a license key
  deprecated: false
  type: path
components:
  schemas:
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

````