# Introduction

> Understand general concepts, response codes, and authentication strategies.

## Base URL

The Creem API is built on REST principles. We enforce HTTPS in every request to improve data security, integrity, and privacy. The API does not support HTTP.

All requests contain the following base URL:

```http
https://api.creem.io
```

## Authentication

To authenticate you need to add an `x-api-key` header with the contents of the header being your API Key.
All API endpoints are authenticated using Api Keys and picked up from the specification file.

```json
{
  "headers": {
    "x-api-key": "creem_123456789"
  }
}
```

## Response codes

Creem uses standard HTTP codes to indicate the success or failure of your requests.
In general, 2xx HTTP codes correspond to success, 4xx codes are for user-related failures, and 5xx codes are for infrastructure issues.

| Status | Description                             |
| ------ | --------------------------------------- |
| 200    | Successful request.                     |
| 400    | Check that the parameters were correct. |
| 401    | The API key used was missing.           |
| 403    | The API key used was invalid.           |
| 404    | The resource was not found.             |
| 429    | The rate limit was exceeded.            |
| 500    | Indicates an error with Creem servers.  |
