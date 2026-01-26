---
merged_at: 2026-01-26T21:00:49.249090
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigqueryenumsautorowids_googlecloudbigqueryjobquerypriority__googl_21d81a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryenumsautorowids_googlecloudbigqueryjobquerypriority__google_7d06fd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumsautorowids_googlecloudbigqueryjobquerypriority.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsautorowids.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.AutoRowIDs -->

# Class AutoRowIDs (3.40.0)

`AutoRowIDs(value)`


How to handle automatic insert IDs when inserting rows as a stream.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobquerypriority.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPriority -->

# Class QueryPriority (3.40.0)

`QueryPriority()`


Specifies a priority for the query. The default value is
`INTERACTIVE`

.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerytabletimepartitioningtype_googlecloudbigqueryenumsqueryprior_595c1e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytabletimepartitioningtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType -->

# Class TimePartitioningType (3.40.0)

`TimePartitioningType()`


Specifies the type of time partitioning to perform.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsquerypriority.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.QueryPriority -->

# Class QueryPriority (3.40.0)

`QueryPriority()`


Specifies a priority for the query. The default value is
`INTERACTIVE`

.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytablebiglakeconfiguration.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration -->

# Class BigLakeConfiguration (3.40.0)

```
BigLakeConfiguration(
connection_id: typing.Optional[str] = None,
storage_uri: typing.Optional[str] = None,
file_format: typing.Optional[str] = None,
table_format: typing.Optional[str] = None,
_properties: typing.Optional[dict] = None,
)
```


Configuration for managed tables for Apache Iceberg, formerly known as BigLake.

## Parameters |
|
|---|---|
Name |
Description |
`connection_id` |
`Optional[str]`
The connection specifying the credentials to be used to read and write to external storage, such as Cloud Storage. The connection_id can have the form |
`storage_uri` |
`Optional[str]`
The fully qualified location prefix of the external folder where table data is stored. The '*' wildcard character is not allowed. The URI should be in the format |
`file_format` |
`Optional[str]`
The file format the table data is stored in. See BigLakeFileFormat for available values. |
`table_format` |
`Optional[str]`
The table format the metadata only snapshots are stored in. See BigLakeTableFormat for available values. |
`_properties` |
`Optional[dict]`
Private. Used to construct object from API resource. |

## Properties

### connection_id

str: The connection specifying the credentials to be used to read and write to external storage, such as Cloud Storage.

### file_format

str: The file format the table data is stored in. See BigLakeFileFormat for available values.

### storage_uri

str: The fully qualified location prefix of the external folder where table data is stored.

### table_format

str: The table format the metadata only snapshots are stored in. See BigLakeTableFormat for available values.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.table.BigLakeConfiguration
```


Factory: construct a BigLakeConfiguration given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this BigLakeConfiguration.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodelbinaryclassificationmetrics__googlecloudbigque_8f8c6f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelbinaryclassificationmetrics__googlecloudbigquer_80305a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelbinaryclassificationmetrics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.BinaryClassificationMetrics -->

# Class BinaryClassificationMetrics (3.40.0)

`BinaryClassificationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for binary classification/classifier models.

## Attributes |
|
|---|---|
Name |
Description |
`aggregate_classification_metrics` |
Aggregate classification metrics. |
`binary_confusion_matrix_list` |
`Sequence[`
Binary confusion matrix at multiple thresholds. |
`positive_label` |
`str`
Label representing the positive class. |
`negative_label` |
`str`
Label representing the negative class. |

## Classes

### BinaryConfusionMatrix

`BinaryConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for binary classification models.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumsbiglakefileformat_googlecloudbigqueryenumsqueryapimetho_d81da8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsbiglakefileformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeFileFormat -->

# Class BigLakeFileFormat (3.40.0)

`BigLakeFileFormat()`


API documentation for `bigquery.enums.BigLakeFileFormat`

class.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsqueryapimethod.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.QueryApiMethod -->

# Class QueryApiMethod (3.40.0)

`QueryApiMethod(value)`


API method used to start the query. The default value is
`INSERT`

.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelregressionmetrics__googlecloudbigqueryenumsbigl_23f4e2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelregressionmetrics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.RegressionMetrics -->

# Class RegressionMetrics (3.40.0)

`RegressionMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for regression and explicit feedback type matrix factorization models.

