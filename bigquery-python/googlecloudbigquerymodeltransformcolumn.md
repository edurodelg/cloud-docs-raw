---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.TransformColumn
fetched_at: 2026-01-25T03:16:14.830243
---

# Class TransformColumn (3.40.0)


      
      Save and categorize content based on your preferences.

`TransformColumn(resource: typing.Dict[str, typing.Any])`


TransformColumn represents a transform column feature.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn)

## Properties

### name

Name of the column.

### transform_sql

The SQL expression used in the column transform.

### type_

Data type of the column after the transform.

Returns |
|
|---|---|
Type |
Description |
`Optional[` |
Data type of the column. |

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.model.TransformColumn
```


Constructs a transform column feature given its API representation