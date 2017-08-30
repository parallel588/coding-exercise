## Webhook API

__Model Attributes__

| Name             | Type       | Description                                                               |
| ---------------- | ---------  | ------------------------------------------------------------------------- |
| `body`           | `string`   | The message's body.                                                       |
| `inserted_at`    | `datetime` | What time was the message received?                                       |
| `token`          | `string`   | Token for async response.                                                 |
| `response_url`   | `string`   | Endpoint to post response to, if doing an async response.                 |
| `metadata`       | `map`      | Any additional data that may have been provided by the sender.            |

Webhooks should accept POST requests with a `application/json` content-type.

When Lab receives a message, it will attempt to POST to the specified endpoint.

__NOTE__ Lab will NOT retry failed requests, once failed, that message will not be delivered again.

### Example

The following example is a simple message from lab.
When responding to the request, messages should be delivered asynchronously.

That is, the http request should be completed immediately, while the response should be delivered to the `response_url`, via a POST request.

#### Request

```
Accept: application/json
Content-Type: application/json
User-Agent: Lab-<version>
```

```json
{
  "token": "gqR0aW1lzwAAAV4xcOHXpXRva2Vu2SQ1YzdlYjI0Yi1jODQ0LTRmMDItYjFhYS1mM2FjMzAxODgyZjA=",
  "response_url": "https://example.com/responses/5c7eb24b-c844-4f02-b1aa-f3ac301882f0",
  "metadata": {"ref": 1},
  "inserted_at": "2017-08-30T04:40:35.022442Z",
  "body": "Hello"
}
```

#### Response

When doing an asynchronous response, respond to the request with a 202 Accepted status and return an empty payload.

__Status__ 202

```
Content-Type: application/json
```

```json
{}
```

##### Request (for response)

Then take the `response_url` and `token` from the request.

Create the response message with the token and then POST the payload to the `response_url`


```
POST https://example.com/responses/5c7eb24b-c844-4f02-b1aa-f3ac301882f0
```

```
Accept: application/json
Content-Type: application/json
```

```json
{
  "token": "gqR0aW1lzwAAAV4xcOHXpXRva2Vu2SQ1YzdlYjI0Yi1jODQ0LTRmMDItYjFhYS1mM2FjMzAxODgyZjA=",
  "body": "Hello, Back"
}
```

A token may be reused as many times within the lifespan of the session.

##### Response (successful)

Lab will respond with a 204 No Content, if the request was successful.

__Status__ 204

##### Response (session does not exist)

Lab will respond with a 404, if the session specified could not be found.

__Status__ 404

##### Response (payload contained an error)

Lab will respond with a 422, if the payload was malformed or the token was invalid.

__Status__ 422
