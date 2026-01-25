---
merged_at: 2026-01-25T21:47:44.408206
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1beta1typesimportfeaturevaluesoperationmetadata_go_dba4b8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typesimportfeaturevaluesoperationmetadata_goo_2d806e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesimportfeaturevaluesoperationmetadata_goog_80bd78.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesimportfeaturevaluesoperationmetadata_googl_0035c2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesimportfeaturevaluesoperationmetadata_google_ab4f51.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesimportfeaturevaluesoperationmetadata_googlec_366abd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesimportfeaturevaluesoperationmetadata_googlecl_1bfea7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportfeaturevaluesoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesOperationMetadata -->

# Class ImportFeatureValuesOperationMetadata (1.134.0)

```
ImportFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform import Feature values.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Featurestore import Feature values. |
`imported_entity_count` |
`int`
Number of entities that have been imported by the operation. |
`imported_feature_value_count` |
`int`
Number of Feature values that have been imported by the operation. |
`source_uris` |
`MutableSequence[str]`
The source URI from where Feature values are imported. |
`invalid_row_count` |
`int`
The number of rows in input source that weren't imported due to either - Not having any featureValues. - Having a null entityId. - Having a null timestamp. - Not being parsable (applicable for CSV sources). |
`timestamp_outside_retention_rows_count` |
`int`
The number rows that weren't ingested due to having timestamps outside the retention boundary. |
`blocking_operation_ids` |
`MutableSequence[int]`
List of ImportFeatureValues operations running under a single EntityType that are blocking this operation. |

## Methods

### ImportFeatureValuesOperationMetadata

```
ImportFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform import Feature values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringalertconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringAlertConfig -->

# Class ModelMonitoringAlertConfig (1.134.0)

`ModelMonitoringAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The alert config for model monitoring.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`email_alert_config` |
Email alert config. This field is a member of `oneof` _ `alert` .
|
`enable_logging` |
`bool`
Dump the anomalies to Cloud Logging. The anomalies will be put to json payload encoded from proto ModelMonitoringStatsAnomalies. This can be further synced to Pub/Sub or any other services supported by Cloud Logging. |
`notification_channels` |
`MutableSequence[str]`
Resource names of the NotificationChannels to send alert. Must be of the format `projects/`
|

## Classes

### EmailAlertConfig

`EmailAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alert.

## Methods

### ModelMonitoringAlertConfig

`ModelMonitoringAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The alert config for model monitoring.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesreadtensorboardusageresponsepermonthusagedata_goo_138e17.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreadtensorboardusageresponsepermonthusagedata_goog_c7fb12.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadtensorboardusageresponsepermonthusagedata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardUsageResponse.PerMonthUsageData -->

# Class PerMonthUsageData (1.134.0)

`PerMonthUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per month usage data

## Attribute |
|
|---|---|
Name |
Description |
`user_usage_data` |
`MutableSequence[`
Usage data for each user in the given month. |

## Methods

### PerMonthUsageData

`PerMonthUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per month usage data


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesuploadragfileconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadRagFileConfig -->

# Class UploadRagFileConfig (1.134.0)

`UploadRagFileConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for uploading RagFile.

## Attribute |
|
|---|---|
Name |
Description |
`rag_file_transformation_config` |
Specifies the transformation config for RagFiles. |

## Methods

### UploadRagFileConfig

`UploadRagFileConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for uploading RagFile.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeswritetensorboardrundataresponse_googlecloudaiplatf_770a01.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeswritetensorboardrundataresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteTensorboardRunDataResponse -->

# Class WriteTensorboardRunDataResponse (1.134.0)

```
WriteTensorboardRunDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.WriteTensorboardRunData.

## Methods

### WriteTensorboardRunDataResponse

```
WriteTensorboardRunDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.WriteTensorboardRunData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesneighbor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Neighbor -->

# Class Neighbor (1.134.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Neighbors for example-based explanations.

## Attributes |
|
|---|---|
Name |
Description |
`neighbor_id` |
`str`
Output only. The neighbor id. |
`neighbor_distance` |
`float`
Output only. The neighbor distance. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Neighbors for example-based explanations.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesextension_registry_servicepagers_googleclo_fe6866.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesextension_registry_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.extension_registry_service.pagers`

module.

## Classes

[ListExtensionsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.pagers.ListExtensionsAsyncPager)

```
ListExtensionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsRequest,
response: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
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


A pager for iterating through `list_extensions`

requests.

This class thinly wraps an initial
[ListExtensionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`extensions`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListExtensions`

requests and continue to iterate
through the `extensions`

field on the
corresponding responses.

All the usual [ListExtensionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListExtensionsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.pagers.ListExtensionsPager)

```
ListExtensionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsRequest,
response: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_extensions`

requests.

This class thinly wraps an initial
[ListExtensionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsResponse) object, and
provides an `__iter__`

method to iterate through its
`extensions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListExtensions`

requests and continue to iterate
through the `extensions`

field on the
corresponding responses.

All the usual [ListExtensionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesindex_endpoint_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.index_endpoint_service.pagers`

module.

## Classes

[ListIndexEndpointsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.pagers.ListIndexEndpointsAsyncPager)

```
ListIndexEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse
],
],
request: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
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


A pager for iterating through `list_index_endpoints`

requests.

This class thinly wraps an initial
[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsResponse) object, and
provides an `__aiter__`

method to iterate through its
`index_endpoints`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListIndexEndpoints`

requests and continue to iterate
through the `index_endpoints`

field on the
corresponding responses.

All the usual [ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListIndexEndpointsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.pagers.ListIndexEndpointsPager)

```
ListIndexEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
],
request: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_index_endpoints`

requests.

This class thinly wraps an initial
[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`index_endpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListIndexEndpoints`

requests and continue to iterate
through the `index_endpoints`

field on the
corresponding responses.

All the usual [ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformtabulardataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TabularDataset -->

# Class TabularDataset (1.134.0)

```
TabularDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


A managed tabular dataset resource for Vertex AI.

Use this class to work with tabular datasets. You can use a CSV file, BigQuery, or a pandas
[ DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html)
to create a tabular dataset. For more information about paging through
BigQuery data, see

