---
merged_at: 2026-01-25T15:38:56.564233
merged_files: 2
---

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
