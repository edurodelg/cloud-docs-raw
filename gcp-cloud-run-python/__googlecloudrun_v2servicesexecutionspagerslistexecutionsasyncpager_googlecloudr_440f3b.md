---
merged_at: 2026-01-25T15:25:49.602041
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2servicesexecutionspagerslistexecutionsasyncpager_googlecloudru_cdbd62.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicesexecutionspagerslistexecutionsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.pagers.ListExecutionsAsyncPager -->

# Class ListExecutionsAsyncPager (0.14.0)

```
ListExecutionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.execution.ListExecutionsResponse],
],
request: google.cloud.run_v2.types.execution.ListExecutionsRequest,
response: google.cloud.run_v2.types.execution.ListExecutionsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_executions`

requests.

This class thinly wraps an initial
[ListExecutionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`executions`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListExecutions`

requests and continue to iterate
through the `executions`

field on the
corresponding responses.

All the usual [ListExecutionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListExecutionsAsyncPager

```
ListExecutionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.execution.ListExecutionsResponse],
],
request: google.cloud.run_v2.types.execution.ListExecutionsRequest,
response: google.cloud.run_v2.types.execution.ListExecutionsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicesworker_poolspagerslistworkerpoolsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.pagers.ListWorkerPoolsAsyncPager -->

# Class ListWorkerPoolsAsyncPager (0.14.0)

```
ListWorkerPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse],
],
request: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsRequest,
response: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_worker_pools`

requests.

This class thinly wraps an initial
[ListWorkerPoolsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsResponse) object, and
provides an `__aiter__`

method to iterate through its
`worker_pools`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListWorkerPools`

requests and continue to iterate
through the `worker_pools`

field on the
corresponding responses.

All the usual [ListWorkerPoolsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListWorkerPoolsAsyncPager

```
ListWorkerPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse],
],
request: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsRequest,
response: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest -->

# Python Client for Cloud Run

[Cloud Run](https://cloud.google.com/run/docs): is a managed compute platform that enables you to run containers that are invocable via requests or events.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a virtual environment using [venv](https://docs.python.org/3/library/venv.html). [venv](https://docs.python.org/3/library/venv.html) is a tool that
creates isolated Python environments. These isolated environments can have separate
versions of Python packages, which allows you to isolate one project’s dependencies
from the dependencies of other projects.

With [venv](https://docs.python.org/3/library/venv.html), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

### Code samples and snippets

Code samples and snippets live in the [samples/](https://github.com/googleapis/google-cloud-python/tree/main/packages/google-cloud-run/samples) folder.

#### Supported Python Versions

Our client libraries are compatible with all current [active](https://devguide.python.org/devcycle/#in-development-main-branch) and [maintenance](https://devguide.python.org/devcycle/#maintenance-branches) versions of
Python.

Python >= 3.7, including 3.14

#### Unsupported Python Versions

Python <= 3.6

If you are using an [end-of-life](https://devguide.python.org/devcycle/#end-of-life-branches)
version of Python, we recommend that you update as soon as possible to an actively supported version.

#### Mac/Linux

```
python3 -m venv <your-env>
source <your-env>/bin/activate
pip install google-cloud-run
```


#### Windows

```
py -m venv <your-env>
.\<your-env>\Scripts\activate
pip install google-cloud-run
```


### Next Steps

Read the

[Client Library Documentation](https://cloud.google.com/python/docs/reference/run/latest/summary_overview)for Cloud Run to see other available methods on the client.Read the

[Cloud Run Product documentation](https://cloud.google.com/run/docs)to learn more about the product and see How-to Guides.View this

[README](https://github.com/googleapis/google-cloud-python/blob/main/README.rst)to see the full list of Cloud APIs that we cover.

## Logging

This library uses the standard Python `logging`

functionality to log some RPC events that could be of interest for debugging and monitoring purposes.
Note the following:

Logs may contain sensitive information. Take care to

**restrict access to the logs**if they are saved, whether it be on local storage or on Google Cloud Logging.Google may refine the occurrence, level, and content of various log messages in this library without flagging such changes as breaking.

**Do not depend on immutability of the logging events**.By default, the logging events from this library are not handled. You must

**explicitly configure log handling**using one of the mechanisms below.

### Simple, environment-based configuration

To enable logging for this library without any changes in your code, set the `GOOGLE_SDK_PYTHON_LOGGING_SCOPE`

environment variable to a valid Google
logging scope. This configures handling of logging events (at level `logging.DEBUG`

or higher) from this library in a default manner, emitting the logged
messages in a structured format. It does not currently allow customizing the logging levels captured nor the handlers, formatters, etc. used for any logging
event.

A logging scope is a period-separated namespace that begins with `google`

, identifying the Python module or package to log.

Valid logging scopes:

`google`

,`google.cloud.asset.v1`

,`google.api`

,`google.auth`

, etc.Invalid logging scopes:

`foo`

,`123`

, etc.

**NOTE**: If the logging scope is invalid, the library does not set up any logging handlers.

#### Environment-Based Examples

- Enabling the default handler for all Google-based loggers

```
export GOOGLE_SDK_PYTHON_LOGGING_SCOPE=google
```


- Enabling the default handler for a specific Google module (for a client library called
`library_v1`

):

```
export GOOGLE_SDK_PYTHON_LOGGING_SCOPE=google.cloud.library_v1
```


### Advanced, code-based configuration

You can also configure a valid logging scope using Python’s standard logging mechanism.

#### Code-Based Examples

- Configuring a handler for all Google-based loggers

```
import logging
from google.cloud import library_v1
base_logger = logging.getLogger("google")
base_logger.addHandler(logging.StreamHandler())
base_logger.setLevel(logging.DEBUG)
```


- Configuring a handler for a specific Google module (for a client library called
`library_v1`

):

```
import logging
from google.cloud import library_v1
base_logger = logging.getLogger("google.cloud.library_v1")
base_logger.addHandler(logging.StreamHandler())
base_logger.setLevel(logging.DEBUG)
```


### Logging details

Regardless of which of the mechanisms above you use to configure logging for this library, by default logging events are not propagated up to the root logger from the google-level logger. If you need the events to be propagated to the root logger, you must explicitly set

`logging.getLogger("google").propagate = True`

in your code.You can mix the different logging configurations above for different Google modules. For example, you may want use a code-based logging configuration for one library, but decide you need to also set up environment-based logging configuration for another library.

- If you attempt to use both code-based and environment-based configuration for the same module, the environment-based configuration will be ineffectual if the code -based configuration gets applied first.

The Google-specific logging configurations (default handlers for environment-based configuration; not propagating logging events to the root logger) get executed the first time

*any*client library is instantiated in your application, and only if the affected loggers have not been previously configured. (This is the reason for 2.i. above.)