[Read data with BigQuery API using pagination](https://cloud.google.com/bigquery/docs/paging-results). For more information about tabular data, see

[Tabular data](https://cloud.google.com/vertex-ai/docs/training-overview#tabular_data).

The following code shows you how to create and import a tabular dataset with a CSV file.

```
my_dataset = aiplatform.TabularDataset.create(
display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])
```


Contrary to unstructured datasets, creating and importing a tabular dataset can only be done in a single step.

If you create a tabular dataset with a pandas
[ DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html),
you need to use a BigQuery table to stage the data for Vertex AI:

```
my_dataset = aiplatform.TabularDataset.create_from_dataframe(
df_source=my_pandas_dataframe,
staging_path=f"bq://{bq_dataset_id}.table-unique"
)
```


## Properties

### column_names

Retrieve the columns for the dataset by extracting it from the Google Cloud Storage or Google BigQuery source.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
When no valid source is found. |

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### metadata_schema_uri

The metadata schema uri of this dataset resource.

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### TabularDataset

```
TabularDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed dataset given a dataset name or ID.

Parameters |
|
|---|---|
Name |
Description |
`dataset_name` |
`str`
Required. A fully-qualified dataset resource name or dataset ID. Example: "projects/123/locations/us-central1/datasets/456" or "456" when project and location are initialized or passed. |
`project` |
`str`
Optional project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to retrieve this Dataset. Overrides credentials set in aiplatform.init. |

### create

```
create(
display_name: typing.Optional[str] = None,
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
bq_source: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.tabular_dataset.TabularDataset
```


Creates a tabular dataset.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the dataset. The name must contain 128 or fewer UTF-8 characters. |
`gcs_source` |
`Union[str, Sequence[str]]`
Optional. The URI to one or more Google Cloud Storage buckets that contain your datasets. For example, |
`bq_source` |
`str`
Optional. The URI to a BigQuery table that's used as an input source. For example, |
`project` |
`str`
Optional. The name of the Google Cloud project to which this |
`location` |
`str`
Optional. The Google Cloud region where this dataset is uploaded. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload the |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings that contain metadata that's sent with the request. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Vertex AI Tensorboards. The maximum length of a key and of a value is 64 unicode characters. Labels and keys can contain only lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (system labels are excluded). For more information and examples of using labels, see |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key that's used to protect the dataset. The format of the key is |
`sync` |
`bool`
If |
`create_request_timeout` |
`float`
Optional. The number of seconds for the timeout of the create request. |

Returns |
|
|---|---|
Type |
Description |
`tabular_dataset (TabularDataset)` |
An instantiated representation of the managed `TabularDataset` resource. |

### create_from_dataframe

```
create_from_dataframe(
df_source: pd.DataFrame,
staging_path: str,
bq_schema: typing.Optional[typing.Union[str, bigquery.SchemaField]] = None,
display_name: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> TabularDataset
```


Creates a new tabular dataset from a pandas `DataFrame`

.

Parameters |
|
|---|---|
Name |
Description |
`df_source` |
`pd.DataFrame`
Required. A pandas `TabularDataset` . This method uses the data types from the provided `DataFrame` when the `TabularDataset` is created. |
`staging_path` |
`str`
Required. The BigQuery table used to stage the data for Vertex AI. Because Vertex AI maintains a reference to this source to create the |
`bq_schema` |
`Optional[Union[str, bigquery.SchemaField]]`
Optional. If not set, BigQuery autodetects the schema using the column types of your |
`display_name` |
`str`
Optional. The user-defined name of the |
`project` |
`str`
Optional. The project to upload this dataset to. This overrides the project set using |
`location` |
`str`
Optional. The location to upload this dataset to. This overrides the location set using |
`credentials` |
`auth_credentials.Credentials`
Optional. The custom credentials used to upload this dataset. This overrides credentials set using |

Returns |
|
|---|---|
Type |
Description |
`tabular_dataset (TabularDataset)` |
An instantiated representation of the managed `TabularDataset` resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### export_data

`export_data(output_dir: str) -> typing.Sequence[str]`


Exports data to output dir to GCS.

Parameter |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |

Returns |
|
|---|---|
Type |
Description |
`exported_files (Sequence[str])` |
All of the files that are exported in this export operation. |

### export_data_for_custom_training

```
export_data_for_custom_training(
output_dir: str,
annotation_filter: typing.Optional[str] = None,
saved_query_id: typing.Optional[str] = None,
annotation_schema_uri: typing.Optional[str] = None,
split: typing.Optional[
typing.Union[typing.Dict[str, str], typing.Dict[str, float]]
] = None,
) -> typing.Dict[str, typing.Any]
```


Exports data to output dir to GCS for custom training use case.

Example annotation_schema_uri (image classification): gs://google-cloud-aiplatform/schema/dataset/annotation/image_classification_1.0.0.yaml

Example split (filter split): { "training_filter": "labels.aiplatform.googleapis.com/ml_use=training", "validation_filter": "labels.aiplatform.googleapis.com/ml_use=validation", "test_filter": "labels.aiplatform.googleapis.com/ml_use=test", } Example split (fraction split): { "training_fraction": 0.7, "validation_fraction": 0.2, "test_fraction": 0.1, }

Parameters |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |
`annotation_filter` |
`str`
Optional. An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in |
`saved_query_id` |
`str`
Optional. The ID of a SavedQuery (annotation set) under this Dataset used for filtering Annotations for training. Only used for custom training data export use cases. Only applicable to Datasets that have SavedQueries. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`annotation_schema_uri` |
`str`
Optional. The Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/annotation/, note that the chosen schema must be consistent with metadata_schema_uri of this Dataset. Only used for custom training data export use cases. Only applicable if this Dataset that have DataItems and Annotations. Only Annotations that both match this schema and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both annotations_filter and annotation_schema_uri. |
`split` |
`Union[Dict[str, str], Dict[str, float]]`
The instructions how the export data should be split between the training, validation and test sets. |

Returns |
|
|---|---|
Type |
Description |
`export_data_response (Dict)` |
Response message for DatasetService.ExportData in Dictionary format. |

### import_data

`import_data()`


Upload data to existing managed dataset.

Parameters |
|
|---|---|
Name |
Description |
`gcs_source` |
`Union[str, Sequence[str]]`
Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see |
`import_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing the import format. Validation will be done against the schema. The schema is defined as an |
`data_item_labels` |
`Dict`
Labels that will be applied to newly imported DataItems. If an identical DataItem as one being imported already exists in the Dataset, then these labels will be appended to these of the already existing one, and if labels with identical key is imported before, the old label value will be overwritten. If two DataItems are identical in the same import data operation, the labels will be combined and if key collision happens in this case, one of the values will be picked randomly. Two DataItems are considered identical if their content bytes are identical (e.g. image bytes or pdf bytes). These labels will be overridden by Annotation labels specified inside index file referenced by |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`import_request_timeout` |
`float`
Optional. The timeout for the import request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Instantiated representation of the managed dataset resource. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


List all instances of this Dataset resource.

Example Usage:

aiplatform.TabularDataset.list( filter='labels.my_key="my_value"', order_by='display_name' )

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: |
`project` |
`str`
Optional. Project to retrieve list from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve list from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve list. Overrides credentials set in aiplatform.init. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
*,
display_name: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
description: typing.Optional[str] = None,
update_request_timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.datasets.dataset._Dataset
```


Update the dataset. Updatable fields:

`display_name`

`description`

`labels`


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the Dataset. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See |
`description` |
`str`
Optional. The description of the Dataset. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Updated dataset. |

### wait

`wait()`


Helper method that blocks until all futures are complete.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesurlcontextmetadata_googlecloudaiplatform_v1typ_fe5329.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesurlcontextmetadata_googlecloudaiplatform_v1type_02a0e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesurlcontextmetadata_googlecloudaiplatform_v1types_f023cd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesurlcontextmetadata_googlecloudaiplatform_v1typess_809987.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesurlcontextmetadata_googlecloudaiplatform_v1typessa_6ddfb7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesurlcontextmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UrlContextMetadata -->

# Class UrlContextMetadata (1.134.0)

`UrlContextMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata related to url context retrieval tool.

## Attribute |
|
|---|---|
Name |
Description |
`url_metadata` |
`MutableSequence[`
Output only. List of url context. |

## Methods

### UrlContextMetadata

`UrlContextMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata related to url context retrieval tool.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessafetysettingharmblockmethod.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SafetySetting.HarmBlockMethod -->

# Class HarmBlockMethod (1.134.0)

`HarmBlockMethod(value)`


Probability vs severity.

## Enums |
|
|---|---|
Name |
Description |
`HARM_BLOCK_METHOD_UNSPECIFIED` |
The harm block method is unspecified. |
`SEVERITY` |
The harm block method uses both probability and severity scores. |
`PROBABILITY` |
The harm block method uses the probability score. |

## Methods

### HarmBlockMethod

`HarmBlockMethod(value)`


Probability vs severity.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnasjobspecmultitrialalgorithmspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobSpec.MultiTrialAlgorithmSpec -->

# Class MultiTrialAlgorithmSpec (1.134.0)

`MultiTrialAlgorithmSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of multi-trial Neural Architecture Search (NAS).

## Attributes |
|
|---|---|
Name |
Description |
`multi_trial_algorithm` |
The multi-trial Neural Architecture Search (NAS) algorithm type. Defaults to `REINFORCEMENT_LEARNING` .
|
`metric` |
Metric specs for the NAS job. Validation for this field is done at `multi_trial_algorithm_spec` field.
|
`search_trial_spec` |
Required. Spec for search trials. |
`train_trial_spec` |
Spec for train trials. Top N [TrainTrialSpec.max_parallel_trial_count] search trials will be trained for every M [TrainTrialSpec.frequency] trials searched. |

## Classes

### MetricSpec

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

### MultiTrialAlgorithm

`MultiTrialAlgorithm(value)`


The available types of multi-trial algorithms.

### SearchTrialSpec

`SearchTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for search trials.

### TrainTrialSpec

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.

## Methods

### MultiTrialAlgorithmSpec

`MultiTrialAlgorithmSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of multi-trial Neural Architecture Search (NAS).


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdatasetversion_googlecloudaiplatformv1schemat_d20411.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdatasetversion.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetVersion -->

# Class DatasetVersion (1.134.0)

`DatasetVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the dataset version.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Identifier. The resource name of the DatasetVersion. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DatasetVersion was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DatasetVersion was last updated. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`big_query_dataset_name` |
`str`
Output only. Name of the associated BigQuery dataset. |
`display_name` |
`str`
The user-defined name of the DatasetVersion. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Required. Output only. Additional information about the DatasetVersion. |
`model_reference` |
`str`
Output only. Reference to the public base model last used by the dataset version. Only set for prompt dataset versions. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Methods

### DatasetVersion

`DatasetVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the dataset version.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstransformationnumericarraytransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.NumericArrayTransformation -->

# Class NumericArrayTransformation (1.134.0)

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

## Attribute |
|
|---|---|
Name |
Description |
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesentitytype___googlecloudaiplatform_v1beta1typesrag_c15f08.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesentitytype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EntityType -->

# Class EntityType (1.134.0)

`EntityType(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. Name of the EntityType. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
The last part entity_type is assigned by the client. The
entity_type can be up to 64 characters long and can consist
only of ASCII Latin letters A-Z and a-z and underscore(\_),
and ASCII digits 0-9 starting with a letter. The value will
be unique given a featurestore.
|
`description` |
`str`
Optional. Description of the EntityType. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this EntityType was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this EntityType was most recently updated. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your EntityTypes. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one EntityType (System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`etag` |
`str`
Optional. Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`monitoring_config` |
Optional. The default monitoring configuration for all Features with value type (Feature.ValueType) BOOL, STRING, DOUBLE or INT64 under this EntityType. If this is populated with [FeaturestoreMonitoringConfig.monitoring_interval] specified, snapshot analysis monitoring is enabled. Otherwise, snapshot analysis monitoring is disabled. |
`offline_storage_ttl_days` |
`int`
Optional. Config for data retention policy in offline storage. TTL in days for feature values that will be stored in offline storage. The Feature Store offline storage periodically removes obsolete feature values older than `offline_storage_ttl_days` since the feature generation
time. If unset (or explicitly set to 0), default to 4000
days TTL.
|
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

## Methods

### EntityType

`EntityType(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesragfileparsingconfigadvancedparser_googleclo_d36e4b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragfileparsingconfigadvancedparser_googleclou_68ab01.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragfileparsingconfigadvancedparser.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileParsingConfig.AdvancedParser -->

# Class AdvancedParser (1.134.0)

`AdvancedParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the advanced parsing for RagFiles.

## Attribute |
|
|---|---|
Name |
Description |
`use_advanced_pdf_parsing` |
`bool`
Whether to use advanced PDF parsing. |

## Methods

### AdvancedParser

`AdvancedParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the advanced parsing for RagFiles.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesurlcontextmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UrlContextMetadata -->

# Class UrlContextMetadata (1.134.0)

`UrlContextMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata related to url context retrieval tool.

## Attribute |
|
|---|---|
Name |
Description |
`url_metadata` |
`MutableSequence[`
Output only. List of url context. |

## Methods

### UrlContextMetadata

`UrlContextMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata related to url context retrieval tool.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestuningdatastats.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TuningDataStats -->

# Class TuningDataStats (1.134.0)

`TuningDataStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The tuning data statistic values for TuningJob.

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
`supervised_tuning_data_stats` |
The SFT Tuning data stats. This field is a member of `oneof` _ `tuning_data_stats` .
|
`distillation_data_stats` |
Output only. Statistics for distillation. This field is a member of `oneof` _ `tuning_data_stats` .
|

## Methods

### TuningDataStats

`TuningDataStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The tuning data statistic values for TuningJob.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslisttensorboardrunsrequest_googlecloudaipla_8a3638.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslisttensorboardrunsrequest_googlecloudaiplat_dca476.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslisttensorboardrunsrequest_googlecloudaiplatf_550433.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisttensorboardrunsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsRequest -->

# Class ListTensorboardRunsRequest (1.134.0)

`ListTensorboardRunsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ListTensorboardRuns.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the TensorboardExperiment to list TensorboardRuns. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|
`filter` |
`str`
Lists the TensorboardRuns that match the filter expression. |
`page_size` |
`int`
The maximum number of TensorboardRuns to return. The service may return fewer than this value. If unspecified, at most 50 TensorboardRuns are returned. The maximum value is 1000; values above 1000 are coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous TensorboardService.ListTensorboardRuns call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to TensorboardService.ListTensorboardRuns must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the list. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListTensorboardRunsRequest

`ListTensorboardRunsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ListTensorboardRuns.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltablesinputstransformationtextarraytransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.TextArrayTransformation -->

# Class TextArrayTransformation (1.134.0)

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

## Methods

### TextArrayTransformation

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

### TextArrayTransformation

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadatarecorderrorr_ce1cf9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadatarecorderrorrecorderrortype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborSearchOperationMetadata.RecordError.RecordErrorType -->

# Class RecordErrorType (1.134.0)

The size of the dense embedding vectors does not match with the specified dimension.

NAMESPACE_MISSING

The `namespace` field is missing.

PARSING_ERROR

Generic catch-all error. Only used for validation failure where the root cause cannot be easily retrieved programmatically.

DUPLICATE_NAMESPACE

There are multiple restricts with the same `namespace` value.

OP_IN_DATAPOINT

Numeric restrict has operator specified in datapoint.

MULTIPLE_VALUES

Numeric restrict has multiple values specified.

INVALID_NUMERIC_VALUE

Numeric restrict has invalid numeric value specified.

INVALID_ENCODING

File is not in UTF_8 format.

INVALID_SPARSE_DIMENSIONS

Error parsing sparse dimensions field.

INVALID_TOKEN_VALUE

Token restrict value is invalid.

INVALID_SPARSE_EMBEDDING

Invalid sparse embedding.

INVALID_EMBEDDING

Invalid dense embedding.

Methods

RecordErrorType

RecordErrorType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescandidatefinishreason.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Candidate.FinishReason -->

# Class FinishReason (1.134.0)

`FinishReason(value)`


The reason why the model stopped generating tokens. If empty, the model has not stopped generating the tokens.

## Enums |
|
|---|---|
Name |
Description |
`FINISH_REASON_UNSPECIFIED` |
The finish reason is unspecified. |
`STOP` |
Token generation reached a natural stopping point or a configured stop sequence. |
`MAX_TOKENS` |
Token generation reached the configured maximum output tokens. |
`SAFETY` |
Token generation stopped because the content potentially contains safety violations. NOTE: When streaming, content is empty if content filters blocks the output. |
`RECITATION` |
Token generation stopped because the content potentially contains copyright violations. |
`OTHER` |
All other reasons that stopped the token generation. |
`BLOCKLIST` |
Token generation stopped because the content contains forbidden terms. |
`PROHIBITED_CONTENT` |
Token generation stopped for potentially containing prohibited content. |
`SPII` |
Token generation stopped because the content potentially contains Sensitive Personally Identifiable Information (SPII). |
`MALFORMED_FUNCTION_CALL` |
The function call generated by the model is invalid. |
`MODEL_ARMOR` |
The model response was blocked by Model Armor. |

## Methods

### FinishReason

`FinishReason(value)`


The reason why the model stopped generating tokens. If empty, the model has not stopped generating the tokens.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesentitytype___googlecloudaiplatform_v1beta1typ_7ecac3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesentitytype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EntityType -->

# Class EntityType (1.134.0)

`EntityType(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. Name of the EntityType. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
The last part entity_type is assigned by the client. The
entity_type can be up to 64 characters long and can consist
only of ASCII Latin letters A-Z and a-z and underscore(\_),
and ASCII digits 0-9 starting with a letter. The value will
be unique given a featurestore.
|
`description` |
`str`
Optional. Description of the EntityType. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this EntityType was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this EntityType was most recently updated. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your EntityTypes. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one EntityType (System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`etag` |
`str`
Optional. Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`monitoring_config` |
Optional. The default monitoring configuration for all Features with value type (Feature.ValueType) BOOL, STRING, DOUBLE or INT64 under this EntityType. If this is populated with [FeaturestoreMonitoringConfig.monitoring_interval] specified, snapshot analysis monitoring is enabled. Otherwise, snapshot analysis monitoring is disabled. |
`offline_storage_ttl_days` |
`int`
Optional. Config for data retention policy in offline storage. TTL in days for feature values that will be stored in offline storage. The Feature Store offline storage periodically removes obsolete feature values older than `offline_storage_ttl_days` since the feature generation
time. If unset (or explicitly set to 0), default to 4000
days TTL.
|
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

## Methods

### EntityType

`EntityType(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdateexplanationdatasetresponse_googlecloud_586fe6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdateexplanationdatasetresponse_googleclouda_1b30e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdateexplanationdatasetresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetResponse -->

# Class UpdateExplanationDatasetResponse (1.134.0)

```
UpdateExplanationDatasetResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message of ModelService.UpdateExplanationDataset operation.

## Methods

### UpdateExplanationDatasetResponse

```
UpdateExplanationDatasetResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message of ModelService.UpdateExplanationDataset operation.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexactmatchinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExactMatchInput -->

# Class ExactMatchInput (1.134.0)

`ExactMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for exact match metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for exact match metric. |
`instances` |
`MutableSequence[`
Required. Repeated exact match instances. |

## Methods

### ExactMatchInput

`ExactMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for exact match metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfractionsplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FractionSplit -->

# Class FractionSplit (1.134.0)

`FractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |

## Methods

### FractionSplit

`FractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvizier_servicevizierserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient -->

# Class VizierServiceAsyncClient (1.134.0)

```
VizierServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Vertex AI Vizier API.

Vertex AI Vizier is a service to solve blackbox optimization problems, such as tuning machine learning hyperparameters and searching over deep learning architectures.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`VizierServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### VizierServiceAsyncClient

```
VizierServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vizier service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VizierServiceTransport,Callable[..., VizierServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the VizierServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTlsChannelError` |
If mutual TLS transport creation failed for any reason. |

### add_trial_measurement

```
add_trial_measurement(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.AddTrialMeasurementRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Adds a measurement of the objective metrics to a Trial. This measurement is assumed to have been taken before the Trial is complete.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_add_trial_measurement():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AddTrialMeasurementRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddTrialMeasurementRequest.html)(
trial_name="trial_name_value",
)
# Make the request
response = await client.[add_trial_measurement](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_add_trial_measurement)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.AddTrialMeasurement. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### check_trial_early_stopping_state

```
check_trial_early_stopping_state(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CheckTrialEarlyStoppingStateRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Checks whether a Trial should stop or not. Returns a long-running operation. When the operation is successful, it will contain a xref_CheckTrialEarlyStoppingStateResponse.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_check_trial_early_stopping_state():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CheckTrialEarlyStoppingStateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CheckTrialEarlyStoppingStateRequest.html)(
trial_name="trial_name_value",
)
# Make the request
operation = client.[check_trial_early_stopping_state](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_check_trial_early_stopping_state)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CheckTrialEarlyStoppingState. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be CheckTrialEarlyStoppingStateResponse Response message for VizierService.CheckTrialEarlyStoppingState. |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### complete_trial

```
complete_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CompleteTrialRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Marks a Trial as complete.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_complete_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CompleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CompleteTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[complete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_complete_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CompleteTrial. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### create_study

```
create_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CreateStudyRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
study: typing.Optional[google.cloud.aiplatform_v1.types.study.Study] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Study
```


Creates a Study. A resource name will be generated after creation of the Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
study = aiplatform_v1.[Study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Study.html)()
study.display_name = "display_name_value"
study.study_spec.metrics.metric_id = "metric_id_value"
study.study_spec.metrics.goal = "MINIMIZE"
study.study_spec.parameters.double_value_spec.min_value = 0.96
study.study_spec.parameters.double_value_spec.max_value = 0.962
study.study_spec.parameters.parameter_id = "parameter_id_value"
request = aiplatform_v1.[CreateStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateStudyRequest.html)(
parent="parent_value",
study=study,
)
# Make the request
response = await client.[create_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_create_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CreateStudy. |
`parent` |
Required. The resource name of the Location to create the CustomJob in. Format: |
`study` |
Required. The Study configuration used to create the Study. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### create_trial

```
create_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CreateTrialRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
trial: typing.Optional[google.cloud.aiplatform_v1.types.study.Trial] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Adds a user provided Trial to a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTrialRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_create_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CreateTrial. |
`parent` |
Required. The resource name of the Study to create the Trial in. Format: |
`trial` |
Required. The Trial to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### custom_job_path

`custom_job_path(project: str, location: str, custom_job: str) -> str`


Returns a fully-qualified custom_job string.

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### delete_study

```
delete_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.DeleteStudyRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteStudyRequest.html)(
name="name_value",
)
# Make the request
await client.[delete_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_delete_study)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.DeleteStudy. |
`name` |
Required. The name of the Study resource to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### delete_trial

```
delete_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.DeleteTrialRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTrialRequest.html)(
name="name_value",
)
# Make the request
await client.[delete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_delete_trial)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.DeleteTrial. |
`name` |
Required. The Trial's name. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### get_study

```
get_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.GetStudyRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Study
```


Gets a Study by name.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetStudyRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_get_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.GetStudy. |
`name` |
Required. The name of the Study resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport
]
```


Returns an appropriate transport class.

Parameter |
|
|---|---|
Name |
Description |
`label` |
`typing.Optional[str]`
The name of the desired transport. If none is provided, then the first transport in the registry is used. |

### get_trial

```
get_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.GetTrialRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Gets a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_get_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.GetTrial. |
`name` |
Required. The name of the Trial resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### list_optimal_trials

```
list_optimal_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.ListOptimalTrialsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vizier_service.ListOptimalTrialsResponse
```


Lists the pareto-optimal Trials for multi-objective Study or the
optimal Trials for single-objective Study. The definition of
pareto-optimal can be checked in wiki page.
[https://en.wikipedia.org/wiki/Pareto_efficiency](https://en.wikipedia.org/wiki/Pareto_efficiency)

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_optimal_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListOptimalTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListOptimalTrialsRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[list_optimal_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_list_optimal_trials)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListOptimalTrials. |
`parent` |
Required. The name of the Study that the optimal Trial belongs to. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListOptimalTrials. |

### list_studies

```
list_studies(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.vizier_service.pagers.ListStudiesAsyncPager
```


Lists all the studies in a region for an associated project.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_studies():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListStudiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_studies](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_list_studies)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListStudies. |
`parent` |
Required. The resource name of the Location to list the Study from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListStudies. Iterating over this object will yield results and resolve additional pages automatically. |

### list_trials

```
list_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsAsyncPager
```


Lists the Trials associated with a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_list_trials)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListTrials. |
`parent` |
Required. The resource name of the Study to list the Trial from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListTrials. Iterating over this object will yield results and resolve additional pages automatically. |

### lookup_study

```
lookup_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.LookupStudyRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Study
```


Looks a study up using the user-defined display_name field instead of the fully qualified resource name.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_lookup_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[LookupStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LookupStudyRequest.html)(
parent="parent_value",
display_name="display_name_value",
)
# Make the request
response = await client.[lookup_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_lookup_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.LookupStudy. |
`parent` |
Required. The resource name of the Location to get the Study from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_custom_job_path

`parse_custom_job_path(path: str) -> typing.Dict[str, str]`


Parses a custom_job path into its component segments.

### parse_study_path

`parse_study_path(path: str) -> typing.Dict[str, str]`


Parses a study path into its component segments.

### parse_trial_path

`parse_trial_path(path: str) -> typing.Dict[str, str]`


Parses a trial path into its component segments.

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### stop_trial

```
stop_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.StopTrialRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Stops a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_stop_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StopTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StopTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[stop_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_stop_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.StopTrial. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### study_path

`study_path(project: str, location: str, study: str) -> str`


Returns a fully-qualified study string.

### suggest_trials

```
suggest_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.SuggestTrialsRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Adds one or more Trials to a Study, with parameter values suggested by Vertex AI Vizier. Returns a long-running operation associated with the generation of Trial suggestions. When this long-running operation succeeds, it will contain a xref_SuggestTrialsResponse.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_suggest_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SuggestTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SuggestTrialsRequest.html)(
parent="parent_value",
suggestion_count=1744,
client_id="client_id_value",
)
# Make the request
operation = client.[suggest_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_suggest_trials)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.SuggestTrials. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be SuggestTrialsResponse Response message for VizierService.SuggestTrials. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### trial_path

`trial_path(project: str, location: str, study: str, trial: str) -> str`


Returns a fully-qualified trial string.

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |


---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1typespointwisemetricinput_googlecloudaiplatform_v_7ae303.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typespointwisemetricinput_googlecloudaiplatform_v1_197567.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typespointwisemetricinput_googlecloudaiplatform_v1b_c61a5b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typespointwisemetricinput_googlecloudaiplatform_v1be_04a68c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typespointwisemetricinput_googlecloudaiplatform_v1bet_cdd3d8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespointwisemetricinput_googlecloudaiplatform_v1beta_33624e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespointwisemetricinput_googlecloudaiplatform_v1beta1_5a99b9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespointwisemetricinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PointwiseMetricInput -->

# Class PointwiseMetricInput (1.134.0)

`PointwiseMetricInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for pointwise metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for pointwise metric. |
`instance` |
Required. Pointwise metric instance. |

## Methods

### PointwiseMetricInput

`PointwiseMetricInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for pointwise metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessafetysettingharmblockmethod.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetySetting.HarmBlockMethod -->

# Class HarmBlockMethod (1.134.0)

`HarmBlockMethod(value)`


Probability vs severity.

## Enums |
|
|---|---|
Name |
Description |
`HARM_BLOCK_METHOD_UNSPECIFIED` |
The harm block method is unspecified. |
`SEVERITY` |
The harm block method uses both probability and severity scores. |
`PROBABILITY` |
The harm block method uses the probability score. |

## Methods

### HarmBlockMethod

`HarmBlockMethod(value)`


Probability vs severity.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesevaluationdataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluationDataset -->

# Class EvaluationDataset (1.134.0)

`EvaluationDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The dataset used for evaluation.

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
`gcs_source` |
Cloud storage source holds the dataset. Currently only one Cloud Storage file path is supported. This field is a member of `oneof` _ `source` .
|
`bigquery_source` |
BigQuery source holds the dataset. This field is a member of `oneof` _ `source` .
|

## Methods

### EvaluationDataset

`EvaluationDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The dataset used for evaluation.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesquestionansweringcorrectnessinstance_googlecl_192401.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquestionansweringcorrectnessinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringCorrectnessInstance -->

# Class QuestionAnsweringCorrectnessInstance (1.134.0)

```
QuestionAnsweringCorrectnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|
`reference` |
`str`
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`context` |
`str`
Optional. Text provided as context to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. The question asked and other instruction in the inference prompt. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringCorrectnessInstance

```
QuestionAnsweringCorrectnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquestionansweringhelpfulnessinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringHelpfulnessInstance -->

# Class QuestionAnsweringHelpfulnessInstance (1.134.0)

```
QuestionAnsweringHelpfulnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|
`reference` |
`str`
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`context` |
`str`
Optional. Text provided as context to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. The question asked and other instruction in the inference prompt. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringHelpfulnessInstance

```
QuestionAnsweringHelpfulnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesvoiceconfig__googlecloudaiplatform_v1typespublish_7bc8c9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesvoiceconfig__googlecloudaiplatform_v1typespublishe_d00630.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesvoiceconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.VoiceConfig -->

# Class VoiceConfig (1.134.0)

`VoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a voice.

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
`prebuilt_voice_config` |
The configuration for a prebuilt voice. This field is a member of `oneof` _ `voice_config` .
|
`replicated_voice_config` |
Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample. This field is a member of `oneof` _ `voice_config` .
|

## Methods

### VoiceConfig

`VoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a voice.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespublishermodelcalltoactiondeploygke_googlecloudaip_1374f2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespublishermodelcalltoactiondeploygke.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.DeployGke -->

# Class DeployGke (1.134.0)

`DeployGke(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations for PublisherModel GKE deployment

## Attribute |
|
|---|---|
Name |
Description |
`gke_yaml_configs` |
`MutableSequence[str]`
Optional. GKE deployment configuration in yaml format. |

## Methods

### DeployGke

`DeployGke(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations for PublisherModel GKE deployment


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgooglemaps.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GoogleMaps -->

# Class GoogleMaps (1.134.0)

`GoogleMaps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to retrieve public maps data for grounding, powered by Google.

## Attribute |
|
|---|---|
Name |
Description |
`enable_widget` |
`bool`
If true, include the widget context token in the response. |

## Methods

### GoogleMaps

`GoogleMaps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to retrieve public maps data for grounding, powered by Google.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodelmonitoringalertconfigemailalertconfig_google_f9fcb4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelmonitoringalertconfigemailalertconfig_googlec_dba051.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringalertconfigemailalertconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringAlertConfig.EmailAlertConfig -->

# Class EmailAlertConfig (1.134.0)

`EmailAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alert.

## Attribute |
|
|---|---|
Name |
Description |
`user_emails` |
`MutableSequence[str]`
The email addresses to send the alert. |

## Methods

### EmailAlertConfig

`EmailAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alert.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupgradenotebookruntimeresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeResponse -->

# Class UpgradeNotebookRuntimeResponse (1.134.0)

```
UpgradeNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.UpgradeNotebookRuntime.

## Methods

### UpgradeNotebookRuntimeResponse

```
UpgradeNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.UpgradeNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeswritetensorboardrundataresponse_googlecloudai_60710b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeswritetensorboardrundataresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteTensorboardRunDataResponse -->

# Class WriteTensorboardRunDataResponse (1.134.0)

```
WriteTensorboardRunDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.WriteTensorboardRunData.

## Methods

### WriteTensorboardRunDataResponse

```
WriteTensorboardRunDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.WriteTensorboardRunData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudystate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Study.State -->

# Class State (1.134.0)

`State(value)`


Describes the Study state.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
The study state is unspecified. |
`ACTIVE` |
The study is active. |
`INACTIVE` |
The study is stopped due to an internal error. |
`COMPLETED` |
The study is done when the service exhausts the parameter search space or max_trial_count is reached. |

## Methods

### State

`State(value)`


Describes the Study state.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesragcorpus___googlecloudaiplatform_v1beta1typ_5b91ff.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragcorpus___googlecloudaiplatform_v1beta1type_e76cae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragcorpus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus -->

# Class RagCorpus (1.134.0)

`RagCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagCorpus is a RagFile container and a project can have multiple RagCorpora.

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
`vector_db_config` |
Optional. Immutable. The config for the Vector DBs. This field is a member of `oneof` _ `backend_config` .
|
`vertex_ai_search_config` |
Optional. Immutable. The config for the Vertex AI Search. This field is a member of `oneof` _ `backend_config` .
|
`name` |
`str`
Output only. The resource name of the RagCorpus. |
`display_name` |
`str`
Required. The display name of the RagCorpus. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the RagCorpus. |
`rag_embedding_model_config` |
Optional. Immutable. The embedding model config of the RagCorpus. |
`rag_vector_db_config` |
Optional. Immutable. The Vector DB config of the RagCorpus. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagCorpus was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagCorpus was last updated. |
`corpus_status` |
Output only. RagCorpus state. |
`rag_files_count` |
`int`
Output only. Number of RagFiles in the RagCorpus. NOTE: This field is not populated in the response of VertexRagDataService.ListRagCorpora. |
`encryption_spec` |
Optional. Immutable. The CMEK key name used to encrypt at-rest data related to this Corpus. Only applicable to RagManagedDb option for Vector DB. This field can only be set at corpus creation time, and cannot be updated or deleted. |
`corpus_type_config` |
Optional. The corpus type config of the RagCorpus. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### CorpusTypeConfig

`CorpusTypeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the corpus type of the RagCorpus.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RagCorpus

`RagCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagCorpus is a RagFile container and a project can have multiple RagCorpora.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgooglemaps_googlecloudaiplatform_v1beta1type_240442.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgooglemaps_googlecloudaiplatform_v1beta1types_9f5dad.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgooglemaps.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GoogleMaps -->

# Class GoogleMaps (1.134.0)

`GoogleMaps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to retrieve public maps data for grounding, powered by Google.

## Attribute |
|
|---|---|
Name |
Description |
`enable_widget` |
`bool`
If true, include the widget context token in the response. |

## Methods

### GoogleMaps

`GoogleMaps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to retrieve public maps data for grounding, powered by Google.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModelConfig -->

# Class PublisherModelConfig (1.134.0)

`PublisherModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message contains configs of a publisher model.

## Attribute |
|
|---|---|
Name |
Description |
`logging_config` |
The prediction request/response logging config. |

## Methods

### PublisherModelConfig

`PublisherModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message contains configs of a publisher model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfractionsplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FractionSplit -->

# Class FractionSplit (1.134.0)

`FractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |

## Methods

### FractionSplit

`FractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesvoiceconfig__googlecloudaiplatform_v1beta1ty_71e307.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesvoiceconfig__googlecloudaiplatform_v1beta1typ_45e038.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesvoiceconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VoiceConfig -->

# Class VoiceConfig (1.134.0)

`VoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a voice.

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
`prebuilt_voice_config` |
The configuration for a prebuilt voice. This field is a member of `oneof` _ `voice_config` .
|
`replicated_voice_config` |
Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample. This field is a member of `oneof` _ `voice_config` .
|

## Methods

### VoiceConfig

`VoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a voice.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesreadtensorboardusageresponsepermonthusagedata_fedaa6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadtensorboardusageresponsepermonthusagedata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardUsageResponse.PerMonthUsageData -->

# Class PerMonthUsageData (1.134.0)

`PerMonthUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per month usage data

## Attribute |
|
|---|---|
Name |
Description |
`user_usage_data` |
`MutableSequence[`
Usage data for each user in the given month. |

## Methods

### PerMonthUsageData

`PerMonthUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per month usage data


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringalertconfigemailalertconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAlertConfig.EmailAlertConfig -->

# Class EmailAlertConfig (1.134.0)

`EmailAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alert.

## Attribute |
|
|---|---|
Name |
Description |
`user_emails` |
`MutableSequence[str]`
The email addresses to send the alert. |

## Methods

### EmailAlertConfig

`EmailAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alert.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesupdateexplanationdatasetresponse_googlecloudaipla_d25f22.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdateexplanationdatasetresponse_googlecloudaiplat_2d4cf0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateexplanationdatasetresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateExplanationDatasetResponse -->

# Class UpdateExplanationDatasetResponse (1.134.0)

```
UpdateExplanationDatasetResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message of ModelService.UpdateExplanationDataset operation.

## Methods

### UpdateExplanationDatasetResponse

```
UpdateExplanationDatasetResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message of ModelService.UpdateExplanationDataset operation.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessafetyratingharmprobability.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SafetyRating.HarmProbability -->

# Class HarmProbability (1.134.0)

`HarmProbability(value)`


Harm probability levels in the content.

## Enums |
|
|---|---|
Name |
Description |
`HARM_PROBABILITY_UNSPECIFIED` |
Harm probability unspecified. |
`NEGLIGIBLE` |
Negligible level of harm. |
`LOW` |
Low level of harm. |
`MEDIUM` |
Medium level of harm. |
`HIGH` |
High level of harm. |

## Methods

### HarmProbability

`HarmProbability(value)`


Harm probability levels in the content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespredictresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PredictResponse -->

# Class PredictResponse (1.134.0)

`PredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Predict.

## Attributes |
|
|---|---|
Name |
Description |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
The predictions that are the output of the predictions call. The schema of any single prediction may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] prediction_schema_uri. |
`deployed_model_id` |
`str`
ID of the Endpoint's DeployedModel that served this prediction. |
`model` |
`str`
Output only. The resource name of the Model which is deployed as the DeployedModel that this prediction hits. |
`model_version_id` |
`str`
Output only. The version ID of the Model which is deployed as the DeployedModel that this prediction hits. |
`model_display_name` |
`str`
Output only. The [display name][google.cloud.aiplatform.v1.Model.display_name] of the Model which is deployed as the DeployedModel that this prediction hits. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Output only. Request-level metadata returned by the model. The metadata type will be dependent upon the model implementation. |

## Methods

### PredictResponse

`PredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Predict.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvertex_rag_servicevertexragserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient -->

# Class VertexRagServiceClient (1.134.0)

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for retrieving relevant contexts.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### VertexRagServiceClient

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagServiceTransport,Callable[..., VertexRagServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If mutual TLS transport creation failed for any reason. |

### __exit__

`__exit__(type, value, traceback)`


Releases underlying transport's resources.

### augment_prompt

```
augment_prompt(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptRequest.Model
] = None,
vertex_rag_store: typing.Optional[
google.cloud.aiplatform_v1.types.tool.VertexRagStore
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptResponse
```


Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_augment_prompt():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AugmentPromptRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AugmentPromptRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[augment_prompt](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceClient_augment_prompt)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for AugmentPrompt. |
`parent` |
`str`
Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: |
`model` |
Optional. Metadata of the backend deployed model. This corresponds to the |
`vertex_rag_store` |
Optional. Retrieves contexts from the Vertex RagStore. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for AugmentPrompt. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### corroborate_content

```
corroborate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.CorroborateContentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
content: typing.Optional[google.cloud.aiplatform_v1.types.content.Content] = None,
facts: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1.types.vertex_rag_service.Fact]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.CorroborateContentResponse
```


Given an input text, it returns a score that evaluates the factuality of the text. It also extracts and returns claims from the text and provides supporting facts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_corroborate_content():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CorroborateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorroborateContentRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[corroborate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceClient_corroborate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for CorroborateContent. |
`parent` |
`str`
Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: |
`content` |
Optional. Input content to corroborate, only text format is supported for now. This corresponds to the |
`facts` |
`MutableSequence[`
Optional. Facts used to generate the text can also be used to corroborate the text. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for CorroborateContent. |

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Deprecated. Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### retrieve_contexts

```
retrieve_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.RetrieveContextsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
query: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_service.RagQuery
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.RetrieveContextsResponse
```


Retrieves relevant contexts for a query.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_retrieve_contexts():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
query = aiplatform_v1.[RagQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagQuery.html)()
query.text = "text_value"
request = aiplatform_v1.[RetrieveContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrieveContextsRequest.html)(
parent="parent_value",
query=query,
)
# Make the request
response = client.[retrieve_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceClient_retrieve_contexts)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VertexRagService.RetrieveContexts. |
`parent` |
`str`
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: |
`query` |
Required. Single RAG retrieve query. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VertexRagService.RetrieveContexts. |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |


---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typestoolcallvalidresults_googlecloudaiplatform_v1_4b36f0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typestoolcallvalidresults_googlecloudaiplatform_v1t_e41650.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typestoolcallvalidresults_googlecloudaiplatform_v1ty_abfcd5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typestoolcallvalidresults_googlecloudaiplatform_v1typ_18075b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typestoolcallvalidresults_googlecloudaiplatform_v1type_74646d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestoolcallvalidresults_googlecloudaiplatform_v1types_c426ee.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolcallvalidresults.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolCallValidResults -->

# Class ToolCallValidResults (1.134.0)

`ToolCallValidResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool call valid metric.

## Attribute |
|
|---|---|
Name |
Description |
`tool_call_valid_metric_values` |
`MutableSequence[`
Output only. Tool call valid metric values. |

## Methods

### ToolCallValidResults

`ToolCallValidResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool call valid metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolnamematchresults.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolNameMatchResults -->

# Class ToolNameMatchResults (1.134.0)

`ToolNameMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool name match metric.

## Attribute |
|
|---|---|
Name |
Description |
`tool_name_match_metric_values` |
`MutableSequence[`
Output only. Tool name match metric values. |

## Methods

### ToolNameMatchResults

`ToolNameMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool name match metric.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesapiauthapikeyconfig_googlecloudaiplatform_v1beta1t_66f96f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesapiauthapikeyconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ApiAuth.ApiKeyConfig -->

# Class ApiKeyConfig (1.134.0)

`ApiKeyConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The API secret.

## Attribute |
|
|---|---|
Name |
Description |
`api_key_secret_version` |
`str`
Required. The SecretManager secret version resource name storing API key. e.g. projects/{project}/secrets/{secret}/versions/{version} |

## Methods

### ApiKeyConfig

`ApiKeyConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The API secret.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespointwisemetricinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricInput -->

# Class PointwiseMetricInput (1.134.0)

`PointwiseMetricInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for pointwise metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for pointwise metric. |
`instance` |
Required. Pointwise metric instance. |

## Methods

### PointwiseMetricInput

`PointwiseMetricInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for pointwise metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesspecialist_pool_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.specialist_pool_service.pagers`

module.

## Classes

[ListSpecialistPoolsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.pagers.ListSpecialistPoolsAsyncPager)

```
ListSpecialistPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse
],
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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


A pager for iterating through `list_specialist_pools`

requests.

This class thinly wraps an initial
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse) object, and
provides an `__aiter__`

method to iterate through its
`specialist_pools`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSpecialistPools`

requests and continue to iterate
through the `specialist_pools`

field on the
corresponding responses.

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListSpecialistPoolsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.pagers.ListSpecialistPoolsPager)

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_specialist_pools`

requests.

This class thinly wraps an initial
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`specialist_pools`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSpecialistPools`

requests and continue to iterate
through the `specialist_pools`

field on the
corresponding responses.

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformpredictionpredictor_googlecloudaiplatform_v1typeslisttens_1ac7a8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformpredictionpredictor_googlecloudaiplatform_v1typeslisttenso_f75d5b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformpredictionpredictor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.Predictor -->

# Class Predictor (1.134.0)

`Predictor()`


Interface of the Predictor class for Custom Prediction Routines.

The Predictor is responsible for the ML logic for processing a prediction request. Specifically, the Predictor must define: (1) How to load all model artifacts used during prediction into memory. (2) The logic that should be executed at predict time.

When using the default `PredictionHandler`

, the `Predictor`

will be invoked as
follows:

```
predictor.postprocess(predictor.predict(predictor.preprocess(prediction_input)))
```


## Methods

### load

`load(artifacts_uri: str) -> None`


Loads the model artifact.

Parameter |
|
|---|---|
Name |
Description |
`artifacts_uri` |
`str`
Required. The value of the environment variable AIP_STORAGE_URI. |

### postprocess

`postprocess(prediction_results: typing.Any) -> typing.Any`


Postprocesses the prediction results.

Parameter |
|
|---|---|
Name |
Description |
`prediction_results` |
`Any`
Required. The prediction results. |

### predict

`predict(instances: typing.Any) -> typing.Any`


Performs prediction.

Parameter |
|
|---|---|
Name |
Description |
`instances` |
`Any`
Required. The instance(s) used for performing prediction. |

### preprocess

`preprocess(prediction_input: typing.Any) -> typing.Any`


Preprocesses the prediction input before doing the prediction.

Parameter |
|
|---|---|
Name |
Description |
`prediction_input` |
`Any`
Required. The prediction input that needs to be preprocessed. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslisttensorboardexperimentsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsRequest -->

# Class ListTensorboardExperimentsRequest (1.134.0)

```
ListTensorboardExperimentsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ListTensorboardExperiments.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Tensorboard to list TensorboardExperiments. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`filter` |
`str`
Lists the TensorboardExperiments that match the filter expression. |
`page_size` |
`int`
The maximum number of TensorboardExperiments to return. The service may return fewer than this value. If unspecified, at most 50 TensorboardExperiments are returned. The maximum value is 1000; values above 1000 are coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous TensorboardService.ListTensorboardExperiments call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to TensorboardService.ListTensorboardExperiments must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the list. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListTensorboardExperimentsRequest

```
ListTensorboardExperimentsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ListTensorboardExperiments.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodelmonitoringinputmodelmonitoringdatasetmo_74e5db.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringinputmodelmonitoringdatasetmod_a355e9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringinputmodelmonitoringdatasetmodelmonitoringgcssourcedataformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput.ModelMonitoringDataset.ModelMonitoringGcsSource.DataFormat -->

# Class DataFormat (1.134.0)

`DataFormat(value)`


Supported data format.

## Enums |
|
|---|---|
Name |
Description |
`DATA_FORMAT_UNSPECIFIED` |
Data format unspecified, used when this field is unset. |
`CSV` |
CSV files. |
`TF_RECORD` |
TfRecord files |
`JSONL` |
JsonL files. |

## Methods

### DataFormat

`DataFormat(value)`


Supported data format.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringnotificationspecemailconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringNotificationSpec.EmailConfig -->

# Class EmailConfig (1.134.0)

`EmailConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alerts.

## Attribute |
|
|---|---|
Name |
Description |
`user_emails` |
`MutableSequence[str]`
The email addresses to send the alerts. |

## Methods

### EmailConfig

`EmailConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alerts.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespredictrequestresponseloggingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictRequestResponseLoggingConfig -->

# Class PredictRequestResponseLoggingConfig (1.134.0)

```
PredictRequestResponseLoggingConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for logging request-response to a BigQuery table.

## Attributes |
|
|---|---|
Name |
Description |
`enabled` |
`bool`
If logging is enabled or not. |
`sampling_rate` |
`float`
Percentage of requests to be logged, expressed as a fraction in range(0,1]. |
`bigquery_destination` |
BigQuery table for logging. If only given a project, a new dataset will be created with name `logging_` where will
be made BigQuery-dataset-name compatible (e.g. most special
characters will become underscores). If no table name is
given, a new table will be created with name
`request_response_logging`
|
`request_response_logging_schema_version` |
`str`
Output only. The schema version used in creating the BigQuery table for the request response logging. The versions are "v1" and "v2". The current default version is "v1". |
`enable_otel_logging` |
`bool`
This field is used for large models. If true, in addition to the original large model logs, logs will be converted in OTel schema format, and saved in otel_log column. Default value is false. |

## Methods

### PredictRequestResponseLoggingConfig

```
PredictRequestResponseLoggingConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for logging request-response to a BigQuery table.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typespointwisemetricspec_googlecloudaiplatform_v_f5f81b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespointwisemetricspec_googlecloudaiplatform_v1_a02826.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespointwisemetricspec_googlecloudaiplatform_v1b_ff9965.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespointwisemetricspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricSpec -->

# Class PointwiseMetricSpec (1.134.0)

`PointwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`metric_prompt_template` |
`str`
Required. Metric prompt template for pointwise metric. This field is a member of `oneof` _ `_metric_prompt_template` .
|
`system_instruction` |
`str`
Optional. System instructions for pointwise metric. This field is a member of `oneof` _ `_system_instruction` .
|
`custom_output_format_config` |
Optional. CustomOutputFormatConfig allows customization of metric output. By default, metrics return a score and explanation. When this config is set, the default output is replaced with either: - The raw output string. - A parsed output based on a user-defined schema. If a custom format is chosen, the `score` and `explanation`
fields in the corresponding metric result will be empty.
|

## Methods

### PointwiseMetricSpec

`PointwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupsertexamplesresponseupsertresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertExamplesResponse.UpsertResult -->

# Class UpsertResult (1.134.0)

`UpsertResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result for creating/updating a single example.

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
`example` |
The example created/updated successfully. This field is a member of `oneof` _ `result` .
|
`status` |
`google.rpc.status_pb2.Status`
The error message of the example that was not created/updated successfully. This field is a member of `oneof` _ `result` .
|

## Methods

### UpsertResult

`UpsertResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result for creating/updating a single example.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportdataconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportDataConfig -->

# Class ExportDataConfig (1.134.0)

`ExportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes what part of the Dataset is to be exported, the destination of the export and how to export.

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
`gcs_destination` |
The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: `export-data-`
where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601
format. All export output will be written into that
directory. Inside that directory, annotations with the same
schema will be grouped into sub directories which are named
with the corresponding annotations' schema title. Inside
these sub directories, a schema.yaml will be created to
describe the output format.
This field is a member of `oneof` _ `destination` .
|
`fraction_split` |
Split based on fractions defining the size of each set. This field is a member of `oneof` _ `split` .
|
`filter_split` |
Split based on the provided filters for each set. This field is a member of `oneof` _ `split` .
|
`annotations_filter` |
`str`
An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in ListAnnotations. |
`saved_query_id` |
`str`
The ID of a SavedQuery (annotation set) under the Dataset specified by ExportDataRequest.name used for filtering Annotations for training. Only used for custom training data export use cases. Only applicable to Datasets that have SavedQueries. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`annotation_schema_uri` |
`str`
The Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`export_use` |
Indicates the usage of the exported files. |

## Classes

### ExportUse

`ExportUse(value)`


ExportUse indicates the usage of the exported files. It restricts file destination, format, annotations to be exported, whether to allow unannotated data to be exported and whether to clone files to temp Cloud Storage bucket.

## Methods

### ExportDataConfig

`ExportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes what part of the Dataset is to be exported, the destination of the export and how to export.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesgen_ai_cache_servicepagers___googlecloudai_982bcc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesgen_ai_cache_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.gen_ai_cache_service.pagers`

module.

## Classes

[ListCachedContentsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.pagers.ListCachedContentsAsyncPager)

```
ListCachedContentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
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


A pager for iterating through `list_cached_contents`

requests.

This class thinly wraps an initial
[ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse) object, and
provides an `__aiter__`

method to iterate through its
`cached_contents`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListCachedContents`

requests and continue to iterate
through the `cached_contents`

field on the
corresponding responses.

All the usual [ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListCachedContentsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.pagers.ListCachedContentsPager)

```
ListCachedContentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_cached_contents`

requests.

This class thinly wraps an initial
[ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse) object, and
provides an `__iter__`

method to iterate through its
`cached_contents`

field.

If there are more pages, the `__iter__`

method will make additional
`ListCachedContents`

requests and continue to iterate
through the `cached_contents`

field on the
corresponding responses.

All the usual [ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespairwisemetricinput_googlecloudaiplatform_v1_4729dd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespairwisemetricinput_googlecloudaiplatform_v1b_45bcfa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespairwisemetricinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseMetricInput -->

# Class PairwiseMetricInput (1.134.0)

`PairwiseMetricInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for pairwise metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for pairwise metric. |
`instance` |
Required. Pairwise metric instance. |

## Methods

### PairwiseMetricInput

`PairwiseMetricInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for pairwise metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestfrecorddestination.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TFRecordDestination -->

# Class TFRecordDestination (1.134.0)

`TFRecordDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The storage details for TFRecord output content.

## Attribute |
|
|---|---|
Name |
Description |
`gcs_destination` |
Required. Google Cloud Storage location. |

## Methods

### TFRecordDestination

`TFRecordDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The storage details for TFRecord output content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltablesinputstransformationnumericarraytransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.NumericArrayTransformation -->

# Class NumericArrayTransformation (1.134.0)

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

## Attribute |
|
|---|---|
Name |
Description |
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvertex_rag_servicevertexragserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient -->

# Class VertexRagServiceClient (1.134.0)

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for retrieving relevant contexts.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### VertexRagServiceClient

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagServiceTransport,Callable[..., VertexRagServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If mutual TLS transport creation failed for any reason. |

### __exit__

`__exit__(type, value, traceback)`


Releases underlying transport's resources.

### augment_prompt

```
augment_prompt(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptRequest.Model
] = None,
vertex_rag_store: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tool.VertexRagStore
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptResponse
```


Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_augment_prompt():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AugmentPromptRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AugmentPromptRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[augment_prompt](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceClient_augment_prompt)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for AugmentPrompt. |
`parent` |
`str`
Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: |
`model` |
Optional. Metadata of the backend deployed model. This corresponds to the |
`vertex_rag_store` |
Optional. Retrieves contexts from the Vertex RagStore. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for AugmentPrompt. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### corroborate_content

```
corroborate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.CorroborateContentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
content: typing.Optional[
google.cloud.aiplatform_v1beta1.types.content.Content
] = None,
facts: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.Fact
]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.CorroborateContentResponse
)
```


Given an input text, it returns a score that evaluates the factuality of the text. It also extracts and returns claims from the text and provides supporting facts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_corroborate_content():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CorroborateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[corroborate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceClient_corroborate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for CorroborateContent. |
`parent` |
`str`
Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: |
`content` |
Optional. Input content to corroborate, only text format is supported for now. This corresponds to the |
`facts` |
`MutableSequence[`
Optional. Facts used to generate the text can also be used to corroborate the text. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for CorroborateContent. |

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Deprecated. Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### retrieve_contexts

```
retrieve_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RetrieveContextsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
query: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RagQuery
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RetrieveContextsResponse
```


Retrieves relevant contexts for a query.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_retrieve_contexts():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
query = aiplatform_v1beta1.[RagQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagQuery.html)()
query.text = "text_value"
request = aiplatform_v1beta1.[RetrieveContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsRequest.html)(
parent="parent_value",
query=query,
)
# Make the request
response = client.[retrieve_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceClient_retrieve_contexts)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VertexRagService.RetrieveContexts. |
`parent` |
`str`
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: |
`query` |
Required. Single RAG retrieve query. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VertexRagService.RetrieveContexts. |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesvizier_servicevizierserviceasyncclient____305700.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesvizier_servicevizierserviceasyncclient_____3082d7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvizier_servicevizierserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient -->

# Class VizierServiceAsyncClient (1.134.0)

```
VizierServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Vertex AI Vizier API.

Vertex AI Vizier is a service to solve blackbox optimization problems, such as tuning machine learning hyperparameters and searching over deep learning architectures.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`VizierServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### VizierServiceAsyncClient

```
VizierServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vizier service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VizierServiceTransport,Callable[..., VizierServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the VizierServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTlsChannelError` |
If mutual TLS transport creation failed for any reason. |

### add_trial_measurement

```
add_trial_measurement(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.AddTrialMeasurementRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
```


Adds a measurement of the objective metrics to a Trial. This measurement is assumed to have been taken before the Trial is complete.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_add_trial_measurement():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AddTrialMeasurementRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddTrialMeasurementRequest.html)(
trial_name="trial_name_value",
)
# Make the request
response = await client.[add_trial_measurement](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_add_trial_measurement)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.AddTrialMeasurement. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### check_trial_early_stopping_state

```
check_trial_early_stopping_state(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.CheckTrialEarlyStoppingStateRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Checks whether a Trial should stop or not. Returns a long-running operation. When the operation is successful, it will contain a xref_CheckTrialEarlyStoppingStateResponse.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_check_trial_early_stopping_state():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CheckTrialEarlyStoppingStateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckTrialEarlyStoppingStateRequest.html)(
trial_name="trial_name_value",
)
# Make the request
operation = client.[check_trial_early_stopping_state](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_check_trial_early_stopping_state)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CheckTrialEarlyStoppingState. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be CheckTrialEarlyStoppingStateResponse Response message for VizierService.CheckTrialEarlyStoppingState. |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### complete_trial

```
complete_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.CompleteTrialRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
```


Marks a Trial as complete.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_complete_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CompleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CompleteTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[complete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_complete_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CompleteTrial. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### create_study

```
create_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.CreateStudyRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
study: typing.Optional[google.cloud.aiplatform_v1beta1.types.study.Study] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Study
```


Creates a Study. A resource name will be generated after creation of the Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
study = aiplatform_v1beta1.[Study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Study.html)()
study.display_name = "display_name_value"
study.study_spec.metrics.metric_id = "metric_id_value"
study.study_spec.metrics.goal = "MINIMIZE"
study.study_spec.parameters.double_value_spec.min_value = 0.96
study.study_spec.parameters.double_value_spec.max_value = 0.962
study.study_spec.parameters.parameter_id = "parameter_id_value"
request = aiplatform_v1beta1.[CreateStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateStudyRequest.html)(
parent="parent_value",
study=study,
)
# Make the request
response = await client.[create_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_create_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CreateStudy. |
`parent` |
Required. The resource name of the Location to create the CustomJob in. Format: |
`study` |
Required. The Study configuration used to create the Study. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### create_trial

```
create_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.CreateTrialRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
trial: typing.Optional[google.cloud.aiplatform_v1beta1.types.study.Trial] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
```


Adds a user provided Trial to a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTrialRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_create_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CreateTrial. |
`parent` |
Required. The resource name of the Study to create the Trial in. Format: |
`trial` |
Required. The Trial to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### custom_job_path

`custom_job_path(project: str, location: str, custom_job: str) -> str`


Returns a fully-qualified custom_job string.

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### delete_study

```
delete_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.DeleteStudyRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteStudyRequest.html)(
name="name_value",
)
# Make the request
await client.[delete_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_delete_study)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.DeleteStudy. |
`name` |
Required. The name of the Study resource to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### delete_trial

```
delete_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.DeleteTrialRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTrialRequest.html)(
name="name_value",
)
# Make the request
await client.[delete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_delete_trial)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.DeleteTrial. |
`name` |
Required. The Trial's name. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### get_study

```
get_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.GetStudyRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Study
```


Gets a Study by name.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetStudyRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_get_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.GetStudy. |
`name` |
Required. The name of the Study resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport
]
```


Returns an appropriate transport class.

Parameter |
|
|---|---|
Name |
Description |
`label` |
`typing.Optional[str]`
The name of the desired transport. If none is provided, then the first transport in the registry is used. |

### get_trial

```
get_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.GetTrialRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
```


Gets a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_get_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.GetTrial. |
`name` |
Required. The name of the Trial resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### list_optimal_trials

```
list_optimal_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListOptimalTrialsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.vizier_service.ListOptimalTrialsResponse
```


Lists the pareto-optimal Trials for multi-objective Study or the
optimal Trials for single-objective Study. The definition of
pareto-optimal can be checked in wiki page.
[https://en.wikipedia.org/wiki/Pareto_efficiency](https://en.wikipedia.org/wiki/Pareto_efficiency)

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_optimal_trials():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListOptimalTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListOptimalTrialsRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[list_optimal_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_list_optimal_trials)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListOptimalTrials. |
`parent` |
Required. The name of the Study that the optimal Trial belongs to. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListOptimalTrials. |

### list_studies

```
list_studies(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListStudiesAsyncPager
)
```


Lists all the studies in a region for an associated project.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_studies():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListStudiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_studies](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_list_studies)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListStudies. |
`parent` |
Required. The resource name of the Location to list the Study from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListStudies. Iterating over this object will yield results and resolve additional pages automatically. |

### list_trials

```
list_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListTrialsAsyncPager
)
```


Lists the Trials associated with a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_trials():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_list_trials)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListTrials. |
`parent` |
Required. The resource name of the Study to list the Trial from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListTrials. Iterating over this object will yield results and resolve additional pages automatically. |

### lookup_study

```
lookup_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.LookupStudyRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Study
```


Looks a study up using the user-defined display_name field instead of the fully qualified resource name.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_lookup_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[LookupStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LookupStudyRequest.html)(
parent="parent_value",
display_name="display_name_value",
)
# Make the request
response = await client.[lookup_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_lookup_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.LookupStudy. |
`parent` |
Required. The resource name of the Location to get the Study from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_custom_job_path

`parse_custom_job_path(path: str) -> typing.Dict[str, str]`


Parses a custom_job path into its component segments.

### parse_study_path

`parse_study_path(path: str) -> typing.Dict[str, str]`


Parses a study path into its component segments.

### parse_trial_path

`parse_trial_path(path: str) -> typing.Dict[str, str]`


Parses a trial path into its component segments.

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### stop_trial

```
stop_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.StopTrialRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
```


Stops a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_stop_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StopTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[stop_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_stop_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.StopTrial. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### study_path

`study_path(project: str, location: str, study: str) -> str`


Returns a fully-qualified study string.

### suggest_trials

```
suggest_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.SuggestTrialsRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Adds one or more Trials to a Study, with parameter values suggested by Vertex AI Vizier. Returns a long-running operation associated with the generation of Trial suggestions. When this long-running operation succeeds, it will contain a xref_SuggestTrialsResponse.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_suggest_trials():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SuggestTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SuggestTrialsRequest.html)(
parent="parent_value",
suggestion_count=1744,
client_id="client_id_value",
)
# Make the request
operation = client.[suggest_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceAsyncClient_suggest_trials)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.SuggestTrials. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be SuggestTrialsResponse Response message for VizierService.SuggestTrials. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### trial_path

`trial_path(project: str, location: str, study: str, trial: str) -> str`


Returns a fully-qualified trial string.

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesindex_endpoint_servicepagers_googleclou_9f189d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesindex_endpoint_servicepagers_googlecloud_5e1c1b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesindex_endpoint_servicepagers_googleclouda_d8ce1f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesindex_endpoint_servicepagers_googlecloudai_b96ec8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesindex_endpoint_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.index_endpoint_service.pagers`

module.

## Classes

[ListIndexEndpointsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers.ListIndexEndpointsAsyncPager)

```
ListIndexEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
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


A pager for iterating through `list_index_endpoints`

requests.

This class thinly wraps an initial
[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse) object, and
provides an `__aiter__`

method to iterate through its
`index_endpoints`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListIndexEndpoints`

requests and continue to iterate
through the `index_endpoints`

field on the
corresponding responses.

All the usual [ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListIndexEndpointsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers.ListIndexEndpointsPager)

```
ListIndexEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_index_endpoints`

requests.

This class thinly wraps an initial
[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`index_endpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListIndexEndpoints`

requests and continue to iterate
through the `index_endpoints`

field on the
corresponding responses.

All the usual [ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesimportdataconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataConfig -->

# Class ImportDataConfig (1.134.0)

`ImportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the location from where we import data into a Dataset, together with the labels that will be applied to the DataItems and the Annotations.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`gcs_source` |
The Google Cloud Storage location for the input content. This field is a member of `oneof` _ `source` .
|
`data_item_labels` |
`MutableMapping[str, str]`
Labels that will be applied to newly imported DataItems. If an identical DataItem as one being imported already exists in the Dataset, then these labels will be appended to these of the already existing one, and if labels with identical key is imported before, the old label value will be overwritten. If two DataItems are identical in the same import data operation, the labels will be combined and if key collision happens in this case, one of the values will be picked randomly. Two DataItems are considered identical if their content bytes are identical (e.g. image bytes or pdf bytes). These labels will be overridden by Annotation labels specified inside index file referenced by import_schema_uri, e.g. jsonl file. |
`annotation_labels` |
`MutableMapping[str, str]`
Labels that will be applied to newly imported Annotations. If two Annotations are identical, one of them will be deduped. Two Annotations are considered identical if their payload, payload_schema_uri and all of their labels are the same. These labels will be overridden by Annotation labels specified inside index file referenced by import_schema_uri, e.g. jsonl file. |
`import_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing the import format. Validation will be done against the schema. The schema is defined as an `OpenAPI 3.0.2 Schema Object |

## Classes

### AnnotationLabelsEntry

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

### DataItemLabelsEntry

`DataItemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

## Methods

### ImportDataConfig

`ImportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the location from where we import data into a Dataset, together with the labels that will be applied to the DataItems and the Annotations.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesreasoning_engine_servicepagers_googlecloudaipla_c63028.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesreasoning_engine_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.reasoning_engine_service.pagers`

module.

## Classes

[ListReasoningEnginesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.pagers.ListReasoningEnginesAsyncPager)

```
ListReasoningEnginesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse
],
],
request: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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


A pager for iterating through `list_reasoning_engines`

requests.

This class thinly wraps an initial
[ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse) object, and
provides an `__aiter__`

method to iterate through its
`reasoning_engines`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListReasoningEngines`

requests and continue to iterate
through the `reasoning_engines`

field on the
corresponding responses.

All the usual [ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListReasoningEnginesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.pagers.ListReasoningEnginesPager)

```
ListReasoningEnginesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
],
request: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_reasoning_engines`

requests.

This class thinly wraps an initial
[ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse) object, and
provides an `__iter__`

method to iterate through its
`reasoning_engines`

field.

If there are more pages, the `__iter__`

method will make additional
`ListReasoningEngines`

requests and continue to iterate
through the `reasoning_engines`

field on the
corresponding responses.

All the usual [ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_garden_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.model_garden_service.pagers`

module.

## Classes

[ListPublisherModelsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.pagers.ListPublisherModelsAsyncPager)

```
ListPublisherModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
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


A pager for iterating through `list_publisher_models`

requests.

This class thinly wraps an initial
[ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse) object, and
provides an `__aiter__`

method to iterate through its
`publisher_models`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListPublisherModels`

requests and continue to iterate
through the `publisher_models`

field on the
corresponding responses.

All the usual [ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListPublisherModelsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.pagers.ListPublisherModelsPager)

```
ListPublisherModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_publisher_models`

requests.

This class thinly wraps an initial
[ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`publisher_models`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPublisherModels`

requests and continue to iterate
through the `publisher_models`

field on the
corresponding responses.

All the usual [ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformfeaturestore.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore -->

# Class Featurestore (1.134.0)

```
Featurestore(
featurestore_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Managed featurestore resource for Vertex AI.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### Featurestore

```
Featurestore(
featurestore_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed featurestore given a featurestore resource name or a featurestore ID.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='projects/123/locations/us-central1/featurestores/my_featurestore_id'
)
or
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id'
)
```


Parameters |
|
|---|---|
Name |
Description |
`featurestore_name` |
`str`
Required. A fully-qualified featurestore resource name or a featurestore ID. Example: "projects/123/locations/us-central1/featurestores/my_featurestore_id" or "my_featurestore_id" when project and location are initialized or passed. |
`project` |
`str`
Optional. Project to retrieve featurestore from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve featurestore from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Featurestore. Overrides credentials set in aiplatform.init. |

### batch_serve_to_bq

```
batch_serve_to_bq(
bq_destination_output_uri: str,
serving_feature_ids: typing.Dict[str, typing.List[str]],
read_instances_uri: str,
pass_through_fields: typing.Optional[typing.List[str]] = None,
feature_destination_fields: typing.Optional[typing.Dict[str, str]] = None,
start_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
serve_request_timeout: typing.Optional[float] = None,
sync: bool = True,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Batch serves feature values to BigQuery destination

Exceptions |
|
|---|---|
Type |
Description |
`NotFound` |
if the BigQuery destination Dataset does not exist. |
`FailedPrecondition` |
if the BigQuery destination Dataset/Table is in a different project. |

Returns |
|
|---|---|
Type |
Description |
`Featurestore` |
The featurestore resource object batch read feature values from. |

### batch_serve_to_df

```
batch_serve_to_df(
serving_feature_ids: typing.Dict[str, typing.List[str]],
read_instances_df: pd.DataFrame,
pass_through_fields: typing.Optional[typing.List[str]] = None,
feature_destination_fields: typing.Optional[typing.Dict[str, str]] = None,
start_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
serve_request_timeout: typing.Optional[float] = None,
bq_dataset_id: typing.Optional[str] = None,
) -> pd.DataFrame
```


Batch serves feature values to pandas DataFrame

Parameters |
|
|---|---|
Name |
Description |
`serving_feature_ids` |
`Dict[str, List[str]]`
Required. A user defined dictionary to define the entity_types and their features for batch serve/read. The keys of the dictionary are the serving entity_type ids and the values are lists of serving feature ids in each entity_type. .. rubric:: Example serving_feature_ids = { 'my_entity_type_id_1': ['feature_id_1_1', 'feature_id_1_2'], 'my_entity_type_id_2': ['feature_id_2_1', 'feature_id_2_2'], } |
`read_instances_df` |
`pd.DataFrame`
Required. Read_instances_df is a pandas DataFrame containing the read instances. Each read instance should consist of exactly one read timestamp and one or more entity IDs identifying entities of the corresponding EntityTypes whose Features are requested. Each output instance contains Feature values of requested entities concatenated together as of the read time. An example read_instances_df may be pd.DataFrame( data=[ { "my_entity_type_id_1": "my_entity_type_id_1_entity_1", "my_entity_type_id_2": "my_entity_type_id_2_entity_1", "timestamp": "2020-01-01T10:00:00.123Z" ], ) An example batch_serve_output_df may be pd.DataFrame( data=[ { "my_entity_type_id_1": "my_entity_type_id_1_entity_1", "my_entity_type_id_2": "my_entity_type_id_2_entity_1", "foo": "feature_id_1_1_feature_value", "feature_id_1_2": "feature_id_1_2_feature_value", "feature_id_2_1": "feature_id_2_1_feature_value", "bar": "feature_id_2_2_feature_value", "timestamp": "2020-01-01T10:00:00.123Z" ], ) Timestamp in each read instance must be millisecond-aligned. The columns can be in any order. Values in the timestamp column must use the RFC 3339 format, e.g. |
`pass_through_fields` |
`List[str]`
Optional. When not empty, the specified fields in the read_instances source will be joined as-is in the output, in addition to those fields from the Featurestore Entity. For BigQuery source, the type of the pass-through values will be automatically inferred. For CSV source, the pass-through values will be passed as opaque bytes. |
`feature_destination_fields` |
`Dict[str, str]`
Optional. A user defined dictionary to map a feature's fully qualified resource name to its destination field name. If the destination field name is not defined, the feature ID will be used as its destination field name. .. rubric:: Example feature_destination_fields = { 'projects/123/locations/us-central1/featurestores/fs_id/entityTypes/et_id1/features/f_id11': 'foo', 'projects/123/locations/us-central1/featurestores/fs_id/entityTypes/et_id2/features/f_id22': 'bar', } |
`serve_request_timeout` |
`float`
Optional. The timeout for the serve request in seconds. |
`bq_dataset_id` |
`str`
Optional. The full dataset ID for the BigQuery dataset to use for temporarily staging data. If specified, caller must have |
`start_time` |
`timestamp_pb2.Timestamp`
Optional. Excludes Feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in Feature Store. Timestamp, if present, must not have higher than millisecond precision. |

Returns |
|
|---|---|
Type |
Description |
`pd.DataFrame` |
The pandas DataFrame containing feature values from batch serving. |

### batch_serve_to_gcs

```
batch_serve_to_gcs(
gcs_destination_output_uri_prefix: str,
gcs_destination_type: str,
serving_feature_ids: typing.Dict[str, typing.List[str]],
read_instances_uri: str,
pass_through_fields: typing.Optional[typing.List[str]] = None,
feature_destination_fields: typing.Optional[typing.Dict[str, str]] = None,
start_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
serve_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Batch serves feature values to GCS destination

Exceptions |
|
|---|---|
Type |
Description |
`ValueErro` |
if gcs_destination_type is not supported.: |

Returns |
|
|---|---|
Type |
Description |
`Featurestore` |
The featurestore resource object batch read feature values from. |

### create

```
create(
featurestore_id: str,
online_store_fixed_node_count: typing.Optional[int] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Creates a Featurestore resource.

Example Usage:

```
my_featurestore = aiplatform.Featurestore.create(
featurestore_id='my_featurestore_id',
)
```


### create_entity_type

```
create_entity_type(
entity_type_id: str,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.entity_type.EntityType
```


Creates an EntityType resource in this Featurestore.

Example Usage:

```
my_featurestore = aiplatform.Featurestore.create(
featurestore_id='my_featurestore_id'
)
my_entity_type = my_featurestore.create_entity_type(
entity_type_id='my_entity_type_id',
)
```


Parameters |
|
|---|---|
Name |
Description |
`entity_type_id` |
`str`
Required. The ID to use for the EntityType, which will become the final component of the EntityType's resource name. This value may be up to 60 characters, and valid characters are |
`description` |
`str`
Optional. Description of the EntityType. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your EntityTypes. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`sync` |
`bool`
Optional. Whether to execute this creation synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### delete

`delete(sync: bool = True, force: bool = False) -> None`


Deletes this Featurestore resource. If force is set to True, all entityTypes in this Featurestore will be deleted prior to featurestore deletion, and all features in each entityType will be deleted prior to each entityType deletion.

WARNING: This deletion is permanent.

### delete_entity_types

```
delete_entity_types(
entity_type_ids: typing.List[str], sync: bool = True, force: bool = False
) -> None
```


Deletes entity_type resources in this Featurestore given their entity_type IDs. WARNING: This deletion is permanent.

### get_entity_type

```
get_entity_type(
entity_type_id: str,
) -> google.cloud.aiplatform.featurestore.entity_type.EntityType
```


Retrieves an existing managed entityType in this Featurestore.

Parameter |
|
|---|---|
Name |
Description |
`entity_type_id` |
`str`
Required. The managed entityType resource ID in this Featurestore. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
parent: typing.Optional[str] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


List all instances of this Vertex AI Resource.

Example Usage:

aiplatform.BatchPredictionJobs.list( filter='state="JOB_STATE_SUCCEEDED" AND display_name="my_job"', )

aiplatform.Model.list(order_by="create_time desc, display_name")

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: |
`project` |
`str`
Optional. Project to retrieve list from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve list from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve list. Overrides credentials set in aiplatform.init. |
`parent` |
`str`
Optional. The parent resource name if any to retrieve list from. |

### list_entity_types

```
list_entity_types(
filter: typing.Optional[str] = None, order_by: typing.Optional[str] = None
) -> typing.List[google.cloud.aiplatform.featurestore.entity_type.EntityType]
```


Lists existing managed entityType resources in this Featurestore.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id',
)
my_featurestore.list_entity_types()
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. Lists the EntityTypes that match the filter expression. The following filters are supported: - |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
labels: typing.Optional[typing.Dict[str, str]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Updates an existing managed featurestore resource.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id',
)
my_featurestore.update(
labels={'update my key': 'update my value'},
)
```


Parameters |
|
|---|---|
Name |
Description |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Featurestores. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

### update_online_store

```
update_online_store(
fixed_node_count: int,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Updates the online store of an existing managed featurestore resource.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id',
)
my_featurestore.update_online_store(
fixed_node_count=2,
)
```


Parameters |
|
|---|---|
Name |
Description |
`fixed_node_count` |
`int`
Required. Config for online serving resources, can only update the node count to >= 1. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

### wait

`wait()`


Helper method that blocks until all futures are complete.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesspecialist_pool_service__googlecloudaip_ee7678.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesspecialist_pool_service__googlecloudaipl_4a29c2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesspecialist_pool_service__googlecloudaipla_0ed285.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesspecialist_pool_service__googlecloudaiplat_492dc8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesspecialist_pool_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service -->

# Package specialist_pool_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.specialist_pool_service`

package.

## Classes

[SpecialistPoolServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient)

A service for creating and managing Customer SpecialistPools. When customers start Data Labeling jobs, they can reuse/create Specialist Pools to bring their own Specialists to label the data. Customers can add/remove Managers for the Specialist Pool on Cloud console, then Managers will get email notifications to manage Specialists and tasks on CrowdCompute console.

[SpecialistPoolServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient)

A service for creating and managing Customer SpecialistPools. When customers start Data Labeling jobs, they can reuse/create Specialist Pools to bring their own Specialists to label the data. Customers can add/remove Managers for the Specialist Pool on Cloud console, then Managers will get email notifications to manage Specialists and tasks on CrowdCompute console.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.pagers)

API documentation for `aiplatform_v1beta1.services.specialist_pool_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfindneighborsresponsenearestneighbors_googleclouda_367901.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfindneighborsresponsenearestneighbors.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FindNeighborsResponse.NearestNeighbors -->

# Class NearestNeighbors (1.134.0)

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
The ID of the query datapoint. |
`neighbors` |
`MutableSequence[`
All its neighbors. |

## Methods

### NearestNeighbors

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesurlmetadataurlretrievalstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UrlMetadata.UrlRetrievalStatus -->

# Class UrlRetrievalStatus (1.134.0)

`UrlRetrievalStatus(value)`


Status of the url retrieval.

## Enums |
|
|---|---|
Name |
Description |
`URL_RETRIEVAL_STATUS_UNSPECIFIED` |
Default value. This value is unused. |
`URL_RETRIEVAL_STATUS_SUCCESS` |
Url retrieval is successful. |
`URL_RETRIEVAL_STATUS_ERROR` |
Url retrieval is failed due to error. |

## Methods

### UrlRetrievalStatus

`UrlRetrievalStatus(value)`


Status of the url retrieval.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexportfractionsplit_googlecloudaiplatform_v1t_47f756.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexportfractionsplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFractionSplit -->

# Class ExportFractionSplit (1.134.0)

`ExportFractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |

## Methods

### ExportFractionSplit

`ExportFractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatefeaturerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureRequest -->

# Class UpdateFeatureRequest (1.134.0)

`UpdateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeature. Request message for FeatureRegistryService.UpdateFeature.

## Attributes |
|
|---|---|
Name |
Description |
`feature` |
Required. The Feature's `name` field is used to identify
the Feature to be updated. Format:
`projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}/features/{feature}`
`projects/{project}/locations/{location}/featureGroups/{feature_group}/features/{feature}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the Features resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all fields.
Updatable fields:
- `description`
- `labels`
- `disable_monitoring` (Not supported for
FeatureRegistryService Feature)
- `point_of_contact` (Not supported for
FeaturestoreService FeatureStore)
|

## Methods

### UpdateFeatureRequest

`UpdateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeature. Request message for FeatureRegistryService.UpdateFeature.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesimportdataconfig___googlecloudaiplatform_v1be_1ef6f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportdataconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataConfig -->

# Class ImportDataConfig (1.134.0)

`ImportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the location from where we import data into a Dataset, together with the labels that will be applied to the DataItems and the Annotations.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`gcs_source` |
The Google Cloud Storage location for the input content. This field is a member of `oneof` _ `source` .
|
`data_item_labels` |
`MutableMapping[str, str]`
Labels that will be applied to newly imported DataItems. If an identical DataItem as one being imported already exists in the Dataset, then these labels will be appended to these of the already existing one, and if labels with identical key is imported before, the old label value will be overwritten. If two DataItems are identical in the same import data operation, the labels will be combined and if key collision happens in this case, one of the values will be picked randomly. Two DataItems are considered identical if their content bytes are identical (e.g. image bytes or pdf bytes). These labels will be overridden by Annotation labels specified inside index file referenced by import_schema_uri, e.g. jsonl file. |
`annotation_labels` |
`MutableMapping[str, str]`
Labels that will be applied to newly imported Annotations. If two Annotations are identical, one of them will be deduped. Two Annotations are considered identical if their payload, payload_schema_uri and all of their labels are the same. These labels will be overridden by Annotation labels specified inside index file referenced by import_schema_uri, e.g. jsonl file. |
`import_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing the import format. Validation will be done against the schema. The schema is defined as an `OpenAPI 3.0.2 Schema Object |

## Classes

### AnnotationLabelsEntry

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

### DataItemLabelsEntry

`DataItemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

## Methods

### ImportDataConfig

`ImportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the location from where we import data into a Dataset, together with the labels that will be applied to the DataItems and the Annotations.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgetindexrequest_googlecloudaiplatform_v1beta_51e03a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgetindexrequest_googlecloudaiplatform_v1beta1_d496ab.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetindexrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetIndexRequest -->

# Class GetIndexRequest (1.134.0)

`GetIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.GetIndex

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Index resource. Format: `projects/{project}/locations/{location}/indexes/{index}`
|

## Methods

### GetIndexRequest

`GetIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.GetIndex


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstructfieldvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StructFieldValue -->

# Class StructFieldValue (1.134.0)

`StructFieldValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One field of a Struct (or object) type feature value.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Name of the field in the struct feature. |
`value` |
The value for this field. |

## Methods

### StructFieldValue

`StructFieldValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One field of a Struct (or object) type feature value.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesextensionmanifest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExtensionManifest -->

# Class ExtensionManifest (1.134.0)

`ExtensionManifest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Manifest spec of an Extension needed for runtime execution.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. Extension name shown to the LLM. The name can be up to 128 characters long. |
`description` |
`str`
Required. The natural language description shown to the LLM. It should describe the usage of the extension, and is essential for the LLM to perform reasoning. e.g., if the extension is a data store, you can let the LLM know what data it contains. |
`api_spec` |
Required. Immutable. The API specification shown to the LLM. |
`auth_config` |
Required. Immutable. Type of auth supported by this extension. |

## Classes

### ApiSpec

`ApiSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The API specification shown to the LLM.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ExtensionManifest

`ExtensionManifest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Manifest spec of an Extension needed for runtime execution.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typestoolcallvalidresults_googlecloudaiplatform_f23902.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typestoolcallvalidresults_googlecloudaiplatform__57e3e9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typestoolcallvalidresults_googlecloudaiplatform_v_ec661e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestoolcallvalidresults_googlecloudaiplatform_v1_c5a2d1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolcallvalidresults.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidResults -->

# Class ToolCallValidResults (1.134.0)

`ToolCallValidResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool call valid metric.

## Attribute |
|
|---|---|
Name |
Description |
`tool_call_valid_metric_values` |
`MutableSequence[`
Output only. Tool call valid metric values. |

## Methods

### ToolCallValidResults

`ToolCallValidResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool call valid metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolnamematchresults.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchResults -->

# Class ToolNameMatchResults (1.134.0)

`ToolNameMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool name match metric.

## Attribute |
|
|---|---|
Name |
Description |
`tool_name_match_metric_values` |
`MutableSequence[`
Output only. Tool name match metric values. |

## Methods

### ToolNameMatchResults

`ToolNameMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool name match metric.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesretrievecontextsresponse_googlecloudaiplatform_v1b_9f2a44.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesretrievecontextsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrieveContextsResponse -->

# Class RetrieveContextsResponse (1.134.0)

`RetrieveContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagService.RetrieveContexts.

## Attribute |
|
|---|---|
Name |
Description |
`contexts` |
The contexts of the query. |

## Methods

### RetrieveContextsResponse

`RetrieveContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagService.RetrieveContexts.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessafetyratingharmprobability.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetyRating.HarmProbability -->

# Class HarmProbability (1.134.0)

`HarmProbability(value)`


Harm probability levels in the content.

## Enums |
|
|---|---|
Name |
Description |
`HARM_PROBABILITY_UNSPECIFIED` |
Harm probability unspecified. |
`NEGLIGIBLE` |
Negligible level of harm. |
`LOW` |
Low level of harm. |
`MEDIUM` |
Medium level of harm. |
`HIGH` |
High level of harm. |

## Methods

### HarmProbability

`HarmProbability(value)`


Harm probability levels in the content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessearchfeaturesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesRequest -->

# Class SearchFeaturesRequest (1.134.0)

`SearchFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.SearchFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`location` |
`str`
Required. The resource name of the Location to search Features. Format: `projects/{project}/locations/{location}`
|
`query` |
`str`
Query string that is a conjunction of field-restricted queries and/or field-restricted filters. Field-restricted queries and filters can be combined using `AND` to form a
conjunction.
A field query is in the form FIELD:QUERY. This implicitly
checks if QUERY exists as a substring within Feature's
FIELD. The QUERY and the FIELD are converted to a sequence
of words (i.e. tokens) for comparison. This is done by:
- Removing leading/trailing whitespace and tokenizing the
search value. Characters that are not one of alphanumeric
`[a-zA-Z0-9]` , underscore `_` , or asterisk `*` are
treated as delimiters for tokens. `*` is treated as a
wildcard that matches characters within a token.
- Ignoring case.
- Prepending an asterisk to the first and appending an
asterisk to the last token in QUERY.
A QUERY must be either a singular token or a phrase. A
phrase is one or multiple words enclosed in double quotation
marks ("). With phrases, the order of the words is
important. Words in the phrase must be matching in order and
consecutively.
Supported FIELDs for field-restricted queries:
- `feature_id`
- `description`
- `entity_type_id`
Examples:
- `feature_id: foo` --> Matches a Feature with ID
containing the substring `foo` (eg. `foo` ,
`foofeature` , `barfoo` ).
- `feature_id: foo*feature` --> Matches a Feature with ID
containing the substring `foo*feature` (eg.
`foobarfeature` ).
- `feature_id: foo AND description: bar` --> Matches a
Feature with ID containing the substring `foo` and
description containing the substring `bar` .
Besides field queries, the following exact-match filters are
supported. The exact-match filters do not support wildcards.
Unlike field-restricted queries, exact-match filters are
case-sensitive.
- `feature_id` : Supports = comparisons.
- `description` : Supports = comparisons. Multi-token
filters should be enclosed in quotes.
- `entity_type_id` : Supports = comparisons.
- `value_type` : Supports = and != comparisons.
- `labels` : Supports key-value equality as well as key
presence.
- `featurestore_id` : Supports = comparisons.
Examples:
- `description = "foo bar"` --> Any Feature with
description exactly equal to `foo bar`
- `value_type = DOUBLE` --> Features whose type is DOUBLE.
- `labels.active = yes AND labels.env = prod` --> Features
having both (active: yes) and (env: prod) labels.
- `labels.env: *` --> Any Feature which has a label with
`env` as the key.
|
`page_size` |
`int`
The maximum number of Features to return. The service may return fewer than this value. If unspecified, at most 100 Features will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100. |
`page_token` |
`str`
A page token, received from a previous FeaturestoreService.SearchFeatures call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeaturestoreService.SearchFeatures, except `page_size` , must match the call that provided the
page token.
|

## Methods

### SearchFeaturesRequest

`SearchFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.SearchFeatures.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslisttensorboardexperimentsrequest_googleclou_b9b849.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslisttensorboardexperimentsrequest_googlecloud_b6a777.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisttensorboardexperimentsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsRequest -->

# Class ListTensorboardExperimentsRequest (1.134.0)

```
ListTensorboardExperimentsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ListTensorboardExperiments.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Tensorboard to list TensorboardExperiments. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`filter` |
`str`
Lists the TensorboardExperiments that match the filter expression. |
`page_size` |
`int`
The maximum number of TensorboardExperiments to return. The service may return fewer than this value. If unspecified, at most 50 TensorboardExperiments are returned. The maximum value is 1000; values above 1000 are coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous TensorboardService.ListTensorboardExperiments call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to TensorboardService.ListTensorboardExperiments must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the list. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListTensorboardExperimentsRequest

```
ListTensorboardExperimentsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ListTensorboardExperiments.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportfractionsplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFractionSplit -->

# Class ExportFractionSplit (1.134.0)

`ExportFractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |

## Methods

### ExportFractionSplit

`ExportFractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespredictresponse__googlecloudaiplatform_v1type_fd5f7d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespredictresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictResponse -->

# Class PredictResponse (1.134.0)

`PredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Predict.

## Attributes |
|
|---|---|
Name |
Description |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
The predictions that are the output of the predictions call. The schema of any single prediction may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] prediction_schema_uri. |
`deployed_model_id` |
`str`
ID of the Endpoint's DeployedModel that served this prediction. |
`model` |
`str`
Output only. The resource name of the Model which is deployed as the DeployedModel that this prediction hits. |
`model_version_id` |
`str`
Output only. The version ID of the Model which is deployed as the DeployedModel that this prediction hits. |
`model_display_name` |
`str`
Output only. The [display name][google.cloud.aiplatform.v1beta1.Model.display_name] of the Model which is deployed as the DeployedModel that this prediction hits. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Output only. Request-level metadata returned by the model. The metadata type will be dependent upon the model implementation. |

## Methods

### PredictResponse

`PredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Predict.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescorpusstatusstate_googlecloudaiplatform_v1typeslog_6e4924.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescorpusstatusstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorpusStatus.State -->

# Class State (1.134.0)

`State(value)`


RagCorpus life state.

## Enums |
|
|---|---|
Name |
Description |
`UNKNOWN` |
This state is not supposed to happen. |
`INITIALIZED` |
RagCorpus resource entry is initialized, but hasn't done validation. |
`ACTIVE` |
RagCorpus is provisioned successfully and is ready to serve. |
`ERROR` |
RagCorpus is in a problematic situation. See `error_message` field for details. |

## Methods

### State

`State(value)`


RagCorpus life state.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslogprobsresulttopcandidates.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LogprobsResult.TopCandidates -->

# Class TopCandidates (1.134.0)

`TopCandidates(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidates with top log probabilities at each decoding step.

## Attribute |
|
|---|---|
Name |
Description |
`candidates` |
`MutableSequence[`
Sorted by log probability in descending order. |

## Methods

### TopCandidates

`TopCandidates(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidates with top log probabilities at each decoding step.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicejobserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient -->

# Class JobServiceClient (1.134.0)

```
JobServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.job_service.transports.base.JobServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.job_service.transports.base.JobServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's jobs.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`JobServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### JobServiceClient

```
JobServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.job_service.transports.base.JobServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.job_service.transports.base.JobServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the job service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,JobServiceTransport,Callable[..., JobServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the JobServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If mutual TLS transport creation failed for any reason. |

### __exit__

`__exit__(type, value, traceback)`


Releases underlying transport's resources.

### batch_prediction_job_path

```
batch_prediction_job_path(
project: str, location: str, batch_prediction_job: str
) -> str
```


Returns a fully-qualified batch_prediction_job string.

### cancel_batch_prediction_job

```
cancel_batch_prediction_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.CancelBatchPredictionJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Cancels a BatchPredictionJob.

Starts asynchronous cancellation on the BatchPredictionJob. The
server makes the best effort to cancel the job, but success is
not guaranteed. Clients can use
xref_JobService.GetBatchPredictionJob
or other methods to check whether the cancellation succeeded or
whether the job completed despite cancellation. On a successful
cancellation, the BatchPredictionJob is not deleted;instead its
xref_BatchPredictionJob.state
is set to `CANCELLED`

. Any files already outputted by the job
are not deleted.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_cancel_batch_prediction_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelBatchPredictionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelBatchPredictionJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_batch_prediction_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_cancel_batch_prediction_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CancelBatchPredictionJob. |
`name` |
`str`
Required. The name of the BatchPredictionJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_custom_job

```
cancel_custom_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.CancelCustomJobRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Cancels a CustomJob. Starts asynchronous cancellation on the
CustomJob. The server makes a best effort to cancel the job, but
success is not guaranteed. Clients can use
xref_JobService.GetCustomJob
or other methods to check whether the cancellation succeeded or
whether the job completed despite cancellation. On successful
cancellation, the CustomJob is not deleted; instead it becomes a
job with a
xref_CustomJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_CustomJob.state is
set to `CANCELLED`

.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_cancel_custom_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelCustomJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelCustomJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_custom_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_cancel_custom_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CancelCustomJob. |
`name` |
`str`
Required. The name of the CustomJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_data_labeling_job

```
cancel_data_labeling_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.CancelDataLabelingJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Cancels a DataLabelingJob. Success of cancellation is not guaranteed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_cancel_data_labeling_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelDataLabelingJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelDataLabelingJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_data_labeling_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_cancel_data_labeling_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CancelDataLabelingJob. |
`name` |
`str`
Required. The name of the DataLabelingJob. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_hyperparameter_tuning_job

```
cancel_hyperparameter_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.CancelHyperparameterTuningJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Cancels a HyperparameterTuningJob. Starts asynchronous
cancellation on the HyperparameterTuningJob. The server makes a
best effort to cancel the job, but success is not guaranteed.
Clients can use
xref_JobService.GetHyperparameterTuningJob
or other methods to check whether the cancellation succeeded or
whether the job completed despite cancellation. On successful
cancellation, the HyperparameterTuningJob is not deleted;
instead it becomes a job with a
xref_HyperparameterTuningJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_HyperparameterTuningJob.state
is set to `CANCELLED`

.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_cancel_hyperparameter_tuning_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelHyperparameterTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelHyperparameterTuningJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_hyperparameter_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_cancel_hyperparameter_tuning_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CancelHyperparameterTuningJob. |
`name` |
`str`
Required. The name of the HyperparameterTuningJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_nas_job

```
cancel_nas_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.CancelNasJobRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Cancels a NasJob. Starts asynchronous cancellation on the
NasJob. The server makes a best effort to cancel the job, but
success is not guaranteed. Clients can use
xref_JobService.GetNasJob
or other methods to check whether the cancellation succeeded or
whether the job completed despite cancellation. On successful
cancellation, the NasJob is not deleted; instead it becomes a
job with a
xref_NasJob.error value
with a `google.rpc.Status.code][google.rpc.Status.code]`

of 1,
corresponding to `Code.CANCELLED`

, and
xref_NasJob.state is set
to `CANCELLED`

.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_cancel_nas_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelNasJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelNasJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_nas_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_cancel_nas_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CancelNasJob. |
`name` |
`str`
Required. The name of the NasJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### context_path

`context_path(project: str, location: str, metadata_store: str, context: str) -> str`


Returns a fully-qualified context string.

### create_batch_prediction_job

```
create_batch_prediction_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.CreateBatchPredictionJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
batch_prediction_job: typing.Optional[
google.cloud.aiplatform_v1.types.batch_prediction_job.BatchPredictionJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.batch_prediction_job.BatchPredictionJob
```


Creates a BatchPredictionJob. A BatchPredictionJob once created will right away be attempted to start.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_batch_prediction_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
batch_prediction_job = aiplatform_v1.[BatchPredictionJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchPredictionJob.html)()
batch_prediction_job.display_name = "display_name_value"
batch_prediction_job.input_config.gcs_source.uris = ['uris_value1', 'uris_value2']
batch_prediction_job.input_config.instances_format = "instances_format_value"
batch_prediction_job.output_config.gcs_destination.output_uri_prefix = "output_uri_prefix_value"
batch_prediction_job.output_config.predictions_format = "predictions_format_value"
request = aiplatform_v1.[CreateBatchPredictionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateBatchPredictionJobRequest.html)(
parent="parent_value",
batch_prediction_job=batch_prediction_job,
)
# Make the request
response = client.[create_batch_prediction_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_create_batch_prediction_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateBatchPredictionJob. |
`parent` |
`str`
Required. The resource name of the Location to create the BatchPredictionJob in. Format: |
`batch_prediction_job` |
Required. The BatchPredictionJob to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A job that uses a Model to produce predictions on multiple [input instances][google.cloud.aiplatform.v1.BatchPredictionJob.input_config]. If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances. |

### create_custom_job

```
create_custom_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.CreateCustomJobRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
custom_job: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.CustomJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.custom_job.CustomJob
```


Creates a CustomJob. A created CustomJob right away will be attempted to be run.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_custom_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
custom_job = aiplatform_v1.[CustomJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CustomJob.html)()
custom_job.display_name = "display_name_value"
custom_job.job_spec.worker_pool_specs.container_spec.image_uri = "image_uri_value"
request = aiplatform_v1.[CreateCustomJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateCustomJobRequest.html)(
parent="parent_value",
custom_job=custom_job,
)
# Make the request
response = client.[create_custom_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_create_custom_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateCustomJob. |
`parent` |
`str`
Required. The resource name of the Location to create the CustomJob in. Format: |
`custom_job` |
Required. The CustomJob to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded). |

### create_data_labeling_job

```
create_data_labeling_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.CreateDataLabelingJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
data_labeling_job: typing.Optional[
google.cloud.aiplatform_v1.types.data_labeling_job.DataLabelingJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.data_labeling_job.DataLabelingJob
```


Creates a DataLabelingJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_data_labeling_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
data_labeling_job = aiplatform_v1.[DataLabelingJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DataLabelingJob.html)()
data_labeling_job.display_name = "display_name_value"
data_labeling_job.datasets = ['datasets_value1', 'datasets_value2']
data_labeling_job.labeler_count = 1375
data_labeling_job.instruction_uri = "instruction_uri_value"
data_labeling_job.inputs_schema_uri = "inputs_schema_uri_value"
data_labeling_job.inputs.null_value = "NULL_VALUE"
request = aiplatform_v1.[CreateDataLabelingJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDataLabelingJobRequest.html)(
parent="parent_value",
data_labeling_job=data_labeling_job,
)
# Make the request
response = client.[create_data_labeling_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_create_data_labeling_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateDataLabelingJob. |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: |
`data_labeling_job` |
Required. The DataLabelingJob to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset: |

### create_hyperparameter_tuning_job

```
create_hyperparameter_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.CreateHyperparameterTuningJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
hyperparameter_tuning_job: typing.Optional[
google.cloud.aiplatform_v1.types.hyperparameter_tuning_job.HyperparameterTuningJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.hyperparameter_tuning_job.HyperparameterTuningJob
```


Creates a HyperparameterTuningJob

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_hyperparameter_tuning_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
hyperparameter_tuning_job = aiplatform_v1.[HyperparameterTuningJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.HyperparameterTuningJob.html)()
hyperparameter_tuning_job.display_name = "display_name_value"
hyperparameter_tuning_job.study_spec.metrics.metric_id = "metric_id_value"
hyperparameter_tuning_job.study_spec.metrics.goal = "MINIMIZE"
hyperparameter_tuning_job.study_spec.parameters.double_value_spec.min_value = 0.96
hyperparameter_tuning_job.study_spec.parameters.double_value_spec.max_value = 0.962
hyperparameter_tuning_job.study_spec.parameters.parameter_id = "parameter_id_value"
hyperparameter_tuning_job.max_trial_count = 1609
hyperparameter_tuning_job.parallel_trial_count = 2128
hyperparameter_tuning_job.trial_job_spec.worker_pool_specs.container_spec.image_uri = "image_uri_value"
request = aiplatform_v1.[CreateHyperparameterTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateHyperparameterTuningJobRequest.html)(
parent="parent_value",
hyperparameter_tuning_job=hyperparameter_tuning_job,
)
# Make the request
response = client.[create_hyperparameter_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_create_hyperparameter_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateHyperparameterTuningJob. |
`parent` |
`str`
Required. The resource name of the Location to create the HyperparameterTuningJob in. Format: |
`hyperparameter_tuning_job` |
Required. The HyperparameterTuningJob to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a HyperparameterTuningJob. A HyperparameterTuningJob has a Study specification and multiple CustomJobs with identical CustomJob specification. |

### create_model_deployment_monitoring_job

```
create_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.CreateModelDeploymentMonitoringJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model_deployment_monitoring_job: typing.Optional[
google.cloud.aiplatform_v1.types.model_deployment_monitoring_job.ModelDeploymentMonitoringJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.types.model_deployment_monitoring_job.ModelDeploymentMonitoringJob
)
```


Creates a ModelDeploymentMonitoringJob. It will run periodically on a configured interval.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
model_deployment_monitoring_job = aiplatform_v1.[ModelDeploymentMonitoringJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringJob.html)()
model_deployment_monitoring_job.display_name = "display_name_value"
model_deployment_monitoring_job.endpoint = "endpoint_value"
request = aiplatform_v1.[CreateModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateModelDeploymentMonitoringJobRequest.html)(
parent="parent_value",
model_deployment_monitoring_job=model_deployment_monitoring_job,
)
# Make the request
response = client.[create_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_create_model_deployment_monitoring_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateModelDeploymentMonitoringJob. |
`parent` |
`str`
Required. The parent of the ModelDeploymentMonitoringJob. Format: |
`model_deployment_monitoring_job` |
Required. The ModelDeploymentMonitoringJob to create This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a job that runs periodically to monitor the deployed models in an endpoint. It will analyze the logged training & prediction data to detect any abnormal behaviors. |

### create_nas_job

```
create_nas_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.CreateNasJobRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
nas_job: typing.Optional[google.cloud.aiplatform_v1.types.nas_job.NasJob] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.nas_job.NasJob
```


Creates a NasJob

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_nas_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
nas_job = aiplatform_v1.[NasJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJob.html)()
nas_job.display_name = "display_name_value"
nas_job.nas_job_spec.multi_trial_algorithm_spec.search_trial_spec.search_trial_job_spec.worker_pool_specs.container_spec.image_uri = "image_uri_value"
nas_job.nas_job_spec.multi_trial_algorithm_spec.search_trial_spec.max_trial_count = 1609
nas_job.nas_job_spec.multi_trial_algorithm_spec.search_trial_spec.max_parallel_trial_count = 2549
request = aiplatform_v1.[CreateNasJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNasJobRequest.html)(
parent="parent_value",
nas_job=nas_job,
)
# Make the request
response = client.[create_nas_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_create_nas_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateNasJob. |
`parent` |
`str`
Required. The resource name of the Location to create the NasJob in. Format: |
`nas_job` |
Required. The NasJob to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a Neural Architecture Search (NAS) job. |

### custom_job_path

`custom_job_path(project: str, location: str, custom_job: str) -> str`


Returns a fully-qualified custom_job string.

### data_labeling_job_path

`data_labeling_job_path(project: str, location: str, data_labeling_job: str) -> str`


Returns a fully-qualified data_labeling_job string.

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

### delete_batch_prediction_job

```
delete_batch_prediction_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.DeleteBatchPredictionJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a BatchPredictionJob. Can only be called on jobs that already finished.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_batch_prediction_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteBatchPredictionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteBatchPredictionJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_batch_prediction_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_delete_batch_prediction_job)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.DeleteBatchPredictionJob. |
`name` |
`str`
Required. The name of the BatchPredictionJob resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_custom_job

```
delete_custom_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.DeleteCustomJobRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a CustomJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_custom_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteCustomJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteCustomJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_custom_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_delete_custom_job)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.DeleteCustomJob. |
`name` |
`str`
Required. The name of the CustomJob resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_data_labeling_job

```
delete_data_labeling_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.DeleteDataLabelingJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a DataLabelingJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_data_labeling_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteDataLabelingJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDataLabelingJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_data_labeling_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_delete_data_labeling_job)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.DeleteDataLabelingJob. |
`name` |
`str`
Required. The name of the DataLabelingJob to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_hyperparameter_tuning_job

```
delete_hyperparameter_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.DeleteHyperparameterTuningJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a HyperparameterTuningJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_hyperparameter_tuning_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteHyperparameterTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteHyperparameterTuningJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_hyperparameter_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_delete_hyperparameter_tuning_job)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.DeleteHyperparameterTuningJob. |
`name` |
`str`
Required. The name of the HyperparameterTuningJob resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_model_deployment_monitoring_job

```
delete_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.DeleteModelDeploymentMonitoringJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a ModelDeploymentMonitoringJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteModelDeploymentMonitoringJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_delete_model_deployment_monitoring_job)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.DeleteModelDeploymentMonitoringJob. |
`name` |
`str`
Required. The resource name of the model monitoring job to delete. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_nas_job

```
delete_nas_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.DeleteNasJobRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a NasJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_nas_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteNasJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNasJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_nas_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_delete_nas_job)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.DeleteNasJob. |
`name` |
`str`
Required. The name of the NasJob resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`JobServiceClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`JobServiceClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`JobServiceClient` |
The constructed client. |

### get_batch_prediction_job

```
get_batch_prediction_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.GetBatchPredictionJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.batch_prediction_job.BatchPredictionJob
```


Gets a BatchPredictionJob

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_batch_prediction_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetBatchPredictionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetBatchPredictionJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_batch_prediction_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_get_batch_prediction_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetBatchPredictionJob. |
`name` |
`str`
Required. The name of the BatchPredictionJob resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A job that uses a Model to produce predictions on multiple [input instances][google.cloud.aiplatform.v1.BatchPredictionJob.input_config]. If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances. |

### get_custom_job

```
get_custom_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.GetCustomJobRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.custom_job.CustomJob
```


Gets a CustomJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_custom_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetCustomJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetCustomJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_custom_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_get_custom_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetCustomJob. |
`name` |
`str`
Required. The name of the CustomJob resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded). |

### get_data_labeling_job

```
get_data_labeling_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.GetDataLabelingJobRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.data_labeling_job.DataLabelingJob
```


Gets a DataLabelingJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_data_labeling_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetDataLabelingJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetDataLabelingJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_data_labeling_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_get_data_labeling_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetDataLabelingJob. |
`name` |
`str`
Required. The name of the DataLabelingJob. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset: |

### get_hyperparameter_tuning_job

```
get_hyperparameter_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.GetHyperparameterTuningJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.hyperparameter_tuning_job.HyperparameterTuningJob
```


Gets a HyperparameterTuningJob

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_hyperparameter_tuning_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetHyperparameterTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetHyperparameterTuningJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_hyperparameter_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_get_hyperparameter_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetHyperparameterTuningJob. |
`name` |
`str`
Required. The name of the HyperparameterTuningJob resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a HyperparameterTuningJob. A HyperparameterTuningJob has a Study specification and multiple CustomJobs with identical CustomJob specification. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_model_deployment_monitoring_job

```
get_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.GetModelDeploymentMonitoringJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.types.model_deployment_monitoring_job.ModelDeploymentMonitoringJob
)
```


Gets a ModelDeploymentMonitoringJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetModelDeploymentMonitoringJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_get_model_deployment_monitoring_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetModelDeploymentMonitoringJob. |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a job that runs periodically to monitor the deployed models in an endpoint. It will analyze the logged training & prediction data to detect any abnormal behaviors. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Deprecated. Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_nas_job

```
get_nas_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.GetNasJobRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.nas_job.NasJob
```


Gets a NasJob

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_nas_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetNasJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNasJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_nas_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_get_nas_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetNasJob. |
`name` |
`str`
Required. The name of the NasJob resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a Neural Architecture Search (NAS) job. |

### get_nas_trial_detail

```
get_nas_trial_detail(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.GetNasTrialDetailRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.nas_job.NasTrialDetail
```


Gets a NasTrialDetail.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_nas_trial_detail():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetNasTrialDetailRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNasTrialDetailRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_nas_trial_detail](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_get_nas_trial_detail)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetNasTrialDetail. |
`name` |
`str`
Required. The name of the NasTrialDetail resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a NasTrial details along with its parameters. If there is a corresponding train NasTrial, the train NasTrial is also returned. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### hyperparameter_tuning_job_path

```
hyperparameter_tuning_job_path(
project: str, location: str, hyperparameter_tuning_job: str
) -> str
```


Returns a fully-qualified hyperparameter_tuning_job string.

### list_batch_prediction_jobs

```
list_batch_prediction_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.job_service.pagers.ListBatchPredictionJobsPager
)
```


Lists BatchPredictionJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_batch_prediction_jobs():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListBatchPredictionJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_batch_prediction_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_list_batch_prediction_jobs)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.ListBatchPredictionJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the BatchPredictionJobs from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListBatchPredictionJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_custom_jobs

```
list_custom_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.ListCustomJobsRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.job_service.pagers.ListCustomJobsPager
```


Lists CustomJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_custom_jobs():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListCustomJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_custom_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_list_custom_jobs)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.ListCustomJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the CustomJobs from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListCustomJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_data_labeling_jobs

```
list_data_labeling_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.job_service.pagers.ListDataLabelingJobsPager
```


Lists DataLabelingJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_data_labeling_jobs():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListDataLabelingJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_data_labeling_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_list_data_labeling_jobs)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.ListDataLabelingJobs. |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListDataLabelingJobs. Iterating over this object will yield results and resolve additional pages automatically. |

### list_hyperparameter_tuning_jobs

```
list_hyperparameter_tuning_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.job_service.pagers.ListHyperparameterTuningJobsPager
)
```


Lists HyperparameterTuningJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_hyperparameter_tuning_jobs():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListHyperparameterTuningJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_hyperparameter_tuning_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_list_hyperparameter_tuning_jobs)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.ListHyperparameterTuningJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the HyperparameterTuningJobs from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListHyperparameterTuningJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_model_deployment_monitoring_jobs

```
list_model_deployment_monitoring_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.job_service.pagers.ListModelDeploymentMonitoringJobsPager
)
```


Lists ModelDeploymentMonitoringJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_model_deployment_monitoring_jobs():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListModelDeploymentMonitoringJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_deployment_monitoring_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_list_model_deployment_monitoring_jobs)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.ListModelDeploymentMonitoringJobs. |
`parent` |
`str`
Required. The parent of the ModelDeploymentMonitoringJob. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListModelDeploymentMonitoringJobs. Iterating over this object will yield results and resolve additional pages automatically. |

### list_nas_jobs

```
list_nas_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.job_service.pagers.ListNasJobsPager
```


Lists NasJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_nas_jobs():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListNasJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_nas_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_list_nas_jobs)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.ListNasJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the NasJobs from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListNasJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_nas_trial_details

```
list_nas_trial_details(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.job_service.pagers.ListNasTrialDetailsPager
```


List top NasTrialDetails of a NasJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_nas_trial_details():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListNasTrialDetailsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_nas_trial_details](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_list_nas_trial_details)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.ListNasTrialDetails. |
`parent` |
`str`
Required. The name of the NasJob resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListNasTrialDetails Iterating over this object will yield results and resolve additional pages automatically. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### model_deployment_monitoring_job_path

```
model_deployment_monitoring_job_path(
project: str, location: str, model_deployment_monitoring_job: str
) -> str
```


Returns a fully-qualified model_deployment_monitoring_job string.

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### nas_job_path

`nas_job_path(project: str, location: str, nas_job: str) -> str`


Returns a fully-qualified nas_job string.

### nas_trial_detail_path

```
nas_trial_detail_path(
project: str, location: str, nas_job: str, nas_trial_detail: str
) -> str
```


Returns a fully-qualified nas_trial_detail string.

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### notification_channel_path

`notification_channel_path(project: str, notification_channel: str) -> str`


Returns a fully-qualified notification_channel string.

### parse_batch_prediction_job_path

`parse_batch_prediction_job_path(path: str) -> typing.Dict[str, str]`


Parses a batch_prediction_job path into its component segments.

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_context_path

`parse_context_path(path: str) -> typing.Dict[str, str]`


Parses a context path into its component segments.

### parse_custom_job_path

`parse_custom_job_path(path: str) -> typing.Dict[str, str]`


Parses a custom_job path into its component segments.

### parse_data_labeling_job_path

`parse_data_labeling_job_path(path: str) -> typing.Dict[str, str]`


Parses a data_labeling_job path into its component segments.

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_hyperparameter_tuning_job_path

`parse_hyperparameter_tuning_job_path(path: str) -> typing.Dict[str, str]`


Parses a hyperparameter_tuning_job path into its component segments.

### parse_model_deployment_monitoring_job_path

`parse_model_deployment_monitoring_job_path(path: str) -> typing.Dict[str, str]`


Parses a model_deployment_monitoring_job path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_nas_job_path

`parse_nas_job_path(path: str) -> typing.Dict[str, str]`


Parses a nas_job path into its component segments.

### parse_nas_trial_detail_path

`parse_nas_trial_detail_path(path: str) -> typing.Dict[str, str]`


Parses a nas_trial_detail path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notification_channel_path

`parse_notification_channel_path(path: str) -> typing.Dict[str, str]`


Parses a notification_channel path into its component segments.

### parse_persistent_resource_path

`parse_persistent_resource_path(path: str) -> typing.Dict[str, str]`


Parses a persistent_resource path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_tensorboard_path

`parse_tensorboard_path(path: str) -> typing.Dict[str, str]`


Parses a tensorboard path into its component segments.

### parse_trial_path

`parse_trial_path(path: str) -> typing.Dict[str, str]`


Parses a trial path into its component segments.

### pause_model_deployment_monitoring_job

```
pause_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.PauseModelDeploymentMonitoringJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Pauses a ModelDeploymentMonitoringJob. If the job is running, the server makes a best effort to cancel the job. Will mark xref_ModelDeploymentMonitoringJob.state to 'PAUSED'.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_pause_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[PauseModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PauseModelDeploymentMonitoringJobRequest.html)(
name="name_value",
)
# Make the request
client.[pause_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_pause_model_deployment_monitoring_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.PauseModelDeploymentMonitoringJob. |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob to pause. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### persistent_resource_path

```
persistent_resource_path(
project: str, location: str, persistent_resource: str
) -> str
```


Returns a fully-qualified persistent_resource string.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### resume_model_deployment_monitoring_job

```
resume_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.ResumeModelDeploymentMonitoringJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Resumes a paused ModelDeploymentMonitoringJob. It will start to run from next scheduled time. A deleted ModelDeploymentMonitoringJob can't be resumed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_resume_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ResumeModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResumeModelDeploymentMonitoringJobRequest.html)(
name="name_value",
)
# Make the request
client.[resume_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_resume_model_deployment_monitoring_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.ResumeModelDeploymentMonitoringJob. |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob to resume. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### search_model_deployment_monitoring_stats_anomalies

```
search_model_deployment_monitoring_stats_anomalies(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
dict,
]
] = None,
*,
model_deployment_monitoring_job: typing.Optional[str] = None,
deployed_model_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesPager
)
```


Searches Model Monitoring Statistics generated within a given time window.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_search_model_deployment_monitoring_stats_anomalies():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SearchModelDeploymentMonitoringStatsAnomaliesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesRequest.html)(
model_deployment_monitoring_job="model_deployment_monitoring_job_value",
deployed_model_id="deployed_model_id_value",
)
# Make the request
page_result = client.[search_model_deployment_monitoring_stats_anomalies](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_search_model_deployment_monitoring_stats_anomalies)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.SearchModelDeploymentMonitoringStatsAnomalies. |
`model_deployment_monitoring_job` |
`str`
Required. ModelDeploymentMonitoring Job resource name. Format: |
`deployed_model_id` |
`str`
Required. The DeployedModel ID of the [ModelDeploymentMonitoringObjectiveConfig.deployed_model_id]. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.SearchModelDeploymentMonitoringStatsAnomalies. Iterating over this object will yield results and resolve additional pages automatically. |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### tensorboard_path

`tensorboard_path(project: str, location: str, tensorboard: str) -> str`


Returns a fully-qualified tensorboard string.

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### trial_path

`trial_path(project: str, location: str, study: str, trial: str) -> str`


Returns a fully-qualified trial string.

### update_model_deployment_monitoring_job

```
update_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.job_service.UpdateModelDeploymentMonitoringJobRequest,
dict,
]
] = None,
*,
model_deployment_monitoring_job: typing.Optional[
google.cloud.aiplatform_v1.types.model_deployment_monitoring_job.ModelDeploymentMonitoringJob
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Updates a ModelDeploymentMonitoringJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
model_deployment_monitoring_job = aiplatform_v1.[ModelDeploymentMonitoringJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringJob.html)()
model_deployment_monitoring_job.display_name = "display_name_value"
model_deployment_monitoring_job.endpoint = "endpoint_value"
request = aiplatform_v1.[UpdateModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateModelDeploymentMonitoringJobRequest.html)(
model_deployment_monitoring_job=model_deployment_monitoring_job,
)
# Make the request
operation = client.[update_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1_services_job_service_JobServiceClient_update_model_deployment_monitoring_job)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.UpdateModelDeploymentMonitoringJob. |
`model_deployment_monitoring_job` |
Required. The model monitoring configuration which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask is used to specify the fields to be overwritten in the ModelDeploymentMonitoringJob resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |
