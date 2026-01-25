---
merged_at: 2026-01-25T21:47:44.383479
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typesimageobject_df6eee.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typesimageobjectd_5e3585.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typesimageobjectde_fae4d2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typesimageobjectdet_a9c71f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typesimageobjectdete_c9c4f4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typesimageobjectdetec_fa9b0f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typesimageobjectdetect_b39aba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typesimageobjectdetectionpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageObjectDetectionPredictionInstance -->

# Class ImageObjectDetectionPredictionInstance (1.134.0)

```
ImageObjectDetectionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Object Detection.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The image bytes or Cloud Storage URI to make the prediction on. |
`mime_type` |
`str`
The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon |

## Methods

### ImageObjectDetectionPredictionInstance

```
ImageObjectDetectionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Object Detection.

### ImageObjectDetectionPredictionInstance

```
ImageObjectDetectionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Object Detection.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadtensorboardtimeseriesdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardTimeSeriesDataRequest -->

# Class ReadTensorboardTimeSeriesDataRequest (1.134.0)

```
ReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`max_data_points` |
`int`
The maximum number of TensorboardTimeSeries' data to return. This value should be a positive integer. This value can be set to -1 to return all data. |
`filter` |
`str`
Reads the TensorboardTimeSeries' data that match the filter expression. |

## Methods

### ReadTensorboardTimeSeriesDataRequest

```
ReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardTimeSeriesData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesannotation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Annotation -->

# Class Annotation (1.134.0)

`Annotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to assign specific AnnotationSpec to a particular area of a DataItem or the whole part of the DataItem.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the Annotation. |
`payload_schema_uri` |
`str`
Required. Google Cloud Storage URI points to a YAML file describing payload. The schema is defined as an `OpenAPI 3.0.2 Schema Object |
`payload` |
`google.protobuf.struct_pb2.Value`
Required. The schema of the payload can be found in payload_schema. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Annotation was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Annotation was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`annotation_source` |
Output only. The source of the Annotation. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your Annotations. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Annotation(System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each Annotation: - "aiplatform.googleapis.com/annotation_set_name": optional, name of the UI's annotation set this Annotation belongs to. If not set, the Annotation is not visible in the UI. - "aiplatform.googleapis.com/payload_schema": output only, its value is the [payload_schema's][google.cloud.aiplatform.v1beta1.Annotation.payload_schema_uri] title. |

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

### Annotation

`Annotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to assign specific AnnotationSpec to a particular area of a DataItem or the whole part of the DataItem.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployedmodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel -->

# Class DeployedModel (1.134.0)

`DeployedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of a Model. Endpoints contain one or more DeployedModels.

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
`dedicated_resources` |
A description of resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration. This field is a member of `oneof` _ `prediction_resources` .
|
`automatic_resources` |
A description of resources that to large degree are decided by Vertex AI, and require only a modest additional configuration. This field is a member of `oneof` _ `prediction_resources` .
|
`shared_resources` |
`str`
The resource name of the shared DeploymentResourcePool to deploy on. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
This field is a member of `oneof` _ `prediction_resources` .
|
`id` |
`str`
Immutable. The ID of the DeployedModel. If not provided upon deployment, Vertex AI will generate a value for this ID. This value should be 1-10 characters, and valid characters are `/[0-9]/` .
|
`model` |
`str`
The resource name of the Model that this is the deployment of. Note that the Model may be in a different location than the DeployedModel's Endpoint. The resource name may contain version id or version alias to specify the version. Example: `projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
if no version is specified, the default version will be
deployed.
|
`model_version_id` |
`str`
Output only. The version ID of the model that is deployed. |
`display_name` |
`str`
The display name of the DeployedModel. If not provided upon creation, the Model's display_name is used. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the DeployedModel was created. |
`explanation_spec` |
Explanation configuration for this DeployedModel. When deploying a Model using EndpointService.DeployModel, this value overrides the value of Model.explanation_spec. All fields of explanation_spec are optional in the request. If a field of explanation_spec is not populated, the value of the same field of Model.explanation_spec is inherited. If the corresponding Model.explanation_spec is not populated, all fields of the explanation_spec will be used for the explanation configuration. |
`disable_explanations` |
`bool`
If true, deploy the model without explainable feature, regardless the existence of Model.explanation_spec or explanation_spec. |
`service_account` |
`str`
The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project. Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service
account.
|
`disable_container_logging` |
`bool`
For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by
default. Please note that the logs incur cost, which are
subject to `Cloud Logging
pricing |
`enable_access_logging` |
`bool`
If true, online prediction access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each prediction request. Note that logs may incur a cost, especially if your project receives prediction requests at a high queries per second rate (QPS). Estimate your costs before enabling this option. |
`private_endpoints` |
Output only. Provide paths for users to send predict/explain/health requests directly to the deployed model services running on Cloud via private services access. This field is populated if network is configured. |
`faster_deployment_config` |
Configuration for faster model deployment. |
`status` |
Output only. Runtime status of the deployed model. |
`system_labels` |
`MutableMapping[str, str]`
System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only. |
`checkpoint_id` |
`str`
The checkpoint id of the model. |
`speculative_decoding_spec` |
Optional. Spec for configuring speculative decoding. |

## Classes

### Status

`Status(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime status of the deployed model.

### SystemLabelsEntry

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### DeployedModel

`DeployedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of a Model. Endpoints contain one or more DeployedModels.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesnasjoboutput_googlecloudaiplatform_v1typesl_4683e4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesnasjoboutput_googlecloudaiplatform_v1typeslo_2f373f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnasjoboutput_googlecloudaiplatform_v1typeslog_ccaa98.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnasjoboutput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobOutput -->

# Class NasJobOutput (1.134.0)

`NasJobOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a uCAIP NasJob output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`multi_trial_job_output` |
Output only. The output of this multi-trial Neural Architecture Search (NAS) job. This field is a member of `oneof` _ `output` .
|

## Classes

### MultiTrialJobOutput

`MultiTrialJobOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The output of a multi-trial Neural Architecture Search (NAS) jobs.

## Methods

### NasJobOutput

`NasJobOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a uCAIP NasJob output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslogprobsresultcandidate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LogprobsResult.Candidate -->

# Class Candidate (1.134.0)

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidate for the logprobs token and score.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`token` |
`str`
The candidate’s token string value. This field is a member of `oneof` _ `_token` .
|
`token_id` |
`int`
The candidate’s token id value. This field is a member of `oneof` _ `_token_id` .
|
`log_probability` |
`float`
The candidate's log probability. This field is a member of `oneof` _ `_log_probability` .
|

## Methods

### Candidate

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidate for the logprobs token and score.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespipelinetaskrerunconfiginputsparametervaluese_1339e7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinetaskrerunconfiginputsparametervaluesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskRerunConfig.Inputs.ParameterValuesEntry -->

# Class ParameterValuesEntry (1.134.0)

`ParameterValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### ParameterValuesEntry

`ParameterValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfigimportfeaturesanalysisstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis.State -->

# Class State (1.134.0)

`State(value)`


The state defines whether to enable ImportFeature analysis.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Should not be used. |
`DEFAULT` |
The default behavior of whether to enable the monitoring. EntityType-level config: disabled. Feature-level config: inherited from the configuration of EntityType this Feature belongs to. |
`ENABLED` |
Explicitly enables import features analysis. EntityType-level config: by default enables import features analysis for all Features under it. Feature-level config: enables import features analysis regardless of the EntityType-level config. |
`DISABLED` |
Explicitly disables import features analysis. EntityType-level config: by default disables import features analysis for all Features under it. Feature-level config: disables import features analysis regardless of the EntityType-level config. |

## Methods

### State

`State(value)`


The state defines whether to enable ImportFeature analysis.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployedindex.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndex -->

# Class DeployedIndex (1.134.0)

`DeployedIndex(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of an Index. IndexEndpoints contain one or more DeployedIndexes.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Required. The user specified ID of the DeployedIndex. The ID can be up to 128 characters long and must start with a letter and only contain letters, numbers, and underscores. The ID must be unique within the project it is created in. |
`index` |
`str`
Required. The name of the Index this is the deployment of. We may refer to this Index as the DeployedIndex's "original" Index. |
`display_name` |
`str`
The display name of the DeployedIndex. If not provided upon creation, the Index's display_name is used. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the DeployedIndex was created. |
`private_endpoints` |
Output only. Provides paths for users to send requests directly to the deployed index services running on Cloud via private services access. This field is populated if network is configured. |
`index_sync_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The DeployedIndex may depend on various data on its original Index. Additionally when certain changes to the original Index are being done (e.g. when what the Index contains is being changed) the DeployedIndex may be asynchronously updated in the background to reflect these changes. If this timestamp's value is at least the Index.update_time of the original Index, it means that this DeployedIndex and the original Index are in sync. If this timestamp is older, then to see which updates this DeployedIndex already contains (and which it does not), one must `list][google.longrunning.Operations.ListOperations]` the
operations that are running on the original Index. Only the
successfully completed Operations with
update_time
equal or before this sync time are contained in this
DeployedIndex.
|
`automatic_resources` |
Optional. A description of resources that the DeployedIndex uses, which to large degree are decided by Vertex AI, and optionally allows only a modest additional configuration. If min_replica_count is not set, the default value is 2 (we don't provide SLA when min_replica_count=1). If max_replica_count is not set, the default value is min_replica_count. The max allowed replica count is 1000. |
`dedicated_resources` |
Optional. A description of resources that are dedicated to the DeployedIndex, and that need a higher degree of manual configuration. The field min_replica_count must be set to a value strictly greater than 0, or else validation will fail. We don't provide SLA when min_replica_count=1. If max_replica_count is not set, the default value is min_replica_count. The max allowed replica count is 1000. Available machine types for SMALL shard: e2-standard-2 and all machine types available for MEDIUM and LARGE shard. Available machine types for MEDIUM shard: e2-standard-16 and all machine types available for LARGE shard. Available machine types for LARGE shard: e2-highmem-16, n2d-standard-32. n1-standard-16 and n1-standard-32 are still available, but we recommend e2-standard-16 and e2-highmem-16 for cost efficiency. |
`enable_access_logging` |
`bool`
Optional. If true, private endpoint's access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each MatchRequest. Note that logs may incur a cost, especially if the deployed index receives a high queries per second rate (QPS). Estimate your costs before enabling this option. |
`enable_datapoint_upsert_logging` |
`bool`
Optional. If true, logs to Cloud Logging errors relating to datapoint upserts. Under normal operation conditions, these log entries should be very rare. However, if incompatible datapoint updates are being uploaded to an index, a high volume of log entries may be generated in a short period of time. Note that logs may incur a cost, especially if the deployed index receives a high volume of datapoint upserts. Estimate your costs before enabling this option. |
`deployed_index_auth_config` |
Optional. If set, the authentication is enabled for the private endpoint. |
`reserved_ip_ranges` |
`MutableSequence[str]`
Optional. A list of reserved ip ranges under the VPC network that can be used for this DeployedIndex. If set, we will deploy the index within the provided ip ranges. Otherwise, the index might be deployed to any ip ranges under the provided VPC network. The value should be the name of the address (https://cloud.google.com/compute/docs/reference/rest/v1/addresses) Example: ['vertex-ai-ip-range']. For more information about subnets and network IP ranges, please see https://cloud.google.com/vpc/docs/subnets#manually_created_subnet_ip_ranges. |
`deployment_group` |
`str`
Optional. The deployment group can be no longer than 64 characters (eg: 'test', 'prod'). If not set, we will use the 'default' deployment group. Creating `deployment_groups` with `reserved_ip_ranges`
is a recommended practice when the peered network has
multiple peering ranges. This creates your deployments from
predictable IP spaces for easier traffic administration.
Also, one deployment_group (except 'default') can only be
used with the same reserved_ip_ranges which means if the
deployment_group has been used with reserved_ip_ranges: [a,
b, c], using it with [a, b] or [d, e] is disallowed.
Note: we only support up to 5 deployment groups(not
including 'default').
|
`psc_automation_configs` |
`MutableSequence[`
Optional. If set for PSC deployed index, PSC connection will be automatically created after deployment is done and the endpoint information is populated in private_endpoints.psc_automated_endpoints. |

## Methods

### DeployedIndex

`DeployedIndex(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of an Index. IndexEndpoints contain one or more DeployedIndexes.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelsasyncpager_googl_5d453b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelsasyncpager_google_e444ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelsasyncpager_googlec_7fadf1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelsAsyncPager -->

# Class ListModelsAsyncPager (1.134.0)

```
ListModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelsResponse,
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


A pager for iterating through `list_models`

requests.

This class thinly wraps an initial
[ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsResponse) object, and
provides an `__aiter__`

method to iterate through its
`models`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModels`

requests and continue to iterate
through the `models`

field on the
corresponding responses.

All the usual [ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelsAsyncPager

```
ListModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicepagerslistexecutionspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListExecutionsPager -->

# Class ListExecutionsPager (1.134.0)

```
ListExecutionsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse,
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


A pager for iterating through `list_executions`

requests.

This class thinly wraps an initial
[ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse) object, and
provides an `__iter__`

method to iterate through its
`executions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListExecutions`

requests and continue to iterate
through the `executions`

field on the
corresponding responses.

All the usual [ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListExecutionsPager

```
ListExecutionsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistmodelversioncheckpointsrequest_googlecloudaip_fa17e8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistmodelversioncheckpointsrequest_googlecloudaipl_a803e4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmodelversioncheckpointsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionCheckpointsRequest -->

# Class ListModelVersionCheckpointsRequest (1.134.0)

```
ListModelVersionCheckpointsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ListModelVersionCheckpoints.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the model version to list checkpoints for. `projects/{project}/locations/{location}/models/{model}@{version}`
Example:
`projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
If no version ID or alias is specified, the latest version
will be used.
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via next_page_token of the previous ListModelVersionCheckpoints call. |

## Methods

### ListModelVersionCheckpointsRequest

```
ListModelVersionCheckpointsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ListModelVersionCheckpoints.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesjirasourcejiraqueries.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.JiraSource.JiraQueries -->

# Class JiraQueries (1.134.0)

`JiraQueries(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


JiraQueries contains the Jira queries and corresponding authentication.

## Attributes |
|
|---|---|
Name |
Description |
`projects` |
`MutableSequence[str]`
A list of Jira projects to import in their entirety. |
`custom_queries` |
`MutableSequence[str]`
A list of custom Jira queries to import. For information about JQL (Jira Query Language), see https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/ |
`email` |
`str`
Required. The Jira email address. |
`server_uri` |
`str`
Required. The Jira server URI. |
`api_key_config` |
Required. The SecretManager secret version resource name (e.g. projects/{project}/secrets/{secret}/versions/{version}) storing the Jira API key. See `Manage API tokens for your Atlassian account |

## Methods

### JiraQueries

`JiraQueries(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


JiraQueries contains the Jira queries and corresponding authentication.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeaturestore_servicepagerslistfeaturespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturesPager -->

# Class ListFeaturesPager (1.134.0)

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
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


A pager for iterating through `list_features`

requests.

This class thinly wraps an initial
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesResponse) object, and
provides an `__iter__`

method to iterate through its
`features`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturesPager

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesjob_servicepagerslistnasjobsasyncpager_googlec_39bf9b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesjob_servicepagerslistnasjobsasyncpager_googlecl_d35a09.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslistnasjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasJobsAsyncPager -->

# Class ListNasJobsAsyncPager (1.134.0)

```
ListNasJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse,
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


A pager for iterating through `list_nas_jobs`

requests.

This class thinly wraps an initial
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`nas_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNasJobs`

requests and continue to iterate
through the `nas_jobs`

field on the
corresponding responses.

All the usual [ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNasJobsAsyncPager

```
ListNasJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistcontextspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListContextsPager -->

# Class ListContextsPager (1.134.0)

```
ListContextsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse,
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


A pager for iterating through `list_contexts`

requests.

This class thinly wraps an initial
[ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListContextsResponse) object, and
provides an `__iter__`

method to iterate through its
`contexts`

field.

If there are more pages, the `__iter__`

method will make additional
`ListContexts`

requests and continue to iterate
through the `contexts`

field on the
corresponding responses.

All the usual [ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListContextsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListContextsPager

```
ListContextsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistartifactsrequest_googlecloudaiplatform_v1types_6f9e34.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistartifactsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsRequest -->

# Class ListArtifactsRequest (1.134.0)

`ListArtifactsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListArtifacts.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The MetadataStore whose Artifacts should be listed. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`page_size` |
`int`
The maximum number of Artifacts to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListArtifacts call. Provide this to retrieve the subsequent page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID_ARGUMENT error.) |
`filter` |
`str`
Filter specifying the boolean condition for the Artifacts to satisfy in order to be part of the result set. The syntax to define filter query is based on https://google.aip.dev/160. The supported set of filters include the following: - **Attribute filtering**: For example: `display_name = "test"` . Supported fields include:
`name` , `display_name` , `uri` , `state` ,
`schema_title` , `create_time` , and `update_time` .
Time fields, such as `create_time` and `update_time` ,
require values specified in RFC-3339 format. For example:
`create_time = "2020-11-19T11:30:00-04:00"`
- **Metadata field**: To filter on metadata fields use
traversal operation as follows:
`metadata.` . For example:
`metadata.field_1.number_value = 10.0` In case the field
name contains special characters (such as colon), one can
embed it inside double quote. For example:
`metadata."field:1".number_value = 10.0`
- **Context based filtering**: To filter Artifacts based on
the contexts to which they belong, use the function
operator with the full resource name
`in_context(` . For example:
`in_context("projects/`
Each of the above supported filter types can be combined
together using logical operators (`AND` & `OR` ). Maximum
nested expression depth allowed is 5.
For example:
`display_name = "test" AND metadata.field1.bool_value = true` .
|
`order_by` |
`str`
How the list of messages is ordered. Specify the values to order by and an ordering operation. The default sorting order is ascending. To specify descending order for a field, users append a " desc" suffix; for example: "foo desc, bar". Subfields are specified with a `.` character, such as
foo.bar. see https://google.aip.dev/132#ordering for more
details.
|

## Methods

### ListArtifactsRequest

`ListArtifactsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListArtifacts.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnasjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJob -->

# Class NasJob (1.134.0)

`NasJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a Neural Architecture Search (NAS) job.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the NasJob. |
`display_name` |
`str`
Required. The display name of the NasJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`nas_job_spec` |
Required. The specification of a NasJob. |
`nas_job_output` |
Output only. Output of the NasJob. |
`state` |
Output only. The detailed state of the job. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the NasJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the NasJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the NasJob entered any of the following states: `JOB_STATE_SUCCEEDED` ,
`JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the NasJob was most recently updated. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when job's state is JOB_STATE_FAILED or JOB_STATE_CANCELLED. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize NasJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key options for a NasJob. If this is set, then all resources created by the NasJob will be encrypted with the provided encryption key. |
`enable_restricted_image_training` |
`bool`
Optional. Enable a separation of Custom model training and restricted image training for tenant project. |
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

### NasJob

`NasJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a Neural Architecture Search (NAS) job.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecdeveloperconn_cfa54a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecdeveloperconne_d78893.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecdeveloperconnec_cf9db7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecdeveloperconnect_503576.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecdeveloperconnectc_0073f4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecdeveloperconnectconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.SourceCodeSpec.DeveloperConnectConfig -->

# Class DeveloperConnectConfig (1.134.0)

`DeveloperConnectConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the configuration for fetching source code from a Git repository that is managed by Developer Connect. This includes the repository, revision, and directory to use.

## Attributes |
|
|---|---|
Name |
Description |
`git_repository_link` |
`str`
Required. The Developer Connect Git repository link, formatted as `projects/*/locations/*/connections/*/gitRepositoryLink/*` .
|
`dir_` |
`str`
Required. Directory, relative to the source root, in which to run the build. |
`revision` |
`str`
Required. The revision to fetch from the Git repository such as a branch, a tag, a commit SHA, or any Git ref. |

## Methods

### DeveloperConnectConfig

`DeveloperConnectConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the configuration for fetching source code from a Git repository that is managed by Developer Connect. This includes the repository, revision, and directory to use.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescometspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CometSpec -->

# Class CometSpec (1.134.0)

`CometSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`version` |
Required. Which version to use for evaluation. This field is a member of `oneof` _ `_version` .
|
`source_language` |
`str`
Optional. Source language in BCP-47 format. |
`target_language` |
`str`
Optional. Target language in BCP-47 format. Covers both prediction and reference. |

## Classes

### CometVersion

`CometVersion(value)`


Comet version options.

## Methods

### CometSpec

`CometSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicessession_servicepagerslistsessionspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListSessionsPager -->

# Class ListSessionsPager (1.134.0)

```
ListSessionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
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


A pager for iterating through `list_sessions`

requests.

This class thinly wraps an initial
[ListSessionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse) object, and
provides an `__iter__`

method to iterate through its
`sessions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSessions`

requests and continue to iterate
through the `sessions`

field on the
corresponding responses.

All the usual [ListSessionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSessionsPager

```
ListSessionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespublishermodelcalltoactionregionalresourcereferen_e37392.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespublishermodelcalltoactionregionalresourcereferenc_587b91.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespublishermodelcalltoactionregionalresourcereferencesreferencesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.RegionalResourceReferences.ReferencesEntry -->

# Class ReferencesEntry (1.134.0)

`ReferencesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### ReferencesEntry

`ReferencesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typesimageclassificationpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageClassificationPredictionInstance -->

# Class ImageClassificationPredictionInstance (1.134.0)

```
ImageClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Classification.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The image bytes or Cloud Storage URI to make the prediction on. |
`mime_type` |
`str`
The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon |

## Methods

### ImageClassificationPredictionInstance

```
ImageClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Classification.

### ImageClassificationPredictionInstance

```
ImageClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Classification.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistdatasetspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetsPager -->

# Class ListDatasetsPager (1.134.0)

```
ListDatasetsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse,
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


A pager for iterating through `list_datasets`

requests.

This class thinly wraps an initial
[ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsResponse) object, and
provides an `__iter__`

method to iterate through its
`datasets`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDatasets`

requests and continue to iterate
through the `datasets`

field on the
corresponding responses.

All the usual [ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDatasetsPager

```
ListDatasetsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesdataset_servicepagerslistannotationspager_goog_a66d3b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdataset_servicepagerslistannotationspager_googl_a14e00.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerslistannotationspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListAnnotationsPager -->

# Class ListAnnotationsPager (1.134.0)

```
ListAnnotationsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse,
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


A pager for iterating through `list_annotations`

requests.

This class thinly wraps an initial
[ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse) object, and
provides an `__iter__`

method to iterate through its
`annotations`

field.

If there are more pages, the `__iter__`

method will make additional
`ListAnnotations`

requests and continue to iterate
through the `annotations`

field on the
corresponding responses.

All the usual [ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListAnnotationsPager

```
ListAnnotationsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslistcustomjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListCustomJobsPager -->

# Class ListCustomJobsPager (1.134.0)

```
ListCustomJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse,
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


A pager for iterating through `list_custom_jobs`

requests.

This class thinly wraps an initial
[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`custom_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListCustomJobs`

requests and continue to iterate
through the `custom_jobs`

field on the
corresponding responses.

All the usual [ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListCustomJobsPager

```
ListCustomJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslogprobsresultcandidate_googlecloudaiplatfor_c6f972.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslogprobsresultcandidate_googlecloudaiplatform_1693ae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslogprobsresultcandidate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LogprobsResult.Candidate -->

# Class Candidate (1.134.0)

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidate for the logprobs token and score.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`token` |
`str`
The candidate’s token string value. This field is a member of `oneof` _ `_token` .
|
`token_id` |
`int`
The candidate’s token id value. This field is a member of `oneof` _ `_token_id` .
|
`log_probability` |
`float`
The candidate's log probability. This field is a member of `oneof` _ `_log_probability` .
|

## Methods

### Candidate

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidate for the logprobs token and score.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfunctioncall.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionCall -->

# Class FunctionCall (1.134.0)

`FunctionCall(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing the parameters and their values.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Optional. The unique id of the function call. If populated, the client to execute the `function_call` and return the
response with the matching `id` .
|
`name` |
`str`
Required. The name of the function to call. Matches [FunctionDeclaration.name]. |
`args` |
`google.protobuf.struct_pb2.Struct`
Optional. Required. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details. |

## Methods

### FunctionCall

`FunctionCall(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing the parameters and their values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvizier_servicepagerslisttrialsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsAsyncPager -->

# Class ListTrialsAsyncPager (1.134.0)

```
ListTrialsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse) object, and
provides an `__aiter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTrials`

requests and continue to iterate
through the `trials`

field on the
corresponding responses.

All the usual [ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTrialsAsyncPager

```
ListTrialsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typespublishermodelcalltoactionregionalresource_208996.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typespublishermodelcalltoactionregionalresourcer_7db79f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespublishermodelcalltoactionregionalresourcere_8d24af.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespublishermodelcalltoactionregionalresourceref_c2da8f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelcalltoactionregionalresourcereferencesreferencesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.RegionalResourceReferences.ReferencesEntry -->

# Class ReferencesEntry (1.134.0)

`ReferencesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### ReferencesEntry

`ReferencesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningenginespecdeploymentspecresourcelimitsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.DeploymentSpec.ResourceLimitsEntry -->

# Class ResourceLimitsEntry (1.134.0)

`ResourceLimitsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### ResourceLimitsEntry

`ResourceLimitsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnearestneighborsearchoperationmetadatacontent_dae8a7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnearestneighborsearchoperationmetadatacontentvalidationstats.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborSearchOperationMetadata.ContentValidationStats -->

# Class ContentValidationStats (1.134.0)

`ContentValidationStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`source_gcs_uri` |
`str`
Cloud Storage URI pointing to the original file in user's bucket. |
`valid_record_count` |
`int`
Number of records in this file that were successfully processed. |
`invalid_record_count` |
`int`
Number of records in this file we skipped due to validate errors. |
`partial_errors` |
`MutableSequence[`
The detail information of the partial failures encountered for those invalid records that couldn't be parsed. Up to 50 partial errors will be reported. |
`valid_sparse_record_count` |
`int`
Number of sparse records in this file that were successfully processed. |
`invalid_sparse_record_count` |
`int`
Number of sparse records in this file we skipped due to validate errors. |

## Methods

### ContentValidationStats

`ContentValidationStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictprediction_v1typestabularclassificationpredictionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TabularClassificationPredictionResult -->

# Class TabularClassificationPredictionResult (1.134.0)

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.

## Attributes |
|
|---|---|
Name |
Description |
`classes` |
`MutableSequence[str]`
The name of the classes being classified, contains all possible values of the target column. |
`scores` |
`MutableSequence[float]`
The model's confidence in each class being correct, higher value means higher confidence. The N-th score corresponds to the N-th class in classes. |

## Methods

### TabularClassificationPredictionResult

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.

### TabularClassificationPredictionResult

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesragembeddingmodelconfigvertexpredictionendpo_6ab4bb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragembeddingmodelconfigvertexpredictionendpoi_a0cbd1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragembeddingmodelconfigvertexpredictionendpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagEmbeddingModelConfig.VertexPredictionEndpoint -->

# Class VertexPredictionEndpoint (1.134.0)

`VertexPredictionEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config representing a model hosted on Vertex Prediction Endpoint.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The endpoint resource name. Format: `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}`
or
`projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`model` |
`str`
Output only. The resource name of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model. Pattern: `projects/{project}/locations/{location}/models/{model}`
|
`model_version_id` |
`str`
Output only. Version ID of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model. |

## Methods

### VertexPredictionEndpoint

`VertexPredictionEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config representing a model hosted on Vertex Prediction Endpoint.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesruntimeconfigcodeinterpreterruntimeconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeConfig.CodeInterpreterRuntimeConfig -->

# Class CodeInterpreterRuntimeConfig (1.134.0)

```
CodeInterpreterRuntimeConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`file_input_gcs_bucket` |
`str`
Optional. The Cloud Storage bucket for file input of this Extension. If specified, support input from the Cloud Storage bucket. Vertex Extension Custom Code Service Agent should be granted file reader to this bucket. If not specified, the extension will only accept file contents from request body and reject Cloud Storage file inputs. |
`file_output_gcs_bucket` |
`str`
Optional. The Cloud Storage bucket for file output of this Extension. If specified, write all output files to the Cloud Storage bucket. Vertex Extension Custom Code Service Agent should be granted file writer to this bucket. If not specified, the file content will be output in response body. |

## Methods

### CodeInterpreterRuntimeConfig

```
CodeInterpreterRuntimeConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmetricxspec_googlecloudaiplatform_v1beta1typesmode_0e877b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmetricxspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetricxSpec -->

# Class MetricxSpec (1.134.0)

`MetricxSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`version` |
Required. Which version to use for evaluation. This field is a member of `oneof` _ `_version` .
|
`source_language` |
`str`
Optional. Source language in BCP-47 format. |
`target_language` |
`str`
Optional. Target language in BCP-47 format. Covers both prediction and reference. |

## Classes

### MetricxVersion

`MetricxVersion(value)`


MetricX Version options.

## Methods

### MetricxSpec

`MetricxSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringnotificationspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringNotificationSpec -->

# Class ModelMonitoringNotificationSpec (1.134.0)

```
ModelMonitoringNotificationSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Notification spec(email, notification channel) for model monitoring statistics/alerts.

## Attributes |
|
|---|---|
Name |
Description |
`email_config` |
Email alert config. |
`enable_cloud_logging` |
`bool`
Dump the anomalies to Cloud Logging. The anomalies will be put to json payload encoded from proto [
|
`notification_channel_configs` |
`MutableSequence[`
Notification channel config. |

## Classes

### EmailConfig

`EmailConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alerts.

### NotificationChannelConfig

`NotificationChannelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Google Cloud Notification Channel config.

## Methods

### ModelMonitoringNotificationSpec

```
ModelMonitoringNotificationSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Notification spec(email, notification channel) for model monitoring statistics/alerts.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelversionspager_goog_4dbd2c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelversionspager_googl_1a3ec9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelversionspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelVersionsPager -->

# Class ListModelVersionsPager (1.134.0)

```
ListModelVersionsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse,
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


A pager for iterating through `list_model_versions`

requests.

This class thinly wraps an initial
[ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionsResponse) object, and
provides an `__iter__`

method to iterate through its
`models`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelVersions`

requests and continue to iterate
through the `models`

field on the
corresponding responses.

All the usual [ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionsPager

```
ListModelVersionsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistdataitemspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDataItemsPager -->

# Class ListDataItemsPager (1.134.0)

```
ListDataItemsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse,
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


A pager for iterating through `list_data_items`

requests.

This class thinly wraps an initial
[ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsResponse) object, and
provides an `__iter__`

method to iterate through its
`data_items`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDataItems`

requests and continue to iterate
through the `data_items`

field on the
corresponding responses.

All the usual [ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDataItemsPager

```
ListDataItemsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistexecutionsrequest_googlecloudaiplatform_v1serv_bcae0d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistexecutionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsRequest -->

# Class ListExecutionsRequest (1.134.0)

`ListExecutionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The MetadataStore whose Executions should be listed. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`page_size` |
`int`
The maximum number of Executions to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListExecutions call. Provide this to retrieve the subsequent page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with an INVALID_ARGUMENT error.) |
`filter` |
`str`
Filter specifying the boolean condition for the Executions to satisfy in order to be part of the result set. The syntax to define filter query is based on https://google.aip.dev/160. Following are the supported set of filters: - **Attribute filtering**: For example: `display_name = "test"` . Supported fields include:
`name` , `display_name` , `state` , `schema_title` ,
`create_time` , and `update_time` . Time fields, such as
`create_time` and `update_time` , require values
specified in RFC-3339 format. For example:
`create_time = "2020-11-19T11:30:00-04:00"` .
- **Metadata field**: To filter on metadata fields use
traversal operation as follows:
`metadata.` For example:
`metadata.field_1.number_value = 10.0` In case the field
name contains special characters (such as colon), one can
embed it inside double quote. For example:
`metadata."field:1".number_value = 10.0`
- **Context based filtering**: To filter Executions based on
the contexts to which they belong use the function
operator with the full resource name:
`in_context(` . For example:
`in_context("projects/`
Each of the above supported filters can be combined together
using logical operators (`AND` & `OR` ). Maximum nested
expression depth allowed is 5.
For example:
`display_name = "test" AND metadata.field1.bool_value = true` .
|
`order_by` |
`str`
How the list of messages is ordered. Specify the values to order by and an ordering operation. The default sorting order is ascending. To specify descending order for a field, users append a " desc" suffix; for example: "foo desc, bar". Subfields are specified with a `.` character, such as
foo.bar. see https://google.aip.dev/132#ordering for more
details.
|

## Methods

### ListExecutionsRequest

`ListExecutionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListExecutions.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesgen_ai_tuning_servicepagerslisttuningjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers.ListTuningJobsPager -->

# Class ListTuningJobsPager (1.134.0)

```
ListTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse,
],
request: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse,
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


A pager for iterating through `list_tuning_jobs`

requests.

This class thinly wraps an initial
[ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`tuning_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTuningJobs`

requests and continue to iterate
through the `tuning_jobs`

field on the
corresponding responses.

All the usual [ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTuningJobsPager

```
ListTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse,
],
request: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformartifact____googlecloudaiplatformv1beta1schemapredictpre_22cea4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformartifact____googlecloudaiplatformv1beta1schemapredictpred_aa3999.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformartifact____googlecloudaiplatformv1beta1schemapredictpredi_49c3a0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformartifact.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Artifact -->

# Class Artifact (1.134.0)

```
Artifact(
artifact_name: str,
*,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
)
```


Metadata Artifact resource for Vertex AI

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

### lineage_console_uri

Cloud console uri to view this Artifact Lineage.

### name

Name of this resource.

### resource_name

Full qualified resource name.

### state

The State for this Artifact.

### update_time

Time this resource was last updated.

### uri

Uri for this Artifact.

## Methods

### Artifact

```
Artifact(
artifact_name: str,
*,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
)
```


Retrieves an existing Metadata Artifact given a resource name or ID.

Parameters |
|
|---|---|
Name |
Description |
`artifact_name` |
`str`
Required. A fully-qualified resource name or resource ID of the Artifact. Example: "projects/123/locations/us-central1/metadataStores/default/artifacts/my-resource". or "my-resource" when project and location are initialized or passed. |
`metadata_store_id` |
`str`
Optional. MetadataStore to retrieve Artifact from. If not set, metadata_store_id is set to "default". If artifact_name is a fully-qualified resource, its metadata_store_id overrides this one. |
`project` |
`str`
Optional. Project to retrieve the artifact from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve the Artifact from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Artifact. Overrides credentials set in aiplatform.init. |

### create

```
create(
schema_title: str,
*,
resource_id: typing.Optional[str] = None,
uri: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
schema_version: typing.Optional[str] = None,
description: typing.Optional[str] = None,
metadata: typing.Optional[typing.Dict] = None,
state: google.cloud.aiplatform_v1.types.artifact.Artifact.State = State.LIVE,
metadata_store_id: typing.Optional[str] = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
) -> google.cloud.aiplatform.metadata.artifact.Artifact
```


Creates a new Metadata Artifact.

Parameters |
|
|---|---|
Name |
Description |
`schema_title` |
`str`
Required. schema_title identifies the schema title used by the Artifact. Please reference |
`resource_id` |
`str`
Optional. The <resource_id> portion of the Artifact name with the format. This is globally unique in a metadataStore: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id>. |
`uri` |
`str`
Optional. The uniform resource identifier of the artifact file. May be empty if there is no actual artifact file. |
`display_name` |
`str`
Optional. The user-defined name of the Artifact. |
`schema_version` |
`str`
Optional. schema_version specifies the version used by the Artifact. If not set, defaults to use the latest version. |
`description` |
`str`
Optional. Describes the purpose of the Artifact to be created. |
`metadata` |
`Dict`
Optional. Contains the metadata information that will be stored in the Artifact. |
`state` |
`google.cloud.gapic.types.Artifact.State`
Optional. The state of this Artifact. This is a property of the Artifact, and does not imply or capture any ongoing process. This property is managed by clients (such as Vertex AI Pipelines), and the system does not prescribe or check the validity of state transitions. |
`metadata_store_id` |
`str`
Optional. The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Optional. Project used to create this Artifact. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location used to create this Artifact. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials used to create this Artifact. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`Artifact` |
Instantiated representation of the managed Metadata Artifact. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### get

```
get(
resource_id: str,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.metadata.resource._Resource
```


Retrieves a Metadata resource.

Parameters |
|
|---|---|
Name |
Description |
`resource_id` |
`str`
Required. The <resource_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id>. |
`metadata_store_id` |
`str`
The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Project used to retrieve or create this resource. Overrides project set in aiplatform.init. |
`location` |
`str`
Location used to retrieve or create this resource. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials used to retrieve or create this resource. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`resource (_Resource)` |
Instantiated representation of the managed Metadata resource or None if no resource was found. |

### get_or_create

```
get_or_create(
resource_id: str,
schema_title: str,
display_name: typing.Optional[str] = None,
schema_version: typing.Optional[str] = None,
description: typing.Optional[str] = None,
metadata: typing.Optional[typing.Dict] = None,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.metadata.resource._Resource
```


Retrieves or Creates (if it does not exist) a Metadata resource.

Parameters |
|
|---|---|
Name |
Description |
`resource_id` |
`str`
Required. The <resource_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id>. |
`schema_title` |
`str`
Required. schema_title identifies the schema title used by the resource. |
`display_name` |
`str`
Optional. The user-defined name of the resource. |
`schema_version` |
`str`
Optional. schema_version specifies the version used by the resource. If not set, defaults to use the latest version. |
`description` |
`str`
Optional. Describes the purpose of the resource to be created. |
`metadata` |
`Dict`
Optional. Contains the metadata information that will be stored in the resource. |
`metadata_store_id` |
`str`
The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Project used to retrieve or create this resource. Overrides project set in aiplatform.init. |
`location` |
`str`
Location used to retrieve or create this resource. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials used to retrieve or create this resource. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`resource (_Resource)` |
Instantiated representation of the managed Metadata resource. |

### get_with_uri

```
get_with_uri(
uri: str,
*,
metadata_store_id: typing.Optional[str] = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
) -> google.cloud.aiplatform.metadata.artifact.Artifact
```


Get an Artifact by it's uri.

If more than one Artifact with this uri is in the metadata store then the Artifact with the latest create_time is returned.

Parameters |
|
|---|---|
Name |
Description |
`uri` |
`str`
Required. Uri of the Artifact to retrieve. |
`metadata_store_id` |
`str`
Optional. MetadataStore to retrieve Artifact from. If not set, metadata_store_id is set to "default". If artifact_name is a fully-qualified resource, its metadata_store_id overrides this one. |
`project` |
`str`
Optional. Project to retrieve the artifact from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve the Artifact from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Artifact. Overrides credentials set in aiplatform.init. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If no Artifact exists with the provided uri. |

Returns |
|
|---|---|
Type |
Description |
`Artifact` |
Artifact with given uri. |

### list

```
list(
filter: typing.Optional[str] = None,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
order_by: typing.Optional[str] = None,
) -> typing.List[google.cloud.aiplatform.metadata.resource._Resource]
```


List resources that match the list filter in target metadataStore.

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. A query to filter available resources for matching results. |
`metadata_store_id` |
`str`
The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Project used to create this resource. Overrides project set in aiplatform.init. |
`location` |
`str`
Location used to create this resource. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials used to create this resource. Overrides credentials set in aiplatform.init. |
`order_by` |
`str`
Optional. How the list of messages is ordered. Specify the values to order by and an ordering operation. The default sorting order is ascending. To specify descending order for a field, users append a " desc" suffix; for example: "foo desc, bar". Subfields are specified with a |

Returns |
|
|---|---|
Type |
Description |
`resources (sequence[_Resource])` |
a list of managed Metadata resource. |

### sync_resource

`sync_resource()`


Syncs local resource with the resource in metadata store.

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
metadata: typing.Optional[typing.Dict] = None,
description: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
location: typing.Optional[str] = None,
)
```


Updates an existing Metadata resource with new metadata.

Parameters |
|
|---|---|
Name |
Description |
`metadata` |
`Dict`
Optional. metadata contains the updated metadata information. |
`description` |
`str`
Optional. Description describes the resource to be updated. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to update this resource. Overrides credentials set in aiplatform.init. |

### wait

`wait()`


Helper method that blocks until all futures are complete.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typestabularclassi_582c76.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typestabularclassif_42a76d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typestabularclassifi_c701c5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typestabularclassificationpredictionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TabularClassificationPredictionResult -->

# Class TabularClassificationPredictionResult (1.134.0)

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.

## Attributes |
|
|---|---|
Name |
Description |
`classes` |
`MutableSequence[str]`
The name of the classes being classified, contains all possible values of the target column. |
`scores` |
`MutableSequence[float]`
The model's confidence in each class being correct, higher value means higher confidence. The N-th score corresponds to the N-th class in classes. |

## Methods

### TabularClassificationPredictionResult

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.

### TabularClassificationPredictionResult

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragembeddingmodelconfigvertexpredictionendpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagEmbeddingModelConfig.VertexPredictionEndpoint -->

# Class VertexPredictionEndpoint (1.134.0)

`VertexPredictionEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config representing a model hosted on Vertex Prediction Endpoint.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The endpoint resource name. Format: `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}`
or
`projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`model` |
`str`
Output only. The resource name of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model. Pattern: `projects/{project}/locations/{location}/models/{model}`
|
`model_version_id` |
`str`
Output only. Version ID of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model. |

## Methods

### VertexPredictionEndpoint

`VertexPredictionEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config representing a model hosted on Vertex Prediction Endpoint.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmetricxspec_googlecloudaiplatform_v1typesragf_fe2915.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmetricxspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxSpec -->

# Class MetricxSpec (1.134.0)

`MetricxSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`version` |
Required. Which version to use for evaluation. This field is a member of `oneof` _ `_version` .
|
`source_language` |
`str`
Optional. Source language in BCP-47 format. |
`target_language` |
`str`
Optional. Target language in BCP-47 format. Covers both prediction and reference. |

## Classes

### MetricxVersion

`MetricxVersion(value)`


MetricX Version options.

## Methods

### MetricxSpec

`MetricxSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragfileparsingconfiglayoutparser.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagFileParsingConfig.LayoutParser -->

# Class LayoutParser (1.134.0)

`LayoutParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Document AI Layout Parser config.

## Attributes |
|
|---|---|
Name |
Description |
`processor_name` |
`str`
The full resource name of a Document AI processor or processor version. The processor must have type `LAYOUT_PARSER_PROCESSOR` . If specified, the
`additional_config.parse_as_scanned_pdf` field must be
false. Format:
- `projects/{project_id}/locations/{location}/processors/{processor_id}`
- `projects/{project_id}/locations/{location}/processors/{processor_id}/processorVersions/{processor_version_id}`
|
`max_parsing_requests_per_min` |
`int`
The maximum number of requests the job is allowed to make to the Document AI processor per minute. Consult https://cloud.google.com/document-ai/quotas and the Quota page for your project to set an appropriate value here. If unspecified, a default value of 120 QPM would be used. |

## Methods

### LayoutParser

`LayoutParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Document AI Layout Parser config.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1beta1schemapredictparams_v1beta1typesimageclassificatio_0bb9d4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictparams_v1beta1typesimageclassification_621c9d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictparams_v1beta1typesimageclassificationpredictionparams.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.ImageClassificationPredictionParams -->

# Class ImageClassificationPredictionParams (1.134.0)

```
ImageClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Classification.

## Attributes |
|
|---|---|
Name |
Description |
`confidence_threshold` |
`float`
The Model only returns predictions with at least this confidence score. Default value is 0.0 |
`max_predictions` |
`int`
The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10. |

## Methods

### ImageClassificationPredictionParams

```
ImageClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Classification.

### ImageClassificationPredictionParams

```
ImageClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Classification.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmigrateresourcerequestmigratemlenginemodelversionconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest.MigrateMlEngineModelVersionConfig -->

# Class MigrateMlEngineModelVersionConfig (1.134.0)

```
MigrateMlEngineModelVersionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating version in ml.googleapis.com to Vertex AI's Model.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The ml.googleapis.com endpoint that this model version should be migrated from. Example values: - ml.googleapis.com - us-centrall-ml.googleapis.com - europe-west4-ml.googleapis.com - asia-east1-ml.googleapis.com |
`model_version` |
`str`
Required. Full resource name of ml engine model version. Format: `projects/{project}/models/{model}/versions/{version}` .
|
`model_display_name` |
`str`
Required. Display name of the model in Vertex AI. System will pick a display name if unspecified. |

## Methods

### MigrateMlEngineModelVersionConfig

```
MigrateMlEngineModelVersionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating version in ml.googleapis.com to Vertex AI's Model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelevaluation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelEvaluation -->

# Class ModelEvaluation (1.134.0)

`ModelEvaluation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of metrics calculated by comparing Model's predictions on all of the test data against annotations from the test data.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the ModelEvaluation. |
`display_name` |
`str`
The display name of the ModelEvaluation. |
`metrics_schema_uri` |
`str`
Points to a YAML file stored on Google Cloud Storage describing the metrics of this ModelEvaluation. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metrics` |
`google.protobuf.struct_pb2.Value`
Evaluation metrics of the Model. The schema of the metrics is stored in metrics_schema_uri |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelEvaluation was created. |
`slice_dimensions` |
`MutableSequence[str]`
All possible dimensions of ModelEvaluationSlices. The dimensions can be used as the filter of the ModelService.ListModelEvaluationSlices request, in the form of `slice.dimension = ` .
|
`data_item_schema_uri` |
`str`
Points to a YAML file stored on Google Cloud Storage describing [EvaluatedDataItemView.data_item_payload][] and EvaluatedAnnotation.data_item_payload. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`annotation_schema_uri` |
`str`
Points to a YAML file stored on Google Cloud Storage describing [EvaluatedDataItemView.predictions][], [EvaluatedDataItemView.ground_truths][], EvaluatedAnnotation.predictions, and EvaluatedAnnotation.ground_truths. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`model_explanation` |
Aggregated explanation metrics for the Model's prediction output over the data this ModelEvaluation uses. This field is populated only if the Model is evaluated with explanations, and only for AutoML tabular Models. |
`explanation_specs` |
`MutableSequence[`
Describes the values of ExplanationSpec that are used for explaining the predicted values on the evaluated data. |
`metadata` |
`google.protobuf.struct_pb2.Value`
The metadata of the ModelEvaluation. For the ModelEvaluation uploaded from Managed Pipeline, metadata contains a structured value with keys of "pipeline_job_id", "evaluation_dataset_type", "evaluation_dataset_path", "row_based_metrics_path". |

## Classes

### ModelEvaluationExplanationSpec

```
ModelEvaluationExplanationSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Methods

### ModelEvaluation

`ModelEvaluation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of metrics calculated by comparing Model's predictions on all of the test data against annotations from the test data.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesindex_servicepagerslistindexesasyncpager__goo_62c4c1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesindex_servicepagerslistindexesasyncpager__goog_9e658d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesindex_servicepagerslistindexesasyncpager__googl_e90058.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesindex_servicepagerslistindexesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.pagers.ListIndexesAsyncPager -->

# Class ListIndexesAsyncPager (1.134.0)

```
ListIndexesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse
],
],
request: google.cloud.aiplatform_v1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse,
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


A pager for iterating through `list_indexes`

requests.

This class thinly wraps an initial
[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesResponse) object, and
provides an `__aiter__`

method to iterate through its
`indexes`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListIndexes`

requests and continue to iterate
through the `indexes`

field on the
corresponding responses.

All the usual [ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListIndexesAsyncPager

```
ListIndexesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse
],
],
request: google.cloud.aiplatform_v1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesexportevalu_fad8c0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesexportevaluateddataitemsconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.ExportEvaluatedDataItemsConfig -->

# Class ExportEvaluatedDataItemsConfig (1.134.0)

```
ExportEvaluatedDataItemsConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for exporting test set predictions to a BigQuery table.

## Attributes |
|
|---|---|
Name |
Description |
`destination_bigquery_uri` |
`str`
URI of desired destination BigQuery table. Expected format: bq:// |
`override_existing_table` |
`bool`
If true and an export destination is specified, then the contents of the destination are overwritten. Otherwise, if the export destination already exists, then the export operation fails. |

## Methods

### ExportEvaluatedDataItemsConfig

```
ExportEvaluatedDataItemsConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for exporting test set predictions to a BigQuery table.

### ExportEvaluatedDataItemsConfig

```
ExportEvaluatedDataItemsConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for exporting test set predictions to a BigQuery table.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnasjoboutput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJobOutput -->

# Class NasJobOutput (1.134.0)

`NasJobOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a uCAIP NasJob output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`multi_trial_job_output` |
Output only. The output of this multi-trial Neural Architecture Search (NAS) job. This field is a member of `oneof` _ `output` .
|

## Classes

### MultiTrialJobOutput

`MultiTrialJobOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The output of a multi-trial Neural Architecture Search (NAS) jobs.

## Methods

### NasJobOutput

`NasJobOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a uCAIP NasJob output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesdeployrequestcustommodel_googlecloudaiplatfo_11e140.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeployrequestcustommodel_googlecloudaiplatfor_abf38a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployrequestcustommodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest.CustomModel -->

# Class CustomModel (1.134.0)

`CustomModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The custom model to deploy from model weights in a Google Cloud Storage URI or Model Registry model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`gcs_uri` |
`str`
Immutable. The Google Cloud Storage URI of the custom model, storing weights and config files (which can be used to infer the base model). This field is a member of `oneof` _ `model_source` .
|

## Methods

### CustomModel

`CustomModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The custom model to deploy from model weights in a Google Cloud Storage URI or Model Registry model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdataitemview.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DataItemView -->

# Class DataItemView (1.134.0)

`DataItemView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A container for a single DataItem and Annotations on it.

## Attributes |
|
|---|---|
Name |
Description |
`data_item` |
`google.cloud.aiplatform_v1.types.DataItem`
The DataItem. |
`annotations` |
`MutableSequence[`
The Annotations on the DataItem. If too many Annotations should be returned for the DataItem, this field will be truncated per annotations_limit in request. If it was, then the has_truncated_annotations will be set to true. |
`has_truncated_annotations` |
`bool`
True if and only if the Annotations field has been truncated. It happens if more Annotations for this DataItem met the request's annotation_filter than are allowed to be returned by annotations_limit. Note that if Annotations field is not being returned due to field mask, then this field will not be set to true no matter how many Annotations are there. |

## Methods

### DataItemView

`DataItemView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A container for a single DataItem and Annotations on it.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvertex_rag_data_servicepagerslistragfilespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagFilesPager -->

# Class ListRagFilesPager (1.134.0)

```
ListRagFilesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse,
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse,
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


A pager for iterating through `list_rag_files`

requests.

This class thinly wraps an initial
[ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagFilesResponse) object, and
provides an `__iter__`

method to iterate through its
`rag_files`

field.

If there are more pages, the `__iter__`

method will make additional
`ListRagFiles`

requests and continue to iterate
through the `rag_files`

field on the
corresponding responses.

All the usual [ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagFilesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRagFilesPager

```
ListRagFilesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse,
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesfeaturestore_servicepagerssearchfeaturespager__f1d10a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeaturestore_servicepagerssearchfeaturespager_g_5110ed.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeaturestore_servicepagerssearchfeaturespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.SearchFeaturesPager -->

# Class SearchFeaturesPager (1.134.0)

```
SearchFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse,
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


A pager for iterating through `search_features`

requests.

This class thinly wraps an initial
[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesResponse) object, and
provides an `__iter__`

method to iterate through its
`features`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchFeaturesPager

```
SearchFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvizier_servicepagersliststudiesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListStudiesAsyncPager -->

# Class ListStudiesAsyncPager (1.134.0)

```
ListStudiesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse
],
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse,
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


A pager for iterating through `list_studies`

requests.

This class thinly wraps an initial
[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse) object, and
provides an `__aiter__`

method to iterate through its
`studies`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListStudies`

requests and continue to iterate
through the `studies`

field on the
corresponding responses.

All the usual [ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListStudiesAsyncPager

```
ListStudiesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse
],
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicespipeline_servicepagerslistpipelinejobspager_goo_4de687.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicespipeline_servicepagerslistpipelinejobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListPipelineJobsPager -->

# Class ListPipelineJobsPager (1.134.0)

```
ListPipelineJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse,
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse,
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


A pager for iterating through `list_pipeline_jobs`

requests.

This class thinly wraps an initial
[ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`pipeline_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPipelineJobs`

requests and continue to iterate
through the `pipeline_jobs`

field on the
corresponding responses.

All the usual [ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPipelineJobsPager

```
ListPipelineJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse,
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnasjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJob -->

# Class NasJob (1.134.0)

`NasJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a Neural Architecture Search (NAS) job.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the NasJob. |
`display_name` |
`str`
Required. The display name of the NasJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`nas_job_spec` |
Required. The specification of a NasJob. |
`nas_job_output` |
Output only. Output of the NasJob. |
`state` |
Output only. The detailed state of the job. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the NasJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the NasJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the NasJob entered any of the following states: `JOB_STATE_SUCCEEDED` ,
`JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the NasJob was most recently updated. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when job's state is JOB_STATE_FAILED or JOB_STATE_CANCELLED. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize NasJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key options for a NasJob. If this is set, then all resources created by the NasJob will be encrypted with the provided encryption key. |
`enable_restricted_image_training` |
`bool`
Optional. Enable a separation of Custom model training and restricted image training for tenant project. |
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

### NasJob

`NasJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a Neural Architecture Search (NAS) job.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1servicesdataset_servicepagerssearchdataitemspager__g_309263.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesdataset_servicepagerssearchdataitemspager__go_b7a631.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesdataset_servicepagerssearchdataitemspager__goo_fca252.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdataset_servicepagerssearchdataitemspager__goog_a1b8e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerssearchdataitemspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.SearchDataItemsPager -->

# Class SearchDataItemsPager (1.134.0)

```
SearchDataItemsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse,
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


A pager for iterating through `search_data_items`

requests.

This class thinly wraps an initial
[SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsResponse) object, and
provides an `__iter__`

method to iterate through its
`data_item_views`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchDataItems`

requests and continue to iterate
through the `data_item_views`

field on the
corresponding responses.

All the usual [SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchDataItemsPager

```
SearchDataItemsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesexportevaluateddatait_13dd9d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesexportevaluateddataitemsconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.ExportEvaluatedDataItemsConfig -->

# Class ExportEvaluatedDataItemsConfig (1.134.0)

```
ExportEvaluatedDataItemsConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for exporting test set predictions to a BigQuery table.

## Attributes |
|
|---|---|
Name |
Description |
`destination_bigquery_uri` |
`str`
URI of desired destination BigQuery table. Expected format: bq:// |
`override_existing_table` |
`bool`
If true and an export destination is specified, then the contents of the destination are overwritten. Otherwise, if the export destination already exists, then the export operation fails. |

## Methods

### ExportEvaluatedDataItemsConfig

```
ExportEvaluatedDataItemsConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for exporting test set predictions to a BigQuery table.

### ExportEvaluatedDataItemsConfig

```
ExportEvaluatedDataItemsConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for exporting test set predictions to a BigQuery table.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplainresponseconcurrentexplanationsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplainResponse.ConcurrentExplanationsEntry -->

# Class ConcurrentExplanationsEntry (1.134.0)

`ConcurrentExplanationsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### ConcurrentExplanationsEntry

`ConcurrentExplanationsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesragqueryranking_googlecloudaiplatform_v1type_2bb9ab.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragqueryranking_googlecloudaiplatform_v1types_ef2141.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragqueryranking.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagQuery.Ranking -->

# Class Ranking (1.134.0)

`Ranking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations for hybrid search results ranking.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`alpha` |
`float`
Optional. Alpha value controls the weight between dense and sparse vector search results. The range is [0, 1], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally. This field is a member of `oneof` _ `_alpha` .
|

## Methods

### Ranking

`Ranking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations for hybrid search results ranking.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatetensorboardrunrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardRunRequest -->

# Class UpdateTensorboardRunRequest (1.134.0)

`UpdateTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboardRun.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardRun resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard_run` |
Required. The TensorboardRun's `name` field is used to
identify the TensorboardRun to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|

## Methods

### UpdateTensorboardRunRequest

`UpdateTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboardRun.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragretrievalconfighybridsearch_googlecloudaip_2d2521.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragretrievalconfighybridsearch.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagRetrievalConfig.HybridSearch -->

# Class HybridSearch (1.134.0)

`HybridSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Hybrid Search.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`alpha` |
`float`
Optional. Alpha value controls the weight between dense and sparse vector search results. The range is [0, 1], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally. This field is a member of `oneof` _ `_alpha` .
|

## Methods

### HybridSearch

`HybridSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Hybrid Search.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmodelversioncheckpointsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsRequest -->

# Class ListModelVersionCheckpointsRequest (1.134.0)

```
ListModelVersionCheckpointsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ListModelVersionCheckpoints.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the model version to list checkpoints for. `projects/{project}/locations/{location}/models/{model}@{version}`
Example:
`projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
If no version ID or alias is specified, the latest version
will be used.
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via next_page_token of the previous ListModelVersionCheckpoints call. |

## Methods

### ListModelVersionCheckpointsRequest

```
ListModelVersionCheckpointsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ListModelVersionCheckpoints.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesendpoint_servicepagerslistendpointspager__1ccc32.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesendpoint_servicepagerslistendpointspager_g_b533b4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesendpoint_servicepagerslistendpointspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers.ListEndpointsPager -->

# Class ListEndpointsPager (1.134.0)

```
ListEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
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


A pager for iterating through `list_endpoints`

requests.

This class thinly wraps an initial
[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`endpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListEndpoints`

requests and continue to iterate
through the `endpoints`

field on the
corresponding responses.

All the usual [ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEndpointsPager

```
ListEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistartifactspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListArtifactsPager -->

# Class ListArtifactsPager (1.134.0)

```
ListArtifactsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse,
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


A pager for iterating through `list_artifacts`

requests.

This class thinly wraps an initial
[ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListArtifactsResponse) object, and
provides an `__iter__`

method to iterate through its
`artifacts`

field.

If there are more pages, the `__iter__`

method will make additional
`ListArtifacts`

requests and continue to iterate
through the `artifacts`

field on the
corresponding responses.

All the usual [ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListArtifactsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListArtifactsPager

```
ListArtifactsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerslistfeaturespage_f79441.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerslistfeaturespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturesPager -->

# Class ListFeaturesPager (1.134.0)

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
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


A pager for iterating through `list_features`

requests.

This class thinly wraps an initial
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse) object, and
provides an `__iter__`

method to iterate through its
`features`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturesPager

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistexecutionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsRequest -->

# Class ListExecutionsRequest (1.134.0)

`ListExecutionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The MetadataStore whose Executions should be listed. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`page_size` |
`int`
The maximum number of Executions to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListExecutions call. Provide this to retrieve the subsequent page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with an INVALID_ARGUMENT error.) |
`filter` |
`str`
Filter specifying the boolean condition for the Executions to satisfy in order to be part of the result set. The syntax to define filter query is based on https://google.aip.dev/160. Following are the supported set of filters: - **Attribute filtering**: For example: `display_name = "test"` . Supported fields include:
`name` , `display_name` , `state` , `schema_title` ,
`create_time` , and `update_time` . Time fields, such as
`create_time` and `update_time` , require values
specified in RFC-3339 format. For example:
`create_time = "2020-11-19T11:30:00-04:00"` .
- **Metadata field**: To filter on metadata fields use
traversal operation as follows:
`metadata.` For example:
`metadata.field_1.number_value = 10.0` In case the field
name contains special characters (such as colon), one can
embed it inside double quote. For example:
`metadata."field:1".number_value = 10.0`
- **Context based filtering**: To filter Executions based on
the contexts to which they belong use the function
operator with the full resource name:
`in_context(` . For example:
`in_context("projects/`
Each of the above supported filters can be combined together
using logical operators (`AND` & `OR` ). Maximum nested
expression depth allowed is 5.
For example:
`display_name = "test" AND metadata.field1.bool_value = true` .
|
`order_by` |
`str`
How the list of messages is ordered. Specify the values to order by and an ordering operation. The default sorting order is ascending. To specify descending order for a field, users append a " desc" suffix; for example: "foo desc, bar". Subfields are specified with a `.` character, such as
foo.bar. see https://google.aip.dev/132#ordering for more
details.
|

## Methods

### ListExecutionsRequest

`ListExecutionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListExecutions.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesschedule_servicepagerslistschedulespager_006aa8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesschedule_servicepagerslistschedulespager__630bdc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesschedule_servicepagerslistschedulespager_g_d82e20.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesschedule_servicepagerslistschedulespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.pagers.ListSchedulesPager -->

# Class ListSchedulesPager (1.134.0)

```
ListSchedulesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
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


A pager for iterating through `list_schedules`

requests.

This class thinly wraps an initial
[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse) object, and
provides an `__iter__`

method to iterate through its
`schedules`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSchedules`

requests and continue to iterate
through the `schedules`

field on the
corresponding responses.

All the usual [ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSchedulesPager

```
ListSchedulesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmemory_bank_servicepagerslistmemoriespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers.ListMemoriesPager -->

# Class ListMemoriesPager (1.134.0)

```
ListMemoriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesRequest,
response: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
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


A pager for iterating through `list_memories`

requests.

This class thinly wraps an initial
[ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse) object, and
provides an `__iter__`

method to iterate through its
`memories`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMemories`

requests and continue to iterate
through the `memories`

field on the
corresponding responses.

All the usual [ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMemoriesPager

```
ListMemoriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesRequest,
response: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelsasyncpager_go_3fa3b8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelsAsyncPager -->

# Class ListModelsAsyncPager (1.134.0)

```
ListModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse,
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


A pager for iterating through `list_models`

requests.

This class thinly wraps an initial
[ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsResponse) object, and
provides an `__aiter__`

method to iterate through its
`models`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModels`

requests and continue to iterate
through the `models`

field on the
corresponding responses.

All the usual [ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelsAsyncPager

```
ListModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistartifactsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListArtifactsRequest -->

# Class ListArtifactsRequest (1.134.0)

`ListArtifactsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListArtifacts.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The MetadataStore whose Artifacts should be listed. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`page_size` |
`int`
The maximum number of Artifacts to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListArtifacts call. Provide this to retrieve the subsequent page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID_ARGUMENT error.) |
`filter` |
`str`
Filter specifying the boolean condition for the Artifacts to satisfy in order to be part of the result set. The syntax to define filter query is based on https://google.aip.dev/160. The supported set of filters include the following: - **Attribute filtering**: For example: `display_name = "test"` . Supported fields include:
`name` , `display_name` , `uri` , `state` ,
`schema_title` , `create_time` , and `update_time` .
Time fields, such as `create_time` and `update_time` ,
require values specified in RFC-3339 format. For example:
`create_time = "2020-11-19T11:30:00-04:00"`
- **Metadata field**: To filter on metadata fields use
traversal operation as follows:
`metadata.` . For example:
`metadata.field_1.number_value = 10.0` In case the field
name contains special characters (such as colon), one can
embed it inside double quote. For example:
`metadata."field:1".number_value = 10.0`
- **Context based filtering**: To filter Artifacts based on
the contexts to which they belong, use the function
operator with the full resource name
`in_context(` . For example:
`in_context("projects/`
Each of the above supported filter types can be combined
together using logical operators (`AND` & `OR` ). Maximum
nested expression depth allowed is 5.
For example:
`display_name = "test" AND metadata.field1.bool_value = true` .
|
`order_by` |
`str`
How the list of messages is ordered. Specify the values to order by and an ordering operation. The default sorting order is ascending. To specify descending order for a field, users append a " desc" suffix; for example: "foo desc, bar". Subfields are specified with a `.` character, such as
foo.bar. see https://google.aip.dev/132#ordering for more
details.
|

## Methods

### ListArtifactsRequest

`ListArtifactsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListArtifacts.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typescreatefeatureonlinestorerequest_googlecloud_fa4ba0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescreatefeatureonlinestorerequest_googleclouda_318a34.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatefeatureonlinestorerequest_googlecloudai_c964c1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatefeatureonlinestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureOnlineStoreRequest -->

# Class CreateFeatureOnlineStoreRequest (1.134.0)

```
CreateFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.CreateFeatureOnlineStore.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create FeatureOnlineStores. Format: `projects/{project}/locations/{location}`
|
`feature_online_store` |
Required. The FeatureOnlineStore to create. |
`feature_online_store_id` |
`str`
Required. The ID to use for this FeatureOnlineStore, which will become the final component of the FeatureOnlineStore's resource name. This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within the project and location.
|

## Methods

### CreateFeatureOnlineStoreRequest

```
CreateFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.CreateFeatureOnlineStore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeploypublishermodeloperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployPublisherModelOperationMetadata -->

# Class DeployPublisherModelOperationMetadata (1.134.0)

```
DeployPublisherModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for ModelGardenService.DeployPublisherModel.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`publisher_model` |
`str`
Output only. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisher_model}@{version_id}` ,
or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001`
|
`destination` |
`str`
Output only. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`
|
`project_number` |
`int`
Output only. The project number where the deploy model request is sent. |

## Methods

### DeployPublisherModelOperationMetadata

```
DeployPublisherModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for ModelGardenService.DeployPublisherModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerslistsavedqueriespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListSavedQueriesPager -->

# Class ListSavedQueriesPager (1.134.0)

```
ListSavedQueriesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse,
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


A pager for iterating through `list_saved_queries`

requests.

This class thinly wraps an initial
[ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSavedQueriesResponse) object, and
provides an `__iter__`

method to iterate through its
`saved_queries`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSavedQueries`

requests and continue to iterate
through the `saved_queries`

field on the
corresponding responses.

All the usual [ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSavedQueriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSavedQueriesPager

```
ListSavedQueriesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesembedcontentrequestembeddingtasktype_googleclouda_6f46e5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesembedcontentrequestembeddingtasktype_googlecloudai_aadab2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesembedcontentrequestembeddingtasktype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EmbedContentRequest.EmbeddingTaskType -->

# Class EmbeddingTaskType (1.134.0)

`EmbeddingTaskType(value)`


Represents a downstream task the embeddings will be used for.

## Enums |
|
|---|---|
Name |
Description |
`UNSPECIFIED` |
Unset value, which will default to one of the other enum values. |
`RETRIEVAL_QUERY` |
Specifies the given text is a query in a search/retrieval setting. |
`RETRIEVAL_DOCUMENT` |
Specifies the given text is a document from the corpus being searched. |
`SEMANTIC_SIMILARITY` |
Specifies the given text will be used for STS. |
`CLASSIFICATION` |
Specifies that the given text will be classified. |
`CLUSTERING` |
Specifies that the embeddings will be used for clustering. |
`QUESTION_ANSWERING` |
Specifies that the embeddings will be used for question answering. |
`FACT_VERIFICATION` |
Specifies that the embeddings will be used for fact verification. |
`CODE_RETRIEVAL_QUERY` |
Specifies that the embeddings will be used for code retrieval. |

## Methods

### EmbeddingTaskType

`EmbeddingTaskType(value)`


Represents a downstream task the embeddings will be used for.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesindexdatapointnumericrestrictionoperator.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexDatapoint.NumericRestriction.Operator -->

# Class Operator (1.134.0)

`Operator(value)`


Which comparison operator to use. Should be specified for queries only; specifying this for a datapoint is an error.

Datapoints for which Operator is true relative to the query's Value field will be allowlisted.

## Enums |
|
|---|---|
Name |
Description |
`OPERATOR_UNSPECIFIED` |
Default value of the enum. |
`LESS` |
Datapoints are eligible iff their value is < the=""> |
`LESS_EQUAL` |
Datapoints are eligible iff their value is <= the=""> |
`EQUAL` |
Datapoints are eligible iff their value is == the query's. |
`GREATER_EQUAL` |
Datapoints are eligible iff their value is >= the query's. |
`GREATER` |
Datapoints are eligible iff their value is > the query's. |
`NOT_EQUAL` |
Datapoints are eligible iff their value is != the query's. |

## Methods

### Operator

`Operator(value)`


Which comparison operator to use. Should be specified for queries only; specifying this for a datapoint is an error.

Datapoints for which Operator is true relative to the query's Value field will be allowlisted.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeploymentstage_googlecloudaiplatform_v1typeslistm_e11f2d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeploymentstage.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeploymentStage -->

# Class DeploymentStage (1.134.0)

`DeploymentStage(value)`


Stage field indicating the current progress of a deployment.

## Enums |
|
|---|---|
Name |
Description |
`DEPLOYMENT_STAGE_UNSPECIFIED` |
Default value. This value is unused. |
`STARTING_DEPLOYMENT` |
The deployment is initializing and setting up the environment. |
`PREPARING_MODEL` |
The deployment is preparing the model assets. |
`CREATING_SERVING_CLUSTER` |
The deployment is creating the underlying serving cluster. |
`ADDING_NODES_TO_CLUSTER` |
The deployment is adding nodes to the serving cluster. |
`GETTING_CONTAINER_IMAGE` |
The deployment is getting the container image for the model server. |
`STARTING_MODEL_SERVER` |
The deployment is starting the model server. |
`FINISHING_UP` |
The deployment is performing finalization steps. |
`DEPLOYMENT_TERMINATED` |
The deployment has terminated. |
`SUCCESSFULLY_DEPLOYED` |
The deployment has succeeded. |
`FAILED_TO_DEPLOY` |
The deployment has failed. |

## Methods

### DeploymentStage

`DeploymentStage(value)`


Stage field indicating the current progress of a deployment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmodelevaluationslicesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationSlicesRequest -->

# Class ListModelEvaluationSlicesRequest (1.134.0)

```
ListModelEvaluationSlicesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ListModelEvaluationSlices.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the ModelEvaluation to list the ModelEvaluationSlices from. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}`
|
`filter` |
`str`
The standard list filter. - `slice.dimension` - for =.
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListModelEvaluationSlicesResponse.next_page_token of the previous ModelService.ListModelEvaluationSlices call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListModelEvaluationSlicesRequest

```
ListModelEvaluationSlicesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ListModelEvaluationSlices.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesdata_foundry_servicedatafoundryserviceasynccl_1af1ed.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesdata_foundry_servicedatafoundryserviceasynccli_a95e75.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdata_foundry_servicedatafoundryserviceasyncclie_2ebe60.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdata_foundry_servicedatafoundryserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceAsyncClient -->

# Class DataFoundryServiceAsyncClient (1.134.0)

```
DataFoundryServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for generating and preparing datasets for Gen AI evaluation.

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
`DataFoundryServiceTransport` |
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

### DataFoundryServiceAsyncClient

```
DataFoundryServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the data foundry service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,DataFoundryServiceTransport,Callable[..., DataFoundryServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the DataFoundryServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
`DataFoundryServiceAsyncClient` |
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
`DataFoundryServiceAsyncClient` |
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
`DataFoundryServiceAsyncClient` |
The constructed client. |

### generate_synthetic_data

```
generate_synthetic_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.data_foundry_service.GenerateSyntheticDataRequest,
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
) -> (
google.cloud.aiplatform_v1.types.data_foundry_service.GenerateSyntheticDataResponse
)
```


Generates synthetic data based on the provided configuration.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_generate_synthetic_data():
# Create a client
client = aiplatform_v1.
```[DataFoundryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceAsyncClient.html)()
# Initialize request argument(s)
task_description = aiplatform_v1.[TaskDescriptionStrategy](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TaskDescriptionStrategy.html)()
task_description.task_description = "task_description_value"
output_field_specs = aiplatform_v1.[OutputFieldSpec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.OutputFieldSpec.html)()
output_field_specs.field_name = "field_name_value"
request = aiplatform_v1.[GenerateSyntheticDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateSyntheticDataRequest.html)(
task_description=task_description,
location="location_value",
count=553,
output_field_specs=output_field_specs,
)
# Make the request
response = await client.[generate_synthetic_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceAsyncClient.html#google_cloud_aiplatform_v1_services_data_foundry_service_DataFoundryServiceAsyncClient_generate_synthetic_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for DataFoundryService.GenerateSyntheticData. |
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
The response containing the generated data. |

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

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typescreatetensorboardtimeseriesrequest_googlec_75e59d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typescreatetensorboardtimeseriesrequest_googlecl_39a433.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescreatetensorboardtimeseriesrequest_googleclo_f67ef5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatetensorboardtimeseriesrequest_googleclou_ec440f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatetensorboardtimeseriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardTimeSeriesRequest -->

# Class CreateTensorboardTimeSeriesRequest (1.134.0)

```
CreateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.CreateTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the TensorboardRun to create the TensorboardTimeSeries in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|
`tensorboard_time_series_id` |
`str`
Optional. The user specified unique ID to use for the TensorboardTimeSeries, which becomes the final component of the TensorboardTimeSeries's resource name. This value should match " `a-z0-9][a-z0-9-]` {0, 127}".
|
`tensorboard_time_series` |
Required. The TensorboardTimeSeries to create. |

## Methods

### CreateTensorboardTimeSeriesRequest

```
CreateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.CreateTensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigpredictiondriftdetectionconfigdriftthresholdsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.PredictionDriftDetectionConfig.DriftThresholdsEntry -->

# Class DriftThresholdsEntry (1.134.0)

`DriftThresholdsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### DriftThresholdsEntry

`DriftThresholdsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesassessdataresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataResponse -->

# Class AssessDataResponse (1.134.0)

`AssessDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.AssessData.

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
`tuning_validation_assessment_result` |
Optional. The result of the tuning validation assessment. This field is a member of `oneof` _ `assessment_result` .
|
`tuning_resource_usage_assessment_result` |
Optional. The result of the tuning resource usage assessment. This field is a member of `oneof` _ `assessment_result` .
|
`batch_prediction_validation_assessment_result` |
Optional. The result of the batch prediction validation assessment. This field is a member of `oneof` _ `assessment_result` .
|
`batch_prediction_resource_usage_assessment_result` |
Optional. The result of the batch prediction resource usage assessment. This field is a member of `oneof` _ `assessment_result` .
|

## Classes

### BatchPredictionResourceUsageAssessmentResult

```
BatchPredictionResourceUsageAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the batch prediction resource usage assessment.

### BatchPredictionValidationAssessmentResult

```
BatchPredictionValidationAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the batch prediction validation assessment.

### TuningResourceUsageAssessmentResult

```
TuningResourceUsageAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the tuning resource usage assessment.

### TuningValidationAssessmentResult

```
TuningValidationAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the tuning validation assessment.

## Methods

### AssessDataResponse

`AssessDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.AssessData.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnearestneighborquerynumericfilter_googlecloud_495a13.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnearestneighborquerynumericfilter.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborQuery.NumericFilter -->

# Class NumericFilter (1.134.0)

`NumericFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Numeric filter is used to search a subset of the entities by using boolean rules on numeric columns. For example: Database Point 0: {name: “a” value_int: 42} {name: “b” value_float: 1.0} Database Point 1: {name: “a” value_int: 10} {name: “b” value_float: 2.0} Database Point 2: {name: “a” value_int: -1} {name: “b” value_float: 3.0} Query: {name: “a” value_int: 12 operator: LESS} // Matches Point 1, 2 {name: “b” value_float: 2.0 operator: EQUAL} // Matches Point 1

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
`value_int` |
`int`
int value type. This field is a member of `oneof` _ `Value` .
|
`value_float` |
`float`
float value type. This field is a member of `oneof` _ `Value` .
|
`value_double` |
`float`
double value type. This field is a member of `oneof` _ `Value` .
|
`name` |
`str`
Required. Column name in BigQuery that used as filters. |
`op` |
Optional. This MUST be specified for queries and must NOT be specified for database points. This field is a member of `oneof` _ `_op` .
|

## Classes

### Operator

`Operator(value)`


Datapoints for which Operator is true relative to the query’s Value field will be allowlisted.

## Methods

### NumericFilter

`NumericFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Numeric filter is used to search a subset of the entities by using boolean rules on numeric columns. For example: Database Point 0: {name: “a” value_int: 42} {name: “b” value_float: 1.0} Database Point 1: {name: “a” value_int: 10} {name: “b” value_float: 2.0} Database Point 2: {name: “a” value_int: -1} {name: “b” value_float: 3.0} Query: {name: “a” value_int: 12 operator: LESS} // Matches Point 1, 2 {name: “b” value_float: 2.0 operator: EQUAL} // Matches Point 1

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistexecutionspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListExecutionsPager -->

# Class ListExecutionsPager (1.134.0)

```
ListExecutionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse,
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


A pager for iterating through `list_executions`

requests.

This class thinly wraps an initial
[ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsResponse) object, and
provides an `__iter__`

method to iterate through its
`executions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListExecutions`

requests and continue to iterate
through the `executions`

field on the
corresponding responses.

All the usual [ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListExecutionsPager

```
ListExecutionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputs____c12f26.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs -->

# Class AutoMlTablesInputs (1.134.0)

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
`optimization_objective_recall_value` |
`float`
Required when optimization_objective is "maximize-precision-at-recall". Must be between 0 and 1, inclusive. This field is a member of `oneof` _ `additional_optimization_objective_config` .
|
`optimization_objective_precision_value` |
`float`
Required when optimization_objective is "maximize-recall-at-precision". Must be between 0 and 1, inclusive. This field is a member of `oneof` _ `additional_optimization_objective_config` .
|
`prediction_type` |
`str`
The type of prediction the Model is to produce. "classification" - Predict one out of multiple target values is picked for each row. "regression" - Predict a value based on its relation to other values. This type is available only to columns that contain semantically numeric values, i.e. integers or floating point number, even if stored as e.g. strings. |
`target_column` |
`str`
The column name of the target column that the model is to predict. |
`transformations` |
`MutableSequence[`
Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. |
`optimization_objective` |
`str`
Objective function the model is optimizing towards. The training process creates a model that maximizes/minimizes the value of the objective function over the validation set. The supported optimization objectives depend on the prediction type. If the field is not set, a default objective function is used. classification (binary): "maximize-au-roc" (default) - Maximize the area under the receiver operating characteristic (ROC) curve. "minimize-log-loss" - Minimize log loss. "maximize-au-prc" - Maximize the area under the precision-recall curve. "maximize-precision-at-recall" - Maximize precision for a specified recall value. "maximize-recall-at-precision" - Maximize recall for a specified precision value. classification (multi-class): "minimize-log-loss" (default) - Minimize log loss. regression: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). |
`train_budget_milli_node_hours` |
`int`
Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won't be attempted and will error. The train budget must be between 1,000 and 72,000 milli node hours, inclusive. |
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. By default, the early stopping feature is enabled, which means that AutoML Tables might stop training before the entire training budget has been used. |
`weight_column_name` |
`str`
Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1. |
`export_evaluated_data_items_config` |
Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed. |
`additional_experiments` |
`MutableSequence[str]`
Additional experiment flags for the Tables training pipeline. |

## Classes

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### AutoMlTablesInputs

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### AutoMlTablesInputs

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistextensionsrequest_googlecloudaiplatform__ce6cfe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistextensionsrequest_googlecloudaiplatform_v_5d197b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistextensionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsRequest -->

# Class ListExtensionsRequest (1.134.0)

`ListExtensionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.ListExtensions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the Extensions from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. The standard list filter. Supported fields: \* `display_name` \* `create_time` \* `update_time`
More detail in `AIP-160 ` __.
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
Example: `display_name, create_time desc` .
|

## Methods

### ListExtensionsRequest

`ListExtensionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.ListExtensions.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmeasurement.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Measurement -->

# Class Measurement (1.134.0)

`Measurement(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Measurement of a Trial. A Measurement contains the Metrics got by executing a Trial using suggested hyperparameter values.

## Attributes |
|
|---|---|
Name |
Description |
`elapsed_duration` |
`google.protobuf.duration_pb2.Duration`
Output only. Time that the Trial has been running at the point of this Measurement. |
`step_count` |
`int`
Output only. The number of steps the machine learning model has been trained for. Must be non-negative. |
`metrics` |
`MutableSequence[`
Output only. A list of metrics got by evaluating the objective functions using suggested Parameter values. |

## Classes

### Metric

`Metric(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a metric in the measurement.

## Methods

### Measurement

`Measurement(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Measurement of a Trial. A Measurement contains the Metrics got by executing a Trial using suggested hyperparameter values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeaturespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeaturesPager -->

# Class ListFeaturesPager (1.134.0)

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
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


A pager for iterating through `list_features`

requests.

This class thinly wraps an initial
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse) object, and
provides an `__iter__`

method to iterate through its
`features`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturesPager

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltab_af96e2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltabl_02ea10.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltable_4aefd2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltablesinputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs -->

# Class AutoMlTablesInputs (1.134.0)

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
`optimization_objective_recall_value` |
`float`
Required when optimization_objective is "maximize-precision-at-recall". Must be between 0 and 1, inclusive. This field is a member of `oneof` _ `additional_optimization_objective_config` .
|
`optimization_objective_precision_value` |
`float`
Required when optimization_objective is "maximize-recall-at-precision". Must be between 0 and 1, inclusive. This field is a member of `oneof` _ `additional_optimization_objective_config` .
|
`prediction_type` |
`str`
The type of prediction the Model is to produce. "classification" - Predict one out of multiple target values is picked for each row. "regression" - Predict a value based on its relation to other values. This type is available only to columns that contain semantically numeric values, i.e. integers or floating point number, even if stored as e.g. strings. |
`target_column` |
`str`
The column name of the target column that the model is to predict. |
`transformations` |
`MutableSequence[`
Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. |
`optimization_objective` |
`str`
Objective function the model is optimizing towards. The training process creates a model that maximizes/minimizes the value of the objective function over the validation set. The supported optimization objectives depend on the prediction type. If the field is not set, a default objective function is used. classification (binary): "maximize-au-roc" (default) - Maximize the area under the receiver operating characteristic (ROC) curve. "minimize-log-loss" - Minimize log loss. "maximize-au-prc" - Maximize the area under the precision-recall curve. "maximize-precision-at-recall" - Maximize precision for a specified recall value. "maximize-recall-at-precision" - Maximize recall for a specified precision value. classification (multi-class): "minimize-log-loss" (default) - Minimize log loss. regression: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). |
`train_budget_milli_node_hours` |
`int`
Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won't be attempted and will error. The train budget must be between 1,000 and 72,000 milli node hours, inclusive. |
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. By default, the early stopping feature is enabled, which means that AutoML Tables might stop training before the entire training budget has been used. |
`weight_column_name` |
`str`
Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1. |
`export_evaluated_data_items_config` |
Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed. |
`additional_experiments` |
`MutableSequence[str]`
Additional experiment flags for the Tables training pipeline. |

## Classes

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### AutoMlTablesInputs

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### AutoMlTablesInputs

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdataset_servicepagerslistdatasetsasyncpager_goo_324a77.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerslistdatasetsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetsAsyncPager -->

# Class ListDatasetsAsyncPager (1.134.0)

```
ListDatasetsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse,
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


A pager for iterating through `list_datasets`

requests.

This class thinly wraps an initial
[ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsResponse) object, and
provides an `__aiter__`

method to iterate through its
`datasets`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDatasets`

requests and continue to iterate
through the `datasets`

field on the
corresponding responses.

All the usual [ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDatasetsAsyncPager

```
ListDatasetsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeaturestore_servicepagerslistentitytypespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListEntityTypesPager -->

# Class ListEntityTypesPager (1.134.0)

```
ListEntityTypesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
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


A pager for iterating through `list_entity_types`

requests.

This class thinly wraps an initial
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse) object, and
provides an `__iter__`

method to iterate through its
`entity_types`

field.

If there are more pages, the `__iter__`

method will make additional
`ListEntityTypes`

requests and continue to iterate
through the `entity_types`

field on the
corresponding responses.

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEntityTypesPager

```
ListEntityTypesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespublishermodel__googlecloudaiplatform_v1typescrea_a33358.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespublishermodel__googlecloudaiplatform_v1typescreat_c0c76b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespublishermodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel -->

# Class PublisherModel (1.134.0)

`PublisherModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Model Garden Publisher Model.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the PublisherModel. |
`version_id` |
`str`
Output only. Immutable. The version ID of the PublisherModel. A new version is committed when a new model version is uploaded under an existing model id. It is an auto-incrementing decimal number in string representation. |
`open_source_category` |
Required. Indicates the open source category of the publisher model. |
`supported_actions` |
Optional. Supported call-to-action options. |
`frameworks` |
`MutableSequence[str]`
Optional. Additional information about the model's Frameworks. |
`launch_stage` |
Optional. Indicates the launch stage of the model. |
`version_state` |
Optional. Indicates the state of the model version. |
`publisher_model_template` |
`str`
Optional. Output only. Immutable. Used to indicate this model has a publisher model and provide the template of the publisher model resource name. |
`predict_schemata` |
Optional. The schemata that describes formats of the PublisherModel's predictions and explanations as given and returned via PredictionService.Predict. |

## Classes

### CallToAction

`CallToAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions could take on this Publisher Model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Documentation

`Documentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A named piece of documentation.

### LaunchStage

`LaunchStage(value)`


An enum representing the launch stage of a PublisherModel.

### OpenSourceCategory

`OpenSourceCategory(value)`


An enum representing the open source category of a PublisherModel.

### ResourceReference

`ResourceReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a resource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### VersionState

`VersionState(value)`


An enum representing the state of the PublicModelVersion.

## Methods

### PublisherModel

`PublisherModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Model Garden Publisher Model.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreatefeatureonlinestorerequest_googlecloudaiplatf_8c9c50.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatefeatureonlinestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureOnlineStoreRequest -->

# Class CreateFeatureOnlineStoreRequest (1.134.0)

```
CreateFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.CreateFeatureOnlineStore.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create FeatureOnlineStores. Format: `projects/{project}/locations/{location}`
|
`feature_online_store` |
Required. The FeatureOnlineStore to create. |
`feature_online_store_id` |
`str`
Required. The ID to use for this FeatureOnlineStore, which will become the final component of the FeatureOnlineStore's resource name. This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within the project and location.
|

## Methods

### CreateFeatureOnlineStoreRequest

```
CreateFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.CreateFeatureOnlineStore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigtrainingpredictionskewdetectionconfigskewthresholdsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.TrainingPredictionSkewDetectionConfig.SkewThresholdsEntry -->

# Class SkewThresholdsEntry (1.134.0)

`SkewThresholdsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### SkewThresholdsEntry

`SkewThresholdsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesvizier_servicepagerslisttrialsasyncpager___b33a21.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvizier_servicepagerslisttrialsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListTrialsAsyncPager -->

# Class ListTrialsAsyncPager (1.134.0)

```
ListTrialsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse,
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


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsResponse) object, and
provides an `__aiter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTrials`

requests and continue to iterate
through the `trials`

field on the
corresponding responses.

All the usual [ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTrialsAsyncPager

```
ListTrialsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdataitemview_googlecloudaiplatform_v1typespip_952877.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdataitemview.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DataItemView -->

# Class DataItemView (1.134.0)

`DataItemView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A container for a single DataItem and Annotations on it.

## Attributes |
|
|---|---|
Name |
Description |
`data_item` |
`google.cloud.aiplatform_v1beta1.types.DataItem`
The DataItem. |
`annotations` |
`MutableSequence[`
The Annotations on the DataItem. If too many Annotations should be returned for the DataItem, this field will be truncated per annotations_limit in request. If it was, then the has_truncated_annotations will be set to true. |
`has_truncated_annotations` |
`bool`
True if and only if the Annotations field has been truncated. It happens if more Annotations for this DataItem met the request's annotation_filter than are allowed to be returned by annotations_limit. Note that if Annotations field is not being returned due to field mask, then this field will not be set to true no matter how many Annotations are there. |

## Methods

### DataItemView

`DataItemView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A container for a single DataItem and Annotations on it.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespipelinejobruntimeconfiginputartifact.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineJob.RuntimeConfig.InputArtifact -->

# Class InputArtifact (1.134.0)

`InputArtifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type of an input artifact.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`artifact_id` |
`str`
Artifact resource id from MLMD. Which is the last portion of an artifact resource name: `projects/{project}/locations/{location}/metadataStores/default/artifacts/{artifact_id}` .
The artifact must stay within the same project, location and
default metadatastore as the pipeline.
This field is a member of `oneof` _ `kind` .
|

## Methods

### InputArtifact

`InputArtifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type of an input artifact.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesllm_utility_servicellmutilityserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceAsyncClient -->

# Class LlmUtilityServiceAsyncClient (1.134.0)

```
LlmUtilityServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for LLM related utility functions.

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
`LlmUtilityServiceTransport` |
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

### LlmUtilityServiceAsyncClient

```
LlmUtilityServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the llm utility service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,LlmUtilityServiceTransport,Callable[..., LlmUtilityServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the LlmUtilityServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### compute_tokens

```
compute_tokens(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.llm_utility_service.ComputeTokensRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.llm_utility_service.ComputeTokensResponse
```


Return a list of tokens based on the input text.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_compute_tokens():
# Create a client
client = aiplatform_v1beta1.
```[LlmUtilityServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ComputeTokensRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ComputeTokensRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = await client.[compute_tokens](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_llm_utility_service_LlmUtilityServiceAsyncClient_compute_tokens)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ComputeTokens RPC call. |
`endpoint` |
Required. The name of the Endpoint requested to get lists of tokens and token ids. This corresponds to the |
`instances` |
`:class:`
Optional. The instances that are the input to token computing API call. Schema is identical to the prediction schema of the text model, even for the non-text models, like chat models, or Codey models. This corresponds to the |
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
Response message for ComputeTokens RPC call. |

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
`LlmUtilityServiceAsyncClient` |
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
`LlmUtilityServiceAsyncClient` |
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
`LlmUtilityServiceAsyncClient` |
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

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesendpoint_serviceendpointserviceclient_____googl_e60674.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesendpoint_serviceendpointserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient -->

# Class EndpointServiceClient (1.134.0)

```
EndpointServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's Endpoints.

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
`EndpointServiceTransport` |
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

### EndpointServiceClient

```
EndpointServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the endpoint service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,EndpointServiceTransport,Callable[..., EndpointServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the EndpointServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_endpoint

```
create_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.endpoint_service.CreateEndpointRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.Endpoint
] = None,
endpoint_id: typing.Optional[str] = None,
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


Creates an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[CreateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEndpointRequest.html)(
parent="parent_value",
endpoint=endpoint,
)
# Make the request
operation = client.[create_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_create_endpoint)(request=request)
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
The request object. Request message for EndpointService.CreateEndpoint. |
`parent` |
`str`
Required. The resource name of the Location to create the Endpoint in. Format: |
`endpoint` |
Required. The Endpoint to create. This corresponds to the |
`endpoint_id` |
`str`
Immutable. The ID to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Vertex AI will generate a value for this ID. If the first character is a letter, this value may be up to 63 characters, and valid characters are |
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

### delete_endpoint

```
delete_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.endpoint_service.DeleteEndpointRequest,
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


Deletes an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_delete_endpoint)(request=request)
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
The request object. Request message for EndpointService.DeleteEndpoint. |
`name` |
`str`
Required. The name of the Endpoint resource to be deleted. Format: |
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

### deploy_model

```
deploy_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.endpoint_service.DeployModelRequest, dict
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.DeployedModel
] = None,
traffic_split: typing.Optional[typing.MutableMapping[str, int]] = None,
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


Deploys a Model into this Endpoint, creating a DeployedModel within it.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_deploy_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[DeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[deploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_deploy_model)(request=request)
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
The request object. Request message for EndpointService.DeployModel. |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to deploy a Model. Format: |
`deployed_model` |
Required. The DeployedModel to be created within the Endpoint. Note that Endpoint.traffic_split must be updated for the DeployedModel to start receiving traffic, either as part of this call, or via EndpointService.UpdateEndpoint. This corresponds to the |
`traffic_split` |
`MutableMapping[str, int]`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If this field is non-empty, then the Endpoint's traffic_split will be overwritten with it. To refer to the ID of the just being deployed Model, a "0" should be used, and the actual ID of the new DeployedModel will be filled in its place by this method. The traffic percentage values must add up to 100. If this field is empty, then the Endpoint's traffic_split is not updated. This corresponds to the |
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

### deployment_resource_pool_path

```
deployment_resource_pool_path(
project: str, location: str, deployment_resource_pool: str
) -> str
```


Returns a fully-qualified deployment_resource_pool string.

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
`EndpointServiceClient` |
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
`EndpointServiceClient` |
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
`EndpointServiceClient` |
The constructed client. |

### get_endpoint

```
get_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.endpoint_service.GetEndpointRequest, dict
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
) -> google.cloud.aiplatform_v1.types.endpoint.Endpoint
```


Gets an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetEndpointRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_get_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for EndpointService.GetEndpoint |
`name` |
`str`
Required. The name of the Endpoint resource. Format: |
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
Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations. |

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

### list_endpoints

```
list_endpoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsRequest, dict
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
) -> google.cloud.aiplatform_v1.services.endpoint_service.pagers.ListEndpointsPager
```


Lists Endpoints in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_endpoints():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_list_endpoints)(request=request)
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
The request object. Request message for EndpointService.ListEndpoints. |
`parent` |
`str`
Required. The resource name of the Location from which to list the Endpoints. Format: |
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
Response message for EndpointService.ListEndpoints. Iterating over this object will yield results and resolve additional pages automatically. |

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

### mutate_deployed_model

```
mutate_deployed_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.endpoint_service.MutateDeployedModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.DeployedModel
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


Updates an existing deployed model. Updatable fields include
`min_replica_count`

, `max_replica_count`

,
`required_replica_count`

, `autoscaling_metric_specs`

,
`disable_container_logging`

(v1 only), and
`enable_container_logging`

(v1beta1 only).

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_mutate_deployed_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[MutateDeployedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[mutate_deployed_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_mutate_deployed_model)(request=request)
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
The request object. Request message for EndpointService.MutateDeployedModel. |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to mutate a DeployedModel. Format: |
`deployed_model` |
Required. The DeployedModel to be mutated within the Endpoint. Only the following fields can be mutated: - |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See |
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

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

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

### parse_deployment_resource_pool_path

`parse_deployment_resource_pool_path(path: str) -> typing.Dict[str, str]`


Parses a deployment_resource_pool path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_deployment_monitoring_job_path

`parse_model_deployment_monitoring_job_path(path: str) -> typing.Dict[str, str]`


Parses a model_deployment_monitoring_job path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

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

### undeploy_model

```
undeploy_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.endpoint_service.UndeployModelRequest, dict
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model_id: typing.Optional[str] = None,
traffic_split: typing.Optional[typing.MutableMapping[str, int]] = None,
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


Undeploys a Model from an Endpoint, removing a DeployedModel from it, and freeing all resources it's using.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_undeploy_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UndeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model_id="deployed_model_id_value",
)
# Make the request
operation = client.[undeploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_undeploy_model)(request=request)
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
The request object. Request message for EndpointService.UndeployModel. |
`endpoint` |
`str`
Required. The name of the Endpoint resource from which to undeploy a Model. Format: |
`deployed_model_id` |
`str`
Required. The ID of the DeployedModel to be undeployed from the Endpoint. This corresponds to the |
`traffic_split` |
`MutableMapping[str, int]`
If this field is provided, then the Endpoint's traffic_split will be overwritten with it. If last DeployedModel is being undeployed from the Endpoint, the [Endpoint.traffic_split] will always end up empty when this call returns. A DeployedModel will be successfully undeployed only if it doesn't have any traffic assigned to it when this method executes, or if this field unassigns any traffic to it. This corresponds to the |
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

### update_endpoint

```
update_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.endpoint_service.UpdateEndpointRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.Endpoint
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
) -> google.cloud.aiplatform_v1.types.endpoint.Endpoint
```


Updates an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[UpdateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointRequest.html)(
endpoint=endpoint,
)
# Make the request
response = client.[update_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_update_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for EndpointService.UpdateEndpoint. |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See |
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
Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations. |

### update_endpoint_long_running

```
update_endpoint_long_running(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.endpoint_service.UpdateEndpointLongRunningRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.Endpoint
] = None,
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


Updates an Endpoint with a long running operation.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_endpoint_long_running():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[UpdateEndpointLongRunningRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointLongRunningRequest.html)(
endpoint=endpoint,
)
# Make the request
operation = client.[update_endpoint_long_running](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_update_endpoint_long_running)(request=request)
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
The request object. Request message for EndpointService.UpdateEndpointLongRunning. |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. Currently we only support updating the |
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


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesjob_servicepagerslistnasjobsasyncpager__954f0b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesjob_servicepagerslistnasjobsasyncpager___5eb676.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesjob_servicepagerslistnasjobsasyncpager__g_27f50d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesjob_servicepagerslistnasjobsasyncpager__go_0025c8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslistnasjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasJobsAsyncPager -->

# Class ListNasJobsAsyncPager (1.134.0)

```
ListNasJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse,
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


A pager for iterating through `list_nas_jobs`

requests.

This class thinly wraps an initial
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`nas_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNasJobs`

requests and continue to iterate
through the `nas_jobs`

field on the
corresponding responses.

All the usual [ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNasJobsAsyncPager

```
ListNasJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesembedcontentrequestembeddingtasktype_googlecl_59a0b7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesembedcontentrequestembeddingtasktype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EmbedContentRequest.EmbeddingTaskType -->

# Class EmbeddingTaskType (1.134.0)

`EmbeddingTaskType(value)`


Represents a downstream task the embeddings will be used for.

## Enums |
|
|---|---|
Name |
Description |
`UNSPECIFIED` |
Unset value, which will default to one of the other enum values. |
`RETRIEVAL_QUERY` |
Specifies the given text is a query in a search/retrieval setting. |
`RETRIEVAL_DOCUMENT` |
Specifies the given text is a document from the corpus being searched. |
`SEMANTIC_SIMILARITY` |
Specifies the given text will be used for STS. |
`CLASSIFICATION` |
Specifies that the given text will be classified. |
`CLUSTERING` |
Specifies that the embeddings will be used for clustering. |
`QUESTION_ANSWERING` |
Specifies that the embeddings will be used for question answering. |
`FACT_VERIFICATION` |
Specifies that the embeddings will be used for fact verification. |
`CODE_RETRIEVAL_QUERY` |
Specifies that the embeddings will be used for code retrieval. |

## Methods

### EmbeddingTaskType

`EmbeddingTaskType(value)`


Represents a downstream task the embeddings will be used for.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictparams_v1typesimageobjectdetectionpredictionparams.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.ImageObjectDetectionPredictionParams -->

# Class ImageObjectDetectionPredictionParams (1.134.0)

```
ImageObjectDetectionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Object Detection.

## Attributes |
|
|---|---|
Name |
Description |
`confidence_threshold` |
`float`
The Model only returns predictions with at least this confidence score. Default value is 0.0 |
`max_predictions` |
`int`
The Model only returns up to that many top, by confidence score, predictions per instance. Note that number of returned predictions is also limited by metadata's predictionsLimit. Default value is 10. |

## Methods

### ImageObjectDetectionPredictionParams

```
ImageObjectDetectionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Object Detection.

### ImageObjectDetectionPredictionParams

```
ImageObjectDetectionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Object Detection.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistannotationspager__28cff5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistannotationspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListAnnotationsPager -->

# Class ListAnnotationsPager (1.134.0)

```
ListAnnotationsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsResponse,
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


A pager for iterating through `list_annotations`

requests.

This class thinly wraps an initial
[ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsResponse) object, and
provides an `__iter__`

method to iterate through its
`annotations`

field.

If there are more pages, the `__iter__`

method will make additional
`ListAnnotations`

requests and continue to iterate
through the `annotations`

field on the
corresponding responses.

All the usual [ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListAnnotationsPager

```
ListAnnotationsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicepagerslistcontextsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListContextsAsyncPager -->

# Class ListContextsAsyncPager (1.134.0)

```
ListContextsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse,
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


A pager for iterating through `list_contexts`

requests.

This class thinly wraps an initial
[ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse) object, and
provides an `__aiter__`

method to iterate through its
`contexts`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListContexts`

requests and continue to iterate
through the `contexts`

field on the
corresponding responses.

All the usual [ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListContextsAsyncPager

```
ListContextsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesjob_servicepagerslistcustomjobsasyncpager_goog_2c0807.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesjob_servicepagerslistcustomjobsasyncpager_googl_303600.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslistcustomjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListCustomJobsAsyncPager -->

# Class ListCustomJobsAsyncPager (1.134.0)

```
ListCustomJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse,
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


A pager for iterating through `list_custom_jobs`

requests.

This class thinly wraps an initial
[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`custom_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListCustomJobs`

requests and continue to iterate
through the `custom_jobs`

field on the
corresponding responses.

All the usual [ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListCustomJobsAsyncPager

```
ListCustomJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslistnastrialdetailspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasTrialDetailsPager -->

# Class ListNasTrialDetailsPager (1.134.0)

```
ListNasTrialDetailsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse,
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


A pager for iterating through `list_nas_trial_details`

requests.

This class thinly wraps an initial
[ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsResponse) object, and
provides an `__iter__`

method to iterate through its
`nas_trial_details`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNasTrialDetails`

requests and continue to iterate
through the `nas_trial_details`

field on the
corresponding responses.

All the usual [ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNasTrialDetailsPager

```
ListNasTrialDetailsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesvertex_rag_data_servicepagerslistragcorporapage_343a03.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvertex_rag_data_servicepagerslistragcorporapager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagCorporaPager -->

# Class ListRagCorporaPager (1.134.0)

```
ListRagCorporaPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
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


A pager for iterating through `list_rag_corpora`

requests.

This class thinly wraps an initial
[ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse) object, and
provides an `__iter__`

method to iterate through its
`rag_corpora`

field.

If there are more pages, the `__iter__`

method will make additional
`ListRagCorpora`

requests and continue to iterate
through the `rag_corpora`

field on the
corresponding responses.

All the usual [ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRagCorporaPager

```
ListRagCorporaPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesrebasetunedmodelrequest_googlecloudaiplatform_v1be_ca3f5e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesrebasetunedmodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebaseTunedModelRequest -->

# Class RebaseTunedModelRequest (1.134.0)

`RebaseTunedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.RebaseTunedModel.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location into which to rebase the Model. Format: `projects/{project}/locations/{location}`
|
`tuned_model_ref` |
Required. TunedModel reference to retrieve the legacy model information. |
`tuning_job` |
Optional. The TuningJob to be updated. Users can use this TuningJob field to overwrite tuning configs. |
`artifact_destination` |
Optional. The Google Cloud Storage location to write the artifacts. |
`deploy_to_same_endpoint` |
`bool`
Optional. By default, bison to gemini migration will always create new model/endpoint, but for gemini-1.0 to gemini-1.5 migration, we default deploy to the same endpoint. See details in this Section. |

## Methods

### RebaseTunedModelRequest

`RebaseTunedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.RebaseTunedModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturestorestate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Featurestore.State -->

# Class State (1.134.0)

`State(value)`


Possible states a featurestore can have.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Default value. This value is unused. |
`STABLE` |
State when the featurestore configuration is not being updated and the fields reflect the current configuration of the featurestore. The featurestore is usable in this state. |
`UPDATING` |
The state of the featurestore configuration when it is being updated. During an update, the fields reflect either the original configuration or the updated configuration of the featurestore. For example, `online_serving_config.fixed_node_count` can take minutes to update. While the update is in progress, the featurestore is in the UPDATING state, and the value of `fixed_node_count` can be the original value or the updated value, depending on the progress of the operation. Until the update completes, the actual number of nodes can still be the original value of `fixed_node_count`. The featurestore is still usable in this state. |

## Methods

### State

`State(value)`


Possible states a featurestore can have.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardspage_4e6c39.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardspager_83044f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardspager__023e54.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardsPager -->

# Class ListTensorboardsPager (1.134.0)

```
ListTensorboardsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse,
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


A pager for iterating through `list_tensorboards`

requests.

This class thinly wraps an initial
[ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboards`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboards`

requests and continue to iterate
through the `tensorboards`

field on the
corresponding responses.

All the usual [ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardsPager

```
ListTensorboardsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicepagerslistragfilespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagFilesPager -->

# Class ListRagFilesPager (1.134.0)

```
ListRagFilesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse,
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


A pager for iterating through `list_rag_files`

requests.

This class thinly wraps an initial
[ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse) object, and
provides an `__iter__`

method to iterate through its
`rag_files`

field.

If there are more pages, the `__iter__`

method will make additional
`ListRagFiles`

requests and continue to iterate
through the `rag_files`

field on the
corresponding responses.

All the usual [ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRagFilesPager

```
ListRagFilesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesexample_store_servicepagersfetchexamplespa_d26771.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesexample_store_servicepagersfetchexamplespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.FetchExamplesPager -->

# Class FetchExamplesPager (1.134.0)

```
FetchExamplesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse,
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


A pager for iterating through `fetch_examples`

requests.

This class thinly wraps an initial
[FetchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse) object, and
provides an `__iter__`

method to iterate through its
`examples`

field.

If there are more pages, the `__iter__`

method will make additional
`FetchExamples`

requests and continue to iterate
through the `examples`

field on the
corresponding responses.

All the usual [FetchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### FetchExamplesPager

```
FetchExamplesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesindex_servicepagerslistindexesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.pagers.ListIndexesAsyncPager -->

# Class ListIndexesAsyncPager (1.134.0)

```
ListIndexesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse,
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


A pager for iterating through `list_indexes`

requests.

This class thinly wraps an initial
[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse) object, and
provides an `__aiter__`

method to iterate through its
`indexes`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListIndexes`

requests and continue to iterate
through the `indexes`

field on the
corresponding responses.

All the usual [ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListIndexesAsyncPager

```
ListIndexesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesragfilechunkingconfig_googlecloudaiplatform_v1be_a99de2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesragfilechunkingconfig_googlecloudaiplatform_v1bet_92deaf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesragfilechunkingconfig_googlecloudaiplatform_v1beta_bf6f70.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragfilechunkingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagFileChunkingConfig -->

# Class RagFileChunkingConfig (1.134.0)

`RagFileChunkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the size and overlap of chunks for RagFiles.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`fixed_length_chunking` |
Specifies the fixed length chunking config. This field is a member of `oneof` _ `chunking_config` .
|

## Classes

### FixedLengthChunking

`FixedLengthChunking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the fixed length chunking config.

## Methods

### RagFileChunkingConfig

`RagFileChunkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the size and overlap of chunks for RagFiles.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectorysingletoolusespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseSpec -->

# Class TrajectorySingleToolUseSpec (1.134.0)

`TrajectorySingleToolUseSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectorySingleToolUse metric - returns 1 if tool is present in the predicted trajectory, else 0.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`tool_name` |
`str`
Required. Spec for tool name to be checked for in the predicted trajectory. This field is a member of `oneof` _ `_tool_name` .
|

## Methods

### TrajectorySingleToolUseSpec

`TrajectorySingleToolUseSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectorySingleToolUse metric - returns 1 if tool is present in the predicted trajectory, else 0.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigtrainingpredictionsk_998e41.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigtrainingpredictionskewdetectionconfigskewthresholdsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.TrainingPredictionSkewDetectionConfig.SkewThresholdsEntry -->

# Class SkewThresholdsEntry (1.134.0)

`SkewThresholdsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### SkewThresholdsEntry

`SkewThresholdsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesindexdatapointnumericrestrictionoperator.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexDatapoint.NumericRestriction.Operator -->

# Class Operator (1.134.0)

`Operator(value)`


Which comparison operator to use. Should be specified for queries only; specifying this for a datapoint is an error.

Datapoints for which Operator is true relative to the query's Value field will be allowlisted.

## Enums |
|
|---|---|
Name |
Description |
`OPERATOR_UNSPECIFIED` |
Default value of the enum. |
`LESS` |
Datapoints are eligible iff their value is < the=""> |
`LESS_EQUAL` |
Datapoints are eligible iff their value is <= the=""> |
`EQUAL` |
Datapoints are eligible iff their value is == the query's. |
`GREATER_EQUAL` |
Datapoints are eligible iff their value is >= the query's. |
`GREATER` |
Datapoints are eligible iff their value is > the query's. |
`NOT_EQUAL` |
Datapoints are eligible iff their value is != the query's. |

## Methods

### Operator

`Operator(value)`


Which comparison operator to use. Should be specified for queries only; specifying this for a datapoint is an error.

Datapoints for which Operator is true relative to the query's Value field will be allowlisted.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestensorboardrun_googlecloudaiplatform_v1beta1servic_4cfe2b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestensorboardrun.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardRun -->

# Class TensorboardRun (1.134.0)

`TensorboardRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the TensorboardRun. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|
`display_name` |
`str`
Required. User provided name of this TensorboardRun. This value must be unique among all TensorboardRuns belonging to the same parent TensorboardExperiment. |
`description` |
`str`
Description of this TensorboardRun. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardRun was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardRun was last updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your TensorboardRuns. This field will be used to filter and visualize Runs in the Tensorboard UI. For example, a Vertex AI training job can set a label aiplatform.googleapis.com/training_job_id=xxxxx to all the runs created within that job. An end user can set a label experiment_id=xxxxx for all the runs produced in a Jupyter notebook. These runs can be grouped by a label value and visualized together in the Tensorboard UI. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one TensorboardRun (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`etag` |
`str`
Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |

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

### TensorboardRun

`TensorboardRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicespipeline_servicepagerslistpipelinejobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListPipelineJobsPager -->

# Class ListPipelineJobsPager (1.134.0)

```
ListPipelineJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsResponse,
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


A pager for iterating through `list_pipeline_jobs`

requests.

This class thinly wraps an initial
[ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`pipeline_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPipelineJobs`

requests and continue to iterate
through the `pipeline_jobs`

field on the
corresponding responses.

All the usual [ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPipelineJobsPager

```
ListPipelineJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |
