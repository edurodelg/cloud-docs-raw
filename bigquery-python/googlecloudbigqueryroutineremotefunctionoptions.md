---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions
fetched_at: 2026-01-25T03:17:06.160559
---

# Class RemoteFunctionOptions (3.40.0)


      
      Save and categorize content based on your preferences.

```
RemoteFunctionOptions(
endpoint=None,
connection=None,
max_batching_rows=None,
user_defined_context=None,
_properties=None,
)
```


Configuration options for controlling remote BigQuery functions.

## Properties

### connection

string: Fully qualified name of the user-provided connection object which holds the authentication information to send requests to the remote service.

Format is "projects/{projectId}/locations/{locationId}/connections/{connectionId}"

### endpoint

string: Endpoint of the user-provided remote service

Example: "[https://us-east1-my_gcf_project.cloudfunctions.net/remote_add](https://us-east1-my_gcf_project.cloudfunctions.net/remote_add)"

### max_batching_rows

int64: Max number of rows in each batch sent to the remote service.

If absent or if 0, BigQuery dynamically decides the number of rows in a batch.

### user_defined_context

Dict[str, str]: User-defined context as a set of key/value pairs, which will be sent as function invocation context together with batched arguments in the requests to the remote service. The total number of bytes of keys and values must be less than 8KB.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RemoteFunctionOptions
```


Factory: construct remote function options given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Resource, as returned from the API. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.RemoteFunctionOptions` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this RemoteFunctionOptions.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Remote function options represented as an API resource. |