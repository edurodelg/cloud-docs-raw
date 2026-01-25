---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem
fetched_at: 2026-01-25T02:05:39.339534
---

# Class DatasetListItem (3.40.0)


      
      Save and categorize content based on your preferences.

`DatasetListItem(resource)`


A read-only dataset resource from a list operation.

For performance reasons, the BigQuery API only includes some of the dataset properties when listing datasets. Notably, xref_access_entries is missing.

For a full list of the properties that the BigQuery API returns, see the
```
REST documentation for datasets.list
<https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/list>
```

_.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, str]`
A dataset-like resource object from a dataset list response. A |

## Properties

### dataset_id

str: Dataset ID.

### friendly_name

Union[str, None]: Title of the dataset as set by the user
(defaults to :data:`None`

).

### full_dataset_id

Union[str, None]: ID for the dataset resource (:data:`None`

until
set from the server)

In the format `project_id:dataset_id`

.

### labels

Dict[str, str]: Labels for the dataset.

### project

str: Project bound to the dataset.

### reference

[google.cloud.bigquery.dataset.DatasetReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference): A reference to this
dataset.

## Methods

### model

`model(model_id)`


Constructs a ModelReference.

Parameter |
|
|---|---|
Name |
Description |
`model_id` |
`str`
the ID of the model. |

Returns |
|
|---|---|
Type |
Description |
|
A ModelReference for a model in this dataset. |

### routine

`routine(routine_id)`


Constructs a RoutineReference.

Parameter |
|
|---|---|
Name |
Description |
`routine_id` |
`str`
the ID of the routine. |

Returns |
|
|---|---|
Type |
Description |
|
A RoutineReference for a routine in this dataset. |

### table

`table(table_id: str) -> google.cloud.bigquery.table.TableReference`


Constructs a TableReference.

Parameter |
|
|---|---|
Name |
Description |
`table_id` |
`str`
The ID of the table. |

Returns |
|
|---|---|
Type |
Description |
|
A table reference for a table in this dataset. |