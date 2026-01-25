---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference
fetched_at: 2026-01-25T03:16:12.685086
---

# Class ModelReference (3.40.0)


      
      Save and categorize content based on your preferences.

`ModelReference()`


ModelReferences are pointers to models.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference)

## Properties

### dataset_id

str: ID of dataset containing the model.

### model_id

str: The model ID.

### path

URL path for the model's APIs.

### project

str: Project bound to the model

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.model.ModelReference
```


Factory: construct a model reference given its API representation.

### from_string

```
from_string(
model_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.model.ModelReference
```


Construct a model reference from model ID string.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `model_id` is not a fully-qualified table ID in standard SQL format. |

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this model reference.