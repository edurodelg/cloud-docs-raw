---
merged_at: 2026-02-01T08:10:00.332387
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ColumnReference -->

# Class ColumnReference (3.40.0)

`ColumnReference(referencing_column: str, referenced_column: str)`


The pair of the foreign key column and primary key column.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Compression -->

# Class Compression (3.40.0)

`Compression(value)`


The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlStructType -->

# Class StandardSqlStructType (3.40.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-09 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue -->

# Class FeatureValue (3.40.0)

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Representative value of a single feature within the cluster.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`feature_column` |
`str`
The feature column name. |
`numerical_value` |
`google.protobuf.wrappers_pb2.DoubleValue`
The numerical feature value. This is the centroid value for this feature. This field is a member of `oneof` _ `value` .
|
`categorical_value` |
The categorical feature value. This field is a member of `oneof` _ `value` .
|

## Classes

### CategoricalValue

`CategoricalValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Representative value of a categorical feature.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix.Entry -->

# Class Entry (3.40.0)

`Entry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single entry in the confusion matrix.

## Attributes |
|
|---|---|
Name |
Description |
`predicted_label` |
`str`
The predicted label. For confidence_threshold > 0, we will also add an entry indicating the number of items under the confidence threshold. |
`item_count` |
`google.protobuf.wrappers_pb2.Int64Value`
Number of items being predicted as this label. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ModelReference -->

# Class ModelReference (3.40.0)

`ModelReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Id path of a model.

## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. The ID of the project containing this model. |
`dataset_id` |
`str`
Required. The ID of the dataset containing this model. |
`model_id` |
`str`
Required. The ID of the model. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (_). The maximum length is 1,024 characters. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model -->

# Module model (3.40.0)

Define resources for the BigQuery ML Models API.

## Classes

[Model](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.Model)

```
Model(
model_ref: typing.Optional[
typing.Union[google.cloud.bigquery.model.ModelReference, str]
],
)
```


Model represents a machine learning model resource.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models](https://cloud.google.com/bigquery/docs/reference/rest/v2/models)

[ModelReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference)

`ModelReference()`


ModelReferences are pointers to models.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference)

[TransformColumn](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.TransformColumn)

`TransformColumn(resource: typing.Dict[str, typing.Any])`


TransformColumn represents a transform column feature.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions -->

# Class ExternalRuntimeOptions (3.40.0)

```
ExternalRuntimeOptions(
container_memory: typing.Optional[str] = None,
container_cpu: typing.Optional[int] = None,
runtime_connection: typing.Optional[str] = None,
max_batching_rows: typing.Optional[int] = None,
runtime_version: typing.Optional[str] = None,
_properties: typing.Optional[typing.Dict] = None,
)
```


Options for the runtime of the external system.

## Parameters |
|
|---|---|
Name |
Description |
`container_memory` |
`str`
Optional. Amount of memory provisioned for a Python UDF container instance. Format: {number}{unit} where unit is one of "M", "G", "Mi" and "Gi" (e.g. 1G, 512Mi). If not specified, the default value is 512Mi. For more information, see |
`container_cpu` |
`int`
Optional. Amount of CPU provisioned for a Python UDF container instance. For more information, see |
`runtime_connection` |
`str`
Optional. Fully qualified name of the connection whose service account will be used to execute the code in the container. Format: "projects/{projectId}/locations/{locationId}/connections/{connectionId}" |
`max_batching_rows` |
`int`
Optional. Maximum number of rows in each batch sent to the external runtime. If absent or if 0, BigQuery dynamically decides the number of rows in a batch. |
`runtime_version` |
`str`
Optional. Language runtime version. Example: python-3.11. |

## Properties

### container_cpu

Optional. Amount of CPU provisioned for a Python UDF container instance.

### container_memory

Optional. Amount of memory provisioned for a Python UDF container instance.

### max_batching_rows

Optional. Maximum number of rows in each batch sent to the external runtime.

### runtime_connection

Optional. Fully qualified name of the connection.

### runtime_version

Optional. Language runtime version.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.ExternalRuntimeOptions
```


Factory: construct external runtime options given its API representation.

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
`google.cloud.bigquery.routine.ExternalRuntimeOptions` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this ExternalRuntimeOptions.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
External runtime options represented as an API resource. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.UnknownJob -->

# Class UnknownJob (3.40.0)

`UnknownJob(job_id, client)`


A job whose type cannot be determined.

## Methods

### from_api_repr

`from_api_repr(resource: dict, client) -> google.cloud.bigquery.job.base.UnknownJob`


Construct an UnknownJob from the JSON representation.

Parameters |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON representation of a job. |
`client` |
Client connected to BigQuery API. |

Returns |
|
|---|---|
Type |
Description |
`UnknownJob` |
Job corresponding to the resource. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.PatchModelRequest -->

# Class PatchModelRequest (3.40.0)

`PatchModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project ID of the model to patch. |
`dataset_id` |
`str`
Required. Dataset ID of the model to patch. |
`model_id` |
`str`
Required. Model ID of the model to patch. |
`model` |
Required. Patched model. Follows RFC5789 patch semantics. Missing fields are not updated. To clear a field, explicitly set to default value. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.GoogleSheetsOptions -->

# Class GoogleSheetsOptions (3.40.0)

`GoogleSheetsOptions()`


Options that describe how to treat Google Sheets as BigQuery tables.

## Properties

### range

str: The range of a sheet that BigQuery will query from.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#GoogleSheetsOptions.FIELDS.range](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#GoogleSheetsOptions.FIELDS.range)

### skip_leading_rows

int: The number of rows at the top of a sheet that BigQuery will skip when reading the data.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.GoogleSheetsOptions
```


Factory: construct a `.external_config.GoogleSheetsOptions`

instance given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, Any]`
Definition of a |

Returns |
|
|---|---|
Type |
Description |
`GoogleSheetsOptions` |
Configuration parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, Any]` |
A dictionary in the format used by the BigQuery API. |
