---
merged_at: 2026-01-25T15:38:56.568654
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquerymodelmodelreference__googlecloudbigquerytableclonedefinitio_05595e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerymodelmodelreference__googlecloudbigquerytableclonedefinition_a3e562.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerymodelmodelreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference -->

# Class ModelReference (3.40.0)

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


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerytableclonedefinition_googlecloudbigqueryexternal_configexter_d60d74.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytableclonedefinition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.CloneDefinition -->

# Class CloneDefinition (3.40.0)

`CloneDefinition(resource: typing.Dict[str, typing.Any])`


Information about base table and clone time of the clone.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#clonedefinition](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#clonedefinition)


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_configexternalsourceformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat -->

# Class ExternalSourceFormat (3.40.0)

`ExternalSourceFormat()`


The format for external data files.

Note that the set of allowed values for external data sources is different
than the set used for loading data (see
[SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat)).


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelclusteringmetricsclusterfeaturevalue_googleclou_d1e509.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelclusteringmetricsclusterfeaturevalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerymodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerydatasetdatasetreference__googlecloudbigqueryexternal_configg_af4424.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydatasetdatasetreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference -->

# Class DatasetReference (3.40.0)

`DatasetReference(project: str, dataset_id: str)`


DatasetReferences are pointers to datasets.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference)

## Parameters |
|
|---|---|
Name |
Description |
`project` |
`str`
The ID of the project |
`dataset_id` |
`str`
The ID of the dataset |

## Properties

### dataset_id

str: Dataset ID.

### path

str: URL path for the dataset based on project and dataset ID.

### project

str: Project ID of the dataset.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.dataset.DatasetReference`


Factory: construct a dataset reference given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, str]`
Dataset reference resource representation returned from the API |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.dataset.DatasetReference` |
Dataset reference parsed from `resource` . |

### from_string

```
from_string(
dataset_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.dataset.DatasetReference
```


Construct a dataset reference from dataset ID string.

Parameters |
|
|---|---|
Name |
Description |
`dataset_id` |
`str`
A dataset ID in standard SQL format. If |
`default_project` |
`Optional[str]`
The project ID to use when |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `dataset_id` is not a fully-qualified dataset ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`DatasetReference .. rubric:: Examples >>> DatasetReference.from_string('my-project-id.some_dataset') DatasetReference('my-project-id', 'some_dataset')` |
Dataset reference parsed from `dataset_id` . |

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

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this dataset reference

Returns |
|
|---|---|
Type |
Description |
`Dict[str, str]` |
dataset reference represented as an API resource |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryexternal_configgooglesheetsoptions_googlecloudbigquery_v2typ_acb58e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_configgooglesheetsoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.GoogleSheetsOptions -->

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


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeltrainingruniterationresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult -->

# Class IterationResult (3.40.0)

`IterationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single iteration of the training run.

## Attributes |
|
|---|---|
Name |
Description |
`index` |
`google.protobuf.wrappers_pb2.Int32Value`
Index of the iteration, 0 based. |
`duration_ms` |
`google.protobuf.wrappers_pb2.Int64Value`
Time taken to run the iteration in milliseconds. |
`training_loss` |
`google.protobuf.wrappers_pb2.DoubleValue`
Loss computed on the training data at the end of iteration. |
`eval_loss` |
`google.protobuf.wrappers_pb2.DoubleValue`
Loss computed on the eval data at the end of iteration. |
`learn_rate` |
`float`
Learn rate used for this iteration. |
`cluster_infos` |
`Sequence[`
Information about top clusters for clustering models. |

## Classes

### ArimaResult

`ArimaResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


(Auto-)arima fitting result. Wrap everything in ArimaResult for easier refactoring if we want to use model-specific iteration results.

### ClusterInfo

`ClusterInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single cluster for clustering model.
