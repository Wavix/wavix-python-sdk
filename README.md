# Wavix Python SDK

[![fern shield](https://img.shields.io/badge/%F0%9F%8C%BF-Built%20with%20Fern-brightgreen)](https://buildwithfern.com?utm_source=github&utm_medium=github&utm_campaign=readme&utm_source=https%3A%2F%2Fgithub.com%2Fwavix%2Fwavix-python)
[![pypi](https://img.shields.io/pypi/v/wavix)](https://pypi.python.org/pypi/wavix)

The official Wavix Python SDK provides programmatic access to the
[Wavix](https://wavix.com) APIs. Use it to add messaging, voice, and account
management capabilities to your application.

Use the SDK to:

- Send and receive SMS and MMS messages.
- Place and programmatically control calls.
- Search for, buy, and manage phone numbers.
- Validate phone numbers.
- Manage SIP trunks.
- Retrieve call detail records (CDRs).


## Table of contents

- [Installation](#installation)
- [Authentication](#authentication)
- [Quickstart](#quickstart)
- [Async client](#async-client)
- [Error handling](#error-handling)
- [Pagination](#pagination)
- [Rate limits and retries](#rate-limits-and-retries)
  - [Retries](#retries)
  - [Idempotency](#idempotency)
- [Advanced](#advanced)
  - [Access raw response data](#access-raw-response-data)
  - [Timeouts](#timeouts)
  - [Custom HTTP client](#custom-http-client)
- [SDK and API compatibility](#sdk-and-api-compatibility)
- [Release notes](#release-notes)
- [Major-version upgrades](#major-version-upgrades)
- [Documentation](#documentation)
- [Resources and support](#resources-and-support)
- [Contributing](#contributing)

## Installation

```sh
pip install wavix
```

**Requirements:** Python 3.10 or later.

## Authentication

Create an API key in the [Wavix portal](https://app.wavix.com). Store the key
in an environment variable and pass it to the client.

```shell
export WAVIX_API_KEY="your-api-key"
```

```python
import os

from wavix import Wavix

client = Wavix(token=os.environ["WAVIX_API_KEY"])
```

> [!CAUTION]
> Don't commit API keys or tokens to source control. In production, store
> credentials in environment variables or a secrets manager.


## Quickstart

Create a client and send an SMS message:

```python
from wavix import Wavix, MessageBody

client = Wavix(
    token="<token>",
)

client.sms_and_mms.messages.send(
    from_="Wavix",
    to="+447537151866",
    message_body=MessageBody(
        text="Hi there, this is a message from Wavix",
        media=None,
    ),
    callback_url="https://you-site.com/webhook",
    validity=3600,
    tag="Fall sale",
)
```

## Async client

Use `AsyncWavix` to make nonblocking API calls. If you provide an `httpx`
client through the `httpx_client` parameter, use `httpx.AsyncClient` with
`AsyncWavix`. Don't use `httpx.Client` with the async client.

```python
import asyncio

from wavix import AsyncWavix, MessageBody

client = AsyncWavix(
    token="<token>",
)


async def main() -> None:
    await client.sms_and_mms.messages.send(
        from_="Wavix",
        to="+447537151866",
        message_body=MessageBody(
            text="Hi there, this is a message from Wavix",
            media=None,
        ),
        callback_url="https://you-site.com/webhook",
        validity=3600,
        tag="Fall sale",
    )


asyncio.run(main())
```

## Error handling

When the API returns a `4xx` or `5xx` status code, the SDK raises a subclass
of `ApiError`. Use the error properties to inspect the status code and
response body:

```python
from wavix.core.api_error import ApiError

try:
    client.sms_and_mms.messages.send(...)
except ApiError as e:
    print(e.status_code)
    print(e.body)
```

Handle errors that aren't instances of `ApiError` separately, or raise them
again so that your application doesn't ignore unexpected failures.

## Pagination

List operations use automatic page-number pagination. The SDK requests
additional pages as you iterate through the results.

The Wavix APIs support these pagination parameters:

- `page`: Specifies the page to retrieve.
- `per_page`: Specifies the number of items per page. The default is `25`.
  The minimum is `1`, and the maximum is `100`.

## Rate limits and retries

Rate limits vary by endpoint. When a request exceeds an endpoint's rate
limit, the Wavix API returns an HTTP `429 Too Many Requests` response.

The SDK can retry `429` responses as described in [Retries](#retries).
Configure retries according to your application's traffic patterns and
latency requirements.

### Retries

The SDK automatically retries eligible requests by using exponential backoff.
By default, the SDK makes up to two retry attempts.

The SDK retries requests that return one of these status codes:

- [`408 Request Timeout`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/408).
- [`409 Conflict`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/409).
- [`429 Too Many Requests`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/429).
- Any [`5xx` server error](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#server_error_responses).

These status codes aren't configurable.

Use `max_retries` to override the retry limit for an individual request:

```python
client.sms_and_mms.messages.send(..., request_options={
    "max_retries": 1
})
```

> [!IMPORTANT]
> A retry can repeat an operation if the server processes the original
> request but the client doesn't receive the response. Before you retry an
> operation that sends a message, places a call, or changes a resource,
> confirm that the operation can be repeated safely.

### Idempotency

The Wavix APIs don't support idempotency keys. A repeated request can repeat
the operation, including sending a message, placing a call, or changing a
resource.

Before you retry a request that changes data or starts an operation, check
whether the original request succeeded. When duplicate operations could
affect customers or incur charges, track request state in your application
and prevent the same operation from being submitted more than once.

## Advanced

### Access raw response data

Use `.with_raw_response` to access the status code, headers, and underlying
response object. The property returns a raw client whose responses provide
`.headers`, `.status_code`, and `.data` attributes:

```python
from wavix import Wavix

client = Wavix(...)
response = client.sms_and_mms.messages.with_raw_response.send(...)
print(response.headers)  # access the response headers
print(response.status_code)  # access the response status code
print(response.data)  # access the underlying object
```

### Timeouts

The default request timeout is 60 seconds. Set a timeout on the client, or
override it for an individual request:

```python
from wavix import Wavix

client = Wavix(..., timeout=20.0)

# Override timeout for a specific method
client.sms_and_mms.messages.send(..., request_options={
    "timeout_in_seconds": 1
})
```

### Custom HTTP client

Provide a custom `httpx` client to configure network behavior such as proxies
and transports:

```python
import httpx
from wavix import Wavix

client = Wavix(
    ...,
    httpx_client=httpx.Client(
        proxy="http://my.test.proxy.example.com",
        transport=httpx.HTTPTransport(local_address="0.0.0.0"),
    ),
)
```

## SDK and API compatibility

Each SDK release supports the current version of the Wavix APIs available
when that SDK version is released. Update the SDK regularly to access the
latest API capabilities and fixes.

Before you update the SDK, review the
[GitHub releases](https://github.com/wavix/wavix-python/releases) for changes
that might affect your application.

## Release notes

See [GitHub releases](https://github.com/wavix/wavix-python/releases) for new
features, fixes, and breaking changes in each SDK release.

## Major-version upgrades

The SDK doesn't provide separate migration guides. Breaking changes ship only
in major versions, so before you upgrade, review the
[GitHub releases](https://github.com/wavix/wavix-python/releases) for breaking
changes, then update and test in a development environment before you deploy.

## Documentation

- For API guides and API reference documentation, see the
  [Wavix documentation](https://docs.wavix.com).
- For SDK methods and types, see the
  [Python SDK reference](https://github.com/wavix/wavix-python/blob/HEAD/reference.md).

## Resources and support

- **Versioning:** The SDK follows [Semantic Versioning](https://semver.org).
  Breaking changes are released in major versions.
- **Security:** Report vulnerabilities privately by following the instructions
  in [SECURITY.md](./SECURITY.md). Don't report vulnerabilities in public
  issues.
- **Support:** For product and API support, contact
  [support@wavix.com](mailto:support@wavix.com).
- **Issues:** To report an SDK bug or request a feature, open a
  [GitHub issue](https://github.com/wavix/wavix-python/issues).
- **License:** The SDK is available under the [MIT License](./LICENSE).

## Contributing

The SDK source code is generated. Changes made directly to generated files are
overwritten in the next release and can't be merged as submitted. Before you
prepare a code change, open an issue to discuss the proposed update.

You can submit README improvements directly in a pull request.
