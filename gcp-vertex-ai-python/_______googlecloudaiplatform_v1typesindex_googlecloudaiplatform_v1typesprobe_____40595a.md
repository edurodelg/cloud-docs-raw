---
merged_at: 2026-01-28T15:11:44.728213
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Index -->

# Class Index (1.134.0)

`Index(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Index. |
`display_name` |
`str`
Required. The display name of the Index. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Index. |
`metadata_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Index, that is specific to it. Unset if the Index does not have any additional information. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metadata` |
`google.protobuf.struct_pb2.Value`
An additional information about the Index; the schema of the metadata can be found in metadata_schema. |
`deployed_indexes` |
`MutableSequence[`
Output only. The pointers to DeployedIndexes created from this Index. An Index can be only deleted if all its DeployedIndexes had been undeployed first. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Indexes. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Index was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Index was most recently updated. This also includes any update to the contents of the Index. Note that Operations working on this Index may have their [Operations.metadata.generic_metadata.update_time] [google.cloud.aiplatform.v1.GenericOperationMetadata.update_time] a little after the value of this timestamp, yet that does not mean their results are not already reflected in the Index. Result of any successfully completed Operation on the Index is reflected in it. |
`index_stats` |
Output only. Stats of the index resource. |
`index_update_method` |
Immutable. The update method to use with this Index. If not set, BATCH_UPDATE will be used by default. |
`encryption_spec` |
Immutable. Customer-managed encryption key spec for an Index. If set, this Index and all sub-resources of this Index will be secured by this key. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### IndexUpdateMethod

`IndexUpdateMethod(value)`


The update method of an Index.

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

### Index

`Index(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Probe -->

# Class Probe (1.134.0)

`Probe(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

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
`exec_` |
ExecAction probes the health of a container by executing a command. This field is a member of `oneof` _ `probe_type` .
|
`http_get` |
HttpGetAction probes the health of a container by sending an HTTP GET request. This field is a member of `oneof` _ `probe_type` .
|
`grpc` |
GrpcAction probes the health of a container by sending a gRPC request. This field is a member of `oneof` _ `probe_type` .
|
`tcp_socket` |
TcpSocketAction probes the health of a container by opening a TCP socket connection. This field is a member of `oneof` _ `probe_type` .
|
`period_seconds` |
`int`
How often (in seconds) to perform the probe. Default to 10 seconds. Minimum value is 1. Must be less than timeout_seconds. Maps to Kubernetes probe argument 'periodSeconds'. |
`timeout_seconds` |
`int`
Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1. Must be greater or equal to period_seconds. Maps to Kubernetes probe argument 'timeoutSeconds'. |
`failure_threshold` |
`int`
Number of consecutive failures before the probe is considered failed. Defaults to 3. Minimum value is 1. Maps to Kubernetes probe argument 'failureThreshold'. |
`success_threshold` |
`int`
Number of consecutive successes before the probe is considered successful. Defaults to 1. Minimum value is 1. Maps to Kubernetes probe argument 'successThreshold'. |
`initial_delay_seconds` |
`int`
Number of seconds to wait before starting the probe. Defaults to 0. Minimum value is 0. Maps to Kubernetes probe argument 'initialDelaySeconds'. |

## Classes

### ExecAction

`ExecAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ExecAction specifies a command to execute.

### GrpcAction

`GrpcAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GrpcAction checks the health of a container using a gRPC service.

### HttpGetAction

`HttpGetAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpGetAction describes an action based on HTTP Get requests.

### HttpHeader

`HttpHeader(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpHeader describes a custom header to be used in HTTP probes

### TcpSocketAction

`TcpSocketAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TcpSocketAction probes the health of a container by opening a TCP socket connection.

## Methods

### Probe

`Probe(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardTimeSeries.Metadata -->

# Class Metadata (1.134.0)

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes metadata for a TensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`max_step` |
`int`
Output only. Max step index of all data points within a TensorboardTimeSeries. |
`max_wall_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Max wall clock timestamp of all data points within a TensorboardTimeSeries. |
`max_blob_sequence_length` |
`int`
Output only. The largest blob sequence length (number of blobs) of all data points in this time series, if its ValueType is BLOB_SEQUENCE. |

## Methods

### Metadata

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes metadata for a TensorboardTimeSeries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BigQueryDestination -->

# Class BigQueryDestination (1.134.0)

`BigQueryDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The BigQuery location for the output content.

## Attribute |
|
|---|---|
Name |
Description |
`output_uri` |
`str`
Required. BigQuery URI to a project or table, up to 2000 characters long. When only the project is specified, the Dataset and Table is created. When the full table reference is specified, the Dataset must exist and table must not exist. Accepted forms: - BigQuery path. For example: `bq://projectId` or
`bq://projectId.bqDatasetId` or
`bq://projectId.bqDatasetId.bqTableId` .
|

## Methods

### BigQueryDestination

`BigQueryDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The BigQuery location for the output content.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesMetadata -->

# Class AutoMlTablesMetadata (1.134.0)

`AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Tables.

## Attribute |
|
|---|---|
Name |
Description |
`train_cost_milli_node_hours` |
`int`
Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget. |

## Methods

### AutoMlTablesMetadata

`AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Tables.

### AutoMlTablesMetadata

`AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Tables.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardBlobDataRequest -->

# Class ReadTensorboardBlobDataRequest (1.134.0)

```
ReadTensorboardBlobDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardBlobData.

## Attributes |
|
|---|---|
Name |
Description |
`time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to list Blobs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`blob_ids` |
`MutableSequence[str]`
IDs of the blobs to read. |

## Methods

### ReadTensorboardBlobDataRequest

```
ReadTensorboardBlobDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardBlobData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Probe -->

# Class Probe (1.134.0)

`Probe(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

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
`exec_` |
ExecAction probes the health of a container by executing a command. This field is a member of `oneof` _ `probe_type` .
|
`http_get` |
HttpGetAction probes the health of a container by sending an HTTP GET request. This field is a member of `oneof` _ `probe_type` .
|
`grpc` |
GrpcAction probes the health of a container by sending a gRPC request. This field is a member of `oneof` _ `probe_type` .
|
`tcp_socket` |
TcpSocketAction probes the health of a container by opening a TCP socket connection. This field is a member of `oneof` _ `probe_type` .
|
`period_seconds` |
`int`
How often (in seconds) to perform the probe. Default to 10 seconds. Minimum value is 1. Must be less than timeout_seconds. Maps to Kubernetes probe argument 'periodSeconds'. |
`timeout_seconds` |
`int`
Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1. Must be greater or equal to period_seconds. Maps to Kubernetes probe argument 'timeoutSeconds'. |
`failure_threshold` |
`int`
Number of consecutive failures before the probe is considered failed. Defaults to 3. Minimum value is 1. Maps to Kubernetes probe argument 'failureThreshold'. |
`success_threshold` |
`int`
Number of consecutive successes before the probe is considered successful. Defaults to 1. Minimum value is 1. Maps to Kubernetes probe argument 'successThreshold'. |
`initial_delay_seconds` |
`int`
Number of seconds to wait before starting the probe. Defaults to 0. Minimum value is 0. Maps to Kubernetes probe argument 'initialDelaySeconds'. |

## Classes

### ExecAction

`ExecAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ExecAction specifies a command to execute.

### GrpcAction

`GrpcAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GrpcAction checks the health of a container using a gRPC service.

### HttpGetAction

`HttpGetAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpGetAction describes an action based on HTTP Get requests.

### HttpHeader

`HttpHeader(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpHeader describes a custom header to be used in HTTP probes

### TcpSocketAction

`TcpSocketAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TcpSocketAction probes the health of a container by opening a TCP socket connection.

## Methods

### Probe

`Probe(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesRequest -->

# Class ListTrainingPipelinesRequest (1.134.0)

```
ListTrainingPipelinesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.ListTrainingPipelines.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the TrainingPipelines from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `training_task_definition` `=` , `!=` comparisons,
and `:` wildcard.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="PIPELINE_STATE_SUCCEEDED" AND display_name:"my_pipeline_*"`
- `state!="PIPELINE_STATE_FAILED" OR display_name="my_pipeline"`
- `NOT display_name="my_pipeline"`
- `create_time>"2021-05-18T00:00:00Z"`
- `training_task_definition:"*automl_text_classification*"`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListTrainingPipelinesResponse.next_page_token of the previous PipelineService.ListTrainingPipelines call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListTrainingPipelinesRequest

```
ListTrainingPipelinesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.ListTrainingPipelines.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeContextsResponse -->

# Class PurgeContextsResponse (1.134.0)

`PurgeContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeContexts.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Contexts that this request deleted (or, if `force` is false, the number of Contexts that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Context names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeContextsResponse

`PurgeContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeContexts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TimeSeriesForecastingPredictionResult -->

# Class TimeSeriesForecastingPredictionResult (1.134.0)

```
TimeSeriesForecastingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Time Series Forecasting.

## Attribute |
|
|---|---|
Name |
Description |
`value` |
`float`
The regression value. |

## Methods

### TimeSeriesForecastingPredictionResult

```
TimeSeriesForecastingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Time Series Forecasting.

### TimeSeriesForecastingPredictionResult

```
TimeSeriesForecastingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Time Series Forecasting.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexEndpoint -->

# Class IndexEndpoint (1.134.0)

`IndexEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the IndexEndpoint. |
`display_name` |
`str`
Required. The display name of the IndexEndpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the IndexEndpoint. |
`deployed_indexes` |
`MutableSequence[`
Output only. The indexes deployed in this endpoint. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your IndexEndpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this IndexEndpoint was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this IndexEndpoint was last updated. This timestamp is not updated when the endpoint's DeployedIndexes are updated, e.g. due to updates of the original Indexes they are the deployments of. |
`network` |
`str`
Optional. The full name of the Google Compute Engine `network ` __
to which the IndexEndpoint should be peered.
Private services access must already be configured for the
network. If left unspecified, the Endpoint is not peered
with any network.
network
and
private_service_connect_config
are mutually exclusive.
`Format ` __:
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in '12345', and {network}
is network name.
|
`enable_private_service_connect` |
`bool`
Optional. Deprecated: If true, expose the IndexEndpoint via private service connect. Only one of the fields, network or enable_private_service_connect, can be set. |
`private_service_connect_config` |
Optional. Configuration for private service connect. network and private_service_connect_config are mutually exclusive. |
`public_endpoint_enabled` |
`bool`
Optional. If true, the deployed index will be accessible through public endpoint. |
`public_endpoint_domain_name` |
`str`
Output only. If public_endpoint_enabled is true, this field will be populated with the domain name to use for this index endpoint. |
`encryption_spec` |
Immutable. Customer-managed encryption key spec for an IndexEndpoint. If set, this IndexEndpoint and all sub-resources of this IndexEndpoint will be secured by this key. |
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

### IndexEndpoint

`IndexEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Index -->

# Class Index (1.134.0)

`Index(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Index. |
`display_name` |
`str`
Required. The display name of the Index. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Index. |
`metadata_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Index, that is specific to it. Unset if the Index does not have any additional information. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metadata` |
`google.protobuf.struct_pb2.Value`
An additional information about the Index; the schema of the metadata can be found in metadata_schema. |
`deployed_indexes` |
`MutableSequence[`
Output only. The pointers to DeployedIndexes created from this Index. An Index can be only deleted if all its DeployedIndexes had been undeployed first. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Indexes. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Index was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Index was most recently updated. This also includes any update to the contents of the Index. Note that Operations working on this Index may have their [Operations.metadata.generic_metadata.update_time] [google.cloud.aiplatform.v1beta1.GenericOperationMetadata.update_time] a little after the value of this timestamp, yet that does not mean their results are not already reflected in the Index. Result of any successfully completed Operation on the Index is reflected in it. |
`index_stats` |
Output only. Stats of the index resource. |
`index_update_method` |
Immutable. The update method to use with this Index. If not set, BATCH_UPDATE will be used by default. |
`encryption_spec` |
Immutable. Customer-managed encryption key spec for an Index. If set, this Index and all sub-resources of this Index will be secured by this key. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### IndexUpdateMethod

`IndexUpdateMethod(value)`


The update method of an Index.

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

### Index

`Index(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetVersionRequest -->

# Class CreateDatasetVersionRequest (1.134.0)

`CreateDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.CreateDatasetVersion.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the Dataset resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`dataset_version` |
Required. The version to be created. The same CMEK policies with the original Dataset will be applied the dataset version. So here we don't need to specify the EncryptionSpecType here. |

## Methods

### CreateDatasetVersionRequest

`CreateDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.CreateDatasetVersion.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsRequest -->

# Class ListNasTrialDetailsRequest (1.134.0)

`ListNasTrialDetailsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListNasTrialDetails.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the NasJob resource. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListNasTrialDetailsResponse.next_page_token of the previous JobService.ListNasTrialDetails call. |

## Methods

### ListNasTrialDetailsRequest

`ListNasTrialDetailsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListNasTrialDetails.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJobSpec.MultiTrialAlgorithmSpec.TrainTrialSpec -->

# Class TrainTrialSpec (1.134.0)

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.

## Attributes |
|
|---|---|
Name |
Description |
`train_trial_job_spec` |
Required. The spec of a train trial job. The same spec applies to all train trials. |
`max_parallel_trial_count` |
`int`
Required. The maximum number of trials to run in parallel. |
`frequency` |
`int`
Required. Frequency of search trials to start train stage. Top N [TrainTrialSpec.max_parallel_trial_count] search trials will be trained for every M [TrainTrialSpec.frequency] trials searched. |

## Methods

### TrainTrialSpec

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesRequest.EntityTypeSpec -->

# Class EntityTypeSpec (1.134.0)

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type_id` |
`str`
Required. ID of the EntityType to select Features. The EntityType id is the entity_type_id specified during EntityType creation. |
`feature_selector` |
Required. Selectors choosing which Feature values to read from the EntityType. |
`settings` |
`MutableSequence[`
Per-Feature settings for the batch read. |

## Methods

### EntityTypeSpec

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexEndpoint -->

# Class IndexEndpoint (1.134.0)

`IndexEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the IndexEndpoint. |
`display_name` |
`str`
Required. The display name of the IndexEndpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the IndexEndpoint. |
`deployed_indexes` |
`MutableSequence[`
Output only. The indexes deployed in this endpoint. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your IndexEndpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this IndexEndpoint was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this IndexEndpoint was last updated. This timestamp is not updated when the endpoint's DeployedIndexes are updated, e.g. due to updates of the original Indexes they are the deployments of. |
`network` |
`str`
Optional. The full name of the Google Compute Engine `network ` __
to which the IndexEndpoint should be peered.
Private services access must already be configured for the
network. If left unspecified, the Endpoint is not peered
with any network.
network
and
private_service_connect_config
are mutually exclusive.
`Format ` __:
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in '12345', and {network}
is network name.
|
`enable_private_service_connect` |
`bool`
Optional. Deprecated: If true, expose the IndexEndpoint via private service connect. Only one of the fields, network or enable_private_service_connect, can be set. |
`private_service_connect_config` |
Optional. Configuration for private service connect. network and private_service_connect_config are mutually exclusive. |
`public_endpoint_enabled` |
`bool`
Optional. If true, the deployed index will be accessible through public endpoint. |
`public_endpoint_domain_name` |
`str`
Output only. If public_endpoint_enabled is true, this field will be populated with the domain name to use for this index endpoint. |
`encryption_spec` |
Immutable. Customer-managed encryption key spec for an IndexEndpoint. If set, this IndexEndpoint and all sub-resources of this IndexEndpoint will be secured by this key. |
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

### IndexEndpoint

`IndexEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.migration_service.pagers`

module.

## Classes

[SearchMigratableResourcesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.pagers.SearchMigratableResourcesAsyncPager)

```
SearchMigratableResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
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


A pager for iterating through `search_migratable_resources`

requests.

This class thinly wraps an initial
[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse) object, and
provides an `__aiter__`

method to iterate through its
`migratable_resources`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchMigratableResources`

requests and continue to iterate
through the `migratable_resources`

field on the
corresponding responses.

All the usual [SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchMigratableResourcesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.pagers.SearchMigratableResourcesPager)

```
SearchMigratableResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
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


A pager for iterating through `search_migratable_resources`

requests.

This class thinly wraps an initial
[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse) object, and
provides an `__iter__`

method to iterate through its
`migratable_resources`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchMigratableResources`

requests and continue to iterate
through the `migratable_resources`

field on the
corresponding responses.

All the usual [SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesRequest -->

# Class ListTrainingPipelinesRequest (1.134.0)

```
ListTrainingPipelinesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.ListTrainingPipelines.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the TrainingPipelines from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `training_task_definition` `=` , `!=` comparisons,
and `:` wildcard.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="PIPELINE_STATE_SUCCEEDED" AND display_name:"my_pipeline_*"`
- `state!="PIPELINE_STATE_FAILED" OR display_name="my_pipeline"`
- `NOT display_name="my_pipeline"`
- `create_time>"2021-05-18T00:00:00Z"`
- `training_task_definition:"*automl_text_classification*"`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListTrainingPipelinesResponse.next_page_token of the previous PipelineService.ListTrainingPipelines call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListTrainingPipelinesRequest

```
ListTrainingPipelinesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.ListTrainingPipelines.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DedicatedResources.ScaleToZeroSpec -->

# Class ScaleToZeroSpec (1.134.0)

`ScaleToZeroSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for scale-to-zero feature.

## Attributes |
|
|---|---|
Name |
Description |
`min_scaleup_period` |
`google.protobuf.duration_pb2.Duration`
Optional. Minimum duration that a deployment will be scaled up before traffic is evaluated for potential scale-down. [MinValue=300] (5 minutes) [MaxValue=28800] (8 hours) |
`idle_scaledown_period` |
`google.protobuf.duration_pb2.Duration`
Optional. Duration of no traffic before scaling to zero. [MinValue=300] (5 minutes) [MaxValue=28800] (8 hours) |

## Methods

### ScaleToZeroSpec

`ScaleToZeroSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for scale-to-zero feature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FunctionCallingConfig.Mode -->

# Class Mode (1.134.0)

`Mode(value)`


Function calling mode.

## Enums |
|
|---|---|
Name |
Description |
`MODE_UNSPECIFIED` |
Unspecified function calling mode. This value should not be used. |
`AUTO` |
Default model behavior, model decides to predict either function calls or natural language response. |
`ANY` |
Model is constrained to always predicting function calls only. If "allowed_function_names" are set, the predicted function calls will be limited to any one of "allowed_function_names", else the predicted function calls will be any one of the provided "function_declarations". |
`NONE` |
Model will not predict any function calls. Model behavior is same as when not passing any function declarations. |

## Methods

### Mode

`Mode(value)`


Function calling mode.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsRequest -->

# Class ListModelsRequest (1.134.0)

`ListModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModels.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the Models from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `model` supports = and !=. `model` represents the
Model ID, i.e. the last segment of the Model's [resource
name][google.cloud.aiplatform.v1.Model.name].
- `display_name` supports = and !=
- `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- \`labels.key:\* or labels:key - key existence
- A key including a space must be quoted.
`labels."a key"` .
- `base_model_name` only supports =
Some examples:
- `model=1234`
- `displayName="myDisplayName"`
- `labels.myKey="myValue"`
- `baseModelName="text-bison"`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListModelsResponse.next_page_token of the previous ModelService.ListModels call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
Example: `display_name, create_time desc` .
|

## Methods

### ListModelsRequest

`ListModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModels.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardBlobDataRequest -->

# Class ReadTensorboardBlobDataRequest (1.134.0)

```
ReadTensorboardBlobDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardBlobData.

## Attributes |
|
|---|---|
Name |
Description |
`time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to list Blobs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`blob_ids` |
`MutableSequence[str]`
IDs of the blobs to read. |

## Methods

### ReadTensorboardBlobDataRequest

```
ReadTensorboardBlobDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardBlobData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresRequest -->

# Class ListExampleStoresRequest (1.134.0)

`ListExampleStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.ListExampleStores.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the ExampleStores from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. The standard list filter. More detail in `AIP-160 ` __.
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |

## Methods

### ListExampleStoresRequest

`ListExampleStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.ListExampleStores.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeArtifactsResponse -->

# Class PurgeArtifactsResponse (1.134.0)

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Artifacts that this request deleted (or, if `force` is false, the number of Artifacts that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Artifact names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeArtifactsResponse

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpeculativeDecodingSpec.NgramSpeculation -->

# Class NgramSpeculation (1.134.0)

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

## Attribute |
|
|---|---|
Name |
Description |
`ngram_size` |
`int`
The number of last N input tokens used as ngram to search/match against the previous prompt sequence. This is equal to the N in N-Gram. The default value is 3 if not specified. |

## Methods

### NgramSpeculation

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataResponse -->

# Class ExportTensorboardTimeSeriesDataResponse (1.134.0)

```
ExportTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ExportTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`time_series_data_points` |
`MutableSequence[`
The returned time series data points. |
`next_page_token` |
`str`
A token, which can be sent as page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ExportTensorboardTimeSeriesDataResponse

```
ExportTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ExportTensorboardTimeSeriesData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service -->

# Package index_endpoint_service (1.134.0)

API documentation for `aiplatform_v1.services.index_endpoint_service`

package.

## Classes

[IndexEndpointServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceAsyncClient)

A service for managing Vertex AI's IndexEndpoints.

[IndexEndpointServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient)

A service for managing Vertex AI's IndexEndpoints.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.pagers)

API documentation for `aiplatform_v1.services.index_endpoint_service.pagers`

module.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureRequest -->

# Class GetFeatureRequest (1.134.0)

`GetFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetFeature. Request message for FeatureRegistryService.GetFeature.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Feature resource. Format for entity_type as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
Format for feature_group as parent:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|

## Methods

### GetFeatureRequest

`GetFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetFeature. Request message for FeatureRegistryService.GetFeature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobSpec.MultiTrialAlgorithmSpec.TrainTrialSpec -->

# Class TrainTrialSpec (1.134.0)

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.

## Attributes |
|
|---|---|
Name |
Description |
`train_trial_job_spec` |
Required. The spec of a train trial job. The same spec applies to all train trials. |
`max_parallel_trial_count` |
`int`
Required. The maximum number of trials to run in parallel. |
`frequency` |
`int`
Required. Frequency of search trials to start train stage. Top N [TrainTrialSpec.max_parallel_trial_count] search trials will be trained for every M [TrainTrialSpec.frequency] trials searched. |

## Methods

### TrainTrialSpec

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchMigrateResourcesOperationMetadata.PartialResult -->

# Class PartialResult (1.134.0)

`PartialResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a partial result in batch migration operation for one MigrateResourceRequest.

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
`error` |
`google.rpc.status_pb2.Status`
The error result of the migration request in case of failure. This field is a member of `oneof` _ `result` .
|
`model` |
`str`
Migrated model resource name. This field is a member of `oneof` _ `result` .
|
`dataset` |
`str`
Migrated dataset resource name. This field is a member of `oneof` _ `result` .
|
`request` |
It's the same as the value in BatchMigrateResourcesRequest.migrate_resource_requests. |

## Methods

### PartialResult

`PartialResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a partial result in batch migration operation for one MigrateResourceRequest.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tool -->

# Class Tool (1.134.0)

`Tool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool details that the model may use to generate response.

A `Tool`

is a piece of code that enables the system to interact
with external systems to perform an action, or set of actions,
outside of knowledge and scope of the model. A Tool object should
contain exactly one type of Tool (e.g FunctionDeclaration, Retrieval
or GoogleSearchRetrieval).

## Attributes |
|
|---|---|
Name |
Description |
`function_declarations` |
`MutableSequence[`
Optional. Function tool type. One or more function declarations to be passed to the model along with the current user query. Model may decide to call a subset of these functions by populating FunctionCall in the response. User should provide a FunctionResponse for each function call in the next turn. Based on the function responses, Model will generate the final response back to the user. Maximum 128 function declarations can be provided. |
`retrieval` |
Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation. |
`google_search` |
Optional. GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google. |
`google_search_retrieval` |
Optional. GoogleSearchRetrieval tool type. Specialized retrieval tool that is powered by Google search. |
`google_maps` |
Optional. GoogleMaps tool type. Tool to support Google Maps in Model. |
`enterprise_web_search` |
Optional. Tool to support searching public web data, powered by Vertex AI Search and Sec4 compliance. |
`code_execution` |
Optional. CodeExecution tool type. Enables the model to execute code as part of generation. |
`url_context` |
Optional. Tool to support URL context retrieval. |
`computer_use` |
Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations. |

## Classes

### CodeExecution

`CodeExecution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool that executes code generated by the model, and automatically returns the result to the model.

See also [ExecutableCode]and [CodeExecutionResult] which are input and output to this tool.

### ComputerUse

`ComputerUse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support computer use.

### GoogleSearch

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### PhishBlockThreshold

`PhishBlockThreshold(value)`


These are available confidence level user can set to block
malicious urls with chosen confidence and above. For
understanding different confidence of webrisk, please refer to
[https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel](https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel)

## Methods

### Tool

`Tool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool details that the model may use to generate response.

A `Tool`

is a piece of code that enables the system to interact
with external systems to perform an action, or set of actions,
outside of knowledge and scope of the model. A Tool object should
contain exactly one type of Tool (e.g FunctionDeclaration, Retrieval
or GoogleSearchRetrieval).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplainResponse -->

# Class ExplainResponse (1.134.0)

`ExplainResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Explain.

## Attributes |
|
|---|---|
Name |
Description |
`explanations` |
`MutableSequence[`
The explanations of the Model's PredictResponse.predictions. It has the same number of elements as instances to be explained. |
`deployed_model_id` |
`str`
ID of the Endpoint's DeployedModel that served this explanation. |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
The predictions that are the output of the predictions call. Same as PredictResponse.predictions. |

## Methods

### ExplainResponse

`ExplainResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Explain.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse -->

# Class ListTensorboardTimeSeriesResponse (1.134.0)

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`MutableSequence[`
The TensorboardTimeSeries mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardTimeSeriesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardTimeSeriesResponse

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesOperationMetadata.PartialResult -->

# Class PartialResult (1.134.0)

`PartialResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a partial result in batch migration operation for one MigrateResourceRequest.

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
`error` |
`google.rpc.status_pb2.Status`
The error result of the migration request in case of failure. This field is a member of `oneof` _ `result` .
|
`model` |
`str`
Migrated model resource name. This field is a member of `oneof` _ `result` .
|
`dataset` |
`str`
Migrated dataset resource name. This field is a member of `oneof` _ `result` .
|
`request` |
It's the same as the value in [MigrateResourceRequest.migrate_resource_requests][]. |

## Methods

### PartialResult

`PartialResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a partial result in batch migration operation for one MigrateResourceRequest.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient -->

# Class PipelineServiceClient (1.134.0)

```
PipelineServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's pipelines. This
includes both `TrainingPipeline`

resources (used for AutoML and
custom training) and `PipelineJob`

resources (used for Vertex AI
Pipelines).

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
`PipelineServiceTransport` |
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

### PipelineServiceClient

```
PipelineServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the pipeline service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PipelineServiceTransport,Callable[..., PipelineServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the PipelineServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### artifact_path

```
artifact_path(
project: str, location: str, metadata_store: str, artifact: str
) -> str
```


Returns a fully-qualified artifact string.

### batch_cancel_pipeline_jobs

```
batch_cancel_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.BatchCancelPipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch cancel PipelineJobs. Firstly the server will check if all the jobs are in non-terminal states, and skip the jobs that are already terminated. If the operation failed, none of the pipeline jobs are cancelled. The server will poll the states of all the pipeline jobs periodically to check the cancellation status. This operation will return an LRO.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_cancel_pipeline_jobs():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[BatchCancelPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCancelPipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_cancel_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_batch_cancel_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchCancelPipelineJobs. |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: |
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

### batch_delete_pipeline_jobs

```
batch_delete_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.BatchDeletePipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch deletes PipelineJobs The Operation is atomic. If it fails, none of the PipelineJobs are deleted. If it succeeds, all of the PipelineJobs are deleted.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_delete_pipeline_jobs():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[BatchDeletePipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchDeletePipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_delete_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_batch_delete_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchDeletePipelineJobs. |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: |
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

### cancel_pipeline_job

```
cancel_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.CancelPipelineJobRequest,
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


Cancels a PipelineJob. Starts asynchronous cancellation on the
PipelineJob. The server makes a best effort to cancel the
pipeline, but success is not guaranteed. Clients can use
xref_PipelineService.GetPipelineJob
or other methods to check whether the cancellation succeeded or
whether the pipeline completed despite cancellation. On
successful cancellation, the PipelineJob is not deleted; instead
it becomes a pipeline with a
xref_PipelineJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_PipelineJob.state
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
def sample_cancel_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelPipelineJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_cancel_pipeline_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CancelPipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_training_pipeline

```
cancel_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.CancelTrainingPipelineRequest,
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


Cancels a TrainingPipeline. Starts asynchronous cancellation on
the TrainingPipeline. The server makes a best effort to cancel
the pipeline, but success is not guaranteed. Clients can use
xref_PipelineService.GetTrainingPipeline
or other methods to check whether the cancellation succeeded or
whether the pipeline completed despite cancellation. On
successful cancellation, the TrainingPipeline is not deleted;
instead it becomes a pipeline with a
xref_TrainingPipeline.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_TrainingPipeline.state
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
def sample_cancel_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_cancel_training_pipeline)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CancelTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline to cancel. Format: |
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

### create_pipeline_job

```
create_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.CreatePipelineJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
pipeline_job: typing.Optional[
google.cloud.aiplatform_v1.types.pipeline_job.PipelineJob
] = None,
pipeline_job_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.pipeline_job.PipelineJob
```


Creates a PipelineJob. A PipelineJob will run immediately when created.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreatePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreatePipelineJobRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_create_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CreatePipelineJob. |
`parent` |
`str`
Required. The resource name of the Location to create the PipelineJob in. Format: |
`pipeline_job` |
Required. The PipelineJob to create. This corresponds to the |
`pipeline_job_id` |
`str`
The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated. This value should be less than 128 characters, and valid characters are |
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
An instance of a machine learning PipelineJob. |

### create_training_pipeline

```
create_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.CreateTrainingPipelineRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
training_pipeline: typing.Optional[
google.cloud.aiplatform_v1.types.training_pipeline.TrainingPipeline
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.training_pipeline.TrainingPipeline
```


Creates a TrainingPipeline. A created TrainingPipeline right away will be attempted to be run.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
training_pipeline = aiplatform_v1.[TrainingPipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TrainingPipeline.html)()
training_pipeline.display_name = "display_name_value"
training_pipeline.training_task_definition = "training_task_definition_value"
training_pipeline.training_task_inputs.null_value = "NULL_VALUE"
request = aiplatform_v1.[CreateTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTrainingPipelineRequest.html)(
parent="parent_value",
training_pipeline=training_pipeline,
)
# Make the request
response = client.[create_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_create_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CreateTrainingPipeline. |
`parent` |
`str`
Required. The resource name of the Location to create the TrainingPipeline in. Format: |
`training_pipeline` |
Required. The TrainingPipeline to create. This corresponds to the |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

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

### delete_pipeline_job

```
delete_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.DeletePipelineJobRequest,
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


Deletes a PipelineJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeletePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeletePipelineJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_delete_pipeline_job)(request=request)
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
The request object. Request message for PipelineService.DeletePipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob resource to be deleted. Format: |
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

### delete_training_pipeline

```
delete_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.DeleteTrainingPipelineRequest,
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


Deletes a TrainingPipeline.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_delete_training_pipeline)(request=request)
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
The request object. Request message for PipelineService.DeleteTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline resource to be deleted. Format: |
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

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### execution_path

```
execution_path(
project: str, location: str, metadata_store: str, execution: str
) -> str
```


Returns a fully-qualified execution string.

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
`PipelineServiceClient` |
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
`PipelineServiceClient` |
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
`PipelineServiceClient` |
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

### get_pipeline_job

```
get_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.GetPipelineJobRequest,
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
) -> google.cloud.aiplatform_v1.types.pipeline_job.PipelineJob
```


Gets a PipelineJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetPipelineJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_get_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.GetPipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob resource. Format: |
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
An instance of a machine learning PipelineJob. |

### get_training_pipeline

```
get_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.GetTrainingPipelineRequest,
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
) -> google.cloud.aiplatform_v1.types.training_pipeline.TrainingPipeline
```


Gets a TrainingPipeline.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_get_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.GetTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline resource. Format: |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

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

### list_pipeline_jobs

```
list_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsRequest,
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
) -> google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListPipelineJobsPager
```


Lists PipelineJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_pipeline_jobs():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_list_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.ListPipelineJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the PipelineJobs from. Format: |
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
Response message for PipelineService.ListPipelineJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_training_pipelines

```
list_training_pipelines(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesRequest,
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
google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListTrainingPipelinesPager
)
```


Lists TrainingPipelines in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_training_pipelines():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTrainingPipelinesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_training_pipelines](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_list_training_pipelines)(request=request)
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
The request object. Request message for PipelineService.ListTrainingPipelines. |
`parent` |
`str`
Required. The resource name of the Location to list the TrainingPipelines from. Format: |
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
Response message for PipelineService.ListTrainingPipelines Iterating over this object will yield results and resolve additional pages automatically. |

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### parse_artifact_path

`parse_artifact_path(path: str) -> typing.Dict[str, str]`


Parses a artifact path into its component segments.

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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_training_pipeline_path

`parse_training_pipeline_path(path: str) -> typing.Dict[str, str]`


Parses a training_pipeline path into its component segments.

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

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

### training_pipeline_path

`training_pipeline_path(project: str, location: str, training_pipeline: str) -> str`


Returns a fully-qualified training_pipeline string.

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient -->

# Class VertexRagDataServiceAsyncClient (1.134.0)

```
VertexRagDataServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing user data for RAG.

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
`VertexRagDataServiceTransport` |
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

### VertexRagDataServiceAsyncClient

```
VertexRagDataServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag data service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagDataServiceTransport,Callable[..., VertexRagDataServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagDataServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_rag_corpus

```
create_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.CreateRagCorpusRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
rag_corpus: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
] = None,
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


Creates a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_corpus = aiplatform_v1beta1.[RagCorpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.html)()
rag_corpus.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateRagCorpusRequest.html)(
parent="parent_value",
rag_corpus=rag_corpus,
)
# Make the request
operation = client.[create_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_create_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.CreateRagCorpus. |
`parent` |
Required. The resource name of the Location to create the RagCorpus in. Format: |
`rag_corpus` |
Required. The RagCorpus to create. This corresponds to the |
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
An object representing a long-running operation. The result type for the operation will be
|

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

### delete_rag_corpus

```
delete_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.DeleteRagCorpusRequest,
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
) -> google.api_core.operation_async.AsyncOperation
```


Deletes a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagCorpusRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_delete_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.DeleteRagCorpus. |
`name` |
Required. The name of the RagCorpus resource to be deleted. Format: |
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
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_rag_file

```
delete_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.DeleteRagFileRequest,
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
) -> google.api_core.operation_async.AsyncOperation
```


Deletes a RagFile.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagFileRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_delete_rag_file)(request=request)
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
The request object. Request message for VertexRagDataService.DeleteRagFile. |
`name` |
Required. The name of the RagFile resource to be deleted. Format: |
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
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

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
`VertexRagDataServiceAsyncClient` |
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
`VertexRagDataServiceAsyncClient` |
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
`VertexRagDataServiceAsyncClient` |
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

### get_rag_corpus

```
get_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagCorpusRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
```


Gets a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagCorpusRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_corpus)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagCorpus |
`name` |
Required. The name of the RagCorpus resource. Format: |
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
A RagCorpus is a RagFile container and a project can have multiple RagCorpora. |

### get_rag_engine_config

```
get_rag_engine_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagEngineConfigRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagEngineConfig
```


Gets a RagEngineConfig.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_rag_engine_config():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagEngineConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagEngineConfigRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_engine_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_engine_config)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagEngineConfig |
`name` |
Required. The name of the RagEngineConfig resource. Format: |
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
Config for RagEngine. |

### get_rag_file

```
get_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagFileRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagFile
```


Gets a RagFile.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagFileRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_file)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagFile |
`name` |
Required. The name of the RagFile resource. Format: |
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
A RagFile contains user data for chunking, embedding and indexing. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport
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

### import_rag_files

```
import_rag_files(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ImportRagFilesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
import_rag_files_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.ImportRagFilesConfig
] = None,
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


Import files from Google Cloud Storage or Google Drive into a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_import_rag_files():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
import_rag_files_config = aiplatform_v1beta1.[ImportRagFilesConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesConfig.html)()
import_rag_files_config.gcs_source.uris = ['uris_value1', 'uris_value2']
import_rag_files_config.partial_failure_gcs_sink.output_uri_prefix = "output_uri_prefix_value"
import_rag_files_config.import_result_gcs_sink.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[ImportRagFilesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesRequest.html)(
parent="parent_value",
import_rag_files_config=import_rag_files_config,
)
# Make the request
operation = client.[import_rag_files](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_import_rag_files)(request=request)
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
The request object. Request message for VertexRagDataService.ImportRagFiles. |
`parent` |
Required. The name of the RagCorpus resource into which to import files. Format: |
`import_rag_files_config` |
Required. The config for the RagFiles to be synced and imported into the RagCorpus. VertexRagDataService.ImportRagFiles. This corresponds to the |
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
An object representing a long-running operation. The result type for the operation will be
|

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

### list_rag_corpora

```
list_rag_corpora(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaRequest,
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
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager
)
```


Lists RagCorpora in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_rag_corpora():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListRagCorporaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_rag_corpora](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_list_rag_corpora)(request=request)
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
The request object. Request message for VertexRagDataService.ListRagCorpora. |
`parent` |
Required. The resource name of the Location from which to list the RagCorpora. Format: |
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
Response message for VertexRagDataService.ListRagCorpora. Iterating over this object will yield results and resolve additional pages automatically. |

### list_rag_files

```
list_rag_files(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesRequest,
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
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagFilesAsyncPager
)
```


Lists RagFiles in a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_rag_files():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListRagFilesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_rag_files](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_list_rag_files)(request=request)
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
The request object. Request message for VertexRagDataService.ListRagFiles. |
`parent` |
Required. The resource name of the RagCorpus from which to list the RagFiles. Format: |
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
Response message for VertexRagDataService.ListRagFiles. Iterating over this object will yield results and resolve additional pages automatically. |

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### parse_rag_engine_config_path

`parse_rag_engine_config_path(path: str) -> typing.Dict[str, str]`


Parses a rag_engine_config path into its component segments.

### parse_rag_file_path

`parse_rag_file_path(path: str) -> typing.Dict[str, str]`


Parses a rag_file path into its component segments.

### parse_secret_version_path

`parse_secret_version_path(path: str) -> typing.Dict[str, str]`


Parses a secret_version path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### rag_engine_config_path

`rag_engine_config_path(project: str, location: str) -> str`


Returns a fully-qualified rag_engine_config string.

### rag_file_path

`rag_file_path(project: str, location: str, rag_corpus: str, rag_file: str) -> str`


Returns a fully-qualified rag_file string.

### secret_version_path

`secret_version_path(project: str, secret: str, secret_version: str) -> str`


Returns a fully-qualified secret_version string.

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

### update_rag_corpus

```
update_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UpdateRagCorpusRequest,
dict,
]
] = None,
*,
rag_corpus: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
] = None,
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


Updates a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_corpus = aiplatform_v1beta1.[RagCorpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.html)()
rag_corpus.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagCorpusRequest.html)(
rag_corpus=rag_corpus,
)
# Make the request
operation = client.[update_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_update_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.UpdateRagCorpus. |
`rag_corpus` |
Required. The RagCorpus which replaces the resource on the server. This corresponds to the |
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
An object representing a long-running operation. The result type for the operation will be
|

### update_rag_engine_config

```
update_rag_engine_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UpdateRagEngineConfigRequest,
dict,
]
] = None,
*,
rag_engine_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagEngineConfig
] = None,
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


Updates a RagEngineConfig.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_rag_engine_config():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateRagEngineConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagEngineConfigRequest.html)(
)
# Make the request
operation = client.[update_rag_engine_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_update_rag_engine_config)(request=request)
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
The request object. Request message for VertexRagDataService.UpdateRagEngineConfig. |
`rag_engine_config` |
Required. The updated RagEngineConfig. NOTE: Downgrading your RagManagedDb's ComputeTier could temporarily increase request latencies until the operation is fully complete. This corresponds to the |
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
An object representing a long-running operation. The result type for the operation will be
|

### upload_rag_file

```
upload_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UploadRagFileRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
rag_file: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagFile
] = None,
upload_rag_file_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.UploadRagFileConfig
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UploadRagFileResponse
)
```


Upload a file into a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_upload_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_file = aiplatform_v1beta1.[RagFile](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFile.html)()
rag_file.gcs_source.uris = ['uris_value1', 'uris_value2']
rag_file.display_name = "display_name_value"
request = aiplatform_v1beta1.[UploadRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadRagFileRequest.html)(
parent="parent_value",
rag_file=rag_file,
)
# Make the request
response = await client.[upload_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_upload_rag_file)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.UploadRagFile. |
`parent` |
Required. The name of the RagCorpus resource into which to upload the file. Format: |
`rag_file` |
Required. The RagFile to upload. This corresponds to the |
`upload_rag_file_config` |
Required. The config for the RagFiles to be uploaded into the RagCorpus. VertexRagDataService.UploadRagFile. This corresponds to the |
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
Response message for VertexRagDataService.UploadRagFile. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookExecutionJobsRequest -->

# Class ListNotebookExecutionJobsRequest (1.134.0)

```
ListNotebookExecutionJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.ListNotebookExecutionJobs]

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `notebookExecutionJob` supports = and !=.
`notebookExecutionJob` represents the
NotebookExecutionJob ID.
- `displayName` supports = and != and regex.
- `schedule` supports = and != and regex.
Some examples:
- `notebookExecutionJob="123"`
- `notebookExecutionJob="my-execution-job"`
- `displayName="myDisplayName"` and
`displayName=` "myDisplayNameRegex"`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListNotebookExecutionJobsResponse.next_page_token of the previous NotebookService.ListNotebookExecutionJobs call. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
Example: `display_name, create_time desc` .
|
`view` |
Optional. The NotebookExecutionJob view. Defaults to BASIC. |

## Methods

### ListNotebookExecutionJobsRequest

```
ListNotebookExecutionJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.ListNotebookExecutionJobs]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesResponse.SelectEntity -->