## Attributes |
|
|---|---|
Name |
Description |
`mean_absolute_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean absolute error. |
`mean_squared_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean squared error. |
`mean_squared_log_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean squared log error. |
`median_absolute_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Median absolute error. |
`r_squared` |
`google.protobuf.wrappers_pb2.DoubleValue`
R^2 score. This corresponds to r2_score in ML.EVALUATE. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumsbiglaketableformat_googlecloudbigquery_v2typesmodeldata_1c5f7c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsbiglaketableformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeTableFormat -->

# Class BigLakeTableFormat (3.40.0)

`BigLakeTableFormat()`


API documentation for `bigquery.enums.BigLakeTableFormat`

class.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeldatafrequency.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DataFrequency -->

# Class DataFrequency (3.40.0)

`DataFrequency(value)`


Type of supported data frequency for time series forecasting models.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine -->

# Class Routine (3.40.0)

`Routine(routine_ref, **kwargs)`


Resource representing a user-defined routine.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines)

## Parameters |
|
|---|---|
Name |
Description |
`routine_ref` |
`Union[str, `
A pointer to a routine. If |
|
`Dict`
Initial property values. |

## Properties

### arguments

List[[google.cloud.bigquery.routine.RoutineArgument](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument)]: Input/output
argument of a function or a stored procedure.

In-place modification is not supported. To set, replace the entire
property value with the modified list of
[RoutineArgument](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument) objects.

### body

str: The body of the routine.

### created

Optional[datetime.datetime]: Datetime at which the routine was
created (:data:`None`

until set from the server).

Read-only.

### data_governance_type

Optional[str]: If set to `DATA_MASKING`

, the function is validated
and made available as a masking function.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not :data:`string` or :data:`None` . |

### dataset_id

str: ID of dataset containing the routine.

### description

Optional[str]: Description of the routine (defaults to
:data:`None`

).

### determinism_level

Optional[str]: (experimental) The determinism level of the JavaScript UDF if defined.

### etag

str: ETag for the resource (:data:`None`

until set from the
server).

Read-only.

### external_runtime_options

Optional[[google.cloud.bigquery.routine.ExternalRuntimeOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions)]:
Configures the external runtime options for a routine.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### imported_libraries

List[str]: The path of the imported JavaScript libraries.

The [language](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine) must
equal `JAVACRIPT`

.

Examples:
Set the `imported_libraries`

to a list of Google Cloud Storage
URIs.

```
.. code-block:: python
routine = bigquery.Routine("proj.dataset.routine_id")
routine.imported_libraries = [
"gs://cloud-samples-data/bigquery/udfs/max-value.js",
]
```


### language

Optional[str]: The language of the routine.

Defaults to `SQL`

.

### modified

Optional[datetime.datetime]: Datetime at which the routine was
last modified (:data:`None`

until set from the server).

Read-only.

### path

str: URL path for the routine's APIs.

### project

str: ID of the project containing the routine.

### reference

[google.cloud.bigquery.routine.RoutineReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference): Reference
describing the ID of this routine.

### remote_function_options

Optional[[google.cloud.bigquery.routine.RemoteFunctionOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions)]:
Configures remote function options for a routine.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### return_table_type

The return type of a Table Valued Function (TVF) routine.

.. versionadded:: 2.22.0

### return_type

google.cloud.bigquery.StandardSqlDataType: Return type of the routine.

If absent, the return type is inferred from
[body](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine) at query time in
each query that references this routine. If present, then the
evaluated result will be cast to the specified returned type at query
time.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Routine.FIELDS.return_type](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Routine.FIELDS.return_type)

### routine_id

str: The routine ID.

### type_

str: The fine-grained type of the routine.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#RoutineType](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#RoutineType)

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.routine.routine.Routine`


Factory: construct a routine given its API representation.

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
`google.cloud.bigquery.routine.Routine` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Routine represented as an API resource. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaForecastingMetrics -->

# Class ArimaForecastingMetrics (3.40.0)

`ArimaForecastingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model evaluation metrics for ARIMA forecasting models.

## Attributes |
|
|---|---|
Name |
Description |
`non_seasonal_order` |
`Sequence[`
Non-seasonal order. |
`arima_fitting_metrics` |
`Sequence[`
Arima model fitting metrics. |
`seasonal_periods` |
`Sequence[`
Seasonal periods. Repeated because multiple periods are supported for one time series. |
`has_drift` |
`Sequence[bool]`
Whether Arima model fitted with drift or not. It is always false when d is not 1. |
`time_series_id` |
`Sequence[str]`
Id to differentiate different time series for the large-scale case. |
`arima_single_model_forecasting_metrics` |
`Sequence[`
Repeated as there can be many metric sets (one for each model) in auto-arima and the large-scale case. |

## Classes

### ArimaSingleModelForecastingMetrics

```
ArimaSingleModelForecastingMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Model evaluation metrics for a single ARIMA forecasting model.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/summary_overview -->

# Google Cloud BigQuery API

Overview of the APIs available for Google Cloud BigQuery API.

## All entries

Classes, methods and properties & attributes for Google Cloud BigQuery API.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.StandardSqlTypeNames -->

# Class StandardSqlTypeNames (3.40.0)

`StandardSqlTypeNames(value)`


Enum of allowed SQL type names in schema.SchemaField.

Datatype used in GoogleSQL.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration -->

# Module encryption_configuration (3.40.0)

Define class for the custom encryption configuration.

## Classes

[EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration)

`EncryptionConfiguration(kms_key_name=None)`


Custom encryption configuration (e.g., Cloud KMS keys).

Parameter |
|
|---|---|
Name |
Description |
`kms_key_name` |
`str`
resource ID of Cloud KMS key used for encryption |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry -->

# Class AccessEntry (3.40.0)

```
AccessEntry(
role: typing.Optional[str] = None,
entity_type: typing.Optional[str] = None,
entity_id: typing.Optional[typing.Union[typing.Dict[str, typing.Any], str]] = None,
**kwargs
)
```


Represents grant of an access role to an entity.

An entry must have exactly one of the allowed
xref_EntityTypes. If anything but `view`

, `routine`

,
or `dataset`

are set, a `role`

is also required. `role`

is omitted for `view`

,
`routine`

, `dataset`

, because they are always read-only.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets).

## Parameters |
|
|---|---|
Name |
Description |
`role` |
`typing.Optional[str]`
Role granted to the entity. The following string values are supported: |
`entity_type` |
`typing.Optional[str]`
Type of entity being granted the role. See |
`entity_id` |
`typing.Union[typing.Dict[str, typing.Any], str, NoneType]`
If the |

## Properties

### condition

Optional[Condition]: The IAM condition associated with this entry.

### dataset

API resource representation of a dataset reference.

### dataset_target_types

Which resources that the dataset in this entry applies to.

### domain

A domain to grant access to.

### entity_id

The entity_id of the entry.

### entity_type

The entity_type of the entry.

### group_by_email

An email address of a Google Group to grant access to.

### role

The role of the entry.

### routine

API resource representation of a routine reference.

### special_group

A special group to grant access to.

### user_by_email

An email address of a user to grant access to.

### view

API resource representation of a view reference.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.dataset.AccessEntry`


Factory: construct an access entry given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Access entry resource representation returned from the API |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.dataset.AccessEntry` |
Access entry parsed from `resource` . |

### to_api_repr

`to_api_repr()`


Construct the API resource representation of this access entry

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Access entry represented as an API resource |
