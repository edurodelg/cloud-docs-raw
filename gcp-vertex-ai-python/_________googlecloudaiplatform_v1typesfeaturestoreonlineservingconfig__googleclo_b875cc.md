---
merged_at: 2026-01-28T15:11:44.779079
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Featurestore.OnlineServingConfig -->

# Class OnlineServingConfig (1.135.0)

`OnlineServingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


OnlineServingConfig specifies the details for provisioning online serving resources.

## Attributes |
|
|---|---|
Name |
Description |
`fixed_node_count` |
`int`
The number of nodes for the online store. The number of nodes doesn't scale automatically, but you can manually update the number of nodes. If set to 0, the featurestore will not have an online store and cannot be used for online serving. |
`scaling` |
Online serving scaling configuration. Only one of `fixed_node_count` and `scaling` can be set. Setting one
will reset the other.
|

## Classes

### Scaling

`Scaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Online serving scaling configuration. If min_node_count and max_node_count are set to the same value, the cluster will be configured with the fixed number of node (no auto-scaling).

## Methods

### OnlineServingConfig

`OnlineServingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


OnlineServingConfig specifies the details for provisioning online serving resources.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchExamplesResponse.SimilarExample -->

# Class SimilarExample (1.135.0)

`SimilarExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result of the similar example.

## Attributes |
|
|---|---|
Name |
Description |
`example` |
The example that is similar to the searched query. |
`similarity_score` |
`float`
The similarity score of this example. |

## Methods

### SimilarExample

`SimilarExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result of the similar example.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingRawPredictResponse -->

# Class StreamingRawPredictResponse (1.135.0)

`StreamingRawPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamingRawPredict.

## Attribute |
|
|---|---|
Name |
Description |
`output` |
`bytes`
The prediction output. |

## Methods

### StreamingRawPredictResponse

`StreamingRawPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamingRawPredict.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PythonPackageSpec -->

# Class PythonPackageSpec (1.135.0)

`PythonPackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Python packaged code.

## Attributes |
|
|---|---|
Name |
Description |
`executor_image_uri` |
`str`
Required. The URI of a container image in Artifact Registry that will run the provided Python package. Vertex AI provides a wide range of executor images with pre-installed packages to meet users' various use cases. See the list of `pre-built containers for training |
`package_uris` |
`MutableSequence[str]`
Required. The Google Cloud Storage location of the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100. |
`python_module` |
`str`
Required. The Python module name to run after installing the packages. |
`args` |
`MutableSequence[str]`
Command line arguments to be passed to the Python task. |
`env` |
`MutableSequence[`
Environment variables to be passed to the python module. Maximum limit is 100. |

## Methods

### PythonPackageSpec

`PythonPackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Python packaged code.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveExamplesResponse -->

# Class RemoveExamplesResponse (1.135.0)

`RemoveExamplesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.RemoveExamples.

## Attribute |
|
|---|---|
Name |
Description |
`example_ids` |
`MutableSequence[str]`
The IDs for the removed examples. |

## Methods

### RemoveExamplesResponse

`RemoveExamplesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.RemoveExamples.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SafetyRating.HarmSeverity -->

# Class HarmSeverity (1.135.0)

`HarmSeverity(value)`


Harm severity levels.

## Enums |
|
|---|---|
Name |
Description |
`HARM_SEVERITY_UNSPECIFIED` |
Harm severity unspecified. |
`HARM_SEVERITY_NEGLIGIBLE` |
Negligible level of harm severity. |
`HARM_SEVERITY_LOW` |
Low level of harm severity. |
`HARM_SEVERITY_MEDIUM` |
Medium level of harm severity. |
`HARM_SEVERITY_HIGH` |
High level of harm severity. |

## Methods

### HarmSeverity

`HarmSeverity(value)`


Harm severity levels.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DataLabelingJob -->

# Class DataLabelingJob (1.135.0)

`DataLabelingJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset:

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the DataLabelingJob. |
`display_name` |
`str`
Required. The user-defined name of the DataLabelingJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. Display name of a DataLabelingJob. |
`datasets` |
`MutableSequence[str]`
Required. Dataset resource names. Right now we only support labeling from a single Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`annotation_labels` |
`MutableMapping[str, str]`
Labels to assign to annotations generated by this DataLabelingJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`labeler_count` |
`int`
Required. Number of labelers to work on each DataItem. |
`instruction_uri` |
`str`
Required. The Google Cloud Storage location of the instruction pdf. This pdf is shared with labelers, and provides detailed description on how to label DataItems in Datasets. |
`inputs_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing the config for a specific type of DataLabelingJob. The schema files that can be used here are found in the https://storage.googleapis.com/google-cloud-aiplatform bucket in the /schema/datalabelingjob/inputs/ folder. |
`inputs` |
`google.protobuf.struct_pb2.Value`
Required. Input config parameters for the DataLabelingJob. |
`state` |
Output only. The detailed state of the job. |
`labeling_progress` |
`int`
Output only. Current labeling job progress percentage scaled in interval [0, 100], indicating the percentage of DataItems that has been finished. |
`current_spend` |
`google.type.money_pb2.Money`
Output only. Estimated cost(in US dollars) that the DataLabelingJob has incurred to date. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataLabelingJob was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataLabelingJob was updated most recently. |
`error` |
`google.rpc.status_pb2.Status`
Output only. DataLabelingJob errors. It is only populated when job's state is `JOB_STATE_FAILED` or
`JOB_STATE_CANCELLED` .
|
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your DataLabelingJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each DataLabelingJob: - "aiplatform.googleapis.com/schema": output only, its value is the inputs_schema's title. |
`specialist_pools` |
`MutableSequence[str]`
The SpecialistPools' resource names associated with this job. |
`encryption_spec` |
Customer-managed encryption key spec for a DataLabelingJob. If set, this DataLabelingJob will be secured by this key. Note: Annotations created in the DataLabelingJob are associated with the EncryptionSpec of the Dataset they are exported to. |
`active_learning_config` |
Parameters that configure the active learning pipeline. Active learning will label the data incrementally via several iterations. For every iteration, it will select a batch of data based on the sampling strategy. |

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

### DataLabelingJob

`DataLabelingJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.InputMetadata.Visualization -->

# Class Visualization (1.135.0)

`Visualization(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Visualization configurations for image explanation.

## Attributes |
|
|---|---|
Name |
Description |
`type_` |
Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.integrated_gradients_attribution]. OUTLINES shows regions of attribution, while PIXELS shows per-pixel attribution. Defaults to OUTLINES. |
`polarity` |
Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE. |
`color_map` |
The color scheme used for the highlighted areas. Defaults to PINK_GREEN for [Integrated Gradients attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.integrated_gradients_attribution], which shows positive attributions in green and negative in pink. Defaults to VIRIDIS for [XRAI attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.xrai_attribution], which highlights the most influential regions in yellow and the least influential in blue. |
`clip_percent_upperbound` |
`float`
Excludes attributions above the specified percentile from the highlighted areas. Using the clip_percent_upperbound and clip_percent_lowerbound together can be useful for filtering out noise and making it easier to see areas of strong attribution. Defaults to 99.9. |
`clip_percent_lowerbound` |
`float`
Excludes attributions below the specified percentile, from the highlighted areas. Defaults to 62. |
`overlay_type` |
How the original image is displayed in the visualization. Adjusting the overlay can help increase visual clarity if the original image makes it difficult to view the visualization. Defaults to NONE. |

## Classes

### ColorMap

`ColorMap(value)`


The color scheme used for highlighting areas.

### OverlayType

`OverlayType(value)`


How the original image is displayed in the visualization.

### Polarity

`Polarity(value)`


Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.

### Type

`Type(value)`


Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.integrated_gradients_attribution].

## Methods

### Visualization

`Visualization(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Visualization configurations for image explanation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.ConditionalParameterSpec -->

# Class ConditionalParameterSpec (1.135.0)

`ConditionalParameterSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a parameter spec with condition from its parent parameter.

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
`parent_discrete_values` |
The spec for matching values from a parent parameter of `DISCRETE` type.
This field is a member of `oneof` _ `parent_value_condition` .
|
`parent_int_values` |
The spec for matching values from a parent parameter of `INTEGER` type.
This field is a member of `oneof` _ `parent_value_condition` .
|
`parent_categorical_values` |
The spec for matching values from a parent parameter of `CATEGORICAL` type.
This field is a member of `oneof` _ `parent_value_condition` .
|
`parameter_spec` |
`google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec`
Required. The spec for a conditional parameter. |

## Classes

### CategoricalValueCondition

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.

### DiscreteValueCondition

`DiscreteValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match discrete values from parent parameter.

### IntValueCondition

`IntValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match integer values from parent parameter.

## Methods

### ConditionalParameterSpec

`ConditionalParameterSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a parameter spec with condition from its parent parameter.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DataLabelingJob -->

# Class DataLabelingJob (1.135.0)

`DataLabelingJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset:

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the DataLabelingJob. |
`display_name` |
`str`
Required. The user-defined name of the DataLabelingJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. Display name of a DataLabelingJob. |
`datasets` |
`MutableSequence[str]`
Required. Dataset resource names. Right now we only support labeling from a single Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`annotation_labels` |
`MutableMapping[str, str]`
Labels to assign to annotations generated by this DataLabelingJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`labeler_count` |
`int`
Required. Number of labelers to work on each DataItem. |
`instruction_uri` |
`str`
Required. The Google Cloud Storage location of the instruction pdf. This pdf is shared with labelers, and provides detailed description on how to label DataItems in Datasets. |
`inputs_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing the config for a specific type of DataLabelingJob. The schema files that can be used here are found in the https://storage.googleapis.com/google-cloud-aiplatform bucket in the /schema/datalabelingjob/inputs/ folder. |
`inputs` |
`google.protobuf.struct_pb2.Value`
Required. Input config parameters for the DataLabelingJob. |
`state` |
Output only. The detailed state of the job. |
`labeling_progress` |
`int`
Output only. Current labeling job progress percentage scaled in interval [0, 100], indicating the percentage of DataItems that has been finished. |
`current_spend` |
`google.type.money_pb2.Money`
Output only. Estimated cost(in US dollars) that the DataLabelingJob has incurred to date. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataLabelingJob was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataLabelingJob was updated most recently. |
`error` |
`google.rpc.status_pb2.Status`
Output only. DataLabelingJob errors. It is only populated when job's state is `JOB_STATE_FAILED` or
`JOB_STATE_CANCELLED` .
|
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your DataLabelingJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each DataLabelingJob: - "aiplatform.googleapis.com/schema": output only, its value is the inputs_schema's title. |
`specialist_pools` |
`MutableSequence[str]`
The SpecialistPools' resource names associated with this job. |
`encryption_spec` |
Customer-managed encryption key spec for a DataLabelingJob. If set, this DataLabelingJob will be secured by this key. Note: Annotations created in the DataLabelingJob are associated with the EncryptionSpec of the Dataset they are exported to. |
`active_learning_config` |
Parameters that configure the active learning pipeline. Active learning will label the data incrementally via several iterations. For every iteration, it will select a batch of data based on the sampling strategy. |

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

### DataLabelingJob

`DataLabelingJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset:

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetCachedContentRequest -->

# Class GetCachedContentRequest (1.135.0)

`GetCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.GetCachedContent.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name referring to the cached content |

## Methods

### GetCachedContentRequest

`GetCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.GetCachedContent.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteOperationMetadata -->

# Class DeleteOperationMetadata (1.135.0)

`DeleteOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform deletes of any entities.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### DeleteOperationMetadata

`DeleteOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform deletes of any entities.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.JobState -->

# Class JobState (1.135.0)

`JobState(value)`


Describes the state of a job.

## Enums |
|
|---|---|
Name |
Description |
`JOB_STATE_UNSPECIFIED` |
The job state is unspecified. |
`JOB_STATE_QUEUED` |
The job has been just created or resumed and processing has not yet begun. |
`JOB_STATE_PENDING` |
The service is preparing to run the job. |
`JOB_STATE_RUNNING` |
The job is in progress. |
`JOB_STATE_SUCCEEDED` |
The job completed successfully. |
`JOB_STATE_FAILED` |
The job failed. |
`JOB_STATE_CANCELLING` |
The job is being cancelled. From this state the job may only go to either `JOB_STATE_SUCCEEDED`, `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED`. |
`JOB_STATE_CANCELLED` |
The job has been cancelled. |
`JOB_STATE_PAUSED` |
The job has been stopped, and can be resumed. |
`JOB_STATE_EXPIRED` |
The job has expired. |
`JOB_STATE_UPDATING` |
The job is being updated. Only jobs in the `RUNNING` state can be updated. After updating, the job goes back to the `RUNNING` state. |
`JOB_STATE_PARTIALLY_SUCCEEDED` |
The job is partially succeeded, some results may be missing due to errors. |

## Methods

### JobState

`JobState(value)`


Describes the state of a job.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateArtifactRequest -->

# Class CreateArtifactRequest (1.135.0)

`CreateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateArtifact.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Artifact should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`artifact` |
Required. The Artifact to create. |
`artifact_id` |
`str`
The {artifact} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
If not provided, the Artifact's ID will be a UUID generated
by the service. Must be 4-128 characters in length. Valid
characters are `/` a-z][0-9]`-/` . Must be unique across all
Artifacts in the parent MetadataStore. (Otherwise the
request will fail with ALREADY_EXISTS, or PERMISSION_DENIED
if the caller can't view the preexisting Artifact.)
|

## Methods

### CreateArtifactRequest

`CreateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateArtifact.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.DirectNotebookSource -->

# Class DirectNotebookSource (1.135.0)

`DirectNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The content of the input notebook in ipynb format.

## Attribute |
|
|---|---|
Name |
Description |
`content` |
`bytes`
The base64-encoded contents of the input notebook file. |

## Methods

### DirectNotebookSource

`DirectNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The content of the input notebook in ipynb format.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeContextsMetadata -->

# Class PurgeContextsMetadata (1.135.0)

`PurgeContextsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeContexts.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for purging Contexts. |

## Methods

### PurgeContextsMetadata

`PurgeContextsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeContexts.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.Deploy.DeployMetadata -->

# Class DeployMetadata (1.135.0)

`DeployMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata information about the deployment for managing deployment config.

## Attributes |
|
|---|---|
Name |
Description |
`labels` |
`MutableMapping[str, str]`
Optional. Labels for the deployment. For managing deployment config like verifying, source of deployment config, etc. |
`sample_request` |
`str`
Optional. Sample request for deployed endpoint. |

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

### DeployMetadata

`DeployMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata information about the deployment for managing deployment config.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidInput -->

# Class ToolCallValidInput (1.135.0)

`ToolCallValidInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for tool call valid metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for tool call valid metric. |
`instances` |
`MutableSequence[`
Required. Repeated tool call valid instances. |

## Methods

### ToolCallValidInput

`ToolCallValidInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for tool call valid metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchInput -->

# Class ToolNameMatchInput (1.135.0)

`ToolNameMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for tool name match metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for tool name match metric. |
`instances` |
`MutableSequence[`
Required. Repeated tool name match instances. |

## Methods

### ToolNameMatchInput

`ToolNameMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for tool name match metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Featurestore.OnlineServingConfig -->

# Class OnlineServingConfig (1.135.0)

`OnlineServingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


OnlineServingConfig specifies the details for provisioning online serving resources.

## Attributes |
|
|---|---|
Name |
Description |
`fixed_node_count` |
`int`
The number of nodes for the online store. The number of nodes doesn't scale automatically, but you can manually update the number of nodes. If set to 0, the featurestore will not have an online store and cannot be used for online serving. |
`scaling` |
Online serving scaling configuration. Only one of `fixed_node_count` and `scaling` can be set. Setting one
will reset the other.
|

## Classes

### Scaling

`Scaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Online serving scaling configuration. If min_node_count and max_node_count are set to the same value, the cluster will be configured with the fixed number of node (no auto-scaling).

## Methods

### OnlineServingConfig

`OnlineServingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


OnlineServingConfig specifies the details for provisioning online serving resources.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PythonPackageSpec -->

# Class PythonPackageSpec (1.135.0)

`PythonPackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Python packaged code.

## Attributes |
|
|---|---|
Name |
Description |
`executor_image_uri` |
`str`
Required. The URI of a container image in Artifact Registry that will run the provided Python package. Vertex AI provides a wide range of executor images with pre-installed packages to meet users' various use cases. See the list of `pre-built containers for training |
`package_uris` |
`MutableSequence[str]`
Required. The Google Cloud Storage location of the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100. |
`python_module` |
`str`
Required. The Python module name to run after installing the packages. |
`args` |
`MutableSequence[str]`
Command line arguments to be passed to the Python task. |
`env` |
`MutableSequence[`
Environment variables to be passed to the python module. Maximum limit is 100. |

## Methods

### PythonPackageSpec

`PythonPackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Python packaged code.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardRun -->

# Class TensorboardRun (1.135.0)

```
TensorboardRun(
tensorboard_run_name: str,
tensorboard_id: typing.Optional[str] = None,
tensorboard_experiment_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Managed tensorboard resource for Vertex AI.

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

### TensorboardRun

```
TensorboardRun(
tensorboard_run_name: str,
tensorboard_id: typing.Optional[str] = None,
tensorboard_experiment_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing tensorboard run given a tensorboard run name or ID.

```
Example Usage:
tb_run = aiplatform.TensorboardRun(
tensorboard_run_name= "projects/123/locations/us-central1/tensorboards/456/experiments/678/run/8910"
)
tb_run = aiplatform.TensorboardRun(
tensorboard_run_name= "8910",
tensorboard_id = "456",
tensorboard_experiment_id = "678"
)
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_run_name` |
`str`
Required. A fully-qualified tensorboard run resource name or resource ID. Example: "projects/123/locations/us-central1/tensorboards/456/experiments/678/runs/8910" or "8910" when tensorboard_id and tensorboard_experiment_id are passed and project and location are initialized or passed. |
`tensorboard_id` |
`str`
Optional. A tensorboard resource ID. |
`tensorboard_experiment_id` |
`str`
Optional. A tensorboard experiment resource ID. |
`project` |
`str`
Optional. Project to retrieve tensorboard from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve tensorboard from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Tensorboard. Overrides credentials set in aiplatform.init. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
if only one of tensorboard_id or tensorboard_experiment_id is provided. |

### create

```
create(
tensorboard_run_id: str,
tensorboard_experiment_name: str,
tensorboard_id: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Sequence[typing.Tuple[str, str]] = (),
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.tensorboard.tensorboard_resource.TensorboardRun
```


Creates a new tensorboard run.

Example Usage:

```
tb_run = aiplatform.TensorboardRun.create(
tensorboard_run_id='my-run'
tensorboard_experiment_name='my-experiment'
tensorboard_id='456'
display_name='my display name',
description='my description',
labels={
'key1': 'value1',
'key2': 'value2'
}
)
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_run_id` |
`str`
Required. The ID to use for the Tensorboard run, which will become the final component of the Tensorboard run's resource name. This value should be 1-128 characters, and valid: characters are / |
`tensorboard_experiment_name` |
`str`
Required. The resource name or ID of the TensorboardExperiment to create the TensorboardRun in. Resource name format: |
`tensorboard_id` |
`str`
Optional. The resource ID of the Tensorboard to create the TensorboardRun in. |
`display_name` |
`str`
Optional. The user-defined name of the Tensorboard Run. This value must be unique among all TensorboardRuns belonging to the same parent TensorboardExperiment. If not provided tensorboard_run_id will be used. |
`description` |
`str`
Optional. Description of this Tensorboard Run. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See |
`project` |
`str`
Optional. Project to upload this model to. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to upload this model to. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`TensorboardRun` |
The TensorboardRun resource. |

### create_tensorboard_time_series

```
create_tensorboard_time_series(
display_name: str,
value_type: typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_time_series.TensorboardTimeSeries.ValueType,
str,
] = "SCALAR",
plugin_name: str = "scalars",
plugin_data: typing.Optional[bytes] = None,
description: typing.Optional[str] = None,
) -> google.cloud.aiplatform.tensorboard.tensorboard_resource.TensorboardTimeSeries
```


Creates a new tensorboard time series.

Example Usage:

```
tb_ts = tensorboard_run.create_tensorboard_time_series(
display_name='my display name',
tensorboard_run_name='my-run'
tensorboard_id='456'
tensorboard_experiment_id='my-experiment'
description='my description',
labels={
'key1': 'value1',
'key2': 'value2'
}
)
```


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. User provided name of this TensorboardTimeSeries. This value should be unique among all TensorboardTimeSeries resources belonging to the same TensorboardRun resource (parent resource). |
`value_type` |
`Union[gca_tensorboard_time_series.TensorboardTimeSeries.ValueType, str]`
Optional. Type of TensorboardTimeSeries value. One of 'SCALAR', 'TENSOR', 'BLOB_SEQUENCE'. |
`plugin_name` |
`str`
Optional. Name of the plugin this time series pertain to. Such as Scalar, Tensor, Blob. |
`plugin_data` |
`bytes`
Optional. Data of the current plugin, with the size limited to 65KB. |
`description` |
`str`
Optional. Description of this TensorboardTimeseries. |

Returns |
|
|---|---|
Type |
Description |
`TensorboardTimeSeries` |
The TensorboardTimeSeries resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### list

```
list(
tensorboard_experiment_name: str,
tensorboard_id: typing.Optional[str] = None,
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[
google.cloud.aiplatform.tensorboard.tensorboard_resource.TensorboardRun
]
```


List all instances of TensorboardRun in TensorboardExperiment.

Example Usage:

```
aiplatform.TensorboardRun.list(
tensorboard_experiment_name='projects/my-project/locations/us-central1/tensorboards/123/experiments/456'
)
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_experiment_name` |
`str`
Required. The resource name or resource ID of the TensorboardExperiment to list TensorboardRun. Format, if resource name: 'projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}' If resource ID is provided then tensorboard_id must be provided. |
`tensorboard_id` |
`str`
Optional. The resource ID of the Tensorboard that contains the TensorboardExperiment to list TensorboardRun. |
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

### read_time_series_data

```
read_time_series_data() -> (
typing.Dict[str, google.cloud.aiplatform_v1.types.tensorboard_data.TimeSeriesData]
)
```


Read the time series data of this run.

```
time_series_data = tensorboard_run.read_time_series_data()
print(time_series_data['loss'].values[-1].scalar.value)
```


### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### write_tensorboard_scalar_data

```
write_tensorboard_scalar_data(
time_series_data: typing.Dict[str, float],
step: int,
wall_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
)
```


Writes tensorboard scalar data to this run.

Parameters |
|
|---|---|
Name |
Description |
`time_series_data` |
`Dict[str, float]`
Required. Dictionary of where keys are TensorboardTimeSeries display name and values are the scalar value.. |
`step` |
`int`
Required. Step index of this data point within the run. |
`wall_time` |
`timestamp_pb2.Timestamp`
Optional. Wall clock timestamp when this data point is generated by the end user. If not provided, this will be generated based on the value from time.time() |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient -->

# Class IndexServiceAsyncClient (1.135.0)

```
IndexServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's Index resources.

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
`IndexServiceTransport` |
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

### IndexServiceAsyncClient

```
IndexServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the index service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,IndexServiceTransport,Callable[..., IndexServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the IndexServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_index

```
create_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.CreateIndexRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
index: typing.Optional[google.cloud.aiplatform_v1.types.index.Index] = None,
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


Creates an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
index = aiplatform_v1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1.[CreateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateIndexRequest.html)(
parent="parent_value",
index=index,
)
# Make the request
operation = client.[create_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_create_index)(request=request)
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
The request object. Request message for IndexService.CreateIndex. |
`parent` |
Required. The resource name of the Location to create the Index in. Format: |
`index` |
Required. The Index to create. This corresponds to the |
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

### delete_index

```
delete_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.DeleteIndexRequest, dict
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


Deletes an Index. An Index can only be deleted when all its xref_DeployedIndexes had been undeployed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteIndexRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_delete_index)(request=request)
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
The request object. Request message for IndexService.DeleteIndex. |
`name` |
Required. The name of the Index resource to be deleted. Format: |
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
`IndexServiceAsyncClient` |
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
`IndexServiceAsyncClient` |
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
`IndexServiceAsyncClient` |
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

### get_index

```
get_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.GetIndexRequest, dict
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
) -> google.cloud.aiplatform_v1.types.index.Index
```


Gets an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetIndexRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_get_index)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.GetIndex |
`name` |
Required. The name of the Index resource. Format: |
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
A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search. |

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
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport
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

### index_endpoint_path

`index_endpoint_path(project: str, location: str, index_endpoint: str) -> str`


Returns a fully-qualified index_endpoint string.

### index_path

`index_path(project: str, location: str, index: str) -> str`


Returns a fully-qualified index string.

### list_indexes

```
list_indexes(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.ListIndexesRequest, dict
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
) -> google.cloud.aiplatform_v1.services.index_service.pagers.ListIndexesAsyncPager
```


Lists Indexes in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_indexes():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListIndexesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_indexes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_list_indexes)(request=request)
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
The request object. Request message for IndexService.ListIndexes. |
`parent` |
Required. The resource name of the Location from which to list the Indexes. Format: |
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
Response message for IndexService.ListIndexes. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_index_endpoint_path

`parse_index_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a index_endpoint path into its component segments.

### parse_index_path

`parse_index_path(path: str) -> typing.Dict[str, str]`


Parses a index path into its component segments.

### remove_datapoints

```
remove_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.RemoveDatapointsRequest, dict
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
) -> google.cloud.aiplatform_v1.types.index_service.RemoveDatapointsResponse
```


Remove Datapoints from an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_remove_datapoints():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RemoveDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RemoveDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = await client.[remove_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_remove_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.RemoveDatapoints |
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
Response message for IndexService.RemoveDatapoints |

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

### update_index

```
update_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.UpdateIndexRequest, dict
]
] = None,
*,
index: typing.Optional[google.cloud.aiplatform_v1.types.index.Index] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
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


Updates an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
index = aiplatform_v1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1.[UpdateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateIndexRequest.html)(
index=index,
)
# Make the request
operation = client.[update_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_update_index)(request=request)
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
The request object. Request message for IndexService.UpdateIndex. |
`index` |
Required. The Index which updates the resource on the server. This corresponds to the |
`update_mask` |
The update mask applies to the resource. For the |
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

### upsert_datapoints

```
upsert_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.UpsertDatapointsRequest, dict
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
) -> google.cloud.aiplatform_v1.types.index_service.UpsertDatapointsResponse
```


Add/update Datapoints into an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_upsert_datapoints():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpsertDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpsertDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = await client.[upsert_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_upsert_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.UpsertDatapoints |
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
Response message for IndexService.UpsertDatapoints |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteTensorboardExperimentDataResponse -->

# Class WriteTensorboardExperimentDataResponse (1.135.0)

```
WriteTensorboardExperimentDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.WriteTensorboardExperimentData.

## Methods

### WriteTensorboardExperimentDataResponse

```
WriteTensorboardExperimentDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.WriteTensorboardExperimentData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntimeTemplateRef -->

# Class NotebookRuntimeTemplateRef (1.135.0)

`NotebookRuntimeTemplateRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a NotebookRuntimeTemplateRef.

## Attribute |
|
|---|---|
Name |
Description |
`notebook_runtime_template` |
`str`
Immutable. A resource name of the NotebookRuntimeTemplate. |

## Methods

### NotebookRuntimeTemplateRef

`NotebookRuntimeTemplateRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a NotebookRuntimeTemplateRef.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagFileChunkingConfig.FixedLengthChunking -->

# Class FixedLengthChunking (1.135.0)

`FixedLengthChunking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the fixed length chunking config.

## Attributes |
|
|---|---|
Name |
Description |
`chunk_size` |
`int`
The size of the chunks. |
`chunk_overlap` |
`int`
The overlap between chunks. |

## Methods

### FixedLengthChunking

`FixedLengthChunking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the fixed length chunking config.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Schedule.RunResponse -->

# Class RunResponse (1.135.0)

`RunResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Status of a scheduled run.

## Attributes |
|
|---|---|
Name |
Description |
`scheduled_run_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The scheduled run time based on the user-specified schedule. |
`run_response` |
`str`
The response of the scheduled run. |

## Methods

### RunResponse

`RunResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Status of a scheduled run.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DnsPeeringConfig -->

# Class DnsPeeringConfig (1.135.0)

`DnsPeeringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DNS peering configuration. These configurations are used to create DNS peering zones in the Vertex tenant project VPC, enabling resolution of records within the specified domain hosted in the target network's Cloud DNS.

## Attributes |
|
|---|---|
Name |
Description |
`domain` |
`str`
Required. The DNS name suffix of the zone being peered to, e.g., "my-internal-domain.corp.". Must end with a dot. |
`target_project` |
`str`
Required. The project ID hosting the Cloud DNS managed zone that contains the 'domain'. The Vertex AI Service Agent requires the dns.peer role on this project. |
`target_network` |
`str`
Required. The VPC network name in the target_project where the DNS zone specified by 'domain' is visible. |

## Methods

### DnsPeeringConfig

`DnsPeeringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DNS peering configuration. These configurations are used to create DNS peering zones in the Vertex tenant project VPC, enabling resolution of records within the specified domain hosted in the target network's Cloud DNS.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.BigQuerySource -->

# Class BigQuerySource (1.135.0)

`BigQuerySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
Required. The BigQuery view URI that will be materialized on each sync trigger based on FeatureView.SyncConfig. |
`entity_id_columns` |
`MutableSequence[str]`
Required. Columns to construct entity_id / row keys. |

## Methods

### BigQuerySource

`BigQuerySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTrialRequest -->

# Class GetTrialRequest (1.135.0)

`GetTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.GetTrial.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Trial resource. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|

## Methods

### GetTrialRequest

`GetTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.GetTrial.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.JobState -->

# Class JobState (1.135.0)

`JobState(value)`


Describes the state of a job.

## Enums |
|
|---|---|
Name |
Description |
`JOB_STATE_UNSPECIFIED` |
The job state is unspecified. |
`JOB_STATE_QUEUED` |
The job has been just created or resumed and processing has not yet begun. |
`JOB_STATE_PENDING` |
The service is preparing to run the job. |
`JOB_STATE_RUNNING` |
The job is in progress. |
`JOB_STATE_SUCCEEDED` |
The job completed successfully. |
`JOB_STATE_FAILED` |
The job failed. |
`JOB_STATE_CANCELLING` |
The job is being cancelled. From this state the job may only go to either `JOB_STATE_SUCCEEDED`, `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED`. |
`JOB_STATE_CANCELLED` |
The job has been cancelled. |
`JOB_STATE_PAUSED` |
The job has been stopped, and can be resumed. |
`JOB_STATE_EXPIRED` |
The job has expired. |
`JOB_STATE_UPDATING` |
The job is being updated. Only jobs in the `RUNNING` state can be updated. After updating, the job goes back to the `RUNNING` state. |
`JOB_STATE_PARTIALLY_SUCCEEDED` |
The job is partially succeeded, some results may be missing due to errors. |

## Methods

### JobState

`JobState(value)`


Describes the state of a job.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateArtifactRequest -->

# Class CreateArtifactRequest (1.135.0)

`CreateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateArtifact.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Artifact should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`artifact` |
Required. The Artifact to create. |
`artifact_id` |
`str`
The {artifact} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
If not provided, the Artifact's ID will be a UUID generated
by the service. Must be 4-128 characters in length. Valid
characters are `/` a-z][0-9]`-/` . Must be unique across all
Artifacts in the parent MetadataStore. (Otherwise the
request will fail with ALREADY_EXISTS, or PERMISSION_DENIED
if the caller can't view the preexisting Artifact.)
|

## Methods

### CreateArtifactRequest

`CreateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateArtifact.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagVectorDbConfig -->

# Class RagVectorDbConfig (1.135.0)

`RagVectorDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vector DB to use for RAG.

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
`rag_managed_db` |
The config for the RAG-managed Vector DB. This field is a member of `oneof` _ `vector_db` .
|
`pinecone` |
The config for the Pinecone. This field is a member of `oneof` _ `vector_db` .
|
`vertex_vector_search` |
The config for the Vertex Vector Search. This field is a member of `oneof` _ `vector_db` .
|
`api_auth` |
Authentication config for the chosen Vector DB. |
`rag_embedding_model_config` |
Optional. Immutable. The embedding model config of the Vector DB. |

## Classes

### Pinecone

`Pinecone(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Pinecone.

### RagManagedDb

`RagManagedDb(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the default RAG-managed Vector DB.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### VertexVectorSearch

`VertexVectorSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Vector Search.

## Methods

### RagVectorDbConfig

`RagVectorDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vector DB to use for RAG.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers -->

# Module pagers (1.135.0)

API documentation for `aiplatform_v1.services.feature_online_store_admin_service.pagers`

module.

## Classes

[ListFeatureOnlineStoresAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresAsyncPager)

```
ListFeatureOnlineStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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


A pager for iterating through `list_feature_online_stores`

requests.

This class thinly wraps an initial
[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_online_stores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureOnlineStores`

requests and continue to iterate
through the `feature_online_stores`

field on the
corresponding responses.

All the usual [ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureOnlineStoresPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresPager)

```
ListFeatureOnlineStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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


A pager for iterating through `list_feature_online_stores`

requests.

This class thinly wraps an initial
[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_online_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureOnlineStores`

requests and continue to iterate
through the `feature_online_stores`

field on the
corresponding responses.

All the usual [ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewSyncsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsAsyncPager)

```
ListFeatureViewSyncsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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


A pager for iterating through `list_feature_view_syncs`

requests.

This class thinly wraps an initial
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_view_syncs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureViewSyncs`

requests and continue to iterate
through the `feature_view_syncs`

field on the
corresponding responses.

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewSyncsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsPager)

```
ListFeatureViewSyncsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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


A pager for iterating through `list_feature_view_syncs`

requests.

This class thinly wraps an initial
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_view_syncs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureViewSyncs`

requests and continue to iterate
through the `feature_view_syncs`

field on the
corresponding responses.

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewsAsyncPager)

```
ListFeatureViewsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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


A pager for iterating through `list_feature_views`

requests.

This class thinly wraps an initial
[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_views`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureViews`

requests and continue to iterate
through the `feature_views`

field on the
corresponding responses.

All the usual [ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewsPager)

```
ListFeatureViewsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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


A pager for iterating through `list_feature_views`

requests.

This class thinly wraps an initial
[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_views`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureViews`

requests and continue to iterate
through the `feature_views`

field on the
corresponding responses.

All the usual [ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.PredictionDriftDetectionConfig.AttributionScoreDriftThresholdsEntry -->

# Class AttributionScoreDriftThresholdsEntry (1.135.0)

```
AttributionScoreDriftThresholdsEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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

### AttributionScoreDriftThresholdsEntry

```
AttributionScoreDriftThresholdsEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetCachedContentRequest -->

# Class GetCachedContentRequest (1.135.0)

`GetCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.GetCachedContent.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name referring to the cached content |

## Methods

### GetCachedContentRequest

`GetCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.GetCachedContent.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Checkpoint -->

# Class Checkpoint (1.135.0)

`Checkpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the machine learning model version checkpoint.

## Attributes |
|
|---|---|
Name |
Description |
`checkpoint_id` |
`str`
The ID of the checkpoint. |
`epoch` |
`int`
The epoch of the checkpoint. |
`step` |
`int`
The step of the checkpoint. |

## Methods

### Checkpoint

`Checkpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the machine learning model version checkpoint.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetyRating.HarmSeverity -->

# Class HarmSeverity (1.135.0)

`HarmSeverity(value)`


Harm severity levels.

## Enums |
|
|---|---|
Name |
Description |
`HARM_SEVERITY_UNSPECIFIED` |
Harm severity unspecified. |
`HARM_SEVERITY_NEGLIGIBLE` |
Negligible level of harm severity. |
`HARM_SEVERITY_LOW` |
Low level of harm severity. |
`HARM_SEVERITY_MEDIUM` |
Medium level of harm severity. |
`HARM_SEVERITY_HIGH` |
High level of harm severity. |

## Methods

### HarmSeverity

`HarmSeverity(value)`


Harm severity levels.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CitationMetadata -->

# Class CitationMetadata (1.135.0)

`CitationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of source attributions for a piece of content.

## Attribute |
|
|---|---|
Name |
Description |
`citations` |
`MutableSequence[google.cloud.aiplatform_v1.types.Citation]`
Output only. List of citations. |

## Methods

### CitationMetadata

`CitationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of source attributions for a piece of content.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeArtifactsMetadata -->

# Class PurgeArtifactsMetadata (1.135.0)

`PurgeArtifactsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeArtifacts.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for purging Artifacts. |

## Methods

### PurgeArtifactsMetadata

`PurgeArtifactsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeArtifacts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddContextArtifactsAndExecutionsResponse -->

# Class AddContextArtifactsAndExecutionsResponse (1.135.0)

```
AddContextArtifactsAndExecutionsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.AddContextArtifactsAndExecutions.

## Methods

### AddContextArtifactsAndExecutionsResponse

```
AddContextArtifactsAndExecutionsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.AddContextArtifactsAndExecutions.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StratifiedSplit -->

# Class StratifiedSplit (1.135.0)

`StratifiedSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to the training, validation, and test sets so
that the distribution of values found in the categorical column (as
specified by the `key`

field) is mirrored within each split. The
fraction values determine the relative sizes of the splits.

For example, if the specified column has three values, with 50% of the rows having value "A", 25% value "B", and 25% value "C", and the split fractions are specified as 80/10/10, then the training set will constitute 80% of the training data, with about 50% of the training set rows having the value "A" for the specified column, about 25% having the value "B", and about 25% having the value "C".

Only the top 500 occurring values are used; any values not in the top 500 values are randomly assigned to a split. If less than three rows contain a specific value, those rows are randomly assigned.

Supported only for tabular Datasets.

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
`key` |
`str`
Required. The key is a name of one of the Dataset's data columns. The key provided must be for a categorical column. |

## Methods

### StratifiedSplit

`StratifiedSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to the training, validation, and test sets so
that the distribution of values found in the categorical column (as
specified by the `key`

field) is mirrored within each split. The
fraction values determine the relative sizes of the splits.

For example, if the specified column has three values, with 50% of the rows having value "A", 25% value "B", and 25% value "C", and the split fractions are specified as 80/10/10, then the training set will constitute 80% of the training data, with about 50% of the training set rows having the value "A" for the specified column, about 25% having the value "B", and about 25% having the value "C".

Only the top 500 occurring values are used; any values not in the top 500 values are randomly assigned to a split. If less than three rows contain a specific value, those rows are randomly assigned.

Supported only for tabular Datasets.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddContextArtifactsAndExecutionsRequest -->

# Class AddContextArtifactsAndExecutionsRequest (1.135.0)

```
AddContextArtifactsAndExecutionsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.AddContextArtifactsAndExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the Context that the Artifacts and Executions belong to. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`artifacts` |
`MutableSequence[str]`
The resource names of the Artifacts to attribute to the Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
|
`executions` |
`MutableSequence[str]`
The resource names of the Executions to associate with the Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|

## Methods

### AddContextArtifactsAndExecutionsRequest

```
AddContextArtifactsAndExecutionsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.AddContextArtifactsAndExecutions.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborSearchOperationMetadata -->

# Class NearestNeighborSearchOperationMetadata (1.135.0)

```
NearestNeighborSearchOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation metadata with regard to Matching Engine Index.

## Attributes |
|
|---|---|
Name |
Description |
`content_validation_stats` |
`MutableSequence[`
The validation stats of the content (per file) to be inserted or updated on the Matching Engine Index resource. Populated if contentsDeltaUri is provided as part of Index.metadata. Please note that, currently for those files that are broken or has unsupported file format, we will not have the stats for those files. |
`data_bytes_count` |
`int`
The ingested data size in bytes. |

## Classes

### ContentValidationStats

`ContentValidationStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### RecordError

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Methods

### NearestNeighborSearchOperationMetadata

```
NearestNeighborSearchOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation metadata with regard to Matching Engine Index.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecRequest -->

# Class RecommendSpecRequest (1.135.0)

`RecommendSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.RecommendSpec.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to recommend specs. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .
|
`gcs_uri` |
`str`
Required. The Google Cloud Storage URI of the custom model, storing weights and config files (which can be used to infer the base model). |
`check_machine_availability` |
`bool`
Optional. If true, check machine availability for the recommended regions. Only return the machine spec in regions where the machine is available. |
`check_user_quota` |
`bool`
Optional. If true, check user quota for the recommended regions. Returns all the machine spec in regions they are available, and also the user quota state for each machine type in each region. |

## Methods

### RecommendSpecRequest

`RecommendSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.RecommendSpec.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.TrainingPredictionSkewDetectionConfig.AttributionScoreSkewThresholdsEntry -->

# Class AttributionScoreSkewThresholdsEntry (1.135.0)

```
AttributionScoreSkewThresholdsEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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

### AttributionScoreSkewThresholdsEntry

```
AttributionScoreSkewThresholdsEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DnsPeeringConfig -->

# Class DnsPeeringConfig (1.135.0)

`DnsPeeringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DNS peering configuration. These configurations are used to create DNS peering zones in the Vertex tenant project VPC, enabling resolution of records within the specified domain hosted in the target network's Cloud DNS.

## Attributes |
|
|---|---|
Name |
Description |
`domain` |
`str`
Required. The DNS name suffix of the zone being peered to, e.g., "my-internal-domain.corp.". Must end with a dot. |
`target_project` |
`str`
Required. The project ID hosting the Cloud DNS managed zone that contains the 'domain'. The Vertex AI Service Agent requires the dns.peer role on this project. |
`target_network` |
`str`
Required. The VPC network name in the target_project where the DNS zone specified by 'domain' is visible. |

## Methods

### DnsPeeringConfig

`DnsPeeringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DNS peering configuration. These configurations are used to create DNS peering zones in the Vertex tenant project VPC, enabling resolution of records within the specified domain hosted in the target network's Cloud DNS.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagFileTransformationConfig -->

# Class RagFileTransformationConfig (1.135.0)

`RagFileTransformationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the transformation config for RagFiles.

## Attribute |
|
|---|---|
Name |
Description |
`rag_file_chunking_config` |
Specifies the chunking config for RagFiles. |

## Methods

### RagFileTransformationConfig

`RagFileTransformationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the transformation config for RagFiles.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateRagCorpusRequest -->

# Class UpdateRagCorpusRequest (1.135.0)

`UpdateRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.UpdateRagCorpus.

## Attribute |
|
|---|---|
Name |
Description |
`rag_corpus` |
Required. The RagCorpus which replaces the resource on the server. |

## Methods

### UpdateRagCorpusRequest

`UpdateRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.UpdateRagCorpus.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DistillationDataStats -->

# Class DistillationDataStats (1.135.0)

`DistillationDataStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Statistics computed for datasets used for distillation.

## Attribute |
|
|---|---|
Name |
Description |
`training_dataset_stats` |
Output only. Statistics computed for the training dataset. |

## Methods

### DistillationDataStats

`DistillationDataStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Statistics computed for datasets used for distillation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTrialRequest -->

# Class DeleteTrialRequest (1.135.0)

`DeleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.DeleteTrial.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|

## Methods

### DeleteTrialRequest

`DeleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.DeleteTrial.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelSourceInfo.ModelSourceType -->

# Class ModelSourceType (1.135.0)

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.

## Enums |
|
|---|---|
Name |
Description |
`MODEL_SOURCE_TYPE_UNSPECIFIED` |
Should not be used. |
`AUTOML` |
The Model is uploaded by automl training pipeline. |
`CUSTOM` |
The Model is uploaded by user or custom training pipeline. |
`BQML` |
The Model is registered and sync'ed from BigQuery ML. |
`MODEL_GARDEN` |
The Model is saved or tuned from Model Garden. |
`GENIE` |
The Model is saved or tuned from Genie. |
`CUSTOM_TEXT_EMBEDDING` |
The Model is uploaded by text embedding finetuning pipeline. |
`MARKETPLACE` |
The Model is saved or tuned from Marketplace. |

## Methods

### ModelSourceType

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StratifiedSplit -->

# Class StratifiedSplit (1.135.0)

`StratifiedSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to the training, validation, and test sets so
that the distribution of values found in the categorical column (as
specified by the `key`

field) is mirrored within each split. The
fraction values determine the relative sizes of the splits.

For example, if the specified column has three values, with 50% of the rows having value "A", 25% value "B", and 25% value "C", and the split fractions are specified as 80/10/10, then the training set will constitute 80% of the training data, with about 50% of the training set rows having the value "A" for the specified column, about 25% having the value "B", and about 25% having the value "C".

Only the top 500 occurring values are used; any values not in the top 500 values are randomly assigned to a split. If less than three rows contain a specific value, those rows are randomly assigned.

Supported only for tabular Datasets.

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
`key` |
`str`
Required. The key is a name of one of the Dataset's data columns. The key provided must be for a categorical column. |

## Methods

### StratifiedSplit

`StratifiedSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to the training, validation, and test sets so
that the distribution of values found in the categorical column (as
specified by the `key`

field) is mirrored within each split. The
fraction values determine the relative sizes of the splits.

For example, if the specified column has three values, with 50% of the rows having value "A", 25% value "B", and 25% value "C", and the split fractions are specified as 80/10/10, then the training set will constitute 80% of the training data, with about 50% of the training set rows having the value "A" for the specified column, about 25% having the value "B", and about 25% having the value "C".

Only the top 500 occurring values are used; any values not in the top 500 values are randomly assigned to a split. If less than three rows contain a specific value, those rows are randomly assigned.

Supported only for tabular Datasets.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient -->

# Class PersistentResourceServiceClient (1.135.0)

```
PersistentResourceServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's machine learning PersistentResource.

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
`PersistentResourceServiceTransport` |
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

### PersistentResourceServiceClient

```
PersistentResourceServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the persistent resource service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PersistentResourceServiceTransport,Callable[..., PersistentResourceServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the PersistentResourceServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_persistent_resource

```
create_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.CreatePersistentResourceRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1beta1.types.persistent_resource.PersistentResource
] = None,
persistent_resource_id: typing.Optional[str] = None,
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


Creates a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePersistentResourceRequest.html)(
parent="parent_value",
persistent_resource_id="persistent_resource_id_value",
)
# Make the request
operation = client.[create_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_create_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.CreatePersistentResource. |
`parent` |
`str`
Required. The resource name of the Location to create the PersistentResource in. Format: |
`persistent_resource` |
Required. The PersistentResource to create. This corresponds to the |
`persistent_resource_id` |
`str`
Required. The ID to use for the PersistentResource, which become the final component of the PersistentResource's resource name. The maximum length is 63 characters, and valid characters are |
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

### delete_persistent_resource

```
delete_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.DeletePersistentResourceRequest,
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


Deletes a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeletePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_delete_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.DeletePersistentResource. |
`name` |
`str`
Required. The name of the PersistentResource to be deleted. Format: |
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
`PersistentResourceServiceClient` |
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
`PersistentResourceServiceClient` |
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
`PersistentResourceServiceClient` |
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

### get_persistent_resource

```
get_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.GetPersistentResourceRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.persistent_resource.PersistentResource
```


Gets a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_get_persistent_resource)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PersistentResourceService.GetPersistentResource. |
`name` |
`str`
Required. The name of the PersistentResource resource. Format: |
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
Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec. |

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

### list_persistent_resources

```
list_persistent_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesRequest,
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
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.pagers.ListPersistentResourcesPager
)
```


Lists PersistentResources in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_persistent_resources():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListPersistentResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_persistent_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_list_persistent_resources)(request=request)
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
The request object. Request message for [PersistentResourceService.ListPersistentResource][]. |
`parent` |
`str`
Required. The resource name of the Location to list the PersistentResources from. Format: |
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
Response message for PersistentResourceService.ListPersistentResources Iterating over this object will yield results and resolve additional pages automatically. |

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### notebook_runtime_template_path

```
notebook_runtime_template_path(
project: str, location: str, notebook_runtime_template: str
) -> str
```


Returns a fully-qualified notebook_runtime_template string.

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

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_persistent_resource_path

`parse_persistent_resource_path(path: str) -> typing.Dict[str, str]`


Parses a persistent_resource path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### persistent_resource_path

```
persistent_resource_path(
project: str, location: str, persistent_resource: str
) -> str
```


Returns a fully-qualified persistent_resource string.

### reboot_persistent_resource

```
reboot_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.RebootPersistentResourceRequest,
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


Reboots a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_reboot_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RebootPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebootPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[reboot_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_reboot_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.RebootPersistentResource. |
`name` |
`str`
Required. The name of the PersistentResource resource. Format: |
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

### update_persistent_resource

```
update_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.UpdatePersistentResourceRequest,
dict,
]
] = None,
*,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1beta1.types.persistent_resource.PersistentResource
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


Updates a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdatePersistentResourceRequest.html)(
)
# Make the request
operation = client.[update_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_update_persistent_resource)(request=request)
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
The request object. Request message for UpdatePersistentResource method. |
`persistent_resource` |
Required. The PersistentResource to update. The PersistentResource's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Specify the fields to be overwritten in the PersistentResource by the update method. This corresponds to the |
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient -->

# Class DatasetServiceClient (1.135.0)

```
DatasetServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The service that manages Vertex AI Dataset and its child resources.

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
`DatasetServiceTransport` |
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

### DatasetServiceClient

```
DatasetServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the dataset service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,DatasetServiceTransport,Callable[..., DatasetServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the DatasetServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### annotation_path

```
annotation_path(
project: str, location: str, dataset: str, data_item: str, annotation: str
) -> str
```


Returns a fully-qualified annotation string.

### annotation_spec_path

```
annotation_spec_path(
project: str, location: str, dataset: str, annotation_spec: str
) -> str
```


Returns a fully-qualified annotation_spec string.

### assemble_data

```
assemble_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.AssembleDataRequest,
dict,
]
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
) -> google.api_core.operation.Operation
```


Assembles each row of a multimodal dataset and writes the result into a BigQuery table.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_assemble_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AssembleDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssembleDataRequest.html)(
name="name_value",
)
# Make the request
operation = client.[assemble_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_assemble_data)(request=request)
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
The request object. Request message for DatasetService.AssembleData. Used only for MULTIMODAL datasets. |
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

### assess_data

```
assess_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.AssessDataRequest,
dict,
]
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
) -> google.api_core.operation.Operation
```


Assesses the state or validity of the dataset with respect to a given use case.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_assess_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
tuning_validation_assessment_config = aiplatform_v1beta1.[TuningValidationAssessmentConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest.TuningValidationAssessmentConfig.html)()
tuning_validation_assessment_config.model_name = "model_name_value"
tuning_validation_assessment_config.dataset_usage = "SFT_VALIDATION"
request = aiplatform_v1beta1.[AssessDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest.html)(
tuning_validation_assessment_config=tuning_validation_assessment_config,
name="name_value",
)
# Make the request
operation = client.[assess_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_assess_data)(request=request)
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
The request object. Request message for DatasetService.AssessData. Used only for MULTIMODAL datasets. |
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

### cached_content_path

`cached_content_path(project: str, location: str, cached_content: str) -> str`


Returns a fully-qualified cached_content string.

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

### create_dataset

```
create_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.CreateDatasetRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
dataset: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset.Dataset
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


Creates a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
dataset = aiplatform_v1beta1.[Dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Dataset.html)()
dataset.display_name = "display_name_value"
dataset.metadata_schema_uri = "metadata_schema_uri_value"
dataset.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[CreateDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetRequest.html)(
parent="parent_value",
dataset=dataset,
)
# Make the request
operation = client.[create_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_create_dataset)(request=request)
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
The request object. Request message for DatasetService.CreateDataset. |
`parent` |
`str`
Required. The resource name of the Location to create the Dataset in. Format: |
`dataset` |
Required. The Dataset to create. This corresponds to the |
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

### create_dataset_version

```
create_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.CreateDatasetVersionRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
dataset_version: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
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


Create a version from a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
dataset_version = aiplatform_v1beta1.[DatasetVersion](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetVersion.html)()
dataset_version.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[CreateDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetVersionRequest.html)(
parent="parent_value",
dataset_version=dataset_version,
)
# Make the request
operation = client.[create_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_create_dataset_version)(request=request)
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
The request object. Request message for DatasetService.CreateDatasetVersion. |
`parent` |
`str`
Required. The name of the Dataset resource. Format: |
`dataset_version` |
Required. The version to be created. The same CMEK policies with the original Dataset will be applied the dataset version. So here we don't need to specify the EncryptionSpecType here. This corresponds to the |
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

### data_item_path

`data_item_path(project: str, location: str, dataset: str, data_item: str) -> str`


Returns a fully-qualified data_item string.

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

### dataset_version_path

```
dataset_version_path(
project: str, location: str, dataset: str, dataset_version: str
) -> str
```


Returns a fully-qualified dataset_version string.

### delete_dataset

```
delete_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.DeleteDatasetRequest,
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


Deletes a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_delete_dataset)(request=request)
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
The request object. Request message for DatasetService.DeleteDataset. |
`name` |
`str`
Required. The resource name of the Dataset to delete. Format: |
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

### delete_dataset_version

```
delete_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.DeleteDatasetVersionRequest,
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


Deletes a Dataset version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_delete_dataset_version)(request=request)
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
The request object. Request message for DatasetService.DeleteDatasetVersion. |
`name` |
`str`
Required. The resource name of the Dataset version to delete. Format: |
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

### delete_saved_query

```
delete_saved_query(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.DeleteSavedQueryRequest,
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


Deletes a SavedQuery.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_saved_query():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteSavedQueryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSavedQueryRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_saved_query](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_delete_saved_query)(request=request)
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
The request object. Request message for DatasetService.DeleteSavedQuery. |
`name` |
`str`
Required. The resource name of the SavedQuery to delete. Format: |
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

### export_data

```
export_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ExportDataRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
export_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset.ExportDataConfig
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


Exports data from a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_export_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
export_config = aiplatform_v1beta1.[ExportDataConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataConfig.html)()
export_config.gcs_destination.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[ExportDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataRequest.html)(
name="name_value",
export_config=export_config,
)
# Make the request
operation = client.[export_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_export_data)(request=request)
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
The request object. Request message for DatasetService.ExportData. |
`name` |
`str`
Required. The name of the Dataset resource. Format: |
`export_config` |
Required. The desired output location. This corresponds to the |
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
`DatasetServiceClient` |
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
`DatasetServiceClient` |
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
`DatasetServiceClient` |
The constructed client. |

### get_annotation_spec

```
get_annotation_spec(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.GetAnnotationSpecRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.annotation_spec.AnnotationSpec
```


Gets an AnnotationSpec.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_annotation_spec():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetAnnotationSpecRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetAnnotationSpecRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_annotation_spec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_get_annotation_spec)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.GetAnnotationSpec. |
`name` |
`str`
Required. The name of the AnnotationSpec resource. Format: |
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
Identifies a concept with which DataItems may be annotated with. |

### get_dataset

```
get_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.GetDatasetRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.dataset.Dataset
```


Gets a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_get_dataset)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.GetDataset. |
`name` |
`str`
Required. The name of the Dataset resource. This corresponds to the |
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
A collection of DataItems and Annotations on them. |

### get_dataset_version

```
get_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.GetDatasetVersionRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
```


Gets a Dataset version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_get_dataset_version)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.GetDatasetVersion. |
`name` |
`str`
Required. The resource name of the Dataset version to delete. Format: |
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
Describes the dataset version. |

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

### import_data

```
import_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ImportDataRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
import_configs: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.dataset.ImportDataConfig
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
) -> google.api_core.operation.Operation
```


Imports data into a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_import_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
import_configs = aiplatform_v1beta1.[ImportDataConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataConfig.html)()
import_configs.gcs_source.uris = ['uris_value1', 'uris_value2']
import_configs.import_schema_uri = "import_schema_uri_value"
request = aiplatform_v1beta1.[ImportDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataRequest.html)(
name="name_value",
import_configs=import_configs,
)
# Make the request
operation = client.[import_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_import_data)(request=request)
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
The request object. Request message for DatasetService.ImportData. |
`name` |
`str`
Required. The name of the Dataset resource. Format: |
`import_configs` |
`MutableSequence[`
Required. The desired input locations. The contents of all input locations will be imported in one batch. This corresponds to the |
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

### list_annotations

```
list_annotations(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsRequest,
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
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListAnnotationsPager
)
```


Lists Annotations belongs to a dataitem.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_annotations():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListAnnotationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_annotations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_list_annotations)(request=request)
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
The request object. Request message for DatasetService.ListAnnotations. |
`parent` |
`str`
Required. The resource name of the DataItem to list Annotations from. Format: |
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
Response message for DatasetService.ListAnnotations. Iterating over this object will yield results and resolve additional pages automatically. |

### list_data_items

```
list_data_items(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsRequest,
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
) -> google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDataItemsPager
```


Lists DataItems in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_data_items():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDataItemsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_data_items](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_list_data_items)(request=request)
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
The request object. Request message for DatasetService.ListDataItems. |
`parent` |
`str`
Required. The resource name of the Dataset to list DataItems from. Format: |
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
Response message for DatasetService.ListDataItems. Iterating over this object will yield results and resolve additional pages automatically. |

### list_dataset_versions

```
list_dataset_versions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsRequest,
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
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetVersionsPager
)
```


Lists DatasetVersions in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_dataset_versions():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDatasetVersionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_dataset_versions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_list_dataset_versions)(request=request)
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
The request object. Request message for DatasetService.ListDatasetVersions. |
`parent` |
`str`
Required. The resource name of the Dataset to list DatasetVersions from. Format: |
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
Response message for DatasetService.ListDatasetVersions. Iterating over this object will yield results and resolve additional pages automatically. |

### list_datasets

```
list_datasets(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsRequest,
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
) -> google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetsPager
```


Lists Datasets in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_datasets():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDatasetsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_datasets](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_list_datasets)(request=request)
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
The request object. Request message for DatasetService.ListDatasets. |
`parent` |
`str`
Required. The name of the Dataset's parent resource. Format: |
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
Response message for DatasetService.ListDatasets. Iterating over this object will yield results and resolve additional pages automatically. |

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

### list_saved_queries

```
list_saved_queries(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesRequest,
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
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListSavedQueriesPager
)
```


Lists SavedQueries in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_saved_queries():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListSavedQueriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_saved_queries](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_list_saved_queries)(request=request)
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
The request object. Request message for DatasetService.ListSavedQueries. |
`parent` |
`str`
Required. The resource name of the Dataset to list SavedQueries from. Format: |
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
Response message for DatasetService.ListSavedQueries. Iterating over this object will yield results and resolve additional pages automatically. |

### parse_annotation_path

`parse_annotation_path(path: str) -> typing.Dict[str, str]`


Parses a annotation path into its component segments.

### parse_annotation_spec_path

`parse_annotation_spec_path(path: str) -> typing.Dict[str, str]`


Parses a annotation_spec path into its component segments.

### parse_cached_content_path

`parse_cached_content_path(path: str) -> typing.Dict[str, str]`


Parses a cached_content path into its component segments.

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

### parse_data_item_path

`parse_data_item_path(path: str) -> typing.Dict[str, str]`


Parses a data_item path into its component segments.

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_dataset_version_path

`parse_dataset_version_path(path: str) -> typing.Dict[str, str]`


Parses a dataset_version path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### parse_saved_query_path

`parse_saved_query_path(path: str) -> typing.Dict[str, str]`


Parses a saved_query path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### restore_dataset_version

```
restore_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.RestoreDatasetVersionRequest,
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


Restores a dataset version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_restore_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RestoreDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RestoreDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[restore_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_restore_dataset_version)(request=request)
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
The request object. Request message for DatasetService.RestoreDatasetVersion. |
`name` |
`str`
Required. The name of the DatasetVersion resource. Format: |
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

### saved_query_path

```
saved_query_path(
project: str, location: str, dataset: str, saved_query: str
) -> str
```


Returns a fully-qualified saved_query string.

### search_data_items

```
search_data_items(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsRequest,
dict,
]
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
) -> (
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.SearchDataItemsPager
)
```


Searches DataItems in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_search_data_items():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SearchDataItemsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsRequest.html)(
order_by_data_item="order_by_data_item_value",
dataset="dataset_value",
)
# Make the request
page_result = client.[search_data_items](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_search_data_items)(request=request)
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
The request object. Request message for DatasetService.SearchDataItems. |
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
Response message for DatasetService.SearchDataItems. Iterating over this object will yield results and resolve additional pages automatically. |

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

### update_dataset

```
update_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.UpdateDatasetRequest,
dict,
]
] = None,
*,
dataset: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset.Dataset
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
) -> google.cloud.aiplatform_v1beta1.types.dataset.Dataset
```


Updates a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
dataset = aiplatform_v1beta1.[Dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Dataset.html)()
dataset.display_name = "display_name_value"
dataset.metadata_schema_uri = "metadata_schema_uri_value"
dataset.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[UpdateDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetRequest.html)(
dataset=dataset,
)
# Make the request
response = client.[update_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_update_dataset)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.UpdateDataset. |
`dataset` |
Required. The Dataset which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the |
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
A collection of DataItems and Annotations on them. |

### update_dataset_version

```
update_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.UpdateDatasetVersionRequest,
dict,
]
] = None,
*,
dataset_version: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
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
) -> google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
```


Updates a DatasetVersion.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
dataset_version = aiplatform_v1beta1.[DatasetVersion](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetVersion.html)()
dataset_version.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[UpdateDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetVersionRequest.html)(
dataset_version=dataset_version,
)
# Make the request
response = client.[update_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_update_dataset_version)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.UpdateDatasetVersion. |
`dataset_version` |
Required. The DatasetVersion which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the |
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
Describes the dataset version. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice.SliceSpec.SliceConfig -->

# Class SliceConfig (1.135.0)

`SliceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification message containing the config for this SliceSpec. When
`kind`

is selected as `value`

and/or `range`

, only a single
slice will be computed. When `all_values`

is present, a separate
slice will be computed for each possible label/value for the
corresponding key in `config`

. Examples, with feature zip_code
with values 12345, 23334, 88888 and feature country with values
"US", "Canada", "Mexico" in the dataset:

Example 1:

::

```
{
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


A single slice for any data with zip_code 12345 in the dataset.

Example 2:

::

```
{
"zip_code": { "range": { "low": 12345, "high": 20000 } }
}
```


A single slice containing data where the zip_codes between 12345 and 20000 For this example, data with the zip_code of 12345 will be in this slice.

Example 3:

::

```
{
"zip_code": { "range": { "low": 10000, "high": 20000 } },
"country": { "value": { "string_value": "US" } }
}
```


A single slice containing data where the zip_codes between 10000 and 20000 has the country "US". For this example, data with the zip_code of 12345 and country "US" will be in this slice.

Example 4:

::

```
{ "country": {"all_values": { "value": true } } }
```


Three slices are computed, one for each unique country in the dataset.

Example 5:

::

```
{
"country": { "all_values": { "value": true } },
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


Three slices are computed, one for each unique country in the dataset where the zip_code is also 12345. For this example, data with zip_code 12345 and country "US" will be in one slice, zip_code 12345 and country "Canada" in another slice, and zip_code 12345 and country "Mexico" in another slice, totaling 3 slices.

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
`value` |
A unique specific value for a given feature. Example: `{ "value": { "string_value": "12345" } }`
This field is a member of `oneof` _ `kind` .
|
`range_` |
A range of values for a numerical feature. Example: `{"range":{"low":10000.0,"high":50000.0}}` will capture
12345 and 23334 in the slice.
This field is a member of `oneof` _ `kind` .
|
`all_values` |
`google.protobuf.wrappers_pb2.BoolValue`
If all_values is set to true, then all possible labels of the keyed feature will have another slice computed. Example: `{"all_values":{"value":true}}`
This field is a member of `oneof` _ `kind` .
|

## Methods

### SliceConfig

`SliceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification message containing the config for this SliceSpec. When
`kind`

is selected as `value`

and/or `range`

, only a single
slice will be computed. When `all_values`

is present, a separate
slice will be computed for each possible label/value for the
corresponding key in `config`

. Examples, with feature zip_code
with values 12345, 23334, 88888 and feature country with values
"US", "Canada", "Mexico" in the dataset:

Example 1:

::

```
{
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


A single slice for any data with zip_code 12345 in the dataset.

Example 2:

::

```
{
"zip_code": { "range": { "low": 12345, "high": 20000 } }
}
```


A single slice containing data where the zip_codes between 12345 and 20000 For this example, data with the zip_code of 12345 will be in this slice.

Example 3:

::

```
{
"zip_code": { "range": { "low": 10000, "high": 20000 } },
"country": { "value": { "string_value": "US" } }
}
```


A single slice containing data where the zip_codes between 10000 and 20000 has the country "US". For this example, data with the zip_code of 12345 and country "US" will be in this slice.

Example 4:

::

```
{ "country": {"all_values": { "value": true } } }
```


Three slices are computed, one for each unique country in the dataset.

Example 5:

::

```
{
"country": { "all_values": { "value": true } },
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


Three slices are computed, one for each unique country in the dataset where the zip_code is also 12345. For this example, data with zip_code 12345 and country "US" will be in one slice, zip_code 12345 and country "Canada" in another slice, and zip_code 12345 and country "Mexico" in another slice, totaling 3 slices.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore -->

# Class FeatureOnlineStore (1.135.0)

`FeatureOnlineStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Online Store provides a centralized repository for serving ML features and embedding indexes at low latency. The Feature Online Store is a top-level container.

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
`bigtable` |
Contains settings for the Cloud Bigtable instance that will be created to serve featureValues for all FeatureViews under this FeatureOnlineStore. This field is a member of `oneof` _ `storage_type` .
|
`optimized` |
Contains settings for the Optimized store that will be created to serve featureValues for all FeatureViews under this FeatureOnlineStore. When choose Optimized storage type, need to set PrivateServiceConnectConfig.enable_private_service_connect to use private endpoint. Otherwise will use public endpoint by default. This field is a member of `oneof` _ `storage_type` .
|
`name` |
`str`
Identifier. Name of the FeatureOnlineStore. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}`
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureOnlineStore was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureOnlineStore was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your FeatureOnlineStore. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureOnlineStore(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`state` |
Output only. State of the featureOnlineStore. |
`dedicated_serving_endpoint` |
Optional. The dedicated serving endpoint for this FeatureOnlineStore, which is different from common Vertex service endpoint. |
`embedding_management` |
Optional. Deprecated: This field is no longer needed anymore and embedding management is automatically enabled when specifying Optimized storage type. |
`encryption_spec` |
Optional. Customer-managed encryption key spec for data storage. If set, online store will be secured by this key. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### Bigtable

`Bigtable(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### DedicatedServingEndpoint

`DedicatedServingEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The dedicated serving endpoint for this FeatureOnlineStore. Only need to set when you choose Optimized storage type. Public endpoint is provisioned by default.

### EmbeddingManagement

`EmbeddingManagement(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Deprecated: This sub message is no longer needed anymore and embedding management is automatically enabled when specifying Optimized storage type. Contains settings for embedding management.

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

### Optimized

`Optimized(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Optimized storage type

### State

`State(value)`


Possible states a featureOnlineStore can have.

## Methods

### FeatureOnlineStore

`FeatureOnlineStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Online Store provides a centralized repository for serving ML features and embedding indexes at low latency. The Feature Online Store is a top-level container.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluationSlice.Slice.SliceSpec.SliceConfig -->

# Class SliceConfig (1.135.0)

`SliceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification message containing the config for this SliceSpec. When
`kind`

is selected as `value`

and/or `range`

, only a single
slice will be computed. When `all_values`

is present, a separate
slice will be computed for each possible label/value for the
corresponding key in `config`

. Examples, with feature zip_code
with values 12345, 23334, 88888 and feature country with values
"US", "Canada", "Mexico" in the dataset:

Example 1:

::

```
{
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


A single slice for any data with zip_code 12345 in the dataset.

Example 2:

::

```
{
"zip_code": { "range": { "low": 12345, "high": 20000 } }
}
```


A single slice containing data where the zip_codes between 12345 and 20000 For this example, data with the zip_code of 12345 will be in this slice.

Example 3:

::

```
{
"zip_code": { "range": { "low": 10000, "high": 20000 } },
"country": { "value": { "string_value": "US" } }
}
```


A single slice containing data where the zip_codes between 10000 and 20000 has the country "US". For this example, data with the zip_code of 12345 and country "US" will be in this slice.

Example 4:

::

```
{ "country": {"all_values": { "value": true } } }
```


Three slices are computed, one for each unique country in the dataset.

Example 5:

::

```
{
"country": { "all_values": { "value": true } },
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


Three slices are computed, one for each unique country in the dataset where the zip_code is also 12345. For this example, data with zip_code 12345 and country "US" will be in one slice, zip_code 12345 and country "Canada" in another slice, and zip_code 12345 and country "Mexico" in another slice, totaling 3 slices.

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
`value` |
A unique specific value for a given feature. Example: `{ "value": { "string_value": "12345" } }`
This field is a member of `oneof` _ `kind` .
|
`range_` |
A range of values for a numerical feature. Example: `{"range":{"low":10000.0,"high":50000.0}}` will capture
12345 and 23334 in the slice.
This field is a member of `oneof` _ `kind` .
|
`all_values` |
`google.protobuf.wrappers_pb2.BoolValue`
If all_values is set to true, then all possible labels of the keyed feature will have another slice computed. Example: `{"all_values":{"value":true}}`
This field is a member of `oneof` _ `kind` .
|

## Methods

### SliceConfig

`SliceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification message containing the config for this SliceSpec. When
`kind`

is selected as `value`

and/or `range`

, only a single
slice will be computed. When `all_values`

is present, a separate
slice will be computed for each possible label/value for the
corresponding key in `config`

. Examples, with feature zip_code
with values 12345, 23334, 88888 and feature country with values
"US", "Canada", "Mexico" in the dataset:

Example 1:

::

```
{
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


A single slice for any data with zip_code 12345 in the dataset.

Example 2:

::

```
{
"zip_code": { "range": { "low": 12345, "high": 20000 } }
}
```


A single slice containing data where the zip_codes between 12345 and 20000 For this example, data with the zip_code of 12345 will be in this slice.

Example 3:

::

```
{
"zip_code": { "range": { "low": 10000, "high": 20000 } },
"country": { "value": { "string_value": "US" } }
}
```


A single slice containing data where the zip_codes between 10000 and 20000 has the country "US". For this example, data with the zip_code of 12345 and country "US" will be in this slice.

Example 4:

::

```
{ "country": {"all_values": { "value": true } } }
```


Three slices are computed, one for each unique country in the dataset.

Example 5:

::

```
{
"country": { "all_values": { "value": true } },
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


Three slices are computed, one for each unique country in the dataset where the zip_code is also 12345. For this example, data with zip_code 12345 and country "US" will be in one slice, zip_code 12345 and country "Canada" in another slice, and zip_code 12345 and country "Mexico" in another slice, totaling 3 slices.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesResponse.SelectTimeRangeAndFeature -->

# Class SelectTimeRangeAndFeature (1.135.0)

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectTimeRangeAndFeature option.

## Attributes |
|
|---|---|
Name |
Description |
`impacted_feature_count` |
`int`
The count of the features or columns impacted. This is the same as the feature count in the request. |
`offline_storage_modified_entity_row_count` |
`int`
The count of modified entity rows in the offline storage. Each row corresponds to the combination of an entity ID and a timestamp. One entity ID can have multiple rows in the offline storage. Within each row, only the features specified in the request are deleted. |
`online_storage_modified_entity_count` |
`int`
The count of modified entities in the online storage. Each entity ID corresponds to one entity. Within each entity, only the features specified in the request are deleted. |

## Methods

### SelectTimeRangeAndFeature

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectTimeRangeAndFeature option.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.PredictionDriftDetectionConfig.AttributionScoreDriftThresholdsEntry -->

# Class AttributionScoreDriftThresholdsEntry (1.135.0)

```
AttributionScoreDriftThresholdsEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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

### AttributionScoreDriftThresholdsEntry

```
AttributionScoreDriftThresholdsEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.OpenFineTuningPipelines -->

# Class OpenFineTuningPipelines (1.135.0)

`OpenFineTuningPipelines(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open fine tuning pipelines.

## Attribute |
|
|---|---|
Name |
Description |
`fine_tuning_pipelines` |
`MutableSequence[`
Required. Regional resource references to fine tuning pipelines. |

## Methods

### OpenFineTuningPipelines

`OpenFineTuningPipelines(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open fine tuning pipelines.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListOptimalTrialsRequest -->

# Class ListOptimalTrialsRequest (1.135.0)

`ListOptimalTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListOptimalTrials.

## Attribute |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the Study that the optimal Trial belongs to. |

## Methods

### ListOptimalTrialsRequest

`ListOptimalTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListOptimalTrials.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardExperimentRequest -->

# Class UpdateTensorboardExperimentRequest (1.135.0)

```
UpdateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardExperiment.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardExperiment resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard_experiment` |
Required. The TensorboardExperiment's `name` field is used
to identify the TensorboardExperiment to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|

## Methods

### UpdateTensorboardExperimentRequest

```
UpdateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardExperiment.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileChunkingConfig.FixedLengthChunking -->

# Class FixedLengthChunking (1.135.0)

`FixedLengthChunking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the fixed length chunking config.

## Attributes |
|
|---|---|
Name |
Description |
`chunk_size` |
`int`
The size of the chunks. |
`chunk_overlap` |
`int`
The overlap between chunks. |

## Methods

### FixedLengthChunking

`FixedLengthChunking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the fixed length chunking config.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schedule.RunResponse -->

# Class RunResponse (1.135.0)

`RunResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Status of a scheduled run.

## Attributes |
|
|---|---|
Name |
Description |
`scheduled_run_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The scheduled run time based on the user-specified schedule. |
`run_response` |
`str`
The response of the scheduled run. |

## Methods

### RunResponse

`RunResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Status of a scheduled run.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddContextArtifactsAndExecutionsRequest -->

# Class AddContextArtifactsAndExecutionsRequest (1.135.0)

```
AddContextArtifactsAndExecutionsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.AddContextArtifactsAndExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the Context that the Artifacts and Executions belong to. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`artifacts` |
`MutableSequence[str]`
The resource names of the Artifacts to attribute to the Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
|
`executions` |
`MutableSequence[str]`
The resource names of the Executions to associate with the Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|

## Methods

### AddContextArtifactsAndExecutionsRequest

```
AddContextArtifactsAndExecutionsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.AddContextArtifactsAndExecutions.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplateRef -->

# Class NotebookRuntimeTemplateRef (1.135.0)

`NotebookRuntimeTemplateRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a NotebookRuntimeTemplateRef.

## Attribute |
|
|---|---|
Name |
Description |
`notebook_runtime_template` |
`str`
Immutable. A resource name of the NotebookRuntimeTemplate. |

## Methods

### NotebookRuntimeTemplateRef

`NotebookRuntimeTemplateRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a NotebookRuntimeTemplateRef.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataResponse.BatchPredictionValidationAssessmentResult -->

# Class BatchPredictionValidationAssessmentResult (1.135.0)

```
BatchPredictionValidationAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the batch prediction validation assessment.

## Methods

### BatchPredictionValidationAssessmentResult

```
BatchPredictionValidationAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the batch prediction validation assessment.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.TrainingPredictionSkewDetectionConfig.AttributionScoreSkewThresholdsEntry -->

# Class AttributionScoreSkewThresholdsEntry (1.135.0)

```
AttributionScoreSkewThresholdsEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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

### AttributionScoreSkewThresholdsEntry

```
AttributionScoreSkewThresholdsEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.Deploy.DeployMetadata -->

# Class DeployMetadata (1.135.0)

`DeployMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata information about the deployment for managing deployment config.

## Attributes |
|
|---|---|
Name |
Description |
`labels` |
`MutableMapping[str, str]`
Optional. Labels for the deployment config. For managing deployment config like verifying, source of deployment config, etc. |
`sample_request` |
`str`
Optional. Sample request for deployed endpoint. |

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

### DeployMetadata

`DeployMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata information about the deployment for managing deployment config.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborSearchOperationMetadata -->

# Class NearestNeighborSearchOperationMetadata (1.135.0)

```
NearestNeighborSearchOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation metadata with regard to Matching Engine Index.

## Attributes |
|
|---|---|
Name |
Description |
`content_validation_stats` |
`MutableSequence[`
The validation stats of the content (per file) to be inserted or updated on the Matching Engine Index resource. Populated if contentsDeltaUri is provided as part of Index.metadata. Please note that, currently for those files that are broken or has unsupported file format, we will not have the stats for those files. |
`data_bytes_count` |
`int`
The ingested data size in bytes. |

## Classes

### ContentValidationStats

`ContentValidationStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### RecordError

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Methods

### NearestNeighborSearchOperationMetadata

```
NearestNeighborSearchOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation metadata with regard to Matching Engine Index.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelSourceInfo.ModelSourceType -->

# Class ModelSourceType (1.135.0)

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.

## Enums |
|
|---|---|
Name |
Description |
`MODEL_SOURCE_TYPE_UNSPECIFIED` |
Should not be used. |
`AUTOML` |
The Model is uploaded by automl training pipeline. |
`CUSTOM` |
The Model is uploaded by user or custom training pipeline. |
`BQML` |
The Model is registered and sync'ed from BigQuery ML. |
`MODEL_GARDEN` |
The Model is saved or tuned from Model Garden. |
`GENIE` |
The Model is saved or tuned from Genie. |
`CUSTOM_TEXT_EMBEDDING` |
The Model is uploaded by text embedding finetuning pipeline. |
`MARKETPLACE` |
The Model is saved or tuned from Marketplace. |

## Methods

### ModelSourceType

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedModelResponse -->

# Class MutateDeployedModelResponse (1.135.0)

`MutateDeployedModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.MutateDeployedModel.

## Attribute |
|
|---|---|
Name |
Description |
`deployed_model` |
The DeployedModel that's being mutated. |

## Methods

### MutateDeployedModelResponse

`MutateDeployedModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.MutateDeployedModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.BigQuerySource -->

# Class BigQuerySource (1.135.0)

`BigQuerySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
Required. The BigQuery view URI that will be materialized on each sync trigger based on FeatureView.SyncConfig. |
`entity_id_columns` |
`MutableSequence[str]`
Required. Columns to construct entity_id / row keys. |

## Methods

### BigQuerySource

`BigQuerySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationVerbosityResult -->

# Class SummarizationVerbosityResult (1.135.0)

```
SummarizationVerbosityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization verbosity result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Summarization Verbosity score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for summarization verbosity score. |
`confidence` |
`float`
Output only. Confidence for summarization verbosity score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### SummarizationVerbosityResult

```
SummarizationVerbosityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization verbosity result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PrivateEndpoints -->

# Class PrivateEndpoints (1.135.0)

`PrivateEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PrivateEndpoints proto is used to provide paths for users to send requests privately. To send request via private service access, use predict_http_uri, explain_http_uri or health_http_uri. To send request via private service connect, use service_attachment.

## Attributes |
|
|---|---|
Name |
Description |
`predict_http_uri` |
`str`
Output only. Http(s) path to send prediction requests. |
`explain_http_uri` |
`str`
Output only. Http(s) path to send explain requests. |
`health_http_uri` |
`str`
Output only. Http(s) path to send health check requests. |
`service_attachment` |
`str`
Output only. The name of the service attachment resource. Populated if private service connect is enabled. |

## Methods

### PrivateEndpoints

`PrivateEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PrivateEndpoints proto is used to provide paths for users to send requests privately. To send request via private service access, use predict_http_uri, explain_http_uri or health_http_uri. To send request via private service connect, use service_attachment.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadFeatureValuesResponse -->

# Class ReadFeatureValuesResponse (1.135.0)

`ReadFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.ReadFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`header` |
Response header. |
`entity_view` |
Entity view with Feature values. This may be the entity in the Featurestore if values for all Features were requested, or a projection of the entity in the Featurestore if values for only some Features were requested. |

## Classes

### EntityView

`EntityView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Entity view with Feature values.

### FeatureDescriptor

`FeatureDescriptor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for requested Features.

### Header

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.

## Methods

### ReadFeatureValuesResponse

`ReadFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.ReadFeatureValues.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesResponse.SelectTimeRangeAndFeature -->

# Class SelectTimeRangeAndFeature (1.135.0)

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectTimeRangeAndFeature option.

## Attributes |
|
|---|---|
Name |
Description |
`impacted_feature_count` |
`int`
The count of the features or columns impacted. This is the same as the feature count in the request. |
`offline_storage_modified_entity_row_count` |
`int`
The count of modified entity rows in the offline storage. Each row corresponds to the combination of an entity ID and a timestamp. One entity ID can have multiple rows in the offline storage. Within each row, only the features specified in the request are deleted. |
`online_storage_modified_entity_count` |
`int`
The count of modified entities in the online storage. Each entity ID corresponds to one entity. Within each entity, only the features specified in the request are deleted. |

## Methods

### SelectTimeRangeAndFeature

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectTimeRangeAndFeature option.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RubricCritiqueResult -->

# Class RubricCritiqueResult (1.135.0)

`RubricCritiqueResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rubric critique result.

## Attributes |
|
|---|---|
Name |
Description |
`rubric` |
`str`
Output only. Rubric to be evaluated. |
`verdict` |
`bool`
Output only. Verdict for the rubric - true if the rubric is met, false otherwise. |

## Methods

### RubricCritiqueResult

`RubricCritiqueResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rubric critique result.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeArtifactsMetadata -->

# Class PurgeArtifactsMetadata (1.135.0)

`PurgeArtifactsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeArtifacts.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for purging Artifacts. |

## Methods

### PurgeArtifactsMetadata

`PurgeArtifactsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeArtifacts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateMetadataStoreRequest -->

# Class CreateMetadataStoreRequest (1.135.0)

`CreateMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataStore.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location where the MetadataStore should be created. Format: `projects/{project}/locations/{location}/`
|
`metadata_store` |
Required. The MetadataStore to create. |
`metadata_store_id` |
`str`
The {metadatastore} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
If not provided, the MetadataStore's ID will be a UUID
generated by the service. Must be 4-128 characters in
length. Valid characters are `/` a-z][0-9]`-/` . Must be
unique across all MetadataStores in the parent Location.
(Otherwise the request will fail with ALREADY_EXISTS, or
PERMISSION_DENIED if the caller can't view the preexisting
MetadataStore.)
|

## Methods

### CreateMetadataStoreRequest

`CreateMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataStore.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tensor -->

# Class Tensor (1.135.0)

`Tensor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A tensor value type.

## Attributes |
|
|---|---|
Name |
Description |
`dtype` |
The data type of tensor. |
`shape` |
`MutableSequence[int]`
Shape of the tensor. |
`bool_val` |
`MutableSequence[bool]`
Type specific representations that make it easy to create tensor protos in all languages. Only the representation corresponding to "dtype" can be set. The values hold the flattened representation of the tensor in row major order. `BOOL][google.aiplatform.master.Tensor.DataType.BOOL]`
|
`string_val` |
`MutableSequence[str]`
`STRING][google.aiplatform.master.Tensor.DataType.STRING]`
|
`bytes_val` |
`MutableSequence[bytes]`
`STRING][google.aiplatform.master.Tensor.DataType.STRING]`
|
`float_val` |
`MutableSequence[float]`
`FLOAT][google.aiplatform.master.Tensor.DataType.FLOAT]`
|
`double_val` |
`MutableSequence[float]`
`DOUBLE][google.aiplatform.master.Tensor.DataType.DOUBLE]`
|
`int_val` |
`MutableSequence[int]`
`INT_8][google.aiplatform.master.Tensor.DataType.INT8]`
`INT_16][google.aiplatform.master.Tensor.DataType.INT16]`
`INT_32][google.aiplatform.master.Tensor.DataType.INT32]`
|
`int64_val` |
`MutableSequence[int]`
`INT64][google.aiplatform.master.Tensor.DataType.INT64]`
|
`uint_val` |
`MutableSequence[int]`
`UINT8][google.aiplatform.master.Tensor.DataType.UINT8]`
`UINT16][google.aiplatform.master.Tensor.DataType.UINT16]`
`UINT32][google.aiplatform.master.Tensor.DataType.UINT32]`
|
`uint64_val` |
`MutableSequence[int]`
`UINT64][google.aiplatform.master.Tensor.DataType.UINT64]`
|
`list_val` |
`MutableSequence[google.cloud.aiplatform_v1beta1.types.Tensor]`
A list of tensor values. |
`struct_val` |
`MutableMapping[str, google.cloud.aiplatform_v1beta1.types.Tensor]`
A map of string to tensor. |
`tensor_val` |
`bytes`
Serialized raw tensor content. |

## Classes

### DataType

`DataType(value)`


Data type of the tensor.

### StructValEntry

`StructValEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### Tensor

`Tensor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A tensor value type.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient -->

# Class PersistentResourceServiceAsyncClient (1.135.0)

```
PersistentResourceServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's machine learning PersistentResource.

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
`PersistentResourceServiceTransport` |
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

### PersistentResourceServiceAsyncClient

```
PersistentResourceServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the persistent resource service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PersistentResourceServiceTransport,Callable[..., PersistentResourceServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the PersistentResourceServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_persistent_resource

```
create_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.CreatePersistentResourceRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
] = None,
persistent_resource_id: typing.Optional[str] = None,
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


Creates a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreatePersistentResourceRequest.html)(
parent="parent_value",
persistent_resource_id="persistent_resource_id_value",
)
# Make the request
operation = client.[create_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_create_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.CreatePersistentResource. |
`parent` |
Required. The resource name of the Location to create the PersistentResource in. Format: |
`persistent_resource` |
Required. The PersistentResource to create. This corresponds to the |
`persistent_resource_id` |
Required. The ID to use for the PersistentResource, which become the final component of the PersistentResource's resource name. The maximum length is 63 characters, and valid characters are |
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

### delete_persistent_resource

```
delete_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.DeletePersistentResourceRequest,
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


Deletes a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeletePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeletePersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_delete_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.DeletePersistentResource. |
`name` |
Required. The name of the PersistentResource to be deleted. Format: |
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
`PersistentResourceServiceAsyncClient` |
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
`PersistentResourceServiceAsyncClient` |
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
`PersistentResourceServiceAsyncClient` |
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

### get_persistent_resource

```
get_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.GetPersistentResourceRequest,
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
) -> google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
```


Gets a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_get_persistent_resource)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PersistentResourceService.GetPersistentResource. |
`name` |
Required. The name of the PersistentResource resource. Format: |
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
Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport
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

### list_persistent_resources

```
list_persistent_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
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
google.cloud.aiplatform_v1.services.persistent_resource_service.pagers.ListPersistentResourcesAsyncPager
)
```


Lists PersistentResources in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_persistent_resources():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListPersistentResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_persistent_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_list_persistent_resources)(request=request)
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
The request object. Request message for PersistentResourceService.ListPersistentResources. |
`parent` |
Required. The resource name of the Location to list the PersistentResources from. Format: |
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
Response message for PersistentResourceService.ListPersistentResources Iterating over this object will yield results and resolve additional pages automatically. |

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

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

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_persistent_resource_path

`parse_persistent_resource_path(path: str) -> typing.Dict[str, str]`


Parses a persistent_resource path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### persistent_resource_path

```
persistent_resource_path(
project: str, location: str, persistent_resource: str
) -> str
```


Returns a fully-qualified persistent_resource string.

### reboot_persistent_resource

```
reboot_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.RebootPersistentResourceRequest,
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


Reboots a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_reboot_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RebootPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebootPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[reboot_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_reboot_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.RebootPersistentResource. |
`name` |
Required. The name of the PersistentResource resource. Format: |
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

### update_persistent_resource

```
update_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.UpdatePersistentResourceRequest,
dict,
]
] = None,
*,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
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


Updates a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdatePersistentResourceRequest.html)(
)
# Make the request
operation = client.[update_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_update_persistent_resource)(request=request)
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
The request object. Request message for UpdatePersistentResource method. |
`persistent_resource` |
Required. The PersistentResource to update. The PersistentResource's |
`update_mask` |
Required. Specify the fields to be overwritten in the PersistentResource by the update method. This corresponds to the |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient -->

# Class PersistentResourceServiceAsyncClient (1.134.0)

```
PersistentResourceServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's machine learning PersistentResource.

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
`PersistentResourceServiceTransport` |
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

### PersistentResourceServiceAsyncClient

```
PersistentResourceServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the persistent resource service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PersistentResourceServiceTransport,Callable[..., PersistentResourceServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the PersistentResourceServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_persistent_resource

```
create_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.CreatePersistentResourceRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
] = None,
persistent_resource_id: typing.Optional[str] = None,
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


Creates a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreatePersistentResourceRequest.html)(
parent="parent_value",
persistent_resource_id="persistent_resource_id_value",
)
# Make the request
operation = client.[create_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_create_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.CreatePersistentResource. |
`parent` |
Required. The resource name of the Location to create the PersistentResource in. Format: |
`persistent_resource` |
Required. The PersistentResource to create. This corresponds to the |
`persistent_resource_id` |
Required. The ID to use for the PersistentResource, which become the final component of the PersistentResource's resource name. The maximum length is 63 characters, and valid characters are |
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

### delete_persistent_resource

```
delete_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.DeletePersistentResourceRequest,
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


Deletes a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeletePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeletePersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_delete_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.DeletePersistentResource. |
`name` |
Required. The name of the PersistentResource to be deleted. Format: |
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
`PersistentResourceServiceAsyncClient` |
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
`PersistentResourceServiceAsyncClient` |
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
`PersistentResourceServiceAsyncClient` |
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

### get_persistent_resource

```
get_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.GetPersistentResourceRequest,
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
) -> google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
```


Gets a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_get_persistent_resource)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PersistentResourceService.GetPersistentResource. |
`name` |
Required. The name of the PersistentResource resource. Format: |
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
Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport
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

### list_persistent_resources

```
list_persistent_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
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
google.cloud.aiplatform_v1.services.persistent_resource_service.pagers.ListPersistentResourcesAsyncPager
)
```


Lists PersistentResources in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_persistent_resources():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListPersistentResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_persistent_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_list_persistent_resources)(request=request)
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
The request object. Request message for PersistentResourceService.ListPersistentResources. |
`parent` |
Required. The resource name of the Location to list the PersistentResources from. Format: |
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
Response message for PersistentResourceService.ListPersistentResources Iterating over this object will yield results and resolve additional pages automatically. |

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

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

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_persistent_resource_path

`parse_persistent_resource_path(path: str) -> typing.Dict[str, str]`


Parses a persistent_resource path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### persistent_resource_path

```
persistent_resource_path(
project: str, location: str, persistent_resource: str
) -> str
```


Returns a fully-qualified persistent_resource string.

### reboot_persistent_resource

```
reboot_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.RebootPersistentResourceRequest,
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


Reboots a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_reboot_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RebootPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebootPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[reboot_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_reboot_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.RebootPersistentResource. |
`name` |
Required. The name of the PersistentResource resource. Format: |
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

### update_persistent_resource

```
update_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.UpdatePersistentResourceRequest,
dict,
]
] = None,
*,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
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