# Class SelectEntity (1.134.0)

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.

## Attributes |
|
|---|---|
Name |
Description |
`offline_storage_deleted_entity_row_count` |
`int`
The count of deleted entity rows in the offline storage. Each row corresponds to the combination of an entity ID and a timestamp. One entity ID can have multiple rows in the offline storage. |
`online_storage_deleted_entity_count` |
`int`
The count of deleted entities in the online storage. Each entity ID corresponds to one entity. |

## Methods

### SelectEntity

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassification -->

# Class AutoMlImageClassification (1.134.0)

`AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

## Attributes |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |
`metadata` |
The metadata information. |

## Methods

### AutoMlImageClassification

`AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

### AutoMlImageClassification

`AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesRequest.EntityTypeSpec -->

# Class EntityTypeSpec (1.134.0)

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type_id` |
`str`
Required. ID of the EntityType to select Features. The EntityType id is the entity_type_id specified during EntityType creation. |
`feature_selector` |
Required. Selectors choosing which Feature values to read from the EntityType. |
`settings` |
`MutableSequence[`
Per-Feature settings for the batch read. |

## Methods

### EntityTypeSpec

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedIndexAuthConfig -->

# Class DeployedIndexAuthConfig (1.134.0)

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.

## Attribute |
|
|---|---|
Name |
Description |
`auth_provider` |
Defines the authentication provider that the DeployedIndex uses. |

## Classes

### AuthProvider

`AuthProvider(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for an authentication provider, including support for
```
JSON Web Token
(JWT) <https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32>
```

__.

## Methods

### DeployedIndexAuthConfig

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service -->

# Package memory_bank_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.memory_bank_service`

package.

## Classes

[MemoryBankServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient)

A service for managing memories for LLM applications.

[MemoryBankServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient)

A service for managing memories for LLM applications.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers)

API documentation for `aiplatform_v1beta1.services.memory_bank_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RougeSpec -->

# Class RougeSpec (1.134.0)

`RougeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.

## Attributes |
|
|---|---|
Name |
Description |
`rouge_type` |
`str`
Optional. Supported rouge types are rougen[1-9], rougeL, and rougeLsum. |
`use_stemmer` |
`bool`
Optional. Whether to use stemmer to compute rouge score. |
`split_summaries` |
`bool`
Optional. Whether to split summaries while using rougeLsum. |

## Methods

### RougeSpec

`RougeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tool -->

# Class Tool (1.134.0)

`Tool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool details that the model may use to generate response.

A `Tool`

is a piece of code that enables the system to interact
with external systems to perform an action, or set of actions,
outside of knowledge and scope of the model. A Tool object should
contain exactly one type of Tool (e.g FunctionDeclaration, Retrieval
or GoogleSearchRetrieval).

## Attributes |
|
|---|---|
Name |
Description |
`function_declarations` |
`MutableSequence[`
Optional. Function tool type. One or more function declarations to be passed to the model along with the current user query. Model may decide to call a subset of these functions by populating FunctionCall in the response. User should provide a FunctionResponse for each function call in the next turn. Based on the function responses, Model will generate the final response back to the user. Maximum 128 function declarations can be provided. |
`retrieval` |
Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation. |
`google_search` |
Optional. GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google. |
`google_search_retrieval` |
Optional. GoogleSearchRetrieval tool type. Specialized retrieval tool that is powered by Google search. |
`google_maps` |
Optional. GoogleMaps tool type. Tool to support Google Maps in Model. |
`enterprise_web_search` |
Optional. Tool to support searching public web data, powered by Vertex AI Search and Sec4 compliance. |
`code_execution` |
Optional. CodeExecution tool type. Enables the model to execute code as part of generation. |
`url_context` |
Optional. Tool to support URL context retrieval. |
`computer_use` |
Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations. |

## Classes

### CodeExecution

`CodeExecution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool that executes code generated by the model, and automatically returns the result to the model.

See also [ExecutableCode]and [CodeExecutionResult] which are input and output to this tool.

### ComputerUse

`ComputerUse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support computer use.

### GoogleSearch

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### PhishBlockThreshold

`PhishBlockThreshold(value)`


These are available confidence level user can set to block
malicious urls with chosen confidence and above. For
understanding different confidence of webrisk, please refer to
[https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel](https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel)

## Methods

### Tool

`Tool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool details that the model may use to generate response.

A `Tool`

is a piece of code that enables the system to interact
with external systems to perform an action, or set of actions,
outside of knowledge and scope of the model. A Tool object should
contain exactly one type of Tool (e.g FunctionDeclaration, Retrieval
or GoogleSearchRetrieval).

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.XraiAttribution -->

# Class XraiAttribution (1.134.0)

`XraiAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An explanation method that redistributes Integrated Gradients attributions to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details:

[https://arxiv.org/abs/1906.02825](https://arxiv.org/abs/1906.02825)

Supported only by image Models.

## Attributes |
|
|---|---|
Name |
Description |
`step_count` |
`int`
Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is met within the desired error range. Valid range of its value is [1, 100], inclusively. |
`smooth_grad_config` |
Config for SmoothGrad approximation of gradients. When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: https://arxiv.org/pdf/1706.03825.pdf |
`blur_baseline_config` |
Config for XRAI with blur baseline. When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: https://arxiv.org/abs/2004.03383 |

## Methods

### XraiAttribution

`XraiAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An explanation method that redistributes Integrated Gradients attributions to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details:

[https://arxiv.org/abs/1906.02825](https://arxiv.org/abs/1906.02825)

Supported only by image Models.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ContainerSpec -->

# Class ContainerSpec (1.134.0)

`ContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Container.

## Attributes |
|
|---|---|
Name |
Description |
`image_uri` |
`str`
Required. The URI of a container image in the Container Registry that is to be run on each worker replica. |
`command` |
`MutableSequence[str]`
The command to be invoked when the container is started. It overrides the entrypoint instruction in Dockerfile when provided. |
`args` |
`MutableSequence[str]`
The arguments to be passed when starting the container. |
`env` |
`MutableSequence[`
Environment variables to be passed to the container. Maximum limit is 100. |

## Methods

### ContainerSpec

`ContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Container.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpeculativeDecodingSpec.NgramSpeculation -->

# Class NgramSpeculation (1.134.0)

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

## Attribute |
|
|---|---|
Name |
Description |
`ngram_size` |
`int`
The number of last N input tokens used as ngram to search/match against the previous prompt sequence. This is equal to the N in N-Gram. The default value is 3 if not specified. |

## Methods

### NgramSpeculation

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchPredictionJob.InstanceConfig -->

# Class InstanceConfig (1.134.0)

`InstanceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration defining how to transform batch prediction input instances to the instances that the Model accepts.

## Attributes |
|
|---|---|
Name |
Description |
`instance_type` |
`str`
The format of the instance that the Model accepts. Vertex AI will convert compatible [batch prediction input instance formats][google.cloud.aiplatform.v1.BatchPredictionJob.InputConfig.instances_format] to the specified format. Supported values are: - `object` : Each input is converted to JSON object format.
- For `bigquery` , each row is converted to an object.
- For `jsonl` , each line of the JSONL input must be an
object.
- Does not apply to `csv` , `file-list` , `tf-record` ,
or `tf-record-gzip` .
- `array` : Each input is converted to JSON array format.
- For `bigquery` , each row is converted to an array. The
order of columns is determined by the BigQuery column
order, unless
included_fields
is populated.
included_fields
must be populated for specifying field orders.
- For `jsonl` , if each line of the JSONL input is an
object,
included_fields
must be populated for specifying field orders.
- Does not apply to `csv` , `file-list` , `tf-record` ,
or `tf-record-gzip` .
If not specified, Vertex AI converts the batch prediction
input as follows:
- For `bigquery` and `csv` , the behavior is the same as
`array` . The order of columns is the same as defined in
the file or table, unless
included_fields
is populated.
- For `jsonl` , the prediction instance format is
determined by each line of the input.
- For `tf-record` /`tf-record-gzip` , each record will be
converted to an object in the format of
`{"b64": ` , where is the
Base64-encoded string of the content of the record.
- For `file-list` , each file in the list will be converted
to an object in the format of `{"b64": ` , where
is the Base64-encoded string of the content of
the file.
|
`key_field` |
`str`
The name of the field that is considered as a key. The values identified by the key field is not included in the transformed instances that is sent to the Model. This is similar to specifying this name of the field in excluded_fields. In addition, the batch prediction output will not include the instances. Instead the output will only include the value of the key field, in a field named `key` in the
output:
- For `jsonl` output format, the output will have a
`key` field instead of the `instance` field.
- For `csv` /`bigquery` output format, the output will
have have a `key` column instead of the instance feature
columns.
The input must be JSONL with objects at each line, CSV,
BigQuery or TfRecord.
|
`included_fields` |
`MutableSequence[str]`
Fields that will be included in the prediction instance that is sent to the Model. If instance_type is `array` , the order of field names in included_fields
also determines the order of the values in the array.
When included_fields is populated,
excluded_fields
must be empty.
The input must be JSONL with objects at each line, BigQuery
or TfRecord.
|
`excluded_fields` |
`MutableSequence[str]`
Fields that will be excluded in the prediction instance that is sent to the Model. Excluded will be attached to the batch prediction output if key_field is not specified. When excluded_fields is populated, included_fields must be empty. The input must be JSONL with objects at each line, BigQuery or TfRecord. |

## Methods

### InstanceConfig

`InstanceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration defining how to transform batch prediction input instances to the instances that the Model accepts.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataResponse -->

# Class ExportTensorboardTimeSeriesDataResponse (1.134.0)

```
ExportTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ExportTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`time_series_data_points` |
`MutableSequence[`
The returned time series data points. |
`next_page_token` |
`str`
A token, which can be sent as page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ExportTensorboardTimeSeriesDataResponse

```
ExportTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ExportTensorboardTimeSeriesData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeArtifactsResponse -->

# Class PurgeArtifactsResponse (1.134.0)

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Artifacts that this request deleted (or, if `force` is false, the number of Artifacts that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Artifact names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeArtifactsResponse

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsRequest -->

# Class ListNotebookExecutionJobsRequest (1.134.0)

```
ListNotebookExecutionJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.ListNotebookExecutionJobs]

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `notebookExecutionJob` supports = and !=.
`notebookExecutionJob` represents the
NotebookExecutionJob ID.
- `displayName` supports = and != and regex.
- `schedule` supports = and != and regex.
Some examples:
- `notebookExecutionJob="123"`
- `notebookExecutionJob="my-execution-job"`
- `displayName="myDisplayName"` and
`displayName=` "myDisplayNameRegex"`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListNotebookExecutionJobsResponse.next_page_token of the previous NotebookService.ListNotebookExecutionJobs call. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
Example: `display_name, create_time desc` .
|
`view` |
Optional. The NotebookExecutionJob view. Defaults to BASIC. |

## Methods

### ListNotebookExecutionJobsRequest

```
ListNotebookExecutionJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.ListNotebookExecutionJobs]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse -->

# Class ListFeatureOnlineStoresResponse (1.134.0)

```
ListFeatureOnlineStoresResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

## Attributes |
|
|---|---|
Name |
Description |
`feature_online_stores` |
`MutableSequence[`
The FeatureOnlineStores matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureOnlineStoresRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureOnlineStoresResponse

```
ListFeatureOnlineStoresResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesRequest -->

# Class ListStudiesRequest (1.134.0)

`ListStudiesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListStudies.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the Study from. Format: `projects/{project}/locations/{location}`
|
`page_token` |
`str`
Optional. A page token to request the next page of results. If unspecified, there are no subsequent pages. |
`page_size` |
`int`
Optional. The maximum number of studies to return per "page" of results. If unspecified, service will pick an appropriate default. |

## Methods

### ListStudiesRequest

`ListStudiesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListStudies.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.XraiAttribution -->

# Class XraiAttribution (1.134.0)

`XraiAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An explanation method that redistributes Integrated Gradients attributions to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details:

[https://arxiv.org/abs/1906.02825](https://arxiv.org/abs/1906.02825)

Supported only by image Models.

## Attributes |
|
|---|---|
Name |
Description |
`step_count` |
`int`
Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is met within the desired error range. Valid range of its value is [1, 100], inclusively. |
`smooth_grad_config` |
Config for SmoothGrad approximation of gradients. When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: https://arxiv.org/pdf/1706.03825.pdf |
`blur_baseline_config` |
Config for XRAI with blur baseline. When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: https://arxiv.org/abs/2004.03383 |

## Methods

### XraiAttribution

`XraiAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An explanation method that redistributes Integrated Gradients attributions to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details:

[https://arxiv.org/abs/1906.02825](https://arxiv.org/abs/1906.02825)

Supported only by image Models.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse -->

# Class ListTensorboardTimeSeriesResponse (1.134.0)

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`MutableSequence[`
The TensorboardTimeSeries mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardTimeSeriesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardTimeSeriesResponse

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagManagedDbConfig.Unprovisioned -->

# Class Unprovisioned (1.134.0)

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

## Methods

### Unprovisioned

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesResponse.SelectEntity -->

# Class SelectEntity (1.134.0)

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.

## Attributes |
|
|---|---|
Name |
Description |
`offline_storage_deleted_entity_row_count` |
`int`
The count of deleted entity rows in the offline storage. Each row corresponds to the combination of an entity ID and a timestamp. One entity ID can have multiple rows in the offline storage. |
`online_storage_deleted_entity_count` |
`int`
The count of deleted entities in the online storage. Each entity ID corresponds to one entity. |

## Methods

### SelectEntity

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndexAuthConfig -->

# Class DeployedIndexAuthConfig (1.134.0)

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.

## Attribute |
|
|---|---|
Name |
Description |
`auth_provider` |
Defines the authentication provider that the DeployedIndex uses. |

## Classes

### AuthProvider

`AuthProvider(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for an authentication provider, including support for
```
JSON Web Token
(JWT) <https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32>
```

__.

## Methods

### DeployedIndexAuthConfig

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchPredictionJob.InstanceConfig -->

# Class InstanceConfig (1.134.0)

`InstanceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration defining how to transform batch prediction input instances to the instances that the Model accepts.

## Attributes |
|
|---|---|
Name |
Description |
`instance_type` |
`str`
The format of the instance that the Model accepts. Vertex AI will convert compatible [batch prediction input instance formats][google.cloud.aiplatform.v1beta1.BatchPredictionJob.InputConfig.instances_format] to the specified format. Supported values are: - `object` : Each input is converted to JSON object format.
- For `bigquery` , each row is converted to an object.
- For `jsonl` , each line of the JSONL input must be an
object.
- Does not apply to `csv` , `file-list` , `tf-record` ,
or `tf-record-gzip` .
- `array` : Each input is converted to JSON array format.
- For `bigquery` , each row is converted to an array. The
order of columns is determined by the BigQuery column
order, unless
included_fields
is populated.
included_fields
must be populated for specifying field orders.
- For `jsonl` , if each line of the JSONL input is an
object,
included_fields
must be populated for specifying field orders.
- Does not apply to `csv` , `file-list` , `tf-record` ,
or `tf-record-gzip` .
If not specified, Vertex AI converts the batch prediction
input as follows:
- For `bigquery` and `csv` , the behavior is the same as
`array` . The order of columns is the same as defined in
the file or table, unless
included_fields
is populated.
- For `jsonl` , the prediction instance format is
determined by each line of the input.
- For `tf-record` /`tf-record-gzip` , each record will be
converted to an object in the format of
`{"b64": ` , where is the
Base64-encoded string of the content of the record.
- For `file-list` , each file in the list will be converted
to an object in the format of `{"b64": ` , where
is the Base64-encoded string of the content of
the file.
|
`key_field` |
`str`
The name of the field that is considered as a key. The values identified by the key field is not included in the transformed instances that is sent to the Model. This is similar to specifying this name of the field in excluded_fields. In addition, the batch prediction output will not include the instances. Instead the output will only include the value of the key field, in a field named `key` in the
output:
- For `jsonl` output format, the output will have a
`key` field instead of the `instance` field.
- For `csv` /`bigquery` output format, the output will
have have a `key` column instead of the instance feature
columns.
The input must be JSONL with objects at each line, CSV,
BigQuery or TfRecord.
|
`included_fields` |
`MutableSequence[str]`
Fields that will be included in the prediction instance that is sent to the Model. If instance_type is `array` , the order of field names in included_fields
also determines the order of the values in the array.
When included_fields is populated,
excluded_fields
must be empty.
The input must be JSONL with objects at each line, BigQuery
or TfRecord.
|
`excluded_fields` |
`MutableSequence[str]`
Fields that will be excluded in the prediction instance that is sent to the Model. Excluded will be attached to the batch prediction output if key_field is not specified. When excluded_fields is populated, included_fields must be empty. The input must be JSONL with objects at each line, BigQuery or TfRecord. |

## Methods

### InstanceConfig

`InstanceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration defining how to transform batch prediction input instances to the instances that the Model accepts.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelOperationMetadata -->

# Class ExportModelOperationMetadata (1.134.0)

```
ExportModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ModelService.ExportModel operation.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |
`output_info` |
Output only. Information further describing the output of this Model export. |

## Classes

### OutputInfo

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes the output of the ExportModel. Supplements ExportModelRequest.OutputConfig.

## Methods

### ExportModelOperationMetadata

```
ExportModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ModelService.ExportModel operation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service -->

# Package notebook_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.notebook_service`

package.

## Classes

[NotebookServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient)

The interface for Vertex Notebook service (a.k.a. Colab on Workbench).

[NotebookServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient)

The interface for Vertex Notebook service (a.k.a. Colab on Workbench).

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers)

API documentation for `aiplatform_v1beta1.services.notebook_service.pagers`

module.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadFeatureValuesResponse.Header -->

# Class Header (1.134.0)

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
The resource name of the EntityType from the ReadFeatureValuesRequest. Value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .
|
`feature_descriptors` |
`MutableSequence[`
List of Feature metadata corresponding to each piece of ReadFeatureValuesResponse.EntityView.data. |

## Methods

### Header

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RougeSpec -->

# Class RougeSpec (1.134.0)

`RougeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.

## Attributes |
|
|---|---|
Name |
Description |
`rouge_type` |
`str`
Optional. Supported rouge types are rougen[1-9], rougeL, and rougeLsum. |
`use_stemmer` |
`bool`
Optional. Whether to use stemmer to compute rouge score. |
`split_summaries` |
`bool`
Optional. Whether to split summaries while using rougeLsum. |

## Methods

### RougeSpec

`RougeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringStatsAnomalies.FeatureHistoricStatsAnomalies -->

# Class FeatureHistoricStatsAnomalies (1.134.0)

```
FeatureHistoricStatsAnomalies(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Historical Stats (and Anomalies) for a specific Feature.

## Attributes |
|
|---|---|
Name |
Description |
`feature_display_name` |
`str`
Display Name of the Feature. |
`threshold` |
Threshold for anomaly detection. |
`training_stats` |
Stats calculated for the Training Dataset. |
`prediction_stats` |
`MutableSequence[`
A list of historical stats generated by different time window's Prediction Dataset. |

## Methods

### FeatureHistoricStatsAnomalies

```
FeatureHistoricStatsAnomalies(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Historical Stats (and Anomalies) for a specific Feature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigratableResource.DataLabelingDataset.DataLabelingAnnotatedDataset -->

# Class DataLabelingAnnotatedDataset (1.134.0)

```
DataLabelingAnnotatedDataset(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents one AnnotatedDataset in datalabeling.googleapis.com.

## Attributes |
|
|---|---|
Name |
Description |
`annotated_dataset` |
`str`
Full resource name of data labeling AnnotatedDataset. Format: `projects/{project}/datasets/{dataset}/annotatedDatasets/{annotated_dataset}` .
|
`annotated_dataset_display_name` |
`str`
The AnnotatedDataset's display name in datalabeling.googleapis.com. |

## Methods

### DataLabelingAnnotatedDataset

```
DataLabelingAnnotatedDataset(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents one AnnotatedDataset in datalabeling.googleapis.com.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ContainerSpec -->

# Class ContainerSpec (1.134.0)

`ContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Container.

## Attributes |
|
|---|---|
Name |
Description |
`image_uri` |
`str`
Required. The URI of a container image in the Container Registry that is to be run on each worker replica. |
`command` |
`MutableSequence[str]`
The command to be invoked when the container is started. It overrides the entrypoint instruction in Dockerfile when provided. |
`args` |
`MutableSequence[str]`
The arguments to be passed when starting the container. |
`env` |
`MutableSequence[`
Environment variables to be passed to the container. Maximum limit is 100. |

## Methods

### ContainerSpec

`ContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Container.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Trial.Parameter -->

# Class Parameter (1.134.0)

`Parameter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a parameter to be tuned.

## Attributes |
|
|---|---|
Name |
Description |
`parameter_id` |
`str`
Output only. The ID of the parameter. The parameter should be defined in [StudySpec's Parameters][google.cloud.aiplatform.v1.StudySpec.parameters]. |
`value` |
`google.protobuf.struct_pb2.Value`
Output only. The value of the parameter. `number_value`
will be set if a parameter defined in StudySpec is in type
'INTEGER', 'DOUBLE' or 'DISCRETE'. `string_value` will be
set if a parameter defined in StudySpec is in type
'CATEGORICAL'.
|

## Methods

### Parameter

`Parameter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a parameter to be tuned.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureRequest -->

# Class DeleteFeatureRequest (1.134.0)

`DeleteFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeature. Request message for FeatureRegistryService.DeleteFeature.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Features to be deleted. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}/features/{feature}`
`projects/{project}/locations/{location}/featureGroups/{feature_group}/features/{feature}`
|

## Methods

### DeleteFeatureRequest

`DeleteFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeature. Request message for FeatureRegistryService.DeleteFeature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse -->

# Class ListFeatureOnlineStoresResponse (1.134.0)

```
ListFeatureOnlineStoresResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

## Attributes |
|
|---|---|
Name |
Description |
`feature_online_stores` |
`MutableSequence[`
The FeatureOnlineStores matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureOnlineStoresRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureOnlineStoresResponse

```
ListFeatureOnlineStoresResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsRequest -->

# Class ListTrialsRequest (1.134.0)

`ListTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListTrials.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Study to list the Trial from. Format: `projects/{project}/locations/{location}/studies/{study}`
|
`page_token` |
`str`
Optional. A page token to request the next page of results. If unspecified, there are no subsequent pages. |
`page_size` |
`int`
Optional. The number of Trials to retrieve per "page" of results. If unspecified, the service will pick an appropriate default. |

## Methods

### ListTrialsRequest

`ListTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListTrials.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeExecutionsResponse -->

# Class PurgeExecutionsResponse (1.134.0)

`PurgeExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Executions that this request deleted (or, if `force` is false, the number of Executions that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Execution names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeExecutionsResponse

`PurgeExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeExecutions.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.persistent_resource_service.pagers`

module.

## Classes

[ListPersistentResourcesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.pagers.ListPersistentResourcesAsyncPager)

```
ListPersistentResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
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


A pager for iterating through `list_persistent_resources`

requests.

This class thinly wraps an initial
[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse) object, and
provides an `__aiter__`

method to iterate through its
`persistent_resources`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListPersistentResources`

requests and continue to iterate
through the `persistent_resources`

field on the
corresponding responses.

All the usual [ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListPersistentResourcesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.pagers.ListPersistentResourcesPager)

```
ListPersistentResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
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


A pager for iterating through `list_persistent_resources`

requests.

This class thinly wraps an initial
[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse) object, and
provides an `__iter__`

method to iterate through its
`persistent_resources`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPersistentResources`

requests and continue to iterate
through the `persistent_resources`

field on the
corresponding responses.

All the usual [ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.HarmCategory -->

# Class HarmCategory (1.134.0)

`HarmCategory(value)`


Harm categories that will block the content.

## Enums |
|
|---|---|
Name |
Description |
`HARM_CATEGORY_UNSPECIFIED` |
The harm category is unspecified. |
`HARM_CATEGORY_HATE_SPEECH` |
The harm category is hate speech. |
`HARM_CATEGORY_DANGEROUS_CONTENT` |
The harm category is dangerous content. |
`HARM_CATEGORY_HARASSMENT` |
The harm category is harassment. |
`HARM_CATEGORY_SEXUALLY_EXPLICIT` |
The harm category is sexually explicit content. |
`HARM_CATEGORY_CIVIC_INTEGRITY` |
Deprecated: Election filter is not longer supported. The harm category is civic integrity. |
`HARM_CATEGORY_JAILBREAK` |
The harm category is for jailbreak prompts. |

## Methods

### HarmCategory

`HarmCategory(value)`


Harm categories that will block the content.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrievalMetadata -->

# Class RetrievalMetadata (1.134.0)

`RetrievalMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata related to retrieval in the grounding flow.

## Attribute |
|
|---|---|
Name |
Description |
`google_search_dynamic_retrieval_score` |
`float`
Optional. Score indicating how likely information from Google Search could help answer the prompt. The score is in the range `[0, 1]` , where 0 is the least likely and 1 is
the most likely. This score is only populated when Google
Search grounding and dynamic retrieval is enabled. It will
be compared to the threshold to determine whether to trigger
Google Search.
|

## Methods

### RetrievalMetadata

`RetrievalMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata related to retrieval in the grounding flow.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse -->

# Class ListTensorboardExperimentsResponse (1.134.0)

```
ListTensorboardExperimentsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardExperiments.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_experiments` |
`MutableSequence[`
The TensorboardExperiments mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardExperimentsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardExperimentsResponse

```
ListTensorboardExperimentsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardExperiments.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesRequest -->

# Class ListStudiesRequest (1.134.0)

`ListStudiesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListStudies.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the Study from. Format: `projects/{project}/locations/{location}`
|
`page_token` |
`str`
Optional. A page token to request the next page of results. If unspecified, there are no subsequent pages. |
`page_size` |
`int`
Optional. The maximum number of studies to return per "page" of results. If unspecified, service will pick an appropriate default. |

## Methods

### ListStudiesRequest

`ListStudiesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListStudies.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.ServiceAgentType -->

# Class ServiceAgentType (1.134.0)

`ServiceAgentType(value)`


Service agent type used during data sync.

## Enums |
|
|---|---|
Name |
Description |
`SERVICE_AGENT_TYPE_UNSPECIFIED` |
By default, the project-level Vertex AI Service Agent is enabled. |
`SERVICE_AGENT_TYPE_PROJECT` |
Indicates the project-level Vertex AI Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) will be used during sync jobs. |
`SERVICE_AGENT_TYPE_FEATURE_VIEW` |
Enable a FeatureView service account to be created by Vertex AI and output in the field `service_account_email`. This service account will be used to read from the source BigQuery table during sync. |

## Methods

### ServiceAgentType

`ServiceAgentType(value)`


Service agent type used during data sync.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagManagedDbConfig.Unprovisioned -->

# Class Unprovisioned (1.134.0)

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

## Methods

### Unprovisioned

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AuthConfig.OauthConfig -->

# Class OauthConfig (1.134.0)

`OauthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for user oauth.

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
`access_token` |
`str`
Access token for extension endpoint. Only used to propagate token from [[ExecuteExtensionRequest.runtime_auth_config]] at request time. This field is a member of `oneof` _ `oauth_config` .
|
`service_account` |
`str`
The service account used to generate access tokens for executing the Extension. - If the service account is specified, the `iam.serviceAccounts.getAccessToken` permission should
be granted to Vertex AI Extension Service Agent
(https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents)
on the provided service account.
This field is a member of `oneof` _ `oauth_config` .
|

## Methods

### OauthConfig

`OauthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for user oauth.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassification -->

# Class AutoMlImageClassification (1.134.0)

`AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

## Attributes |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |
`metadata` |
The metadata information. |

## Methods

### AutoMlImageClassification

`AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

### AutoMlImageClassification

`AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportModelOperationMetadata -->

# Class ExportModelOperationMetadata (1.134.0)

```
ExportModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ModelService.ExportModel operation.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |
`output_info` |
Output only. Information further describing the output of this Model export. |

## Classes

### OutputInfo

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes the output of the ExportModel. Supplements ExportModelRequest.OutputConfig.

## Methods

### ExportModelOperationMetadata

```
ExportModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ModelService.ExportModel operation.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadFeatureValuesResponse.Header -->

# Class Header (1.134.0)

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
The resource name of the EntityType from the ReadFeatureValuesRequest. Value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .
|
`feature_descriptors` |
`MutableSequence[`
List of Feature metadata corresponding to each piece of ReadFeatureValuesResponse.EntityView.data. |

## Methods

### Header

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.ScaleType -->

# Class ScaleType (1.134.0)

`ScaleType(value)`


The type of scaling that should be applied to this parameter.

## Enums |
|
|---|---|
Name |
Description |
`SCALE_TYPE_UNSPECIFIED` |
By default, no scaling is applied. |
`UNIT_LINEAR_SCALE` |
Scales the feasible space to (0, 1) linearly. |
`UNIT_LOG_SCALE` |
Scales the feasible space logarithmically to (0, 1). The entire feasible space must be strictly positive. |
`UNIT_REVERSE_LOG_SCALE` |
Scales the feasible space "reverse" logarithmically to (0, 1). The result is that values close to the top of the feasible space are spread out more than points near the bottom. The entire feasible space must be strictly positive. |

## Methods

### ScaleType

`ScaleType(value)`


The type of scaling that should be applied to this parameter.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient -->

# Class PipelineServiceClient (1.135.0)

```
PipelineServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's pipelines. This
includes both `TrainingPipeline`

resources (used for AutoML and
custom training) and `PipelineJob`

resources (used for Vertex AI
Pipelines).

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
`PipelineServiceTransport` |
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

### PipelineServiceClient

```
PipelineServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the pipeline service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PipelineServiceTransport,Callable[..., PipelineServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the PipelineServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### artifact_path

```
artifact_path(
project: str, location: str, metadata_store: str, artifact: str
) -> str
```


Returns a fully-qualified artifact string.

### batch_cancel_pipeline_jobs

```
batch_cancel_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.BatchCancelPipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch cancel PipelineJobs. Firstly the server will check if all the jobs are in non-terminal states, and skip the jobs that are already terminated. If the operation failed, none of the pipeline jobs are cancelled. The server will poll the states of all the pipeline jobs periodically to check the cancellation status. This operation will return an LRO.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_cancel_pipeline_jobs():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[BatchCancelPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCancelPipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_cancel_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_batch_cancel_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchCancelPipelineJobs. |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: |
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

### batch_delete_pipeline_jobs

```
batch_delete_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.BatchDeletePipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch deletes PipelineJobs The Operation is atomic. If it fails, none of the PipelineJobs are deleted. If it succeeds, all of the PipelineJobs are deleted.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_delete_pipeline_jobs():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[BatchDeletePipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchDeletePipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_delete_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_batch_delete_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchDeletePipelineJobs. |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: |
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

### cancel_pipeline_job

```
cancel_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.CancelPipelineJobRequest,
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


Cancels a PipelineJob. Starts asynchronous cancellation on the
PipelineJob. The server makes a best effort to cancel the
pipeline, but success is not guaranteed. Clients can use
xref_PipelineService.GetPipelineJob
or other methods to check whether the cancellation succeeded or
whether the pipeline completed despite cancellation. On
successful cancellation, the PipelineJob is not deleted; instead
it becomes a pipeline with a
xref_PipelineJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_PipelineJob.state
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
def sample_cancel_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelPipelineJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_cancel_pipeline_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CancelPipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_training_pipeline

```
cancel_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.CancelTrainingPipelineRequest,
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


Cancels a TrainingPipeline. Starts asynchronous cancellation on
the TrainingPipeline. The server makes a best effort to cancel
the pipeline, but success is not guaranteed. Clients can use
xref_PipelineService.GetTrainingPipeline
or other methods to check whether the cancellation succeeded or
whether the pipeline completed despite cancellation. On
successful cancellation, the TrainingPipeline is not deleted;
instead it becomes a pipeline with a
xref_TrainingPipeline.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_TrainingPipeline.state
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
def sample_cancel_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_cancel_training_pipeline)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CancelTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline to cancel. Format: |
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

### create_pipeline_job

```
create_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.CreatePipelineJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
pipeline_job: typing.Optional[
google.cloud.aiplatform_v1.types.pipeline_job.PipelineJob
] = None,
pipeline_job_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.pipeline_job.PipelineJob
```


Creates a PipelineJob. A PipelineJob will run immediately when created.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreatePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreatePipelineJobRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_create_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CreatePipelineJob. |
`parent` |
`str`
Required. The resource name of the Location to create the PipelineJob in. Format: |
`pipeline_job` |
Required. The PipelineJob to create. This corresponds to the |
`pipeline_job_id` |
`str`
The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated. This value should be less than 128 characters, and valid characters are |
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
An instance of a machine learning PipelineJob. |

### create_training_pipeline

```
create_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.CreateTrainingPipelineRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
training_pipeline: typing.Optional[
google.cloud.aiplatform_v1.types.training_pipeline.TrainingPipeline
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.training_pipeline.TrainingPipeline
```


Creates a TrainingPipeline. A created TrainingPipeline right away will be attempted to be run.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
training_pipeline = aiplatform_v1.[TrainingPipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TrainingPipeline.html)()
training_pipeline.display_name = "display_name_value"
training_pipeline.training_task_definition = "training_task_definition_value"
training_pipeline.training_task_inputs.null_value = "NULL_VALUE"
request = aiplatform_v1.[CreateTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTrainingPipelineRequest.html)(
parent="parent_value",
training_pipeline=training_pipeline,
)
# Make the request
response = client.[create_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_create_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CreateTrainingPipeline. |
`parent` |
`str`
Required. The resource name of the Location to create the TrainingPipeline in. Format: |
`training_pipeline` |
Required. The TrainingPipeline to create. This corresponds to the |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

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

### delete_pipeline_job

```
delete_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.DeletePipelineJobRequest,
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


Deletes a PipelineJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeletePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeletePipelineJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_delete_pipeline_job)(request=request)
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
The request object. Request message for PipelineService.DeletePipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob resource to be deleted. Format: |
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

### delete_training_pipeline

```
delete_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.DeleteTrainingPipelineRequest,
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


Deletes a TrainingPipeline.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_delete_training_pipeline)(request=request)
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
The request object. Request message for PipelineService.DeleteTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline resource to be deleted. Format: |
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

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### execution_path

```
execution_path(
project: str, location: str, metadata_store: str, execution: str
) -> str
```


Returns a fully-qualified execution string.

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
`PipelineServiceClient` |
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
`PipelineServiceClient` |
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
`PipelineServiceClient` |
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

### get_pipeline_job

```
get_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.GetPipelineJobRequest,
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
) -> google.cloud.aiplatform_v1.types.pipeline_job.PipelineJob
```


Gets a PipelineJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetPipelineJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_get_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.GetPipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob resource. Format: |
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
An instance of a machine learning PipelineJob. |

### get_training_pipeline

```
get_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.GetTrainingPipelineRequest,
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
) -> google.cloud.aiplatform_v1.types.training_pipeline.TrainingPipeline
```


Gets a TrainingPipeline.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_get_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.GetTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline resource. Format: |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

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

### list_pipeline_jobs

```
list_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsRequest,
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
) -> google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListPipelineJobsPager
```


Lists PipelineJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_pipeline_jobs():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_list_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.ListPipelineJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the PipelineJobs from. Format: |
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
Response message for PipelineService.ListPipelineJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_training_pipelines

```
list_training_pipelines(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesRequest,
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
google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListTrainingPipelinesPager
)
```


Lists TrainingPipelines in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_training_pipelines():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTrainingPipelinesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_training_pipelines](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_list_training_pipelines)(request=request)
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
The request object. Request message for PipelineService.ListTrainingPipelines. |
`parent` |
`str`
Required. The resource name of the Location to list the TrainingPipelines from. Format: |
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
Response message for PipelineService.ListTrainingPipelines Iterating over this object will yield results and resolve additional pages automatically. |

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### parse_artifact_path

`parse_artifact_path(path: str) -> typing.Dict[str, str]`


Parses a artifact path into its component segments.

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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_training_pipeline_path

`parse_training_pipeline_path(path: str) -> typing.Dict[str, str]`


Parses a training_pipeline path into its component segments.

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

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

### training_pipeline_path

`training_pipeline_path(project: str, location: str, training_pipeline: str) -> str`


Returns a fully-qualified training_pipeline string.

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.pagers -->

# Module pagers (1.135.0)

API documentation for `aiplatform_v1beta1.services.migration_service.pagers`

module.

## Classes

[SearchMigratableResourcesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.pagers.SearchMigratableResourcesAsyncPager)

```
SearchMigratableResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
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


A pager for iterating through `search_migratable_resources`

requests.

This class thinly wraps an initial
[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse) object, and
provides an `__aiter__`

method to iterate through its
`migratable_resources`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchMigratableResources`

requests and continue to iterate
through the `migratable_resources`

field on the
corresponding responses.

All the usual [SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchMigratableResourcesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.pagers.SearchMigratableResourcesPager)

```
SearchMigratableResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
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


A pager for iterating through `search_migratable_resources`

requests.

This class thinly wraps an initial
[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse) object, and
provides an `__iter__`

method to iterate through its
`migratable_resources`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchMigratableResources`

requests and continue to iterate
through the `migratable_resources`

field on the
corresponding responses.

All the usual [SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesRequest.EntityTypeSpec -->

# Class EntityTypeSpec (1.135.0)

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type_id` |
`str`
Required. ID of the EntityType to select Features. The EntityType id is the entity_type_id specified during EntityType creation. |
`feature_selector` |
Required. Selectors choosing which Feature values to read from the EntityType. |
`settings` |
`MutableSequence[`
Per-Feature settings for the batch read. |

## Methods

### EntityTypeSpec

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DedicatedResources.ScaleToZeroSpec -->

# Class ScaleToZeroSpec (1.135.0)

`ScaleToZeroSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for scale-to-zero feature.

## Attributes |
|
|---|---|
Name |
Description |
`min_scaleup_period` |
`google.protobuf.duration_pb2.Duration`
Optional. Minimum duration that a deployment will be scaled up before traffic is evaluated for potential scale-down. [MinValue=300] (5 minutes) [MaxValue=28800] (8 hours) |
`idle_scaledown_period` |
`google.protobuf.duration_pb2.Duration`
Optional. Duration of no traffic before scaling to zero. [MinValue=300] (5 minutes) [MaxValue=28800] (8 hours) |

## Methods

### ScaleToZeroSpec

`ScaleToZeroSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for scale-to-zero feature.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FunctionCallingConfig.Mode -->

# Class Mode (1.135.0)

`Mode(value)`


Function calling mode.

## Enums |
|
|---|---|
Name |
Description |
`MODE_UNSPECIFIED` |
Unspecified function calling mode. This value should not be used. |
`AUTO` |
Default model behavior, model decides to predict either function calls or natural language response. |
`ANY` |
Model is constrained to always predicting function calls only. If "allowed_function_names" are set, the predicted function calls will be limited to any one of "allowed_function_names", else the predicted function calls will be any one of the provided "function_declarations". |
`NONE` |
Model will not predict any function calls. Model behavior is same as when not passing any function declarations. |

## Methods

### Mode

`Mode(value)`


Function calling mode.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardBlobDataRequest -->

# Class ReadTensorboardBlobDataRequest (1.135.0)

```
ReadTensorboardBlobDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardBlobData.

## Attributes |
|
|---|---|
Name |
Description |
`time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to list Blobs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`blob_ids` |
`MutableSequence[str]`
IDs of the blobs to read. |

## Methods

### ReadTensorboardBlobDataRequest

```
ReadTensorboardBlobDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardBlobData.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsRequest -->

# Class ListModelsRequest (1.135.0)

`ListModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModels.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the Models from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `model` supports = and !=. `model` represents the
Model ID, i.e. the last segment of the Model's [resource
name][google.cloud.aiplatform.v1.Model.name].
- `display_name` supports = and !=
- `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- \`labels.key:\* or labels:key - key existence
- A key including a space must be quoted.
`labels."a key"` .
- `base_model_name` only supports =
Some examples:
- `model=1234`
- `displayName="myDisplayName"`
- `labels.myKey="myValue"`
- `baseModelName="text-bison"`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListModelsResponse.next_page_token of the previous ModelService.ListModels call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
Example: `display_name, create_time desc` .
|

## Methods

### ListModelsRequest

`ListModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModels.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service -->

# Package index_endpoint_service (1.135.0)

API documentation for `aiplatform_v1.services.index_endpoint_service`

package.

## Classes

[IndexEndpointServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceAsyncClient)

A service for managing Vertex AI's IndexEndpoints.

[IndexEndpointServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient)

A service for managing Vertex AI's IndexEndpoints.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.pagers)

API documentation for `aiplatform_v1.services.index_endpoint_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeArtifactsResponse -->

# Class PurgeArtifactsResponse (1.135.0)

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Artifacts that this request deleted (or, if `force` is false, the number of Artifacts that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Artifact names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeArtifactsResponse

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresRequest -->

# Class ListExampleStoresRequest (1.135.0)

`ListExampleStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.ListExampleStores.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the ExampleStores from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. The standard list filter. More detail in `AIP-160 ` __.
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |

## Methods

### ListExampleStoresRequest

`ListExampleStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.ListExampleStores.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataResponse -->

# Class ExportTensorboardTimeSeriesDataResponse (1.135.0)

```
ExportTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ExportTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`time_series_data_points` |
`MutableSequence[`
The returned time series data points. |
`next_page_token` |
`str`
A token, which can be sent as page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ExportTensorboardTimeSeriesDataResponse

```
ExportTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ExportTensorboardTimeSeriesData.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpeculativeDecodingSpec.NgramSpeculation -->

# Class NgramSpeculation (1.135.0)

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

## Attribute |
|
|---|---|
Name |
Description |
`ngram_size` |
`int`
The number of last N input tokens used as ngram to search/match against the previous prompt sequence. This is equal to the N in N-Gram. The default value is 3 if not specified. |

## Methods

### NgramSpeculation

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureRequest -->

# Class GetFeatureRequest (1.135.0)

`GetFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetFeature. Request message for FeatureRegistryService.GetFeature.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Feature resource. Format for entity_type as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
Format for feature_group as parent:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|

## Methods

### GetFeatureRequest

`GetFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetFeature. Request message for FeatureRegistryService.GetFeature.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchMigrateResourcesOperationMetadata.PartialResult -->

# Class PartialResult (1.135.0)

`PartialResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a partial result in batch migration operation for one MigrateResourceRequest.

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
`error` |
`google.rpc.status_pb2.Status`
The error result of the migration request in case of failure. This field is a member of `oneof` _ `result` .
|
`model` |
`str`
Migrated model resource name. This field is a member of `oneof` _ `result` .
|
`dataset` |
`str`
Migrated dataset resource name. This field is a member of `oneof` _ `result` .
|
`request` |
It's the same as the value in BatchMigrateResourcesRequest.migrate_resource_requests. |

## Methods

### PartialResult

`PartialResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a partial result in batch migration operation for one MigrateResourceRequest.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobSpec.MultiTrialAlgorithmSpec.TrainTrialSpec -->

# Class TrainTrialSpec (1.135.0)

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.

## Attributes |
|
|---|---|
Name |
Description |
`train_trial_job_spec` |
Required. The spec of a train trial job. The same spec applies to all train trials. |
`max_parallel_trial_count` |
`int`
Required. The maximum number of trials to run in parallel. |
`frequency` |
`int`
Required. Frequency of search trials to start train stage. Top N [TrainTrialSpec.max_parallel_trial_count] search trials will be trained for every M [TrainTrialSpec.frequency] trials searched. |

## Methods

### TrainTrialSpec

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplainResponse -->

# Class ExplainResponse (1.135.0)

`ExplainResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Explain.

## Attributes |
|
|---|---|
Name |
Description |
`explanations` |
`MutableSequence[`
The explanations of the Model's PredictResponse.predictions. It has the same number of elements as instances to be explained. |
`deployed_model_id` |
`str`
ID of the Endpoint's DeployedModel that served this explanation. |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
The predictions that are the output of the predictions call. Same as PredictResponse.predictions. |

## Methods

### ExplainResponse

`ExplainResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Explain.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tool -->

# Class Tool (1.135.0)

`Tool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool details that the model may use to generate response.

A `Tool`

is a piece of code that enables the system to interact
with external systems to perform an action, or set of actions,
outside of knowledge and scope of the model. A Tool object should
contain exactly one type of Tool (e.g FunctionDeclaration, Retrieval
or GoogleSearchRetrieval).

## Attributes |
|
|---|---|
Name |
Description |
`function_declarations` |
`MutableSequence[`
Optional. Function tool type. One or more function declarations to be passed to the model along with the current user query. Model may decide to call a subset of these functions by populating FunctionCall in the response. User should provide a FunctionResponse for each function call in the next turn. Based on the function responses, Model will generate the final response back to the user. Maximum 128 function declarations can be provided. |
`retrieval` |
Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation. |
`google_search` |
Optional. GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google. |
`google_search_retrieval` |
Optional. GoogleSearchRetrieval tool type. Specialized retrieval tool that is powered by Google search. |
`google_maps` |
Optional. GoogleMaps tool type. Tool to support Google Maps in Model. |
`enterprise_web_search` |
Optional. Tool to support searching public web data, powered by Vertex AI Search and Sec4 compliance. |
`code_execution` |
Optional. CodeExecution tool type. Enables the model to execute code as part of generation. |
`url_context` |
Optional. Tool to support URL context retrieval. |
`computer_use` |
Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations. |

## Classes

### CodeExecution

`CodeExecution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool that executes code generated by the model, and automatically returns the result to the model.

See also [ExecutableCode]and [CodeExecutionResult] which are input and output to this tool.

### ComputerUse

`ComputerUse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support computer use.

### GoogleSearch

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### PhishBlockThreshold

`PhishBlockThreshold(value)`


These are available confidence level user can set to block
malicious urls with chosen confidence and above. For
understanding different confidence of webrisk, please refer to
[https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel](https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel)

## Methods

### Tool

`Tool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool details that the model may use to generate response.

A `Tool`

is a piece of code that enables the system to interact
with external systems to perform an action, or set of actions,
outside of knowledge and scope of the model. A Tool object should
contain exactly one type of Tool (e.g FunctionDeclaration, Retrieval
or GoogleSearchRetrieval).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagManagedDbConfig.Basic -->

# Class Basic (1.135.0)

`Basic(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Basic tier is a cost-effective and low compute tier suitable for the following cases:

- Experimenting with RagManagedDb.
- Small data size.
- Latency insensitive workload.
- Only using RAG Engine with external vector DBs.

NOTE: This is the default tier under Spanner mode if not explicitly chosen.

## Methods

### Basic

`Basic(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Basic tier is a cost-effective and low compute tier suitable for the following cases:

- Experimenting with RagManagedDb.
- Small data size.
- Latency insensitive workload.
- Only using RAG Engine with external vector DBs.

NOTE: This is the default tier under Spanner mode if not explicitly chosen.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse -->

# Class ListTensorboardTimeSeriesResponse (1.135.0)

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`MutableSequence[`
The TensorboardTimeSeries mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardTimeSeriesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardTimeSeriesResponse

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesOperationMetadata.PartialResult -->

# Class PartialResult (1.135.0)

`PartialResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a partial result in batch migration operation for one MigrateResourceRequest.

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
`error` |
`google.rpc.status_pb2.Status`
The error result of the migration request in case of failure. This field is a member of `oneof` _ `result` .
|
`model` |
`str`
Migrated model resource name. This field is a member of `oneof` _ `result` .
|
`dataset` |
`str`
Migrated dataset resource name. This field is a member of `oneof` _ `result` .
|
`request` |
It's the same as the value in [MigrateResourceRequest.migrate_resource_requests][]. |

## Methods

### PartialResult

`PartialResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a partial result in batch migration operation for one MigrateResourceRequest.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookExecutionJobsRequest -->

# Class ListNotebookExecutionJobsRequest (1.135.0)

```
ListNotebookExecutionJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.ListNotebookExecutionJobs]

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `notebookExecutionJob` supports = and !=.
`notebookExecutionJob` represents the
NotebookExecutionJob ID.
- `displayName` supports = and != and regex.
- `schedule` supports = and != and regex.
Some examples:
- `notebookExecutionJob="123"`
- `notebookExecutionJob="my-execution-job"`
- `displayName="myDisplayName"` and
`displayName=` "myDisplayNameRegex"`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListNotebookExecutionJobsResponse.next_page_token of the previous NotebookService.ListNotebookExecutionJobs call. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
Example: `display_name, create_time desc` .
|
`view` |
Optional. The NotebookExecutionJob view. Defaults to BASIC. |

## Methods

### ListNotebookExecutionJobsRequest

```
ListNotebookExecutionJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.ListNotebookExecutionJobs]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesResponse.SelectEntity -->

# Class SelectEntity (1.135.0)

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.

## Attributes |
|
|---|---|
Name |
Description |
`offline_storage_deleted_entity_row_count` |
`int`
The count of deleted entity rows in the offline storage. Each row corresponds to the combination of an entity ID and a timestamp. One entity ID can have multiple rows in the offline storage. |
`online_storage_deleted_entity_count` |
`int`
The count of deleted entities in the online storage. Each entity ID corresponds to one entity. |

## Methods

### SelectEntity

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassification -->

# Class AutoMlImageClassification (1.135.0)

`AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

## Attributes |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |
`metadata` |
The metadata information. |

## Methods

### AutoMlImageClassification

`AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

### AutoMlImageClassification

`AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesRequest.EntityTypeSpec -->

# Class EntityTypeSpec (1.135.0)

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type_id` |
`str`
Required. ID of the EntityType to select Features. The EntityType id is the entity_type_id specified during EntityType creation. |
`feature_selector` |
Required. Selectors choosing which Feature values to read from the EntityType. |
`settings` |
`MutableSequence[`
Per-Feature settings for the batch read. |

## Methods

### EntityTypeSpec

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedIndexAuthConfig -->

# Class DeployedIndexAuthConfig (1.135.0)

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.

## Attribute |
|
|---|---|
Name |
Description |
`auth_provider` |
Defines the authentication provider that the DeployedIndex uses. |

## Classes

### AuthProvider

`AuthProvider(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for an authentication provider, including support for
```
JSON Web Token
(JWT) <https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32>
```

__.

## Methods

### DeployedIndexAuthConfig

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service -->

# Package memory_bank_service (1.135.0)

API documentation for `aiplatform_v1beta1.services.memory_bank_service`

package.

## Classes

[MemoryBankServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient)

A service for managing memories for LLM applications.

[MemoryBankServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient)

A service for managing memories for LLM applications.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers)

API documentation for `aiplatform_v1beta1.services.memory_bank_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RougeSpec -->

# Class RougeSpec (1.135.0)

`RougeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.

## Attributes |
|
|---|---|
Name |
Description |
`rouge_type` |
`str`
Optional. Supported rouge types are rougen[1-9], rougeL, and rougeLsum. |
`use_stemmer` |
`bool`
Optional. Whether to use stemmer to compute rouge score. |
`split_summaries` |
`bool`
Optional. Whether to split summaries while using rougeLsum. |

## Methods

### RougeSpec

`RougeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tool -->

# Class Tool (1.135.0)

`Tool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool details that the model may use to generate response.

A `Tool`

is a piece of code that enables the system to interact
with external systems to perform an action, or set of actions,
outside of knowledge and scope of the model. A Tool object should
contain exactly one type of Tool (e.g FunctionDeclaration, Retrieval
or GoogleSearchRetrieval).

## Attributes |
|
|---|---|
Name |
Description |
`function_declarations` |
`MutableSequence[`
Optional. Function tool type. One or more function declarations to be passed to the model along with the current user query. Model may decide to call a subset of these functions by populating FunctionCall in the response. User should provide a FunctionResponse for each function call in the next turn. Based on the function responses, Model will generate the final response back to the user. Maximum 128 function declarations can be provided. |
`retrieval` |
Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation. |
`google_search` |
Optional. GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google. |
`google_search_retrieval` |
Optional. GoogleSearchRetrieval tool type. Specialized retrieval tool that is powered by Google search. |
`google_maps` |
Optional. GoogleMaps tool type. Tool to support Google Maps in Model. |
`enterprise_web_search` |
Optional. Tool to support searching public web data, powered by Vertex AI Search and Sec4 compliance. |
`code_execution` |
Optional. CodeExecution tool type. Enables the model to execute code as part of generation. |
`url_context` |
Optional. Tool to support URL context retrieval. |
`computer_use` |
Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations. |

## Classes

### CodeExecution

`CodeExecution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool that executes code generated by the model, and automatically returns the result to the model.

See also [ExecutableCode]and [CodeExecutionResult] which are input and output to this tool.

### ComputerUse

`ComputerUse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support computer use.

### GoogleSearch

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### PhishBlockThreshold

`PhishBlockThreshold(value)`


These are available confidence level user can set to block
malicious urls with chosen confidence and above. For
understanding different confidence of webrisk, please refer to
[https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel](https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel)

## Methods

### Tool

`Tool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool details that the model may use to generate response.

A `Tool`

is a piece of code that enables the system to interact
with external systems to perform an action, or set of actions,
outside of knowledge and scope of the model. A Tool object should
contain exactly one type of Tool (e.g FunctionDeclaration, Retrieval
or GoogleSearchRetrieval).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.XraiAttribution -->

# Class XraiAttribution (1.135.0)

`XraiAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An explanation method that redistributes Integrated Gradients attributions to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details:

[https://arxiv.org/abs/1906.02825](https://arxiv.org/abs/1906.02825)

Supported only by image Models.

## Attributes |
|
|---|---|
Name |
Description |
`step_count` |
`int`
Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is met within the desired error range. Valid range of its value is [1, 100], inclusively. |
`smooth_grad_config` |
Config for SmoothGrad approximation of gradients. When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: https://arxiv.org/pdf/1706.03825.pdf |
`blur_baseline_config` |
Config for XRAI with blur baseline. When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: https://arxiv.org/abs/2004.03383 |

## Methods

### XraiAttribution

`XraiAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An explanation method that redistributes Integrated Gradients attributions to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details:

[https://arxiv.org/abs/1906.02825](https://arxiv.org/abs/1906.02825)

Supported only by image Models.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ContainerSpec -->

# Class ContainerSpec (1.135.0)

`ContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Container.

## Attributes |
|
|---|---|
Name |
Description |
`image_uri` |
`str`
Required. The URI of a container image in the Container Registry that is to be run on each worker replica. |
`command` |
`MutableSequence[str]`
The command to be invoked when the container is started. It overrides the entrypoint instruction in Dockerfile when provided. |
`args` |
`MutableSequence[str]`
The arguments to be passed when starting the container. |
`env` |
`MutableSequence[`
Environment variables to be passed to the container. Maximum limit is 100. |

## Methods

### ContainerSpec

`ContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Container.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpeculativeDecodingSpec.NgramSpeculation -->

# Class NgramSpeculation (1.135.0)

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

## Attribute |
|
|---|---|
Name |
Description |
`ngram_size` |
`int`
The number of last N input tokens used as ngram to search/match against the previous prompt sequence. This is equal to the N in N-Gram. The default value is 3 if not specified. |

## Methods

### NgramSpeculation

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchPredictionJob.InstanceConfig -->

# Class InstanceConfig (1.135.0)

`InstanceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration defining how to transform batch prediction input instances to the instances that the Model accepts.

## Attributes |
|
|---|---|
Name |
Description |
`instance_type` |
`str`
The format of the instance that the Model accepts. Vertex AI will convert compatible [batch prediction input instance formats][google.cloud.aiplatform.v1.BatchPredictionJob.InputConfig.instances_format] to the specified format. Supported values are: - `object` : Each input is converted to JSON object format.
- For `bigquery` , each row is converted to an object.
- For `jsonl` , each line of the JSONL input must be an
object.
- Does not apply to `csv` , `file-list` , `tf-record` ,
or `tf-record-gzip` .
- `array` : Each input is converted to JSON array format.
- For `bigquery` , each row is converted to an array. The
order of columns is determined by the BigQuery column
order, unless
included_fields
is populated.
included_fields
must be populated for specifying field orders.
- For `jsonl` , if each line of the JSONL input is an
object,
included_fields
must be populated for specifying field orders.
- Does not apply to `csv` , `file-list` , `tf-record` ,
or `tf-record-gzip` .
If not specified, Vertex AI converts the batch prediction
input as follows:
- For `bigquery` and `csv` , the behavior is the same as
`array` . The order of columns is the same as defined in
the file or table, unless
included_fields
is populated.
- For `jsonl` , the prediction instance format is
determined by each line of the input.
- For `tf-record` /`tf-record-gzip` , each record will be
converted to an object in the format of
`{"b64": ` , where is the
Base64-encoded string of the content of the record.
- For `file-list` , each file in the list will be converted
to an object in the format of `{"b64": ` , where
is the Base64-encoded string of the content of
the file.
|
`key_field` |
`str`
The name of the field that is considered as a key. The values identified by the key field is not included in the transformed instances that is sent to the Model. This is similar to specifying this name of the field in excluded_fields. In addition, the batch prediction output will not include the instances. Instead the output will only include the value of the key field, in a field named `key` in the
output:
- For `jsonl` output format, the output will have a
`key` field instead of the `instance` field.
- For `csv` /`bigquery` output format, the output will
have have a `key` column instead of the instance feature
columns.
The input must be JSONL with objects at each line, CSV,
BigQuery or TfRecord.
|
`included_fields` |
`MutableSequence[str]`
Fields that will be included in the prediction instance that is sent to the Model. If instance_type is `array` , the order of field names in included_fields
also determines the order of the values in the array.
When included_fields is populated,
excluded_fields
must be empty.
The input must be JSONL with objects at each line, BigQuery
or TfRecord.
|
`excluded_fields` |
`MutableSequence[str]`
Fields that will be excluded in the prediction instance that is sent to the Model. Excluded will be attached to the batch prediction output if key_field is not specified. When excluded_fields is populated, included_fields must be empty. The input must be JSONL with objects at each line, BigQuery or TfRecord. |

## Methods

### InstanceConfig

`InstanceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration defining how to transform batch prediction input instances to the instances that the Model accepts.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataResponse -->

# Class ExportTensorboardTimeSeriesDataResponse (1.135.0)

```
ExportTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ExportTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`time_series_data_points` |
`MutableSequence[`
The returned time series data points. |
`next_page_token` |
`str`
A token, which can be sent as page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ExportTensorboardTimeSeriesDataResponse

```
ExportTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ExportTensorboardTimeSeriesData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeArtifactsResponse -->

# Class PurgeArtifactsResponse (1.135.0)

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Artifacts that this request deleted (or, if `force` is false, the number of Artifacts that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Artifact names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeArtifactsResponse

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsRequest -->

# Class ListNotebookExecutionJobsRequest (1.135.0)

```
ListNotebookExecutionJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.ListNotebookExecutionJobs]

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `notebookExecutionJob` supports = and !=.
`notebookExecutionJob` represents the
NotebookExecutionJob ID.
- `displayName` supports = and != and regex.
- `schedule` supports = and != and regex.
Some examples:
- `notebookExecutionJob="123"`
- `notebookExecutionJob="my-execution-job"`
- `displayName="myDisplayName"` and
`displayName=` "myDisplayNameRegex"`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListNotebookExecutionJobsResponse.next_page_token of the previous NotebookService.ListNotebookExecutionJobs call. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
Example: `display_name, create_time desc` .
|
`view` |
Optional. The NotebookExecutionJob view. Defaults to BASIC. |

## Methods

### ListNotebookExecutionJobsRequest

```
ListNotebookExecutionJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.ListNotebookExecutionJobs]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse -->

# Class ListFeatureOnlineStoresResponse (1.135.0)

```
ListFeatureOnlineStoresResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

## Attributes |
|
|---|---|
Name |
Description |
`feature_online_stores` |
`MutableSequence[`
The FeatureOnlineStores matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureOnlineStoresRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureOnlineStoresResponse

```
ListFeatureOnlineStoresResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesRequest -->

# Class ListStudiesRequest (1.135.0)

`ListStudiesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListStudies.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the Study from. Format: `projects/{project}/locations/{location}`
|
`page_token` |
`str`
Optional. A page token to request the next page of results. If unspecified, there are no subsequent pages. |
`page_size` |
`int`
Optional. The maximum number of studies to return per "page" of results. If unspecified, service will pick an appropriate default. |

## Methods

### ListStudiesRequest

`ListStudiesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListStudies.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.XraiAttribution -->

# Class XraiAttribution (1.135.0)

`XraiAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An explanation method that redistributes Integrated Gradients attributions to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details:

[https://arxiv.org/abs/1906.02825](https://arxiv.org/abs/1906.02825)

Supported only by image Models.

## Attributes |
|
|---|---|
Name |
Description |
`step_count` |
`int`
Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is met within the desired error range. Valid range of its value is [1, 100], inclusively. |
`smooth_grad_config` |
Config for SmoothGrad approximation of gradients. When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: https://arxiv.org/pdf/1706.03825.pdf |
`blur_baseline_config` |
Config for XRAI with blur baseline. When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: https://arxiv.org/abs/2004.03383 |

## Methods

### XraiAttribution

`XraiAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An explanation method that redistributes Integrated Gradients attributions to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details:

[https://arxiv.org/abs/1906.02825](https://arxiv.org/abs/1906.02825)

Supported only by image Models.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse -->

# Class ListTensorboardTimeSeriesResponse (1.135.0)

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`MutableSequence[`
The TensorboardTimeSeries mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardTimeSeriesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardTimeSeriesResponse

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagManagedDbConfig.Unprovisioned -->

# Class Unprovisioned (1.135.0)

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

## Methods

### Unprovisioned

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesResponse.SelectEntity -->

# Class SelectEntity (1.135.0)

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.

## Attributes |
|
|---|---|
Name |
Description |
`offline_storage_deleted_entity_row_count` |
`int`
The count of deleted entity rows in the offline storage. Each row corresponds to the combination of an entity ID and a timestamp. One entity ID can have multiple rows in the offline storage. |
`online_storage_deleted_entity_count` |
`int`
The count of deleted entities in the online storage. Each entity ID corresponds to one entity. |

## Methods

### SelectEntity

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndexAuthConfig -->

# Class DeployedIndexAuthConfig (1.135.0)

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.

## Attribute |
|
|---|---|
Name |
Description |
`auth_provider` |
Defines the authentication provider that the DeployedIndex uses. |

## Classes

### AuthProvider

`AuthProvider(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for an authentication provider, including support for
```
JSON Web Token
(JWT) <https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32>
```

__.

## Methods

### DeployedIndexAuthConfig

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchPredictionJob.InstanceConfig -->

# Class InstanceConfig (1.135.0)

`InstanceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration defining how to transform batch prediction input instances to the instances that the Model accepts.

## Attributes |
|
|---|---|
Name |
Description |
`instance_type` |
`str`
The format of the instance that the Model accepts. Vertex AI will convert compatible [batch prediction input instance formats][google.cloud.aiplatform.v1beta1.BatchPredictionJob.InputConfig.instances_format] to the specified format. Supported values are: - `object` : Each input is converted to JSON object format.
- For `bigquery` , each row is converted to an object.
- For `jsonl` , each line of the JSONL input must be an
object.
- Does not apply to `csv` , `file-list` , `tf-record` ,
or `tf-record-gzip` .
- `array` : Each input is converted to JSON array format.
- For `bigquery` , each row is converted to an array. The
order of columns is determined by the BigQuery column
order, unless
included_fields
is populated.
included_fields
must be populated for specifying field orders.
- For `jsonl` , if each line of the JSONL input is an
object,
included_fields
must be populated for specifying field orders.
- Does not apply to `csv` , `file-list` , `tf-record` ,
or `tf-record-gzip` .
If not specified, Vertex AI converts the batch prediction
input as follows:
- For `bigquery` and `csv` , the behavior is the same as
`array` . The order of columns is the same as defined in
the file or table, unless
included_fields
is populated.
- For `jsonl` , the prediction instance format is
determined by each line of the input.
- For `tf-record` /`tf-record-gzip` , each record will be
converted to an object in the format of
`{"b64": ` , where is the
Base64-encoded string of the content of the record.
- For `file-list` , each file in the list will be converted
to an object in the format of `{"b64": ` , where
is the Base64-encoded string of the content of
the file.
|
`key_field` |
`str`
The name of the field that is considered as a key. The values identified by the key field is not included in the transformed instances that is sent to the Model. This is similar to specifying this name of the field in excluded_fields. In addition, the batch prediction output will not include the instances. Instead the output will only include the value of the key field, in a field named `key` in the
output:
- For `jsonl` output format, the output will have a
`key` field instead of the `instance` field.
- For `csv` /`bigquery` output format, the output will
have have a `key` column instead of the instance feature
columns.
The input must be JSONL with objects at each line, CSV,
BigQuery or TfRecord.
|
`included_fields` |
`MutableSequence[str]`
Fields that will be included in the prediction instance that is sent to the Model. If instance_type is `array` , the order of field names in included_fields
also determines the order of the values in the array.
When included_fields is populated,
excluded_fields
must be empty.
The input must be JSONL with objects at each line, BigQuery
or TfRecord.
|
`excluded_fields` |
`MutableSequence[str]`
Fields that will be excluded in the prediction instance that is sent to the Model. Excluded will be attached to the batch prediction output if key_field is not specified. When excluded_fields is populated, included_fields must be empty. The input must be JSONL with objects at each line, BigQuery or TfRecord. |

## Methods

### InstanceConfig

`InstanceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration defining how to transform batch prediction input instances to the instances that the Model accepts.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient -->

# Class VertexRagDataServiceAsyncClient (1.135.0)

```
VertexRagDataServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing user data for RAG.

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
`VertexRagDataServiceTransport` |
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

### VertexRagDataServiceAsyncClient

```
VertexRagDataServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag data service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagDataServiceTransport,Callable[..., VertexRagDataServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagDataServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_rag_corpus

```
create_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.CreateRagCorpusRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
rag_corpus: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
] = None,
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


Creates a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_corpus = aiplatform_v1beta1.[RagCorpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.html)()
rag_corpus.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateRagCorpusRequest.html)(
parent="parent_value",
rag_corpus=rag_corpus,
)
# Make the request
operation = client.[create_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_create_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.CreateRagCorpus. |
`parent` |
Required. The resource name of the Location to create the RagCorpus in. Format: |
`rag_corpus` |
Required. The RagCorpus to create. This corresponds to the |
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
An object representing a long-running operation. The result type for the operation will be
|

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

### delete_rag_corpus

```
delete_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.DeleteRagCorpusRequest,
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
) -> google.api_core.operation_async.AsyncOperation
```


Deletes a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagCorpusRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_delete_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.DeleteRagCorpus. |
`name` |
Required. The name of the RagCorpus resource to be deleted. Format: |
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
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_rag_file

```
delete_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.DeleteRagFileRequest,
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
) -> google.api_core.operation_async.AsyncOperation
```


Deletes a RagFile.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagFileRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_delete_rag_file)(request=request)
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
The request object. Request message for VertexRagDataService.DeleteRagFile. |
`name` |
Required. The name of the RagFile resource to be deleted. Format: |
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
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

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
`VertexRagDataServiceAsyncClient` |
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
`VertexRagDataServiceAsyncClient` |
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
`VertexRagDataServiceAsyncClient` |
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

### get_rag_corpus

```
get_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagCorpusRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
```


Gets a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagCorpusRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_corpus)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagCorpus |
`name` |
Required. The name of the RagCorpus resource. Format: |
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
A RagCorpus is a RagFile container and a project can have multiple RagCorpora. |

### get_rag_engine_config

```
get_rag_engine_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagEngineConfigRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagEngineConfig
```


Gets a RagEngineConfig.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_rag_engine_config():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagEngineConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagEngineConfigRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_engine_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_engine_config)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagEngineConfig |
`name` |
Required. The name of the RagEngineConfig resource. Format: |
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
Config for RagEngine. |

### get_rag_file

```
get_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagFileRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagFile
```


Gets a RagFile.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagFileRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_file)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagFile |
`name` |
Required. The name of the RagFile resource. Format: |
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
A RagFile contains user data for chunking, embedding and indexing. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport
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

### import_rag_files

```
import_rag_files(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ImportRagFilesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
import_rag_files_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.ImportRagFilesConfig
] = None,
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


Import files from Google Cloud Storage or Google Drive into a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_import_rag_files():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
import_rag_files_config = aiplatform_v1beta1.[ImportRagFilesConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesConfig.html)()
import_rag_files_config.gcs_source.uris = ['uris_value1', 'uris_value2']
import_rag_files_config.partial_failure_gcs_sink.output_uri_prefix = "output_uri_prefix_value"
import_rag_files_config.import_result_gcs_sink.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[ImportRagFilesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesRequest.html)(
parent="parent_value",
import_rag_files_config=import_rag_files_config,
)
# Make the request
operation = client.[import_rag_files](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_import_rag_files)(request=request)
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
The request object. Request message for VertexRagDataService.ImportRagFiles. |
`parent` |
Required. The name of the RagCorpus resource into which to import files. Format: |
`import_rag_files_config` |
Required. The config for the RagFiles to be synced and imported into the RagCorpus. VertexRagDataService.ImportRagFiles. This corresponds to the |
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
An object representing a long-running operation. The result type for the operation will be
|

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

### list_rag_corpora

```
list_rag_corpora(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaRequest,
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
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager
)
```


Lists RagCorpora in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_rag_corpora():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListRagCorporaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_rag_corpora](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_list_rag_corpora)(request=request)
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
The request object. Request message for VertexRagDataService.ListRagCorpora. |
`parent` |
Required. The resource name of the Location from which to list the RagCorpora. Format: |
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
Response message for VertexRagDataService.ListRagCorpora. Iterating over this object will yield results and resolve additional pages automatically. |

### list_rag_files

```
list_rag_files(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesRequest,
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
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagFilesAsyncPager
)
```


Lists RagFiles in a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_rag_files():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListRagFilesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_rag_files](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_list_rag_files)(request=request)
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
The request object. Request message for VertexRagDataService.ListRagFiles. |
`parent` |
Required. The resource name of the RagCorpus from which to list the RagFiles. Format: |
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
Response message for VertexRagDataService.ListRagFiles. Iterating over this object will yield results and resolve additional pages automatically. |

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### parse_rag_engine_config_path

`parse_rag_engine_config_path(path: str) -> typing.Dict[str, str]`


Parses a rag_engine_config path into its component segments.

### parse_rag_file_path

`parse_rag_file_path(path: str) -> typing.Dict[str, str]`


Parses a rag_file path into its component segments.

### parse_secret_version_path

`parse_secret_version_path(path: str) -> typing.Dict[str, str]`


Parses a secret_version path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### rag_engine_config_path

`rag_engine_config_path(project: str, location: str) -> str`


Returns a fully-qualified rag_engine_config string.

### rag_file_path

`rag_file_path(project: str, location: str, rag_corpus: str, rag_file: str) -> str`


Returns a fully-qualified rag_file string.

### secret_version_path

`secret_version_path(project: str, secret: str, secret_version: str) -> str`


Returns a fully-qualified secret_version string.

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

### update_rag_corpus

```
update_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UpdateRagCorpusRequest,
dict,
]
] = None,
*,
rag_corpus: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
] = None,
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


Updates a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_corpus = aiplatform_v1beta1.[RagCorpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.html)()
rag_corpus.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagCorpusRequest.html)(
rag_corpus=rag_corpus,
)
# Make the request
operation = client.[update_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_update_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.UpdateRagCorpus. |
`rag_corpus` |
Required. The RagCorpus which replaces the resource on the server. This corresponds to the |
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
An object representing a long-running operation. The result type for the operation will be
|

### update_rag_engine_config

```
update_rag_engine_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UpdateRagEngineConfigRequest,
dict,
]
] = None,
*,
rag_engine_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagEngineConfig
] = None,
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


Updates a RagEngineConfig.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_rag_engine_config():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateRagEngineConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagEngineConfigRequest.html)(
)
# Make the request
operation = client.[update_rag_engine_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_update_rag_engine_config)(request=request)
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
The request object. Request message for VertexRagDataService.UpdateRagEngineConfig. |
`rag_engine_config` |
Required. The updated RagEngineConfig. NOTE: Downgrading your RagManagedDb's ComputeTier could temporarily increase request latencies until the operation is fully complete. This corresponds to the |
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
An object representing a long-running operation. The result type for the operation will be
|

### upload_rag_file

```
upload_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UploadRagFileRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
rag_file: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagFile
] = None,
upload_rag_file_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.UploadRagFileConfig
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UploadRagFileResponse
)
```


Upload a file into a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_upload_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_file = aiplatform_v1beta1.[RagFile](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFile.html)()
rag_file.gcs_source.uris = ['uris_value1', 'uris_value2']
rag_file.display_name = "display_name_value"
request = aiplatform_v1beta1.[UploadRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadRagFileRequest.html)(
parent="parent_value",
rag_file=rag_file,
)
# Make the request
response = await client.[upload_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_upload_rag_file)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.UploadRagFile. |
`parent` |
Required. The name of the RagCorpus resource into which to upload the file. Format: |
`rag_file` |
Required. The RagFile to upload. This corresponds to the |
`upload_rag_file_config` |
Required. The config for the RagFiles to be uploaded into the RagCorpus. VertexRagDataService.UploadRagFile. This corresponds to the |
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
Response message for VertexRagDataService.UploadRagFile. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient -->

# Class PipelineServiceClient (1.135.0)

```
PipelineServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's pipelines. This
includes both `TrainingPipeline`

resources (used for AutoML and
custom training) and `PipelineJob`

resources (used for Vertex AI
Pipelines).

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
`PipelineServiceTransport` |
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

### PipelineServiceClient

```
PipelineServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the pipeline service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PipelineServiceTransport,Callable[..., PipelineServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the PipelineServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### artifact_path

```
artifact_path(
project: str, location: str, metadata_store: str, artifact: str
) -> str
```


Returns a fully-qualified artifact string.

### batch_cancel_pipeline_jobs

```
batch_cancel_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.BatchCancelPipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch cancel PipelineJobs. Firstly the server will check if all the jobs are in non-terminal states, and skip the jobs that are already terminated. If the operation failed, none of the pipeline jobs are cancelled. The server will poll the states of all the pipeline jobs periodically to check the cancellation status. This operation will return an LRO.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_batch_cancel_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchCancelPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_cancel_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_batch_cancel_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchCancelPipelineJobs. |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: |
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

### batch_delete_pipeline_jobs

```
batch_delete_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.BatchDeletePipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch deletes PipelineJobs The Operation is atomic. If it fails, none of the PipelineJobs are deleted. If it succeeds, all of the PipelineJobs are deleted.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_batch_delete_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchDeletePipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchDeletePipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_delete_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_batch_delete_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchDeletePipelineJobs. |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: |
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

### cancel_pipeline_job

```
cancel_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CancelPipelineJobRequest,
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


Cancels a PipelineJob. Starts asynchronous cancellation on the
PipelineJob. The server makes a best effort to cancel the
pipeline, but success is not guaranteed. Clients can use
xref_PipelineService.GetPipelineJob
or other methods to check whether the cancellation succeeded or
whether the pipeline completed despite cancellation. On
successful cancellation, the PipelineJob is not deleted; instead
it becomes a pipeline with a
xref_PipelineJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_PipelineJob.state
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
from google.cloud import aiplatform_v1beta1
def sample_cancel_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelPipelineJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_cancel_pipeline_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CancelPipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_training_pipeline

```
cancel_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CancelTrainingPipelineRequest,
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


Cancels a TrainingPipeline. Starts asynchronous cancellation on
the TrainingPipeline. The server makes a best effort to cancel
the pipeline, but success is not guaranteed. Clients can use
xref_PipelineService.GetTrainingPipeline
or other methods to check whether the cancellation succeeded or
whether the pipeline completed despite cancellation. On
successful cancellation, the TrainingPipeline is not deleted;
instead it becomes a pipeline with a
xref_TrainingPipeline.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_TrainingPipeline.state
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
from google.cloud import aiplatform_v1beta1
def sample_cancel_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_cancel_training_pipeline)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CancelTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline to cancel. Format: |
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

### create_pipeline_job

```
create_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CreatePipelineJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
pipeline_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.pipeline_job.PipelineJob
] = None,
pipeline_job_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.pipeline_job.PipelineJob
```


Creates a PipelineJob. A PipelineJob will run immediately when created.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreatePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePipelineJobRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_create_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CreatePipelineJob. |
`parent` |
`str`
Required. The resource name of the Location to create the PipelineJob in. Format: |
`pipeline_job` |
Required. The PipelineJob to create. This corresponds to the |
`pipeline_job_id` |
`str`
The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated. This value should be less than 128 characters, and valid characters are |
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
An instance of a machine learning PipelineJob. |

### create_training_pipeline

```
create_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CreateTrainingPipelineRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
training_pipeline: typing.Optional[
google.cloud.aiplatform_v1beta1.types.training_pipeline.TrainingPipeline
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.training_pipeline.TrainingPipeline
```


Creates a TrainingPipeline. A created TrainingPipeline right away will be attempted to be run.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
training_pipeline = aiplatform_v1beta1.[TrainingPipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrainingPipeline.html)()
training_pipeline.display_name = "display_name_value"
training_pipeline.training_task_definition = "training_task_definition_value"
training_pipeline.training_task_inputs.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[CreateTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTrainingPipelineRequest.html)(
parent="parent_value",
training_pipeline=training_pipeline,
)
# Make the request
response = client.[create_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_create_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CreateTrainingPipeline. |
`parent` |
`str`
Required. The resource name of the Location to create the TrainingPipeline in. Format: |
`training_pipeline` |
Required. The TrainingPipeline to create. This corresponds to the |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

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

### delete_pipeline_job

```
delete_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.DeletePipelineJobRequest,
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


Deletes a PipelineJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeletePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePipelineJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_delete_pipeline_job)(request=request)
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
The request object. Request message for PipelineService.DeletePipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob resource to be deleted. Format: |
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

### delete_training_pipeline

```
delete_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.DeleteTrainingPipelineRequest,
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


Deletes a TrainingPipeline.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_delete_training_pipeline)(request=request)
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
The request object. Request message for PipelineService.DeleteTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline resource to be deleted. Format: |
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

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### execution_path

```
execution_path(
project: str, location: str, metadata_store: str, execution: str
) -> str
```


Returns a fully-qualified execution string.

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
`PipelineServiceClient` |
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
`PipelineServiceClient` |
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
`PipelineServiceClient` |
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

### get_pipeline_job

```
get_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.GetPipelineJobRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.pipeline_job.PipelineJob
```


Gets a PipelineJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPipelineJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_get_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.GetPipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob resource. Format: |
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
An instance of a machine learning PipelineJob. |

### get_training_pipeline

```
get_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.GetTrainingPipelineRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.training_pipeline.TrainingPipeline
```


Gets a TrainingPipeline.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_get_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.GetTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline resource. Format: |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

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

### list_pipeline_jobs

```
list_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListPipelineJobsPager
)
```


Lists PipelineJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_list_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.ListPipelineJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the PipelineJobs from. Format: |
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
Response message for PipelineService.ListPipelineJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_training_pipelines

```
list_training_pipelines(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesRequest,
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
google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesPager
)
```


Lists TrainingPipelines in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_training_pipelines():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTrainingPipelinesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_training_pipelines](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_list_training_pipelines)(request=request)
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
The request object. Request message for PipelineService.ListTrainingPipelines. |
`parent` |
`str`
Required. The resource name of the Location to list the TrainingPipelines from. Format: |
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
Response message for PipelineService.ListTrainingPipelines Iterating over this object will yield results and resolve additional pages automatically. |

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### parse_artifact_path

`parse_artifact_path(path: str) -> typing.Dict[str, str]`


Parses a artifact path into its component segments.

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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_training_pipeline_path

`parse_training_pipeline_path(path: str) -> typing.Dict[str, str]`


Parses a training_pipeline path into its component segments.

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

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

### training_pipeline_path

`training_pipeline_path(project: str, location: str, training_pipeline: str) -> str`


Returns a fully-qualified training_pipeline string.

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