Updates a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdatePersistentResourceRequest.html)(
)
# Make the request
operation = client.[update_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_update_persistent_resource)(request=request)
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
The request object. Request message for UpdatePersistentResource method. |
`persistent_resource` |
Required. The PersistentResource to update. The PersistentResource's |
`update_mask` |
Required. Specify the fields to be overwritten in the PersistentResource by the update method. This corresponds to the |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PrivateEndpoint -->

# Class PrivateEndpoint (1.134.0)

```
PrivateEndpoint(
endpoint_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Represents a Vertex AI PrivateEndpoint resource.

## Classes

### PrivateServiceConnectConfig

```
PrivateServiceConnectConfig(
project_allowlist: typing.Optional[typing.Sequence[str]] = None,
)
```


Represents a Vertex AI PrivateServiceConnectConfig resource.

## Properties

### create_time

Time this resource was created.

### dedicated_endpoint_dns

The dedicated endpoint dns for this Endpoint.

This property is only available if dedicated endpoint is enabled. If dedicated endpoint is not enabled, this property returns None.

### dedicated_endpoint_enabled

The dedicated endpoint is enabled for this Endpoint.

This property will be true if dedicated endpoint is enabled.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### explain_http_uri

HTTP path to send explain requests to, used when calling `PrivateEndpoint.explain()`


### gca_resource

The underlying resource proto representation.

### health_http_uri

HTTP path to send health check requests to, used when calling `PrivateEndpoint.health_check()`


### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### network

The full name of the Google Compute Engine
[network](https://cloud.google.com/vpc/docs/vpc#networks) to which this
Endpoint should be peered.

Takes the format `projects/{project}/global/networks/{network}`

. Where
{project} is a project number, as in `12345`

, and {network} is a network name.

Private services access must already be configured for the network. If left unspecified, the Endpoint is not peered with any network.

### predict_http_uri

HTTP path to send prediction requests to, used when calling `PrivateEndpoint.predict()`


### preview

Return an Endpoint instance with preview features enabled.

### private_service_connect_config

The Private Service Connect configuration for this Endpoint.

### resource_name

Full qualified resource name.

### traffic_split

A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel.

If a DeployedModel's ID is not listed in this map, then it receives no traffic.

The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment.

### update_time

Time this resource was last updated.

## Methods

### PrivateEndpoint

```
PrivateEndpoint(
endpoint_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves a PrivateEndpoint resource.

Example usage: my_private_endpoint = aiplatform.PrivateEndpoint( endpoint_name="projects/123/locations/us-central1/endpoints/1234567891234567890" )

```
or (when project and location are initialized)
my_private_endpoint = aiplatform.PrivateEndpoint(
endpoint_name="1234567891234567890"
)
```


Parameters |
|
|---|---|
Name |
Description |
`endpoint_name` |
`str`
Required. A fully-qualified endpoint resource name or endpoint ID. Example: "projects/123/locations/us-central1/endpoints/my_endpoint_id" or "my_endpoint_id" when project and location are initialized or passed. |
`project` |
`str`
Optional. Project to retrieve endpoint from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve endpoint from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the Endpoint being retrieved is not a PrivateEndpoint. |
`ImportError` |
If there is an issue importing the `urllib3` package. |

### create

```
create(
display_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
network: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync=True,
private_service_connect_config: typing.Union[
google.cloud.aiplatform.models.PrivateEndpoint.PrivateServiceConnectConfig,
None,
google.cloud.aiplatform_v1.types.service_networking.PrivateServiceConnectConfig,
] = None,
enable_request_response_logging=False,
request_response_logging_sampling_rate: typing.Optional[float] = None,
request_response_logging_bq_destination_table: typing.Optional[str] = None,
inference_timeout: typing.Optional[int] = None,
) -> google.cloud.aiplatform.models.PrivateEndpoint
```


Creates a new PrivateEndpoint.

Example usage: For PSA based private endpoint: my_private_endpoint = aiplatform.PrivateEndpoint.create( display_name="my_endpoint_name", project="my_project_id", location="us-central1", network="projects/123456789123/global/networks/my_vpc" )

```
or (when project and location are initialized)
my_private_endpoint = aiplatform.PrivateEndpoint.create(
display_name="my_endpoint_name",
network="projects/123456789123/global/networks/my_vpc"
)
```


For PSC based private endpoint: my_private_endpoint = aiplatform.PrivateEndpoint.create( display_name="my_endpoint_name", project="my_project_id", location="us-central1", private_service_connect=aiplatform.compat.types.service_networking.PrivateServiceConnectConfig( enable_private_service_connect=True, project_allowlist=["test-project"]), )

```
or (when project and location are initialized)
my_private_endpoint = aiplatform.PrivateEndpoint.create(
display_name="my_endpoint_name",
private_service_connect=aiplatform.compat.types.service_networking.PrivateServiceConnectConfig(
enable_private_service_connect=True,
project_allowlist=["test-project"]),
)
```


Parameters |
|
|---|---|
Name |
Description |
`private_service_connect_config` |
`typing.Union[google.cloud.aiplatform.models.PrivateEndpoint.PrivateServiceConnectConfig, NoneType, `
(aiplatform.compat.types.service_networking.PrivateServiceConnectConfig): |
`request_response_logging_sampling_rate` |
`float`
Optional. The request response logging sampling rate. If not set, default is 0.0. |
`request_response_logging_bq_destination_table` |
`str`
Optional. The request response logging bigquery destination. If not set, will create a table with name: |
`inference_timeout` |
`int`
Optional. It defines the prediction timeout, in seconds, for online predictions using cloud-based endpoints. This applies to either PSC endpoints, when private_service_connect_config is set, or dedicated endpoints, when dedicated_endpoint_enabled is true. |
`display_name` |
`str`
Required. The user-defined name of the Endpoint. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`project` |
`str`
Optional. Project to retrieve endpoint from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve endpoint from. If not set, location set in aiplatform.init will be used. |
`network` |
`str`
Optional. The full name of the Compute Engine network to which this Endpoint will be peered. E.g. "projects/123456789123/global/networks/my_vpc". Private services access must already be configured for the network. If left unspecified, the network set with aiplatform.init will be used. Cannot be set together with private_service_connect_config. |
`description` |
`str`
Optional. The description of the Endpoint. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Endpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |
`encryption_spec_key_name` |
`str`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_request_response_logging` |
`bool`
Optional. Whether to enable request & response logging for this endpoint. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A network must be instantiated when creating a |
`PrivateEndpoint.` |

Returns |
|
|---|---|
Type |
Description |
`endpoint (aiplatform.PrivateEndpoint)` |
Created endpoint. |

### delete

`delete(force: bool = False, sync: bool = True) -> None`


Deletes this Vertex AI PrivateEndpoint resource. If force is set to True, all models on this PrivateEndpoint will be undeployed prior to deletion.

Parameters |
|
|---|---|
Name |
Description |
`force` |
`bool`
Required. If force is set to True, all deployed models on this Endpoint will be undeployed first. Default is False. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

Exceptions |
|
|---|---|
Type |
Description |
`FailedPrecondition` |
If models are deployed on this Endpoint and force = False. |

### deploy

```
deploy(
model: google.cloud.aiplatform.models.Model,
deployed_model_display_name: typing.Optional[str] = None,
machine_type: typing.Optional[str] = None,
min_replica_count: int = 1,
max_replica_count: int = 1,
accelerator_type: typing.Optional[str] = None,
accelerator_count: typing.Optional[int] = None,
gpu_partition_size: typing.Optional[str] = None,
tpu_topology: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync=True,
disable_container_logging: bool = False,
traffic_percentage: typing.Optional[int] = 0,
traffic_split: typing.Optional[typing.Dict[str, int]] = None,
reservation_affinity_type: typing.Optional[str] = None,
reservation_affinity_key: typing.Optional[str] = None,
reservation_affinity_values: typing.Optional[typing.List[str]] = None,
spot: bool = False,
system_labels: typing.Optional[typing.Dict[str, str]] = None,
required_replica_count: typing.Optional[int] = 0,
autoscaling_target_cpu_utilization: typing.Optional[int] = None,
autoscaling_target_accelerator_duty_cycle: typing.Optional[int] = None,
autoscaling_target_request_count_per_minute: typing.Optional[int] = None,
autoscaling_target_pubsub_num_undelivered_messages: typing.Optional[int] = None,
autoscaling_pubsub_subscription_labels: typing.Optional[
typing.Dict[str, str]
] = None,
) -> None
```


Deploys a Model to the PrivateEndpoint.

Example Usage: PSA based private endpoint my_private_endpoint.deploy( model=my_model )

```
PSC based private endpoint
psc_endpoint.deploy(
model=first_model,
)
psc_endpoint.deploy(
model=second_model,
traffic_percentage=50,
)
psc_endpoint.deploy(
model=third_model,
traffic_percentage={
'first_model_id': 40,
'second_model_id': 30,
'third_model_id': 30
},
)
```


Parameters |
|
|---|---|
Name |
Description |
`deployed_model_display_name` |
`str`
Optional. The display name of the DeployedModel. If not provided upon creation, the Model's display_name is used. |
`machine_type` |
`str`
Optional. The type of machine. Not specifying machine type will result in model to be deployed with automatic resources. |
`min_replica_count` |
`int`
Optional. The minimum number of machine replicas this deployed model will be always deployed on. If traffic against it increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed. |
`max_replica_count` |
`int`
Optional. The maximum number of replicas this deployed model may be deployed on when the traffic against it increases. If requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale the model to that many replicas is guaranteed (barring service outages). If traffic against the deployed model increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, the larger value of min_replica_count or 1 will be used. If value provided is smaller than min_replica_count, it will automatically be increased to be min_replica_count. |
`accelerator_type` |
`str`
Optional. Hardware accelerator type. Must also set accelerator_count if used. One of ACCELERATOR_TYPE_UNSPECIFIED, NVIDIA_TESLA_K80, NVIDIA_TESLA_P100, NVIDIA_TESLA_V100, NVIDIA_TESLA_P4, NVIDIA_TESLA_T4 |
`accelerator_count` |
`int`
Optional. The number of accelerators to attach to a worker replica. |
`gpu_partition_size` |
`str`
Optional. The GPU partition Size for Nvidia MIG. |
`tpu_topology` |
`str`
Optional. The TPU topology to use for the DeployedModel. Required for CloudTPU multihost deployments. |
`service_account` |
`str`
The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project. Users deploying the Model must have the |
`explanation_metadata` |
`aiplatform.explain.ExplanationMetadata`
Optional. Metadata describing the Model's input and output for explanation. |
`explanation_parameters` |
`aiplatform.explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. For more details, see |
`metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`traffic_percentage` |
`int`
Optional. Desired traffic to newly deployed model. Defaults to 0 if there are pre-existing deployed models. Defaults to 100 if there are no pre-existing deployed models. Defaults to 100 for PSA based private endpoint. Negative values should not be provided. Traffic of previously deployed models at the endpoint will be scaled down to accommodate new deployed model's traffic. Should not be provided if traffic_split is provided. |
`traffic_split` |
`Dict[str, int]`
Optional. Only supported by PSC base private endpoint. A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If a DeployedModel's ID is not listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at the moment. Key for model being deployed is "0". Should not be provided if traffic_percentage is provided. |
`reservation_affinity_type` |
`str`
Optional. The type of reservation affinity. One of NO_RESERVATION, ANY_RESERVATION, SPECIFIC_RESERVATION, SPECIFIC_THEN_ANY_RESERVATION, SPECIFIC_THEN_NO_RESERVATION |
`reservation_affinity_key` |
`str`
Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use |
`reservation_affinity_values` |
`List[str]`
Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation. Format: 'projects/{project_id_or_number}/zones/{zone}/reservations/{reservation_name}' |
`spot` |
`bool`
Optional. Whether to schedule the deployment workload on spot VMs. |
`system_labels` |
`Dict[str, str]`
Optional. System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only. |
`required_replica_count` |
`int`
Optional. Number of required available replicas for the deployment to succeed. This field is only needed when partial model deployment/mutation is desired, with a value greater than or equal to 1 and fewer than or equal to min_replica_count. If set, the model deploy/mutate operation will succeed once available_replica_count reaches required_replica_count, and the rest of the replicas will be retried. |
`model` |
`aiplatform.Model`
Required. Model to be deployed. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### direct_predict

```
direct_predict(
inputs: typing.List,
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Prediction
```


Makes a direct (gRPC) prediction against this Endpoint for a pre-built image.

Parameters |
|
|---|---|
Name |
Description |
`inputs` |
`List`
Required. The inputs that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### direct_predict_async

```
direct_predict_async(
inputs: typing.List,
*,
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Makes an asynchronous direct (gRPC) prediction against this Endpoint for a pre-built image.

Example usage:

```
response = await my_endpoint.direct_predict_async(inputs=[...])
my_predictions = response.predictions
```
```


Parameters |
|
|---|---|
Name |
Description |
`inputs` |
`List`
Required. The inputs that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### direct_raw_predict

```
direct_raw_predict(
method_name: str, request: bytes, timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Makes a direct (gRPC) prediction request using arbitrary headers for a custom container.

Example usage:

```
my_endpoint = aiplatform.Endpoint(ENDPOINT_ID)
response = my_endpoint.direct_raw_predict(request=b'...')
```
```


Parameters |
|
|---|---|
Name |
Description |
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform prediction. |
`request` |
`bytes`
The body of the prediction request in bytes. |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### direct_raw_predict_async

```
direct_raw_predict_async(
method_name: str, request: bytes, timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Makes a direct (gRPC) prediction request for a custom container.

Example usage:

```
my_endpoint = aiplatform.Endpoint(ENDPOINT_ID)
response = await my_endpoint.direct_raw_predict(request=b'...')
```
```


Parameters |
|
|---|---|
Name |
Description |
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform prediction. |
`request` |
`bytes`
The body of the prediction request in bytes. |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### explain

`explain()`


Make a prediction with explanations against this Endpoint.

Example usage: response = my_endpoint.explain(instances=[...]) my_explanations = response.explanations

Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`deployed_model_id` |
`str`
Optional. If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding this Endpoint's traffic split. |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction with returned predictions, explanations, and Model ID. |

### explain_async

```
explain_async(
instances: typing.List[typing.Dict],
*,
parameters: typing.Optional[typing.Dict] = None,
deployed_model_id: typing.Optional[str] = None,
timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Make a prediction with explanations against this Endpoint.

Example usage:

```
response = await my_endpoint.explain_async(instances=[...])
my_explanations = response.explanations
```
```


Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`deployed_model_id` |
`str`
Optional. If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding this Endpoint's traffic split. |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction with returned predictions, explanations, and Model ID. |

### health_check

`health_check() -> bool`


Makes a request to this PrivateEndpoint's health check URI. Must be within network that this PrivateEndpoint is in. This is only supported by PSA based private endpoint.

Example Usage: if my_private_endpoint.health_check(): print("PrivateEndpoint is healthy!")

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If a model has not been deployed a request cannot be made. |
`RuntimeError` |
If the endpoint is PSC based private endpoint. |

Returns |
|
|---|---|
Type |
Description |
`bool` |
Checks if calls can be made to this PrivateEndpoint. |

### invoke

```
invoke(
request_path: str,
body: bytes,
headers: typing.Dict[str, str],
deployed_model_id: typing.Optional[str] = None,
stream: bool = False,
timeout: typing.Optional[float] = None,
endpoint_override: typing.Optional[str] = None,
) -> typing.Iterator[bytes]
```


Makes a prediction request for arbitrary paths.

Example usage: my_endpoint = aiplatform.PrivateEndpoint(ENDPOINT_ID) response = my_endpoint.invoke( request_path="/v1/chat/completions", body = json.dumps(DATA).encode("utf-8"), headers = {'Content-Type':'application/json'}, endpoint_override="10.128.0.3", ) status_code = response.status_code results = json.dumps(response.text)

```
for stream_response in my_endpoint.invoke(
request_path="/v1/chat/completions",
body = json.dumps(DATA).encode("utf-8"),
headers = {'Content-Type':'application/json'},
stream=True,
endpoint_override="10.128.0.3",
):
stream_response_text = stream_response.decode('utf-8')
```


Parameters |
|
|---|---|
Name |
Description |
`request_path` |
`str`
The request url to the model server. The request path must be a string that starts with a forward slash. Root can't be accessed. |
`body` |
`bytes`
The body of the prediction request in bytes. This must not exceed 1.5 mb per request. |
`headers` |
`Dict[str, str]`
The header of the request as a dictionary. There are no restrictions on the header. |
`deployed_model_id` |
`str`
Optional. If specified, this InvokeRequest will be served by the chosen DeployedModel, overriding this Endpoint's traffic split. |
`stream` |
`bool`
If set to True, streaming will be enabled. |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |
`endpoint_override` |
`Optional[str]`
The Private Service Connect endpoint's IP address or DNS that points to the endpoint's service attachment. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If a endpoint override is not provided for PSC based endpoint. |
`ValueError` |
If a endpoint override is invalid for PSC based endpoint. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.models.PrivateEndpoint]
```


List all PrivateEndpoint resource instances.

Example Usage: my_private_endpoints = aiplatform.PrivateEndpoint.list()

```
or
my_private_endpoints = aiplatform.PrivateEndpoint.list(
filter='labels.my_label="my_label_value" OR display_name=!"old_endpoint"',
)
```


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

Returns |
|
|---|---|
Type |
Description |
`List[models.PrivateEndpoint]` |
A list of PrivateEndpoint resource objects. |

### list_models

```
list_models() -> (
typing.List[google.cloud.aiplatform_v1.types.endpoint.DeployedModel]
)
```


Returns a list of the models deployed to this Endpoint.

Returns |
|
|---|---|
Type |
Description |
`deployed_models (List[aiplatform.gapic.DeployedModel])` |
A list of the models deployed in this Endpoint. |

### predict

```
predict(
instances: typing.List,
parameters: typing.Optional[typing.Dict] = None,
endpoint_override: typing.Optional[str] = None,
) -> google.cloud.aiplatform.models.Prediction
```


Make a prediction against this PrivateEndpoint using a HTTP request.
For PSA based private endpoint, this method must be called within the
network the PrivateEndpoint is peered to. Otherwise, the predict() call
will fail with error code 404. To check, use `PrivateEndpoint.network`

.

For PSC based priviate endpoint, the project where caller credential are from must be allowlisted.

Example usage: PSA based private endpoint:

```
response = my_private_endpoint.predict(instances=[...], parameters={...})
my_predictions = response.predictions
PSC based private endpoint:
After creating PSC Endpoint pointing to the endpoint's
ServiceAttachment, use the PSC Endpoint IP Address or DNS as
endpoint_override.
psc_endpoint_address = "10.0.1.23"
or
psc_endpoint_address = "test.my.prediction"
response = my_private_endpoint.predict(instances=[...],
endpoint_override=psc_endpoint_address)
my_predictions = response.predictions
```


Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. Instance types mut be JSON serializable. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`endpoint_override` |
`Optional[str]`
The Private Service Connect endpoint's IP address or DNS that points to the endpoint's service attachment. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If a model has not been deployed a request cannot be made for PSA based endpoint. |
`ValueError` |
If a endpoint override is not provided for PSC based endpoint. |
`ValueError` |
If a endpoint override is invalid for PSC based endpoint. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction object with returned predictions and Model ID. |

### predict_async

```
predict_async(
instances: typing.List,
*,
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Make an asynchronous prediction against this Endpoint. Example usage:

```
response = await my_endpoint.predict_async(instances=[...])
my_predictions = response.predictions
```
```


Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction with returned predictions and Model ID. |

### raw_predict

```
raw_predict(
body: bytes,
headers: typing.Dict[str, str],
endpoint_override: typing.Optional[str] = None,
) -> requests.models.Response
```


Make a prediction request using arbitrary headers.
This method must be called within the network the PrivateEndpoint is peered to.
Otherwise, the predict() call will fail with error code 404. To check, use `PrivateEndpoint.network`

.

Example usage: my_endpoint = aiplatform.PrivateEndpoint(ENDPOINT_ID)

```
# PSA based private endpint
response = my_endpoint.raw_predict(
body = b'{"instances":[{"feat_1":val_1, "feat_2":val_2}]}',
headers = {'Content-Type':'application/json'}
)
# PSC based private endpoint
response = my_endpoint.raw_predict(
body = b'{"instances":[{"feat_1":val_1, "feat_2":val_2}]}',
headers = {'Content-Type':'application/json'},
endpoint_override = "10.1.0.23"
)
status_code = response.status_code
results = json.dumps(response.text)
```


Parameters |
|
|---|---|
Name |
Description |
`body` |
`bytes`
The body of the prediction request in bytes. This must not exceed 1.5 mb per request. |
`headers` |
`Dict[str, str]`
The header of the request as a dictionary. There are no restrictions on the header. |
`endpoint_override` |
`Optional[str]`
The Private Service Connect endpoint's IP address or DNS that points to the endpoint's service attachment. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If a endpoint override is not provided for PSC based endpoint. |
`ValueError` |
If a endpoint override is invalid for PSC based endpoint. |

### stream_direct_predict

```
stream_direct_predict(
inputs_iterator: typing.Iterator[typing.List],
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None,
) -> typing.Iterator[google.cloud.aiplatform.models.Prediction]
```


Makes a streaming direct (gRPC) prediction against this Endpoint for a pre-built image.

Parameters |
|
|---|---|
Name |
Description |
`inputs_iterator` |
`Iterator[List]`
Required. An iterator of the inputs that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`Optional[float] :Yields: *predictions (Iterator[aiplatform.Prediction])* -- The resulting streamed predictions.`
Optional. The timeout for this request in seconds. |

### stream_direct_raw_predict

```
stream_direct_raw_predict(
method_name: str,
requests: typing.Iterator[bytes],
timeout: typing.Optional[float] = None,
) -> typing.Iterator[google.cloud.aiplatform.models.Prediction]
```


Makes a direct (gRPC) streaming prediction request for a custom container.

Example usage:

```
my_endpoint = aiplatform.Endpoint(ENDPOINT_ID)
for stream_response in my_endpoint.stream_direct_raw_predict(
request=b'...'
):
yield stream_response
```
```


Parameters |
|
|---|---|
Name |
Description |
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform prediction. |
`requests` |
`Iterator[bytes]`
The body of the prediction requests in bytes. |
`timeout` |
`Optional[float] :Yields: *predictions (Iterator[aiplatform.Prediction])* -- The resulting streamed predictions.`
Optional. The timeout for this request in seconds. |

### stream_raw_predict

```
stream_raw_predict(
body: bytes,
headers: typing.Dict[str, str],
endpoint_override: typing.Optional[str] = None,
) -> typing.Iterator[bytes]
```


Make a streaming prediction request using arbitrary headers.

Example usage: my_endpoint = aiplatform.PrivateEndpoint(ENDPOINT_ID)

```
# Prepare the request body
request_body = json.dumps({...}).encode('utf-8')
# Define the headers
headers = {
'Content-Type': 'application/json',
}
# Use stream_raw_predict to send the request and process the response
for stream_response in psc_endpoint.stream_raw_predict(
body=request_body,
headers=headers,
endpoint_override="10.128.0.26" # Replace with your actual endpoint
):
stream_response_text = stream_response.decode('utf-8')
```


Parameters |
|
|---|---|
Name |
Description |
`body` |
`bytes`
The body of the prediction request in bytes. This must not exceed 10 mb per request. |
`headers` |
`Dict[str, str]`
The header of the request as a dictionary. There are no restrictions on the header. |
`endpoint_override` |
`Optional[str] :Yields: *predictions (Iterator[bytes])* -- The streaming prediction results as lines of bytes.`
The Private Service Connect endpoint's IP address or DNS that points to the endpoint's service attachment. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If a endpoint override is not provided for PSC based endpoint. |
`ValueError` |
If a endpoint override is invalid for PSC based endpoint. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### undeploy

```
undeploy(
deployed_model_id: str,
sync=True,
traffic_split: typing.Optional[typing.Dict[str, int]] = None,
) -> None
```


Undeploys a deployed model from the PrivateEndpoint.

Example Usage: PSA based private endpoint: my_private_endpoint.undeploy( deployed_model_id="1234567891232567891" )

```
or
my_deployed_model_id = my_private_endpoint.list_models()[0].id
my_private_endpoint.undeploy(
deployed_model_id=my_deployed_model_id
)
```


Parameters |
|
|---|---|
Name |
Description |
`traffic_split` |
`Dict[str, int]`
Optional. Only supported by PSC based private endpoint. A map of DeployedModel IDs to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. Required if undeploying a model with non-zero traffic from an Endpoint with multiple deployed models. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at the moment. If a DeployedModel's ID is not listed in this map, then it receives no traffic. |
`deployed_model_id` |
`str`
Required. The ID of the DeployedModel to be undeployed from the PrivateEndpoint. Use PrivateEndpoint.list_models() to get the deployed model ID. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### undeploy_all

`undeploy_all(sync: bool = True) -> google.cloud.aiplatform.models.PrivateEndpoint`


Undeploys every model deployed to this PrivateEndpoint.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### update

```
update(
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
traffic_split: typing.Optional[typing.Dict[str, int]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.PrivateEndpoint
```


Updates a PrivateEndpoint.

Example usage: PSC based private endpoint

```
my_endpoint = my_endpoint.update(
display_name='my-updated-endpoint',
description='my updated description',
labels={'key': 'value'},
traffic_split={
'123456': 20,
'234567': 80,
},
)
```


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The display name of the Endpoint. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the Endpoint. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Endpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`traffic_split` |
`Dict[str, int]`
Optional. Only supported by PSC based private endpoint A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If a DeployedModel's ID is not listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `traffic_split` is set for PSA based private endpoint. |

Returns |
|
|---|---|
Type |
Description |
`Endpoint (aiplatform.Prediction)` |
Updated endpoint resource. |

### wait

`wait()`


Helper method that blocks until all futures are complete.

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Checkpoint -->

# Class Checkpoint (1.134.0)

`Checkpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the machine learning model version checkpoint.

## Attributes |
|
|---|---|
Name |
Description |
`checkpoint_id` |
`str`
The ID of the checkpoint. |
`epoch` |
`int`
The epoch of the checkpoint. |
`step` |
`int`
The step of the checkpoint. |

## Methods

### Checkpoint

`Checkpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the machine learning model version checkpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelNasJobRequest -->

# Class CancelNasJobRequest (1.134.0)

`CancelNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CancelNasJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NasJob to cancel. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}`
|

## Methods

### CancelNasJobRequest

`CancelNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CancelNasJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardExperimentRequest -->

# Class UpdateTensorboardExperimentRequest (1.134.0)

```
UpdateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardExperiment.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardExperiment resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard_experiment` |
Required. The TensorboardExperiment's `name` field is used
to identify the TensorboardExperiment to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|

## Methods

### UpdateTensorboardExperimentRequest

```
UpdateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardExperiment.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateExecutionRequest -->

# Class CreateExecutionRequest (1.134.0)

`CreateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateExecution.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Execution should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`execution` |
Required. The Execution to create. |
`execution_id` |
`str`
The {execution} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
If not provided, the Execution's ID will be a UUID generated
by the service. Must be 4-128 characters in length. Valid
characters are `/` a-z][0-9]`-/` . Must be unique across all
Executions in the parent MetadataStore. (Otherwise the
request will fail with ALREADY_EXISTS, or PERMISSION_DENIED
if the caller can't view the preexisting Execution.)
|

## Methods

### CreateExecutionRequest

`CreateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateExecution.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddContextArtifactsAndExecutionsResponse -->

# Class AddContextArtifactsAndExecutionsResponse (1.134.0)

```
AddContextArtifactsAndExecutionsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.AddContextArtifactsAndExecutions.

## Methods

### AddContextArtifactsAndExecutionsResponse

```
AddContextArtifactsAndExecutionsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.AddContextArtifactsAndExecutions.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTrialRequest -->

# Class DeleteTrialRequest (1.134.0)

`DeleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.DeleteTrial.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|

## Methods

### DeleteTrialRequest

`DeleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.DeleteTrial.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateFeaturesResponse -->

# Class BatchCreateFeaturesResponse (1.134.0)

`BatchCreateFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.BatchCreateFeatures.

## Attribute |
|
|---|---|
Name |
Description |
`features` |
`MutableSequence[`
The Features created. |

## Methods

### BatchCreateFeaturesResponse

`BatchCreateFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.BatchCreateFeatures.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagCorpusRequest -->

# Class UpdateRagCorpusRequest (1.134.0)

`UpdateRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.UpdateRagCorpus.

## Attribute |
|
|---|---|
Name |
Description |
`rag_corpus` |
Required. The RagCorpus which replaces the resource on the server. |

## Methods

### UpdateRagCorpusRequest

`UpdateRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.UpdateRagCorpus.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationVerbosityResult -->

# Class SummarizationVerbosityResult (1.134.0)

```
SummarizationVerbosityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization verbosity result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Summarization Verbosity score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for summarization verbosity score. |
`confidence` |
`float`
Output only. Confidence for summarization verbosity score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### SummarizationVerbosityResult

```
SummarizationVerbosityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization verbosity result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolConfig -->

# Class ToolConfig (1.134.0)

`ToolConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool config. This config is shared for all tools provided in the request.

## Attributes |
|
|---|---|
Name |
Description |
`function_calling_config` |
Optional. Function calling config. |
`retrieval_config` |
Optional. Retrieval config. |

## Methods

### ToolConfig

`ToolConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool config. This config is shared for all tools provided in the request.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileTransformationConfig -->

# Class RagFileTransformationConfig (1.134.0)

`RagFileTransformationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the transformation config for RagFiles.

## Attribute |
|
|---|---|
Name |
Description |
`rag_file_chunking_config` |
Specifies the chunking config for RagFiles. |

## Methods

### RagFileTransformationConfig

`RagFileTransformationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the transformation config for RagFiles.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PrivateEndpoints -->

# Class PrivateEndpoints (1.134.0)

`PrivateEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PrivateEndpoints proto is used to provide paths for users to send requests privately. To send request via private service access, use predict_http_uri, explain_http_uri or health_http_uri. To send request via private service connect, use service_attachment.

## Attributes |
|
|---|---|
Name |
Description |
`predict_http_uri` |
`str`
Output only. Http(s) path to send prediction requests. |
`explain_http_uri` |
`str`
Output only. Http(s) path to send explain requests. |
`health_http_uri` |
`str`
Output only. Http(s) path to send health check requests. |
`service_attachment` |
`str`
Output only. The name of the service attachment resource. Populated if private service connect is enabled. |

## Methods

### PrivateEndpoints

`PrivateEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PrivateEndpoints proto is used to provide paths for users to send requests privately. To send request via private service access, use predict_http_uri, explain_http_uri or health_http_uri. To send request via private service connect, use service_attachment.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.notebook_service.pagers`

module.

## Classes

[ListNotebookExecutionJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookExecutionJobsAsyncPager)

```
ListNotebookExecutionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
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


A pager for iterating through `list_notebook_execution_jobs`

requests.

This class thinly wraps an initial
[ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_execution_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookExecutionJobs`

requests and continue to iterate
through the `notebook_execution_jobs`

field on the
corresponding responses.

All the usual [ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNotebookExecutionJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookExecutionJobsPager)

```
ListNotebookExecutionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
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


A pager for iterating through `list_notebook_execution_jobs`

requests.

This class thinly wraps an initial
[ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_execution_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookExecutionJobs`

requests and continue to iterate
through the `notebook_execution_jobs`

field on the
corresponding responses.

All the usual [ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNotebookRuntimeTemplatesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesAsyncPager)

```
ListNotebookRuntimeTemplatesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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


A pager for iterating through `list_notebook_runtime_templates`

requests.

This class thinly wraps an initial
[ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_runtime_templates`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookRuntimeTemplates`

requests and continue to iterate
through the `notebook_runtime_templates`

field on the
corresponding responses.

All the usual [ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNotebookRuntimeTemplatesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesPager)

```
ListNotebookRuntimeTemplatesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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


A pager for iterating through `list_notebook_runtime_templates`

requests.

This class thinly wraps an initial
[ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_runtime_templates`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookRuntimeTemplates`

requests and continue to iterate
through the `notebook_runtime_templates`

field on the
corresponding responses.

All the usual [ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNotebookRuntimesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimesAsyncPager)

```
ListNotebookRuntimesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
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


A pager for iterating through `list_notebook_runtimes`

requests.

This class thinly wraps an initial
[ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_runtimes`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookRuntimes`

requests and continue to iterate
through the `notebook_runtimes`

field on the
corresponding responses.

All the usual [ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNotebookRuntimesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimesPager)

```
ListNotebookRuntimesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
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


A pager for iterating through `list_notebook_runtimes`

requests.

This class thinly wraps an initial
[ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_runtimes`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookRuntimes`

requests and continue to iterate
through the `notebook_runtimes`

field on the
corresponding responses.

All the usual [ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseSummarizationQualityResult -->

# Class PairwiseSummarizationQualityResult (1.134.0)

```
PairwiseSummarizationQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`pairwise_choice` |
Output only. Pairwise summarization prediction choice. |
`explanation` |
`str`
Output only. Explanation for summarization quality score. |
`confidence` |
`float`
Output only. Confidence for summarization quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### PairwiseSummarizationQualityResult

```
PairwiseSummarizationQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadFeatureValuesResponse -->

# Class ReadFeatureValuesResponse (1.134.0)

`ReadFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.ReadFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`header` |
Response header. |
`entity_view` |
Entity view with Feature values. This may be the entity in the Featurestore if values for all Features were requested, or a projection of the entity in the Featurestore if values for only some Features were requested. |

## Classes

### EntityView

`EntityView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Entity view with Feature values.

### FeatureDescriptor

`FeatureDescriptor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for requested Features.

### Header

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.

## Methods

### ReadFeatureValuesResponse

`ReadFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.ReadFeatureValues.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.SourceCodeSpec.PythonSpec -->

# Class PythonSpec (1.134.0)

`PythonSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for running a Python application from source.

## Attributes |
|
|---|---|
Name |
Description |
`version` |
`str`
Optional. The version of Python to use. Support version includes 3.9, 3.10, 3.11, 3.12, 3.13. If not specified, default value is 3.10. |
`entrypoint_module` |
`str`
Optional. The Python module to load as the entrypoint, specified as a fully qualified module name. For example: path.to.agent. If not specified, defaults to "agent". The project root will be added to Python sys.path, allowing imports to be specified relative to the root. |
`entrypoint_object` |
`str`
Optional. The name of the callable object within the `entrypoint_module` to use as the application If not
specified, defaults to "root_agent".
|
`requirements_file` |
`str`
Optional. The path to the requirements file, relative to the source root. If not specified, defaults to "requirements.txt". |

## Methods

### PythonSpec

`PythonSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for running a Python application from source.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitor.ModelMonitoringTarget -->

# Class ModelMonitoringTarget (1.134.0)

`ModelMonitoringTarget(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The monitoring target refers to the entity that is subject to analysis. e.g. Vertex AI Model version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`vertex_model` |
Model in Vertex AI Model Registry. This field is a member of `oneof` _ `source` .
|

## Classes

### VertexModelSource

`VertexModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model in Vertex AI Model Registry.

## Methods

### ModelMonitoringTarget

`ModelMonitoringTarget(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The monitoring target refers to the entity that is subject to analysis. e.g. Vertex AI Model version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntime.HealthState -->

# Class HealthState (1.134.0)

`HealthState(value)`


The substate of the NotebookRuntime to display health information.

## Enums |
|
|---|---|
Name |
Description |
`HEALTH_STATE_UNSPECIFIED` |
Unspecified health state. |
`HEALTHY` |
NotebookRuntime is in healthy state. Applies to ACTIVE state. |
`UNHEALTHY` |
NotebookRuntime is in unhealthy state. Applies to ACTIVE state. |

## Methods

### HealthState

`HealthState(value)`


The substate of the NotebookRuntime to display health information.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.OpenFineTuningPipelines -->

# Class OpenFineTuningPipelines (1.134.0)

`OpenFineTuningPipelines(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open fine tuning pipelines.

## Attribute |
|
|---|---|
Name |
Description |
`fine_tuning_pipelines` |
`MutableSequence[`
Required. Regional resource references to fine tuning pipelines. |

## Methods

### OpenFineTuningPipelines

`OpenFineTuningPipelines(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open fine tuning pipelines.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMetadataStoreRequest -->

# Class CreateMetadataStoreRequest (1.134.0)

`CreateMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataStore.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location where the MetadataStore should be created. Format: `projects/{project}/locations/{location}/`
|
`metadata_store` |
Required. The MetadataStore to create. |
`metadata_store_id` |
`str`
The {metadatastore} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
If not provided, the MetadataStore's ID will be a UUID
generated by the service. Must be 4-128 characters in
length. Valid characters are `/` a-z][0-9]`-/` . Must be
unique across all MetadataStores in the parent Location.
(Otherwise the request will fail with ALREADY_EXISTS, or
PERMISSION_DENIED if the caller can't view the preexisting
MetadataStore.)
|

## Methods

### CreateMetadataStoreRequest

`CreateMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataStore.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadModelOperationMetadata -->

# Class UploadModelOperationMetadata (1.134.0)

```
UploadModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ModelService.UploadModel operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### UploadModelOperationMetadata

```
UploadModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ModelService.UploadModel operation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeExecutionsMetadata -->

# Class PurgeExecutionsMetadata (1.134.0)

`PurgeExecutionsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeExecutions.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for purging Executions. |

## Methods

### PurgeExecutionsMetadata

`PurgeExecutionsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeExecutions.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateExecutionRequest -->

# Class CreateExecutionRequest (1.134.0)

`CreateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateExecution.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Execution should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`execution` |
Required. The Execution to create. |
`execution_id` |
`str`
The {execution} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
If not provided, the Execution's ID will be a UUID generated
by the service. Must be 4-128 characters in length. Valid
characters are `/` a-z][0-9]`-/` . Must be unique across all
Executions in the parent MetadataStore. (Otherwise the
request will fail with ALREADY_EXISTS, or PERMISSION_DENIED
if the caller can't view the preexisting Execution.)
|

## Methods

### CreateExecutionRequest

`CreateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateExecution.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RawPredictRequest -->

# Class RawPredictRequest (1.134.0)

`RawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.RawPredict.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. A DeployedModel may have an upper limit on the number of instances it supports per request. When this limit it is exceeded for an AutoML model, the RawPredict method returns an error. When this limit is exceeded for a custom-trained model, the behavior varies depending on the model. You can specify the schema for each instance in the predict_schemata.instance_schema_uri field when you create a Model. This schema applies when you deploy the `Model` as a `DeployedModel`
to an Endpoint and
use the `RawPredict` method.
|

## Methods

### RawPredictRequest

`RawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.RawPredict.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolUseExample.ExtensionOperation -->

# Class ExtensionOperation (1.134.0)

`ExtensionOperation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Identifies one operation of the extension.

## Attributes |
|
|---|---|
Name |
Description |
`extension` |
`str`
Resource name of the extension. |
`operation_id` |
`str`
Required. Operation ID of the extension. |

## Methods

### ExtensionOperation

`ExtensionOperation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Identifies one operation of the extension.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListOptimalTrialsRequest -->

# Class ListOptimalTrialsRequest (1.134.0)

`ListOptimalTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListOptimalTrials.

## Attribute |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the Study that the optimal Trial belongs to. |

## Methods

### ListOptimalTrialsRequest

`ListOptimalTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListOptimalTrials.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedModelResponse -->

# Class MutateDeployedModelResponse (1.134.0)

`MutateDeployedModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.MutateDeployedModel.

## Attribute |
|
|---|---|
Name |
Description |
`deployed_model` |
The DeployedModel that's being mutated. |

## Methods

### MutateDeployedModelResponse

`MutateDeployedModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.MutateDeployedModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorRequest -->

# Class GetFeatureMonitorRequest (1.134.0)

`GetFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.GetFeatureMonitor.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureMonitor resource. |

## Methods

### GetFeatureMonitorRequest

`GetFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.GetFeatureMonitor.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DynamicRetrievalConfig -->

# Class DynamicRetrievalConfig (1.134.0)

`DynamicRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the options to customize dynamic retrieval.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`mode` |
The mode of the predictor to be used in dynamic retrieval. |
`dynamic_threshold` |
`float`
Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used. This field is a member of `oneof` _ `_dynamic_threshold` .
|

## Classes

### Mode

`Mode(value)`


The mode of the predictor to be used in dynamic retrieval.

## Methods

### DynamicRetrievalConfig

`DynamicRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the options to customize dynamic retrieval.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryRecallInstance -->

# Class TrajectoryRecallInstance (1.134.0)

`TrajectoryRecallInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryRecall instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`predicted_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for predicted tool call trajectory. This field is a member of `oneof` _ `_predicted_trajectory` .
|
`reference_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for reference tool call trajectory. This field is a member of `oneof` _ `_reference_trajectory` .
|

## Methods

### TrajectoryRecallInstance

`TrajectoryRecallInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryRecall instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseSummarizationQualityResult -->

# Class PairwiseSummarizationQualityResult (1.134.0)

```
PairwiseSummarizationQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`pairwise_choice` |
Output only. Pairwise summarization prediction choice. |
`explanation` |
`str`
Output only. Explanation for summarization quality score. |
`confidence` |
`float`
Output only. Confidence for summarization quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### PairwiseSummarizationQualityResult

```
PairwiseSummarizationQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.SourceCodeSpec.PythonSpec -->

# Class PythonSpec (1.134.0)

`PythonSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for running a Python application from source.

## Attributes |
|
|---|---|
Name |
Description |
`version` |
`str`
Optional. The version of Python to use. Support version includes 3.9, 3.10, 3.11, 3.12, 3.13. If not specified, default value is 3.10. |
`entrypoint_module` |
`str`
Optional. The Python module to load as the entrypoint, specified as a fully qualified module name. For example: path.to.agent. If not specified, defaults to "agent". The project root will be added to Python sys.path, allowing imports to be specified relative to the root. |
`entrypoint_object` |
`str`
Optional. The name of the callable object within the `entrypoint_module` to use as the application If not
specified, defaults to "root_agent".
|
`requirements_file` |
`str`
Optional. The path to the requirements file, relative to the source root. If not specified, defaults to "requirements.txt". |

## Methods

### PythonSpec

`PythonSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for running a Python application from source.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateDatasetOperationMetadata -->

# Class EvaluateDatasetOperationMetadata (1.134.0)

```
EvaluateDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Operation metadata for Dataset Evaluation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Generic operation metadata. |

## Methods

### EvaluateDatasetOperationMetadata

```
EvaluateDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Operation metadata for Dataset Evaluation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AugmentPromptRequest.Model -->

# Class Model (1.134.0)

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the backend deployed model.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Optional. The model that the user will send the augmented prompt for content generation. |
`model_version` |
`str`
Optional. The model version of the backend deployed model. |

## Methods

### Model

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the backend deployed model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient -->

# Class ModelGardenServiceClient (1.134.0)

```
ModelGardenServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.model_garden_service.transports.base.ModelGardenServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.model_garden_service.transports.base.ModelGardenServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The interface of Model Garden Service.

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
`ModelGardenServiceTransport` |
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

### ModelGardenServiceClient

```
ModelGardenServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.model_garden_service.transports.base.ModelGardenServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.model_garden_service.transports.base.ModelGardenServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the model garden service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ModelGardenServiceTransport,Callable[..., ModelGardenServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the ModelGardenServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### accept_publisher_model_eula

```
accept_publisher_model_eula(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.AcceptPublisherModelEulaRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
publisher_model: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.model_garden_service.PublisherModelEulaAcceptance
)
```


Accepts the EULA acceptance status of a publisher model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_accept_publisher_model_eula():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AcceptPublisherModelEulaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AcceptPublisherModelEulaRequest.html)(
parent="parent_value",
publisher_model="publisher_model_value",
)
# Make the request
response = client.[accept_publisher_model_eula](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_accept_publisher_model_eula)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelGardenService.AcceptPublisherModelEula. |
`parent` |
`str`
Required. The project requesting access for named model. The format is |
`publisher_model` |
`str`
Required. The name of the PublisherModel resource. Format: |
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
Response message for [ModelGardenService.UpdatePublisherModelEula][]. |

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

### check_publisher_model_eula_acceptance

```
check_publisher_model_eula_acceptance(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.CheckPublisherModelEulaAcceptanceRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
publisher_model: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.model_garden_service.PublisherModelEulaAcceptance
)
```


Checks the EULA acceptance status of a publisher model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_check_publisher_model_eula_acceptance():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CheckPublisherModelEulaAcceptanceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckPublisherModelEulaAcceptanceRequest.html)(
parent="parent_value",
publisher_model="publisher_model_value",
)
# Make the request
response = client.[check_publisher_model_eula_acceptance](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_check_publisher_model_eula_acceptance)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [ModelGardenService.CheckPublisherModelEula][]. |
`parent` |
`str`
Required. The project requesting access for named model. The format is |
`publisher_model` |
`str`
Required. The name of the PublisherModel resource. Format: |
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
Response message for [ModelGardenService.UpdatePublisherModelEula][]. |

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

### deploy

```
deploy(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.DeployRequest,
dict,
]
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
) -> google.api_core.operation.Operation
```


Deploys a model to a new endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_deploy():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeployRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest.html)(
publisher_model_name="publisher_model_name_value",
destination="destination_value",
)
# Make the request
operation = client.[deploy](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_deploy)(request=request)
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
The request object. Request message for ModelGardenService.Deploy. |
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

### deploy_publisher_model

```
deploy_publisher_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.DeployPublisherModelRequest,
dict,
]
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
) -> google.api_core.operation.Operation
```


Deploys publisher models.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_deploy_publisher_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeployPublisherModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployPublisherModelRequest.html)(
model="model_value",
destination="destination_value",
)
# Make the request
operation = client.[deploy_publisher_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_deploy_publisher_model)(request=request)
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
The request object. Request message for ModelGardenService.DeployPublisherModel. |
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

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### export_publisher_model

```
export_publisher_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.ExportPublisherModelRequest,
dict,
]
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
) -> google.api_core.operation.Operation
```


Exports a publisher model to a user provided Google Cloud Storage bucket.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_export_publisher_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
destination = aiplatform_v1beta1.[GcsDestination](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GcsDestination.html)()
destination.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[ExportPublisherModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportPublisherModelRequest.html)(
name="name_value",
destination=destination,
parent="parent_value",
)
# Make the request
operation = client.[export_publisher_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_export_publisher_model)(request=request)
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
The request object. Request message for ModelGardenService.ExportPublisherModel. |
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
`ModelGardenServiceClient` |
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
`ModelGardenServiceClient` |
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
`ModelGardenServiceClient` |
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

### get_publisher_model

```
get_publisher_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.GetPublisherModelRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.publisher_model.PublisherModel
```


Gets a Model Garden publisher model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_publisher_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetPublisherModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPublisherModelRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_publisher_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_get_publisher_model)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelGardenService.GetPublisherModel |
`name` |
`str`
Required. The name of the PublisherModel resource. Format: |
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
A Model Garden Publisher Model. |

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

### list_publisher_models

```
list_publisher_models(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
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
google.cloud.aiplatform_v1beta1.services.model_garden_service.pagers.ListPublisherModelsPager
)
```


Lists publisher models in Model Garden.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_publisher_models():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListPublisherModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_publisher_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_list_publisher_models)(request=request)
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
The request object. Request message for ModelGardenService.ListPublisherModels. |
`parent` |
`str`
Required. The name of the Publisher from which to list the PublisherModels. Format: |
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
Response message for ModelGardenService.ListPublisherModels. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_publisher_model_path

`parse_publisher_model_path(path: str) -> typing.Dict[str, str]`


Parses a publisher_model path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### publisher_model_path

`publisher_model_path(publisher: str, model: str) -> str`


Returns a fully-qualified publisher_model string.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient -->

# Class DeploymentResourcePoolServiceClient (1.134.0)

```
DeploymentResourcePoolServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service that manages the DeploymentResourcePool resource.

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
`DeploymentResourcePoolServiceTransport` |
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

### DeploymentResourcePoolServiceClient

```
DeploymentResourcePoolServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the deployment resource pool service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,DeploymentResourcePoolServiceTransport,Callable[..., DeploymentResourcePoolServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the DeploymentResourcePoolServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_deployment_resource_pool

```
create_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.CreateDeploymentResourcePoolRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
deployment_resource_pool: typing.Optional[
google.cloud.aiplatform_v1.types.deployment_resource_pool.DeploymentResourcePool
] = None,
deployment_resource_pool_id: typing.Optional[str] = None,
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


Create a DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
deployment_resource_pool = aiplatform_v1.[DeploymentResourcePool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeploymentResourcePool.html)()
deployment_resource_pool.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[CreateDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDeploymentResourcePoolRequest.html)(
parent="parent_value",
deployment_resource_pool=deployment_resource_pool,
deployment_resource_pool_id="deployment_resource_pool_id_value",
)
# Make the request
operation = client.[create_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_create_deployment_resource_pool)(request=request)
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
The request object. Request message for CreateDeploymentResourcePool method. |
`parent` |
`str`
Required. The parent location resource where this DeploymentResourcePool will be created. Format: |
`deployment_resource_pool` |
Required. The DeploymentResourcePool to create. This corresponds to the |
`deployment_resource_pool_id` |
`str`
Required. The ID to use for the DeploymentResourcePool, which will become the final component of the DeploymentResourcePool's resource name. The maximum length is 63 characters, and valid characters are |
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

### delete_deployment_resource_pool

```
delete_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.DeleteDeploymentResourcePoolRequest,
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


Delete a DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDeploymentResourcePoolRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_delete_deployment_resource_pool)(request=request)
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
The request object. Request message for DeleteDeploymentResourcePool method. |
`name` |
`str`
Required. The name of the DeploymentResourcePool to delete. Format: |
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
`DeploymentResourcePoolServiceClient` |
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
`DeploymentResourcePoolServiceClient` |
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
`DeploymentResourcePoolServiceClient` |
The constructed client. |

### get_deployment_resource_pool

```
get_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.GetDeploymentResourcePoolRequest,
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
) -> google.cloud.aiplatform_v1.types.deployment_resource_pool.DeploymentResourcePool
```


Get a DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetDeploymentResourcePoolRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_get_deployment_resource_pool)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GetDeploymentResourcePool method. |
`name` |
`str`
Required. The name of the DeploymentResourcePool to retrieve. Format: |
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
A description of resources that can be shared by multiple DeployedModels, whose underlying specification consists of a DedicatedResources. |

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

### list_deployment_resource_pools

```
list_deployment_resource_pools(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
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
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsPager
)
```


List DeploymentResourcePools in a location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_deployment_resource_pools():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListDeploymentResourcePoolsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_deployment_resource_pools](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_list_deployment_resource_pools)(request=request)
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
The request object. Request message for ListDeploymentResourcePools method. |
`parent` |
`str`
Required. The parent Location which owns this collection of DeploymentResourcePools. Format: |
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
Response message for ListDeploymentResourcePools method. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_deployment_resource_pool_path

`parse_deployment_resource_pool_path(path: str) -> typing.Dict[str, str]`


Parses a deployment_resource_pool path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### query_deployed_models

```
query_deployed_models(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
dict,
]
] = None,
*,
deployment_resource_pool: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsPager
)
```


List DeployedModels that have been deployed on this DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_query_deployed_models():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[QueryDeployedModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsRequest.html)(
deployment_resource_pool="deployment_resource_pool_value",
)
# Make the request
page_result = client.[query_deployed_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_query_deployed_models)(request=request)
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
The request object. Request message for QueryDeployedModels method. |
`deployment_resource_pool` |
`str`
Required. The name of the target DeploymentResourcePool to query. Format: |
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
Response message for QueryDeployedModels method. Iterating over this object will yield results and resolve additional pages automatically. |

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

### update_deployment_resource_pool

```
update_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.UpdateDeploymentResourcePoolRequest,
dict,
]
] = None,
*,
deployment_resource_pool: typing.Optional[
google.cloud.aiplatform_v1.types.deployment_resource_pool.DeploymentResourcePool
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


Update a DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
deployment_resource_pool = aiplatform_v1.[DeploymentResourcePool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeploymentResourcePool.html)()
deployment_resource_pool.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[UpdateDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateDeploymentResourcePoolRequest.html)(
deployment_resource_pool=deployment_resource_pool,
)
# Make the request
operation = client.[update_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_update_deployment_resource_pool)(request=request)
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
The request object. Request message for UpdateDeploymentResourcePool method. |
`deployment_resource_pool` |
Required. The DeploymentResourcePool to update. The DeploymentResourcePool's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The list of fields to update. This corresponds to the |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient -->

# Class SessionServiceClient (1.134.0)

```
SessionServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.session_service.transports.base.SessionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.session_service.transports.base.SessionServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The service that manages Vertex Session related resources.

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
`SessionServiceTransport` |
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

### SessionServiceClient

```
SessionServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.session_service.transports.base.SessionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.session_service.transports.base.SessionServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the session service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,SessionServiceTransport,Callable[..., SessionServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the SessionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### append_event

```
append_event(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.AppendEventRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
event: typing.Optional[
google.cloud.aiplatform_v1beta1.types.session.SessionEvent
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.session_service.AppendEventResponse
```


Appends an event to a given session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_append_event():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
event = aiplatform_v1beta1.[SessionEvent](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SessionEvent.html)()
event.author = "author_value"
event.invocation_id = "invocation_id_value"
request = aiplatform_v1beta1.[AppendEventRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AppendEventRequest.html)(
name="name_value",
event=event,
)
# Make the request
response = client.[append_event](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_append_event)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for SessionService.AppendEvent. |
`name` |
`str`
Required. The resource name of the session to append event to. Format: |
`event` |
Required. The event to append to the session. This corresponds to the |
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
Response message for SessionService.AppendEvent. |

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

### create_session

```
create_session(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.CreateSessionRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
session: typing.Optional[
google.cloud.aiplatform_v1beta1.types.session.Session
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


Creates a new xref_Session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
session = aiplatform_v1beta1.[Session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Session.html)()
session.user_id = "user_id_value"
request = aiplatform_v1beta1.[CreateSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSessionRequest.html)(
parent="parent_value",
session=session,
)
# Make the request
operation = client.[create_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_create_session)(request=request)
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
The request object. Request message for SessionService.CreateSession. |
`parent` |
`str`
Required. The resource name of the location to create the session in. Format: |
`session` |
Required. The session to create. This corresponds to the |
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
An object representing a long-running operation. The result type for the operation will be Session A session contains a set of actions between users and Vertex agents. |

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

### delete_session

```
delete_session(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.DeleteSessionRequest,
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


Deletes details of the specific xref_Session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSessionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_delete_session)(request=request)
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
The request object. Request message for SessionService.DeleteSession. |
`name` |
`str`
Required. The resource name of the session. Format: |
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
`SessionServiceClient` |
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
`SessionServiceClient` |
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
`SessionServiceClient` |
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

### get_session

```
get_session(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.GetSessionRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.session.Session
```


Gets details of the specific xref_Session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetSessionRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_get_session)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for SessionService.GetSession. |
`name` |
`str`
Required. The resource name of the session. Format: |
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
A session contains a set of actions between users and Vertex agents. |

### list_events

```
list_events(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.ListEventsRequest,
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
) -> google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListEventsPager
```


Lists xref_Events in a given session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_events():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListEventsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_events](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_list_events)(request=request)
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
The request object. Request message for SessionService.ListEvents. |
`parent` |
`str`
Required. The resource name of the session to list events from. Format: |
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
Response message for SessionService.ListEvents. Iterating over this object will yield results and resolve additional pages automatically. |

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

### list_sessions

```
list_sessions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsRequest,
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
) -> google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListSessionsPager
```


Lists xref_Sessions in a given reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_sessions():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListSessionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_sessions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_list_sessions)(request=request)
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
The request object. Request message for SessionService.ListSessions. |
`parent` |
`str`
Required. The resource name of the location to list sessions from. Format: |
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
Response message for SessionService.ListSessions. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### parse_session_event_path

`parse_session_event_path(path: str) -> typing.Dict[str, str]`


Parses a session_event path into its component segments.

### parse_session_path

`parse_session_path(path: str) -> typing.Dict[str, str]`


Parses a session path into its component segments.

### reasoning_engine_path

`reasoning_engine_path(project: str, location: str, reasoning_engine: str) -> str`


Returns a fully-qualified reasoning_engine string.

### session_event_path

```
session_event_path(
project: str, location: str, reasoning_engine: str, session: str, event: str
) -> str
```


Returns a fully-qualified session_event string.

### session_path

```
session_path(
project: str, location: str, reasoning_engine: str, session: str
) -> str
```


Returns a fully-qualified session string.

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

### update_session

```
update_session(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.UpdateSessionRequest,
dict,
]
] = None,
*,
session: typing.Optional[
google.cloud.aiplatform_v1beta1.types.session.Session
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
) -> google.cloud.aiplatform_v1beta1.types.session.Session
```


Updates the specific xref_Session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
session = aiplatform_v1beta1.[Session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Session.html)()
session.user_id = "user_id_value"
request = aiplatform_v1beta1.[UpdateSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateSessionRequest.html)(
session=session,
)
# Make the request
response = client.[update_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_update_session)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for SessionService.UpdateSession. |
`session` |
Required. The session to update. Format: |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Field mask is used to control which fields get updated. If the mask is not present, all fields will be updated. This corresponds to the |
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
A session contains a set of actions between users and Vertex agents. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient -->

# Class MemoryBankServiceClient (1.134.0)

```
MemoryBankServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.memory_bank_service.transports.base.MemoryBankServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.memory_bank_service.transports.base.MemoryBankServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing memories for LLM applications.

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
`MemoryBankServiceTransport` |
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

### MemoryBankServiceClient

```
MemoryBankServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.memory_bank_service.transports.base.MemoryBankServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.memory_bank_service.transports.base.MemoryBankServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the memory bank service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MemoryBankServiceTransport,Callable[..., MemoryBankServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MemoryBankServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_memory

```
create_memory(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.CreateMemoryRequest,
dict,
]
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
) -> google.api_core.operation.Operation
```


Create a Memory.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
memory = aiplatform_v1beta1.[Memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Memory.html)()
memory.fact = "fact_value"
request = aiplatform_v1beta1.[CreateMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMemoryRequest.html)(
parent="parent_value",
memory=memory,
)
# Make the request
operation = client.[create_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_create_memory)(request=request)
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
The request object. Request message for MemoryBankService.CreateMemory. |
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

### delete_memory

```
delete_memory(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.DeleteMemoryRequest,
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


Delete a Memory.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteMemoryRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_delete_memory)(request=request)
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
The request object. Request message for MemoryBankService.DeleteMemory. |
`name` |
`str`
Required. The resource name of the Memory to delete. Format: |
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
`MemoryBankServiceClient` |
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
`MemoryBankServiceClient` |
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
`MemoryBankServiceClient` |
The constructed client. |

### generate_memories

```
generate_memories(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.GenerateMemoriesRequest,
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
) -> google.api_core.operation.Operation
```


Generate memories.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_generate_memories():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
vertex_session_source = aiplatform_v1beta1.[VertexSessionSource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.VertexSessionSource.html)()
vertex_session_source.session = "session_value"
request = aiplatform_v1beta1.[GenerateMemoriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.html)(
vertex_session_source=vertex_session_source,
parent="parent_value",
)
# Make the request
operation = client.[generate_memories](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_generate_memories)(request=request)
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
The request object. Request message for MemoryBankService.GenerateMemories. |
`parent` |
`str`
Required. The resource name of the ReasoningEngine to generate memories for. Format: |
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

### get_memory

```
get_memory(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.GetMemoryRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.memory_bank.Memory
```


Get a Memory.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetMemoryRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_get_memory)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MemoryBankService.GetMemory. |
`name` |
`str`
Required. The resource name of the Memory. Format: |
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
A memory. |

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

### list_memories

```
list_memories(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesRequest,
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
google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers.ListMemoriesPager
)
```


List Memories.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_memories():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListMemoriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_memories](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_list_memories)(request=request)
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
The request object. Request message for MemoryBankService.ListMemories. |
`parent` |
`str`
Required. The resource name of the ReasoningEngine to list the Memories under. Format: |
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
Response message for MemoryBankService.ListMemories. Iterating over this object will yield results and resolve additional pages automatically. |

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

### memory_path

`memory_path(project: str, location: str, reasoning_engine: str, memory: str) -> str`


Returns a fully-qualified memory string.

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

### parse_memory_path

`parse_memory_path(path: str) -> typing.Dict[str, str]`


Parses a memory path into its component segments.

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### parse_session_path

`parse_session_path(path: str) -> typing.Dict[str, str]`


Parses a session path into its component segments.

### reasoning_engine_path

`reasoning_engine_path(project: str, location: str, reasoning_engine: str) -> str`


Returns a fully-qualified reasoning_engine string.

### retrieve_memories

```
retrieve_memories(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.RetrieveMemoriesRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.memory_bank_service.RetrieveMemoriesResponse
```


Retrieve memories.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_retrieve_memories():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
similarity_search_params = aiplatform_v1beta1.[SimilaritySearchParams](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest.SimilaritySearchParams.html)()
similarity_search_params.search_query = "search_query_value"
request = aiplatform_v1beta1.[RetrieveMemoriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest.html)(
similarity_search_params=similarity_search_params,
parent="parent_value",
)
# Make the request
response = client.[retrieve_memories](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_retrieve_memories)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MemoryBankService.RetrieveMemories. |
`parent` |
`str`
Required. The resource name of the ReasoningEngine to retrieve memories from. Format: |
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
Response message for MemoryBankService.RetrieveMemories. |

### session_path

```
session_path(
project: str, location: str, reasoning_engine: str, session: str
) -> str
```


Returns a fully-qualified session string.

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

### update_memory

```
update_memory(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.UpdateMemoryRequest,
dict,
]
] = None,
*,
memory: typing.Optional[
google.cloud.aiplatform_v1beta1.types.memory_bank.Memory
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


Update a Memory.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
memory = aiplatform_v1beta1.[Memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Memory.html)()
memory.fact = "fact_value"
request = aiplatform_v1beta1.[UpdateMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateMemoryRequest.html)(
memory=memory,
)
# Make the request
operation = client.[update_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_update_memory)(request=request)
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
The request object. Request message for MemoryBankService.UpdateMemory. |
`memory` |
Required. The Memory which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to update. Supported fields: :: * |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RawPredictRequest -->

# Class RawPredictRequest (1.134.0)

`RawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.RawPredict.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. A DeployedModel may have an upper limit on the number of instances it supports per request. When this limit it is exceeded for an AutoML model, the RawPredict method returns an error. When this limit is exceeded for a custom-trained model, the behavior varies depending on the model. You can specify the schema for each instance in the predict_schemata.instance_schema_uri field when you create a Model. This schema applies when you deploy the `Model` as a `DeployedModel`
to an Endpoint
and use the `RawPredict` method.
|

## Methods

### RawPredictRequest

`RawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.RawPredict.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CitationMetadata -->

# Class CitationMetadata (1.134.0)

`CitationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of source attributions for a piece of content.

## Attribute |
|
|---|---|
Name |
Description |
`citations` |
`MutableSequence[google.cloud.aiplatform_v1beta1.types.Citation]`
Output only. List of citations. |

## Methods

### CitationMetadata

`CitationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of source attributions for a piece of content.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKVMatchSpec -->

# Class ToolParameterKVMatchSpec (1.134.0)

`ToolParameterKVMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool parameter key value match metric.

## Attribute |
|
|---|---|
Name |
Description |
`use_strict_string_match` |
`bool`
Optional. Whether to use STRICT string match on parameter values. |

## Methods

### ToolParameterKVMatchSpec

`ToolParameterKVMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool parameter key value match metric.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelNasJobRequest -->

# Class CancelNasJobRequest (1.134.0)

`CancelNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CancelNasJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NasJob to cancel. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}`
|

## Methods

### CancelNasJobRequest

`CancelNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CancelNasJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetEndpointRequest -->

# Class GetEndpointRequest (1.134.0)

`GetEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.GetEndpoint

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Endpoint resource. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|

## Methods

### GetEndpointRequest

`GetEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.GetEndpoint

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DynamicRetrievalConfig -->

# Class DynamicRetrievalConfig (1.134.0)

`DynamicRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the options to customize dynamic retrieval.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`mode` |
The mode of the predictor to be used in dynamic retrieval. |
`dynamic_threshold` |
`float`
Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used. This field is a member of `oneof` _ `_dynamic_threshold` .
|

## Classes

### Mode

`Mode(value)`


The mode of the predictor to be used in dynamic retrieval.

## Methods

### DynamicRetrievalConfig

`DynamicRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the options to customize dynamic retrieval.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagManagedDbConfig -->

# Class RagManagedDbConfig (1.134.0)

`RagManagedDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration message for RagManagedDb used by RagEngine.

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
`scaled` |
Sets the RagManagedDb to the Scaled tier. This field is a member of `oneof` _ `tier` .
|
`basic` |
Sets the RagManagedDb to the Basic tier. This field is a member of `oneof` _ `tier` .
|
`unprovisioned` |
Sets the RagManagedDb to the Unprovisioned tier. This field is a member of `oneof` _ `tier` .
|

## Classes

### Basic

`Basic(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Basic tier is a cost-effective and low compute tier suitable for the following cases:

- Experimenting with RagManagedDb.
- Small data size.
- Latency insensitive workload.
- Only using RAG Engine with external vector DBs.

NOTE: This is the default tier if not explicitly chosen.

### Scaled

`Scaled(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

### Unprovisioned

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

## Methods

### RagManagedDbConfig

`RagManagedDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration message for RagManagedDb used by RagEngine.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolConfig -->

# Class ToolConfig (1.134.0)

`ToolConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool config. This config is shared for all tools provided in the request.

## Attributes |
|
|---|---|
Name |
Description |
`function_calling_config` |
Optional. Function calling config. |
`retrieval_config` |
Optional. Retrieval config. |

## Methods

### ToolConfig

`ToolConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool config. This config is shared for all tools provided in the request.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssembleDataResponse -->

# Class AssembleDataResponse (1.134.0)

`AssembleDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.AssembleData.

## Attribute |
|
|---|---|
Name |
Description |
`bigquery_destination` |
`str`
Destination BigQuery table path containing the assembled data as a single column. |

## Methods

### AssembleDataResponse

`AssembleDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.AssembleData.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadIndexDatapointsResponse -->

# Class ReadIndexDatapointsResponse (1.134.0)

`ReadIndexDatapointsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The response message for MatchService.ReadIndexDatapoints.

## Attribute |
|
|---|---|
Name |
Description |
`datapoints` |
`MutableSequence[`
The result list of datapoints. |

## Methods

### ReadIndexDatapointsResponse

`ReadIndexDatapointsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The response message for MatchService.ReadIndexDatapoints.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Execution.State -->

# Class State (1.134.0)

`State(value)`


Describes the state of the Execution.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Unspecified Execution state |
`NEW` |
The Execution is new |
`RUNNING` |
The Execution is running |
`COMPLETE` |
The Execution has finished running |
`FAILED` |
The Execution has failed |
`CACHED` |
The Execution completed through Cache hit. |
`CANCELLED` |
The Execution was cancelled. |

## Methods

### State

`State(value)`


Describes the state of the Execution.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesResponse -->

# Class BatchCreateFeaturesResponse (1.134.0)

`BatchCreateFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.BatchCreateFeatures.

## Attribute |
|
|---|---|
Name |
Description |
`features` |
`MutableSequence[`
The Features created. |

## Methods

### BatchCreateFeaturesResponse

`BatchCreateFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.BatchCreateFeatures.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteModelRequest -->

# Class DeleteModelRequest (1.134.0)

`DeleteModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.DeleteModel.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Model resource to be deleted. Format: `projects/{project}/locations/{location}/models/{model}`
|

## Methods

### DeleteModelRequest

`DeleteModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.DeleteModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ServiceAccountSpec -->

# Class ServiceAccountSpec (1.134.0)

`ServiceAccountSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the use of custom service account to run the workloads.

## Attributes |
|
|---|---|
Name |
Description |
`enable_custom_service_account` |
`bool`
Required. If true, custom user-managed service account is enforced to run any workloads (for example, Vertex Jobs) on the resource. Otherwise, uses the `Vertex AI Custom Code Service Agent |
`service_account` |
`str`
Optional. Required when all below conditions are met - `enable_custom_service_account` is true;
- any runtime is specified via `ResourceRuntimeSpec` on
creation time, for example, Ray
The users must have `iam.serviceAccounts.actAs` permission
on this service account and then the specified runtime
containers will run as it.
Do not set this field if you want to submit jobs using
custom service account to this PersistentResource after
creation, but only specify the `service_account` inside
the job.
|

## Methods

### ServiceAccountSpec

`ServiceAccountSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the use of custom service account to run the workloads.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GeminiTemplateConfig -->

# Class GeminiTemplateConfig (1.134.0)

`GeminiTemplateConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Template configuration to create Gemini examples from a multimodal dataset.

## Attributes |
|
|---|---|
Name |
Description |
`gemini_example` |
Required. The template that will be used for assembling the request to use for downstream applications. |
`field_mapping` |
`MutableMapping[str, str]`
Required. Map of template parameters to the columns in the dataset table. |

## Classes

### FieldMappingEntry

`FieldMappingEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### GeminiTemplateConfig

`GeminiTemplateConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Template configuration to create Gemini examples from a multimodal dataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureViewRequest -->

# Class CreateFeatureViewRequest (1.134.0)

`CreateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.CreateFeatureView.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureOnlineStore to create FeatureViews. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}`
|
`feature_view` |
Required. The FeatureView to create. |
`feature_view_id` |
`str`
Required. The ID to use for the FeatureView, which will become the final component of the FeatureView's resource name. This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within a FeatureOnlineStore.
|
`run_sync_immediately` |
`bool`
Immutable. If set to true, one on demand sync will be run immediately, regardless whether the FeatureView.sync_config is configured or not. |

## Methods

### CreateFeatureViewRequest

`CreateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.CreateFeatureView.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service -->

# Package evaluation_service (1.134.0)

API documentation for `aiplatform_v1.services.evaluation_service`

package.

## Classes

[EvaluationServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service.EvaluationServiceAsyncClient)

Vertex AI Online Evaluation Service.

[EvaluationServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service.EvaluationServiceClient)

Vertex AI Online Evaluation Service.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntime.HealthState -->

# Class HealthState (1.134.0)

`HealthState(value)`


The substate of the NotebookRuntime to display health information.

## Enums |
|
|---|---|
Name |
Description |
`HEALTH_STATE_UNSPECIFIED` |
Unspecified health state. |
`HEALTHY` |
NotebookRuntime is in healthy state. Applies to ACTIVE state. |
`UNHEALTHY` |
NotebookRuntime is in unhealthy state. Applies to ACTIVE state. |

## Methods

### HealthState

`HealthState(value)`


The substate of the NotebookRuntime to display health information.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadModelOperationMetadata -->

# Class UploadModelOperationMetadata (1.134.0)

```
UploadModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ModelService.UploadModel operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### UploadModelOperationMetadata

```
UploadModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ModelService.UploadModel operation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetScheduleRequest -->

# Class GetScheduleRequest (1.134.0)

`GetScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.GetSchedule.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|

## Methods

### GetScheduleRequest

`GetScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.GetSchedule.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice.SliceSpec.Range -->

# Class Range (1.134.0)

`Range(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A range of values for slice(s). `low`

is inclusive, `high`

is
exclusive.

## Attributes |
|
|---|---|
Name |
Description |
`low` |
`float`
Inclusive low value for the range. |
`high` |
`float`
Exclusive high value for the range. |

## Methods

### Range

`Range(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A range of values for slice(s). `low`

is inclusive, `high`

is
exclusive.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DestinationFeatureSetting -->

# Class DestinationFeatureSetting (1.134.0)

`DestinationFeatureSetting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`feature_id` |
`str`
Required. The ID of the Feature to apply the setting to. |
`destination_field` |
`str`
Specify the field name in the export destination. If not specified, Feature ID is used. |

## Methods

### DestinationFeatureSetting

`DestinationFeatureSetting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteIndexRequest -->

# Class DeleteIndexRequest (1.134.0)

`DeleteIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.DeleteIndex.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Index resource to be deleted. Format: `projects/{project}/locations/{location}/indexes/{index}`
|

## Methods

### DeleteIndexRequest

`DeleteIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.DeleteIndex.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SampleConfig.SampleStrategy -->

# Class SampleStrategy (1.134.0)

`SampleStrategy(value)`


Sample strategy decides which subset of DataItems should be selected for human labeling in every batch.

## Enums |
|
|---|---|
Name |
Description |
`SAMPLE_STRATEGY_UNSPECIFIED` |
Default will be treated as UNCERTAINTY. |
`UNCERTAINTY` |
Sample the most uncertain data to label. |

## Methods

### SampleStrategy

`SampleStrategy(value)`


Sample strategy decides which subset of DataItems should be selected for human labeling in every batch.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.feature_online_store_admin_service.pagers`

module.

## Classes

[ListFeatureOnlineStoresAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresAsyncPager)

```
ListFeatureOnlineStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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


A pager for iterating through `list_feature_online_stores`

requests.

This class thinly wraps an initial
[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_online_stores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureOnlineStores`

requests and continue to iterate
through the `feature_online_stores`

field on the
corresponding responses.

All the usual [ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureOnlineStoresPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresPager)

```
ListFeatureOnlineStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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


A pager for iterating through `list_feature_online_stores`

requests.

This class thinly wraps an initial
[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_online_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureOnlineStores`

requests and continue to iterate
through the `feature_online_stores`

field on the
corresponding responses.

All the usual [ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewSyncsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsAsyncPager)

```
ListFeatureViewSyncsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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


A pager for iterating through `list_feature_view_syncs`

requests.

This class thinly wraps an initial
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_view_syncs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureViewSyncs`

requests and continue to iterate
through the `feature_view_syncs`

field on the
corresponding responses.

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewSyncsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsPager)

```
ListFeatureViewSyncsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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


A pager for iterating through `list_feature_view_syncs`

requests.

This class thinly wraps an initial
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_view_syncs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureViewSyncs`

requests and continue to iterate
through the `feature_view_syncs`

field on the
corresponding responses.

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewsAsyncPager)

```
ListFeatureViewsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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


A pager for iterating through `list_feature_views`

requests.

This class thinly wraps an initial
[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_views`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureViews`

requests and continue to iterate
through the `feature_views`

field on the
corresponding responses.

All the usual [ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewsPager)

```
ListFeatureViewsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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


A pager for iterating through `list_feature_views`

requests.

This class thinly wraps an initial
[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_views`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureViews`

requests and continue to iterate
through the `feature_views`

field on the
corresponding responses.

All the usual [ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model -->

# Class Model (1.134.0)

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A trained machine learning Model.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The resource name of the Model. |
`version_id` |
`str`
Output only. Immutable. The version ID of the model. A new version is committed when a new model version is uploaded or trained under an existing model id. It is an auto-incrementing decimal number in string representation. |
`version_aliases` |
`MutableSequence[str]`
User provided version aliases so that a model version can be referenced via alias (i.e. `projects/{project}/locations/{location}/models/{model_id}@{version_alias}`
instead of auto-generated version id (i.e.
`projects/{project}/locations/{location}/models/{model_id}@{version_id})` .
The format is `a-z][a-zA-Z0-9-]` {0,126}[a-z0-9] to
distinguish from version_id. A default version alias will be
created for the first version of the model, and there must
be exactly one default version alias for a model.
|
`version_create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this version was created. |
`version_update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this version was most recently updated. |
`display_name` |
`str`
Required. The display name of the Model. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Model. |
`version_description` |
`str`
The description of this version. |
`default_checkpoint_id` |
`str`
The default checkpoint id of a model version. |
`predict_schemata` |
The schemata that describe formats of the Model's predictions and explanations as given and returned via PredictionService.Predict and PredictionService.Explain. |
`metadata_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Model, that is specific to it. Unset if the Model does not have any additional information. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metadata` |
`google.protobuf.struct_pb2.Value`
Immutable. An additional information about the Model; the schema of the metadata can be found in metadata_schema. Unset if the Model does not have any additional information. |
`supported_export_formats` |
`MutableSequence[`
Output only. The formats in which this Model may be exported. If empty, this Model is not available for export. |
`training_pipeline` |
`str`
Output only. The resource name of the TrainingPipeline that uploaded this Model, if any. |
`container_spec` |
Input only. The specification of the container that is to be used when deploying this Model. The specification is ingested upon ModelService.UploadModel, and all binaries it contains are copied and stored internally by Vertex AI. Not required for AutoML Models. |
`artifact_uri` |
`str`
Immutable. The path to the directory containing the Model artifact and any of its supporting files. Not required for AutoML Models. |
`supported_deployment_resources_types` |
`MutableSequence[`
Output only. When this Model is deployed, its prediction resources are described by the `prediction_resources`
field of the
Endpoint.deployed_models
object. Because not all Models support all resource
configuration types, the configuration types this Model
supports are listed here. If no configuration types are
listed, the Model cannot be deployed to an
Endpoint and
does not support online predictions
(PredictionService.Predict
or
PredictionService.Explain).
Such a Model can serve predictions by using a
BatchPredictionJob,
if it has at least one entry each in
supported_input_storage_formats
and
supported_output_storage_formats.
|
`supported_input_storage_formats` |
`MutableSequence[str]`
Output only. The formats this Model supports in BatchPredictionJob.input_config. If PredictSchemata.instance_schema_uri exists, the instances should be given as per that schema. The possible formats are: - `jsonl` The JSON Lines format, where each instance is a
single line. Uses
GcsSource.
- `csv` The CSV format, where each instance is a single
comma-separated line. The first line in the file is the
header, containing comma-separated field names. Uses
GcsSource.
- `tf-record` The TFRecord format, where each instance is
a single record in tfrecord syntax. Uses
GcsSource.
- `tf-record-gzip` Similar to `tf-record` , but the file
is gzipped. Uses
GcsSource.
- `bigquery` Each instance is a single row in BigQuery.
Uses
BigQuerySource.
- `file-list` Each line of the file is the location of an
instance to process, uses `gcs_source` field of the
InputConfig
object.
If this Model doesn't support any of these formats it means
it cannot be used with a
BatchPredictionJob.
However, if it has
supported_deployment_resources_types,
it could serve online predictions by using
PredictionService.Predict
or
PredictionService.Explain.
|
`supported_output_storage_formats` |
`MutableSequence[str]`
Output only. The formats this Model supports in BatchPredictionJob.output_config. If both PredictSchemata.instance_schema_uri and PredictSchemata.prediction_schema_uri exist, the predictions are returned together with their instances. In other words, the prediction has the original instance data first, followed by the actual prediction content (as per the schema). The possible formats are: - `jsonl` The JSON Lines format, where each prediction is
a single line. Uses
GcsDestination.
- `csv` The CSV format, where each prediction is a single
comma-separated line. The first line in the file is the
header, containing comma-separated field names. Uses
GcsDestination.
- `bigquery` Each prediction is a single row in a BigQuery
table, uses
BigQueryDestination
.
If this Model doesn't support any of these formats it means
it cannot be used with a
BatchPredictionJob.
However, if it has
supported_deployment_resources_types,
it could serve online predictions by using
PredictionService.Predict
or
PredictionService.Explain.
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Model was uploaded into Vertex AI. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Model was most recently updated. |
`deployed_models` |
`MutableSequence[`
Output only. The pointers to DeployedModels created from this Model. Note that Model could have been deployed to Endpoints in different Locations. |
`explanation_spec` |
The default explanation specification for this Model. The Model can be used for [requesting explanation][google.cloud.aiplatform.v1beta1.PredictionService.Explain] after being deployed if it is populated. The Model can be used for [batch explanation][google.cloud.aiplatform.v1beta1.BatchPredictionJob.generate_explanation] if it is populated. All fields of the explanation_spec can be overridden by explanation_spec of DeployModelRequest.deployed_model, or explanation_spec of BatchPredictionJob. If the default explanation specification is not set for this Model, this Model can still be used for [requesting explanation][google.cloud.aiplatform.v1beta1.PredictionService.Explain] by setting explanation_spec of DeployModelRequest.deployed_model and for [batch explanation][google.cloud.aiplatform.v1beta1.BatchPredictionJob.generate_explanation] by setting explanation_spec of BatchPredictionJob. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key spec for a Model. If set, this Model and all sub-resources of this Model will be secured by this key. |
`model_source_info` |
Output only. Source of a model. It can either be automl training pipeline, custom training pipeline, BigQuery ML, or saved and tuned from Genie or Model Garden. |
`original_model_info` |
Output only. If this Model is a copy of another Model, this contains info about the original. |
`metadata_artifact` |
`str`
Output only. The resource name of the Artifact that was created in MetadataStore when creating the Model. The Artifact resource name pattern is `projects/{project}/locations/{location}/metadataStores/{metadata_store}/artifacts/{artifact}` .
|
`base_model_source` |
Optional. User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`checkpoints` |
`MutableSequence[`
Optional. Output only. The checkpoints of the model. |

## Classes

### BaseModelSource

`BaseModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### DeploymentResourcesType

`DeploymentResourcesType(value)`


Identifies a type of Model's prediction resources.

### ExportFormat

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

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

### OriginalModelInfo

`OriginalModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the original Model if this Model is a copy.

## Methods

### Model

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A trained machine learning Model.
