---
merged_at: 2026-01-28T15:11:44.760775
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.TimestampTransformation -->

# Class TimestampTransformation (1.135.0)

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


## Attribute |
|
|---|---|
Name |
Description |
`time_format` |
`str`
The format in which that time field is expressed. The time_format must either be one of: - `unix-seconds`
- `unix-milliseconds`
- `unix-microseconds`
- `unix-nanoseconds`
(for respectively number of seconds, milliseconds,
microseconds and nanoseconds since start of the Unix epoch);
or be written in `strftime` syntax.
If time_format is not set, then the default format is RFC
3339 `date-time` format, where `time-offset` = `"Z"`
(e.g. 1985-04-12T23:20:50.52Z)
|

## Methods

### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluationSlice.Slice.SliceSpec.ConfigsEntry -->

# Class ConfigsEntry (1.135.0)

`ConfigsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ConfigsEntry

`ConfigsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeResponse -->

# Class StartNotebookRuntimeResponse (1.135.0)

```
StartNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.StartNotebookRuntime.

## Methods

### StartNotebookRuntimeResponse

```
StartNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.StartNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput.ModelMonitoringDataset.ModelMonitoringGcsSource.DataFormat -->

# Class DataFormat (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TextSentimentPredictionResult -->

# Class TextSentimentPredictionResult (1.135.0)

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

## Attribute |
|
|---|---|
Name |
Description |
`sentiment` |
`int`
The integer sentiment labels between 0 (inclusive) and sentimentMax label (inclusive), while 0 maps to the least positive sentiment and sentimentMax maps to the most positive one. The higher the score is, the more positive the sentiment in the text snippet is. Note: sentimentMax is an integer value between 1 (inclusive) and 10 (inclusive). |

## Methods

### TextSentimentPredictionResult

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

### TextSentimentPredictionResult

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCachedContentsRequest -->

# Class ListCachedContentsRequest (1.135.0)

`ListCachedContentsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request to list CachedContents.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent, which owns this collection of cached contents. |
`page_size` |
`int`
Optional. The maximum number of cached contents to return. The service may return fewer than this value. If unspecified, some default (under maximum) number of items will be returned. The maximum value is 1000; values above 1000 will be coerced to 1000. |
`page_token` |
`str`
Optional. A page token, received from a previous `ListCachedContents` call. Provide this to retrieve the
subsequent page.
When paginating, all other parameters provided to
`ListCachedContents` must match the call that provided the
page token.
|

## Methods

### ListCachedContentsRequest

`ListCachedContentsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request to list CachedContents.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExampleStore -->

# Class ExampleStore (1.135.0)

`ExampleStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an executable service to manage and retrieve examples.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. The resource name of the ExampleStore. This is a unique identifier. Format: projects/{project}/locations/{location}/exampleStores/{example_store} |
`display_name` |
`str`
Required. Display name of the ExampleStore. |
`description` |
`str`
Optional. Description of the ExampleStore. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ExampleStore was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ExampleStore was most recently updated. |
`example_store_config` |
Required. Example Store config. |

## Methods

### ExampleStore

`ExampleStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an executable service to manage and retrieve examples.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFeatureValuesRequest.SnapshotExport -->

# Class SnapshotExport (1.135.0)

`SnapshotExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting the latest Feature values of all entities of the EntityType between [start_time, snapshot_time].

## Attributes |
|
|---|---|
Name |
Description |
`snapshot_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Exports Feature values as of this timestamp. If not set, retrieve values as of now. Timestamp, if present, must not have higher than millisecond precision. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Excludes Feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in Feature Store. Timestamp, if present, must not have higher than millisecond precision. |

## Methods

### SnapshotExport

`SnapshotExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting the latest Feature values of all entities of the EntityType between [start_time, snapshot_time].

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoObjectTrackingPredictionResult -->

# Class VideoObjectTrackingPredictionResult (1.135.0)

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
The resource ID of the AnnotationSpec that had been identified. |
`display_name` |
`str`
The display name of the AnnotationSpec that had been identified. |
`time_segment_start` |
`google.protobuf.duration_pb2.Duration`
The beginning, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. |
`time_segment_end` |
`google.protobuf.duration_pb2.Duration`
The end, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. |
`confidence` |
`google.protobuf.wrappers_pb2.FloatValue`
The Model's confidence in correction of this prediction, higher value means higher confidence. |
`frames` |
`MutableSequence[`
All of the frames of the video in which a single object instance has been detected. The bounding boxes in the frames identify the same object. |

## Classes

### Frame

`Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.

## Methods

### VideoObjectTrackingPredictionResult

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

### VideoObjectTrackingPredictionResult

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringNotificationSpec.EmailConfig -->

# Class EmailConfig (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExample.SearchKeyGenerationMethod.LastEntry -->

# Class LastEntry (1.135.0)

`LastEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for using only the last entry of the conversation history as the search key.

## Methods

### LastEntry

`LastEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for using only the last entry of the conversation history as the search key.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CompleteTrialRequest -->

# Class CompleteTrialRequest (1.135.0)

`CompleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CompleteTrial.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|
`final_measurement` |
Optional. If provided, it will be used as the completed Trial's final_measurement; Otherwise, the service will auto-select a previously reported measurement as the final-measurement |
`trial_infeasible` |
`bool`
Optional. True if the Trial cannot be run with the given Parameter, and final_measurement will be ignored. |
`infeasible_reason` |
`str`
Optional. A human readable reason why the trial was infeasible. This should only be provided if `trial_infeasible` is true.
|

## Methods

### CompleteTrialRequest

`CompleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CompleteTrial.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel.SystemLabelsEntry -->

# Class SystemLabelsEntry (1.135.0)

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployModelRequest.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.135.0)

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### TrafficSplitEntry

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service -->

# Package vizier_service (1.135.0)

API documentation for `aiplatform_v1beta1.services.vizier_service`

package.

## Classes

[VizierServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient)

Vertex AI Vizier API.

Vertex AI Vizier is a service to solve blackbox optimization problems, such as tuning machine learning hyperparameters and searching over deep learning architectures.

[VizierServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient)

Vertex AI Vizier API.

Vertex AI Vizier is a service to solve blackbox optimization problems, such as tuning machine learning hyperparameters and searching over deep learning architectures.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers)

API documentation for `aiplatform_v1beta1.services.vizier_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service -->

# Package model_monitoring_service (1.135.0)

API documentation for `aiplatform_v1beta1.services.model_monitoring_service`

package.

## Classes

[ModelMonitoringServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceAsyncClient)

A service for creating and managing Vertex AI Model moitoring. This
includes `ModelMonitor`

resources, `ModelMonitoringJob`

resources.

[ModelMonitoringServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient)

A service for creating and managing Vertex AI Model moitoring. This
includes `ModelMonitor`

resources, `ModelMonitoringJob`

resources.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers)

API documentation for `aiplatform_v1beta1.services.model_monitoring_service.pagers`

module.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RolloutOptions -->

# Class RolloutOptions (1.135.0)

`RolloutOptions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for rolling deployments.

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
`max_unavailable_replicas` |
`int`
Absolute count of replicas allowed to be unavailable. This field is a member of `oneof` _ `max_unavailable` .
|
`max_unavailable_percentage` |
`int`
Percentage of replicas allowed to be unavailable. For autoscaling deployments, this refers to the target replica count. This field is a member of `oneof` _ `max_unavailable` .
|
`max_surge_replicas` |
`int`
Absolute count of allowed additional replicas. This field is a member of `oneof` _ `max_surge` .
|
`max_surge_percentage` |
`int`
Percentage of allowed additional replicas. For autoscaling deployments, this refers to the target replica count. This field is a member of `oneof` _ `max_surge` .
|
`previous_deployed_model` |
`str`
ID of the DeployedModel that this deployment should replace. |
`revision_number` |
`int`
Output only. Read-only. Revision number determines the relative priority of DeployedModels in the same rollout. The DeployedModel with the largest revision number specifies the intended state of the deployment. |

## Methods

### RolloutOptions

`RolloutOptions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for rolling deployments.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RougeInput -->

# Class RougeInput (1.135.0)

`RougeInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for rouge metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for rouge score metric. |
`instances` |
`MutableSequence[`
Required. Repeated rouge instances. |

## Methods

### RougeInput

`RougeInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for rouge metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RemoveContextChildrenResponse -->

# Class RemoveContextChildrenResponse (1.135.0)

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.

## Methods

### RemoveContextChildrenResponse

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomJob.WebAccessUrisEntry -->

# Class WebAccessUrisEntry (1.135.0)

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### WebAccessUrisEntry

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CometResult -->

# Class CometResult (1.135.0)

`CometResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet result - calculates the comet score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Comet score. Range depends on version. This field is a member of `oneof` _ `_score` .
|

## Methods

### CometResult

`CometResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet result - calculates the comet score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.Deploy.DeployMetadata.LabelsEntry -->

# Class LabelsEntry (1.135.0)

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployModelRequest.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.135.0)

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### TrafficSplitEntry

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskRerunConfig.Inputs.ArtifactsEntry -->

# Class ArtifactsEntry (1.135.0)

`ArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ArtifactsEntry

`ArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchMetricValue -->

# Class TrajectoryAnyOrderMatchMetricValue (1.135.0)

```
TrajectoryAnyOrderMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectoryAnyOrderMatch metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. TrajectoryAnyOrderMatch score. This field is a member of `oneof` _ `_score` .
|

## Methods

### TrajectoryAnyOrderMatchMetricValue

```
TrajectoryAnyOrderMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectoryAnyOrderMatch metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.ParametersEntry -->

# Class ParametersEntry (1.135.0)

`ParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ParametersEntry

`ParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesRequest -->

# Class ListEntityTypesRequest (1.135.0)

`ListEntityTypesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListEntityTypes.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Featurestore to list EntityTypes. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`filter` |
`str`
Lists the EntityTypes that match the filter expression. The following filters are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality as well as key
presence.
Examples:
- `create_time > \"2020-01-31T15:30:00.000000Z\" OR update_time > \"2020-01-31T15:30:00.000000Z\"`
--> EntityTypes created or updated after
2020-01-31T15:30:00.000000Z.
- `labels.active = yes AND labels.env = prod` -->
EntityTypes having both (active: yes) and (env: prod)
labels.
- `labels.env: *` --> Any EntityType which has a label
with 'env' as the key.
|
`page_size` |
`int`
The maximum number of EntityTypes to return. The service may return fewer than this value. If unspecified, at most 1000 EntityTypes will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeaturestoreService.ListEntityTypes call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeaturestoreService.ListEntityTypes must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `entity_type_id`
- `create_time`
- `update_time`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListEntityTypesRequest

`ListEntityTypesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListEntityTypes.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchInstance -->

# Class ExactMatchInstance (1.135.0)

`ExactMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for exact match instance.

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
Required. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|

## Methods

### ExactMatchInstance

`ExactMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for exact match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseMetricValue -->

# Class TrajectorySingleToolUseMetricValue (1.135.0)

```
TrajectorySingleToolUseMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectorySingleToolUse metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. TrajectorySingleToolUse score. This field is a member of `oneof` _ `_score` .
|

## Methods

### TrajectorySingleToolUseMetricValue

```
TrajectorySingleToolUseMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectorySingleToolUse metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsRequest -->

# Class ListCachedContentsRequest (1.135.0)

`ListCachedContentsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request to list CachedContents.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent, which owns this collection of cached contents. |
`page_size` |
`int`
Optional. The maximum number of cached contents to return. The service may return fewer than this value. If unspecified, some default (under maximum) number of items will be returned. The maximum value is 1000; values above 1000 will be coerced to 1000. |
`page_token` |
`str`
Optional. A page token, received from a previous `ListCachedContents` call. Provide this to retrieve the
subsequent page.
When paginating, all other parameters provided to
`ListCachedContents` must match the call that provided the
page token.
|

## Methods

### ListCachedContentsRequest

`ListCachedContentsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request to list CachedContents.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Presets.Query -->

# Class Query (1.135.0)

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off

## Enums |
|
|---|---|
Name |
Description |
`PRECISE` |
More precise neighbors as a trade-off against slower response. |
`FAST` |
Faster response as a trade-off against less precise neighbors. |

## Methods

### Query

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CoherenceInput -->

# Class CoherenceInput (1.135.0)

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for coherence score metric. |
`instance` |
Required. Coherence instance. |

## Methods

### CoherenceInput

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKVMatchMetricValue -->

# Class ToolParameterKVMatchMetricValue (1.135.0)

```
ToolParameterKVMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key value match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Tool parameter key value match score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ToolParameterKVMatchMetricValue

```
ToolParameterKVMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key value match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesRequest.SnapshotExport -->

# Class SnapshotExport (1.135.0)

`SnapshotExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting the latest Feature values of all entities of the EntityType between [start_time, snapshot_time].

## Attributes |
|
|---|---|
Name |
Description |
`snapshot_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Exports Feature values as of this timestamp. If not set, retrieve values as of now. Timestamp, if present, must not have higher than millisecond precision. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Excludes Feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in Feature Store. Timestamp, if present, must not have higher than millisecond precision. |

## Methods

### SnapshotExport

`SnapshotExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting the latest Feature values of all entities of the EntityType between [start_time, snapshot_time].

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult -->

# Class VideoObjectTrackingPredictionResult (1.135.0)

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
The resource ID of the AnnotationSpec that had been identified. |
`display_name` |
`str`
The display name of the AnnotationSpec that had been identified. |
`time_segment_start` |
`google.protobuf.duration_pb2.Duration`
The beginning, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. |
`time_segment_end` |
`google.protobuf.duration_pb2.Duration`
The end, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. |
`confidence` |
`google.protobuf.wrappers_pb2.FloatValue`
The Model's confidence in correction of this prediction, higher value means higher confidence. |
`frames` |
`MutableSequence[`
All of the frames of the video in which a single object instance has been detected. The bounding boxes in the frames identify the same object. |

## Classes

### Frame

`Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.

## Methods

### VideoObjectTrackingPredictionResult

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

### VideoObjectTrackingPredictionResult

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntime.RuntimeState -->

# Class RuntimeState (1.135.0)

`RuntimeState(value)`


The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

## Enums |
|
|---|---|
Name |
Description |
`RUNTIME_STATE_UNSPECIFIED` |
Unspecified runtime state. |
`RUNNING` |
NotebookRuntime is in running state. |
`BEING_STARTED` |
NotebookRuntime is in starting state. This is when the runtime is being started from a stopped state. |
`BEING_STOPPED` |
NotebookRuntime is in stopping state. |
`STOPPED` |
NotebookRuntime is in stopped state. |
`BEING_UPGRADED` |
NotebookRuntime is in upgrading state. It is in the middle of upgrading process. |
`ERROR` |
NotebookRuntime was unable to start/stop properly. |
`INVALID` |
NotebookRuntime is in invalid state. Cannot be recovered. |

## Methods

### RuntimeState

`RuntimeState(value)`


The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EventActions.ArtifactDeltaEntry -->

# Class ArtifactDeltaEntry (1.135.0)

`ArtifactDeltaEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ArtifactDeltaEntry

`ArtifactDeltaEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CompleteTrialRequest -->

# Class CompleteTrialRequest (1.135.0)

`CompleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CompleteTrial.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|
`final_measurement` |
Optional. If provided, it will be used as the completed Trial's final_measurement; Otherwise, the service will auto-select a previously reported measurement as the final-measurement |
`trial_infeasible` |
`bool`
Optional. True if the Trial cannot be run with the given Parameter, and final_measurement will be ignored. |
`infeasible_reason` |
`str`
Optional. A human readable reason why the trial was infeasible. This should only be provided if `trial_infeasible` is true.
|

## Methods

### CompleteTrialRequest

`CompleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CompleteTrial.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Event.Type -->

# Class Type (1.135.0)

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Unspecified whether input or output of the Execution. |
`INPUT` |
An input of the Execution. |
`OUTPUT` |
An output of the Execution. |

## Methods

### Type

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteFeatureValuesResponse -->

# Class WriteFeatureValuesResponse (1.135.0)

`WriteFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.WriteFeatureValues.

## Methods

### WriteFeatureValuesResponse

`WriteFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.WriteFeatureValues.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesRequest -->

# Class ListEntityTypesRequest (1.135.0)

`ListEntityTypesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListEntityTypes.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Featurestore to list EntityTypes. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`filter` |
`str`
Lists the EntityTypes that match the filter expression. The following filters are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality as well as key
presence.
Examples:
- `create_time > \"2020-01-31T15:30:00.000000Z\" OR update_time > \"2020-01-31T15:30:00.000000Z\"`
--> EntityTypes created or updated after
2020-01-31T15:30:00.000000Z.
- `labels.active = yes AND labels.env = prod` -->
EntityTypes having both (active: yes) and (env: prod)
labels.
- `labels.env: *` --> Any EntityType which has a label
with 'env' as the key.
|
`page_size` |
`int`
The maximum number of EntityTypes to return. The service may return fewer than this value. If unspecified, at most 1000 EntityTypes will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeaturestoreService.ListEntityTypes call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeaturestoreService.ListEntityTypes must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `entity_type_id`
- `create_time`
- `update_time`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListEntityTypesRequest

`ListEntityTypesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListEntityTypes.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDeploymentResourcePoolRequest -->

# Class CreateDeploymentResourcePoolRequest (1.135.0)

```
CreateDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for CreateDeploymentResourcePool method.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent location resource where this DeploymentResourcePool will be created. Format: `projects/{project}/locations/{location}`
|
`deployment_resource_pool` |
Required. The DeploymentResourcePool to create. |
`deployment_resource_pool_id` |
`str`
Required. The ID to use for the DeploymentResourcePool, which will become the final component of the DeploymentResourcePool's resource name. The maximum length is 63 characters, and valid characters are `/^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$/` .
|

## Methods

### CreateDeploymentResourcePoolRequest

```
CreateDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for CreateDeploymentResourcePool method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse -->

# Class QueryDeployedModelsResponse (1.135.0)

`QueryDeployedModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for QueryDeployedModels method.

## Attributes |
|
|---|---|
Name |
Description |
`deployed_models` |
`MutableSequence[`
DEPRECATED Use deployed_model_refs instead. |
`next_page_token` |
`str`
A token, which can be sent as `page_token` to retrieve the
next page. If this field is omitted, there are no subsequent
pages.
|
`deployed_model_refs` |
`MutableSequence[`
References to the DeployedModels that share the specified deploymentResourcePool. |
`total_deployed_model_count` |
`int`
The total number of DeployedModels on this DeploymentResourcePool. |
`total_endpoint_count` |
`int`
The total number of Endpoints that have DeployedModels on this DeploymentResourcePool. |

## Methods

### QueryDeployedModelsResponse

`QueryDeployedModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for QueryDeployedModels method.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelRequest.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.135.0)

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### TrafficSplitEntry

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.Deploy.DeployMetadata.LabelsEntry -->

# Class LabelsEntry (1.135.0)

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.PredictionDriftDetectionConfig -->

# Class PredictionDriftDetectionConfig (1.135.0)

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

## Attributes |
|
|---|---|
Name |
Description |
`drift_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. If a feature needs to be monitored for drift, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between different time windws. |
`attribution_score_drift_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. The threshold here is against attribution score distance between different time windows. |
`default_drift_threshold` |
Drift anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features. |

## Classes

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

## Methods

### PredictionDriftDetectionConfig

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GeminiTemplateConfig.FieldMappingEntry -->

# Class FieldMappingEntry (1.135.0)

`FieldMappingEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelRequest.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.135.0)

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### TrafficSplitEntry

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataConfig.DataItemLabelsEntry -->

# Class DataItemLabelsEntry (1.135.0)

`DataItemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TextSentimentPredictionResult -->

# Class TextSentimentPredictionResult (1.135.0)

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

## Attribute |
|
|---|---|
Name |
Description |
`sentiment` |
`int`
The integer sentiment labels between 0 (inclusive) and sentimentMax label (inclusive), while 0 maps to the least positive sentiment and sentimentMax maps to the most positive one. The higher the score is, the more positive the sentiment in the text snippet is. Note: sentimentMax is an integer value between 1 (inclusive) and 10 (inclusive). |

## Methods

### TextSentimentPredictionResult

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

### TextSentimentPredictionResult

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchMetricValue -->

# Class ToolParameterKVMatchMetricValue (1.135.0)

```
ToolParameterKVMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key value match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Tool parameter key value match score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ToolParameterKVMatchMetricValue

```
ToolParameterKVMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key value match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployRequest.DeployConfig.SystemLabelsEntry -->

# Class SystemLabelsEntry (1.135.0)

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardRequest -->

# Class UpdateTensorboardRequest (1.135.0)

`UpdateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboard.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the Tensorboard resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard` |
Required. The Tensorboard's `name` field is used to
identify the Tensorboard to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|

## Methods

### UpdateTensorboardRequest

`UpdateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboard.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AssignNotebookRuntimeRequest -->

# Class AssignNotebookRuntimeRequest (1.135.0)

```
AssignNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.AssignNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to get the NotebookRuntime assignment. Format: `projects/{project}/locations/{location}`
|
`notebook_runtime_template` |
`str`
Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one). |
`notebook_runtime` |
Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. |
`notebook_runtime_id` |
`str`
Optional. User specified ID for the notebook runtime. |

## Methods

### AssignNotebookRuntimeRequest

```
AssignNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.AssignNotebookRuntime.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.PredictionDriftDetectionConfig -->

# Class PredictionDriftDetectionConfig (1.135.0)

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

## Attributes |
|
|---|---|
Name |
Description |
`drift_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. If a feature needs to be monitored for drift, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between different time windws. |
`attribution_score_drift_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. The threshold here is against attribution score distance between different time windows. |
`default_drift_threshold` |
Drift anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features. |

## Classes

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

## Methods

### PredictionDriftDetectionConfig

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntime.RuntimeState -->

# Class RuntimeState (1.135.0)

`RuntimeState(value)`


The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

## Enums |
|
|---|---|
Name |
Description |
`RUNTIME_STATE_UNSPECIFIED` |
Unspecified runtime state. |
`RUNNING` |
NotebookRuntime is in running state. |
`BEING_STARTED` |
NotebookRuntime is in starting state. This is when the runtime is being started from a stopped state. |
`BEING_STOPPED` |
NotebookRuntime is in stopping state. |
`STOPPED` |
NotebookRuntime is in stopped state. |
`BEING_UPGRADED` |
NotebookRuntime is in upgrading state. It is in the middle of upgrading process. |
`ERROR` |
NotebookRuntime was unable to start/stop properly. |
`INVALID` |
NotebookRuntime is in invalid state. Cannot be recovered. |

## Methods

### RuntimeState

`RuntimeState(value)`


The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardExperimentRequest -->

# Class CreateTensorboardExperimentRequest (1.135.0)

```
CreateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.CreateTensorboardExperiment.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Tensorboard to create the TensorboardExperiment in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`tensorboard_experiment` |
The TensorboardExperiment to create. |
`tensorboard_experiment_id` |
`str`
Required. The ID to use for the Tensorboard experiment, which becomes the final component of the Tensorboard experiment's resource name. This value should be 1-128 characters, and valid characters are `/` a-z][0-9]`-/` .
|

## Methods

### CreateTensorboardExperimentRequest

```
CreateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.CreateTensorboardExperiment.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricResult -->

# Class PointwiseMetricResult (1.135.0)

`PointwiseMetricResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Pointwise metric score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for pointwise metric score. |
`custom_output` |
Output only. Spec for custom output. |

## Methods

### PointwiseMetricResult

`PointwiseMetricResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LogprobsResult -->

# Class LogprobsResult (1.135.0)

`LogprobsResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Logprobs Result

## Attributes |
|
|---|---|
Name |
Description |
`top_candidates` |
`MutableSequence[`
Length = total number of decoding steps. |
`chosen_candidates` |
`MutableSequence[`
Length = total number of decoding steps. The chosen candidates may or may not be in top_candidates. |

## Classes

### Candidate

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidate for the logprobs token and score.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### TopCandidates

`TopCandidates(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidates with top log probabilities at each decoding step.

## Methods

### LogprobsResult

`LogprobsResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Logprobs Result

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FulfillmentInstance -->

# Class FulfillmentInstance (1.135.0)

`FulfillmentInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment instance.

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
`instruction` |
`str`
Required. Inference instruction prompt to compare prediction with. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### FulfillmentInstance

`FulfillmentInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse -->

# Class QueryDeployedModelsResponse (1.135.0)

`QueryDeployedModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for QueryDeployedModels method.

## Attributes |
|
|---|---|
Name |
Description |
`deployed_models` |
`MutableSequence[`
DEPRECATED Use deployed_model_refs instead. |
`next_page_token` |
`str`
A token, which can be sent as `page_token` to retrieve the
next page. If this field is omitted, there are no subsequent
pages.
|
`deployed_model_refs` |
`MutableSequence[`
References to the DeployedModels that share the specified deploymentResourcePool. |
`total_deployed_model_count` |
`int`
The total number of DeployedModels on this DeploymentResourcePool. |
`total_endpoint_count` |
`int`
The total number of Endpoints that have DeployedModels on this DeploymentResourcePool. |

## Methods

### QueryDeployedModelsResponse

`QueryDeployedModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for QueryDeployedModels method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient -->

# Class NotebookServiceAsyncClient (1.135.0)

```
NotebookServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.notebook_service.transports.base.NotebookServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.notebook_service.transports.base.NotebookServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The interface for Vertex Notebook service (a.k.a. Colab on Workbench).

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
`NotebookServiceTransport` |
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

### NotebookServiceAsyncClient

```
NotebookServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.notebook_service.transports.base.NotebookServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.notebook_service.transports.base.NotebookServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the notebook service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,NotebookServiceTransport,Callable[..., NotebookServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the NotebookServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### assign_notebook_runtime

```
assign_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.AssignNotebookRuntimeRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_runtime_template: typing.Optional[str] = None,
notebook_runtime: typing.Optional[
google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntime
] = None,
notebook_runtime_id: typing.Optional[str] = None,
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


Assigns a NotebookRuntime to a user for a particular Notebook file. This method will either returns an existing assignment or generates a new one.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_assign_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime = aiplatform_v1.[NotebookRuntime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntime.html)()
notebook_runtime.runtime_user = "runtime_user_value"
notebook_runtime.display_name = "display_name_value"
request = aiplatform_v1.[AssignNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AssignNotebookRuntimeRequest.html)(
parent="parent_value",
notebook_runtime_template="notebook_runtime_template_value",
notebook_runtime=notebook_runtime,
)
# Make the request
operation = client.[assign_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_assign_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.AssignNotebookRuntime. |
`parent` |
Required. The resource name of the Location to get the NotebookRuntime assignment. Format: |
`notebook_runtime_template` |
Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one). This corresponds to the |
`notebook_runtime` |
Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. This corresponds to the |
`notebook_runtime_id` |
Optional. User specified ID for the notebook runtime. This corresponds to the |
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

### create_notebook_execution_job

```
create_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.CreateNotebookExecutionJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_execution_job: typing.Optional[
google.cloud.aiplatform_v1.types.notebook_execution_job.NotebookExecutionJob
] = None,
notebook_execution_job_id: typing.Optional[str] = None,
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


Creates a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_notebook_execution_job():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_execution_job = aiplatform_v1.[NotebookExecutionJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJob.html)()
notebook_execution_job.notebook_runtime_template_resource_name = "notebook_runtime_template_resource_name_value"
notebook_execution_job.gcs_output_uri = "gcs_output_uri_value"
notebook_execution_job.execution_user = "execution_user_value"
request = aiplatform_v1.[CreateNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNotebookExecutionJobRequest.html)(
parent="parent_value",
notebook_execution_job=notebook_execution_job,
)
# Make the request
operation = client.[create_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_create_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.CreateNotebookExecutionJob] |
`parent` |
Required. The resource name of the Location to create the NotebookExecutionJob. Format: |
`notebook_execution_job` |
Required. The NotebookExecutionJob to create. This corresponds to the |
`notebook_execution_job_id` |
Optional. User specified ID for the NotebookExecutionJob. This corresponds to the |
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

### create_notebook_runtime_template

```
create_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.CreateNotebookRuntimeTemplateRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_runtime_template: typing.Optional[
google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntimeTemplate
] = None,
notebook_runtime_template_id: typing.Optional[str] = None,
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


Creates a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1.[CreateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNotebookRuntimeTemplateRequest.html)(
parent="parent_value",
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
operation = client.[create_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_create_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.CreateNotebookRuntimeTemplate. |
`parent` |
Required. The resource name of the Location to create the NotebookRuntimeTemplate. Format: |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to create. This corresponds to the |
`notebook_runtime_template_id` |
Optional. User specified ID for the notebook runtime template. This corresponds to the |
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

### delete_notebook_execution_job

```
delete_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.DeleteNotebookExecutionJobRequest,
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


Deletes a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_notebook_execution_job():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.DeleteNotebookExecutionJob] |
`name` |
Required. The name of the NotebookExecutionJob resource to be deleted. This corresponds to the |
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

### delete_notebook_runtime

```
delete_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.DeleteNotebookRuntimeRequest,
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


Deletes a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be deleted. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### delete_notebook_runtime_template

```
delete_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.DeleteNotebookRuntimeTemplateRequest,
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


Deletes a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntimeTemplate. |
`name` |
Required. The name of the NotebookRuntimeTemplate resource to be deleted. Format: |
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
`NotebookServiceAsyncClient` |
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
`NotebookServiceAsyncClient` |
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
`NotebookServiceAsyncClient` |
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

### get_notebook_execution_job

```
get_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.GetNotebookExecutionJobRequest,
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
) -> google.cloud.aiplatform_v1.types.notebook_execution_job.NotebookExecutionJob
```


Gets a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_notebook_execution_job():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_execution_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [NotebookService.GetNotebookExecutionJob] |
`name` |
Required. The name of the NotebookExecutionJob resource. This corresponds to the |
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
NotebookExecutionJob represents an instance of a notebook execution. |

### get_notebook_runtime

```
get_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.GetNotebookRuntimeRequest,
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
) -> google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntime
```


Gets a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_runtime)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.GetNotebookRuntime |
`name` |
Required. The name of the NotebookRuntime resource. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade. |

### get_notebook_runtime_template

```
get_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.GetNotebookRuntimeTemplateRequest,
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
) -> google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntimeTemplate
```


Gets a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.GetNotebookRuntimeTemplate |
`name` |
Required. The name of the NotebookRuntimeTemplate resource. Format: |
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
A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template. |

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
google.cloud.aiplatform_v1.services.notebook_service.transports.base.NotebookServiceTransport
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

### list_notebook_execution_jobs

```
list_notebook_execution_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsRequest,
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
google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookExecutionJobsAsyncPager
)
```


Lists NotebookExecutionJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_notebook_execution_jobs():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListNotebookExecutionJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookExecutionJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_execution_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_execution_jobs)(request=request)
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
The request object. Request message for [NotebookService.ListNotebookExecutionJobs] |
`parent` |
Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: |
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
Response message for [NotebookService.CreateNotebookExecutionJob] Iterating over this object will yield results and resolve additional pages automatically. |

### list_notebook_runtime_templates

```
list_notebook_runtime_templates(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
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
google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesAsyncPager
)
```


Lists NotebookRuntimeTemplates in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_notebook_runtime_templates():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListNotebookRuntimeTemplatesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtime_templates](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_runtime_templates)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimeTemplates. |
`parent` |
Required. The resource name of the Location from which to list the NotebookRuntimeTemplates. Format: |
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
Response message for NotebookService.ListNotebookRuntimeTemplates. Iterating over this object will yield results and resolve additional pages automatically. |

### list_notebook_runtimes

```
list_notebook_runtimes(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesRequest,
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
google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimesAsyncPager
)
```


Lists NotebookRuntimes in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_notebook_runtimes():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListNotebookRuntimesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtimes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_runtimes)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimes. |
`parent` |
Required. The resource name of the Location from which to list the NotebookRuntimes. Format: |
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
Response message for NotebookService.ListNotebookRuntimes. Iterating over this object will yield results and resolve additional pages automatically. |

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

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### notebook_execution_job_path

```
notebook_execution_job_path(
project: str, location: str, notebook_execution_job: str
) -> str
```


Returns a fully-qualified notebook_execution_job string.

### notebook_runtime_path

`notebook_runtime_path(project: str, location: str, notebook_runtime: str) -> str`


Returns a fully-qualified notebook_runtime string.

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

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_execution_job_path

`parse_notebook_execution_job_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_execution_job path into its component segments.

### parse_notebook_runtime_path

`parse_notebook_runtime_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_schedule_path

`parse_schedule_path(path: str) -> typing.Dict[str, str]`


Parses a schedule path into its component segments.

### parse_subnetwork_path

`parse_subnetwork_path(path: str) -> typing.Dict[str, str]`


Parses a subnetwork path into its component segments.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### schedule_path

`schedule_path(project: str, location: str, schedule: str) -> str`


Returns a fully-qualified schedule string.

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

### start_notebook_runtime

```
start_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.StartNotebookRuntimeRequest,
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


Starts a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_start_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StartNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StartNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[start_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_start_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StartNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be started. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### stop_notebook_runtime

```
stop_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.StopNotebookRuntimeRequest,
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


Stops a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_stop_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StopNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StopNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[stop_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_stop_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StopNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### subnetwork_path

`subnetwork_path(project: str, region: str, subnetwork: str) -> str`


Returns a fully-qualified subnetwork string.

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

### update_notebook_runtime_template

```
update_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.UpdateNotebookRuntimeTemplateRequest,
dict,
]
] = None,
*,
notebook_runtime_template: typing.Optional[
google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntimeTemplate
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
) -> google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntimeTemplate
```


Updates a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1.[UpdateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateNotebookRuntimeTemplateRequest.html)(
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
response = await client.[update_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_update_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.UpdateNotebookRuntimeTemplate. |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to update. This corresponds to the |
`update_mask` |
Required. The update mask applies to the resource. For the |
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
A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template. |

### upgrade_notebook_runtime

```
upgrade_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.UpgradeNotebookRuntimeRequest,
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


Upgrades a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_upgrade_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpgradeNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpgradeNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[upgrade_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_upgrade_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.UpgradeNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be upgrade. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.OutputInfo -->

# Class OutputInfo (1.135.0)

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the info for output of EvaluationService.EvaluateDataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`gcs_output_directory` |
`str`
Output only. The full path of the Cloud Storage directory created, into which the evaluation results and aggregation results are written. This field is a member of `oneof` _ `output_location` .
|

## Methods

### OutputInfo

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the info for output of EvaluationService.EvaluateDataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchNearestEntitiesRequest -->

# Class SearchNearestEntitiesRequest (1.135.0)

```
SearchNearestEntitiesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The request message for FeatureOnlineStoreService.SearchNearestEntities.

## Attributes |
|
|---|---|
Name |
Description |
`feature_view` |
`str`
Required. FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`
|
`query` |
Required. The query. |
`return_full_entity` |
`bool`
Optional. If set to true, the full entities (including all vector values and metadata) of the nearest neighbors are returned; otherwise only entity id of the nearest neighbors will be returned. Note that returning full entities will significantly increase the latency and cost of the query. |

## Methods

### SearchNearestEntitiesRequest

```
SearchNearestEntitiesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The request message for FeatureOnlineStoreService.SearchNearestEntities.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDeploymentResourcePoolRequest -->

# Class CreateDeploymentResourcePoolRequest (1.135.0)

```
CreateDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for CreateDeploymentResourcePool method.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent location resource where this DeploymentResourcePool will be created. Format: `projects/{project}/locations/{location}`
|
`deployment_resource_pool` |
Required. The DeploymentResourcePool to create. |
`deployment_resource_pool_id` |
`str`
Required. The ID to use for the DeploymentResourcePool, which will become the final component of the DeploymentResourcePool's resource name. The maximum length is 63 characters, and valid characters are `/^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$/` .
|

## Methods

### CreateDeploymentResourcePoolRequest

```
CreateDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for CreateDeploymentResourcePool method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresRequest -->

# Class ListMetadataStoresRequest (1.135.0)

`ListMetadataStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataStores.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The Location whose MetadataStores should be listed. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
The maximum number of Metadata Stores to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListMetadataStores call. Provide this to retrieve the subsequent page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID_ARGUMENT error.) |

## Methods

### ListMetadataStoresRequest

`ListMetadataStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataStores.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.Bigtable -->

# Class Bigtable (1.135.0)

`Bigtable(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`auto_scaling` |
Required. Autoscaling config applied to Bigtable Instance. |
`enable_direct_bigtable_access` |
`bool`
If true, enable direct access to the Bigtable instance. |
`bigtable_metadata` |
Metadata of the Bigtable instance. Output only. |
`zone` |
`str`
Optional. The zone where the underlying Bigtable cluster for the primary Bigtable instance will be provisioned. Only the zone must be provided. For example, only "us-central1-a" should be provided. |

## Classes

### AutoScaling

`AutoScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### BigtableMetadata

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the Bigtable instance. This is used by direct read access to the Bigtable in tenant project.

## Methods

### Bigtable

`Bigtable(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CoherenceResult -->

# Class CoherenceResult (1.135.0)

`CoherenceResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Coherence score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for coherence score. |
`confidence` |
`float`
Output only. Confidence for coherence score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### CoherenceResult

`CoherenceResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseChoice -->

# Class PairwiseChoice (1.135.0)

`PairwiseChoice(value)`


Pairwise prediction autorater preference.

## Enums |
|
|---|---|
Name |
Description |
`PAIRWISE_CHOICE_UNSPECIFIED` |
Unspecified prediction choice. |
`BASELINE` |
Baseline prediction wins |
`CANDIDATE` |
Candidate prediction wins |
`TIE` |
Winner cannot be determined |

## Methods

### PairwiseChoice

`PairwiseChoice(value)`


Pairwise prediction autorater preference.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveContextChildrenResponse -->

# Class RemoveContextChildrenResponse (1.135.0)

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.

## Methods

### RemoveContextChildrenResponse

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteFeatureValuesPayload.FeatureValuesEntry -->

# Class FeatureValuesEntry (1.135.0)

`FeatureValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### FeatureValuesEntry

`FeatureValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ActiveLearningConfig -->

# Class ActiveLearningConfig (1.135.0)

`ActiveLearningConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that configure the active learning pipeline. Active learning will label the data incrementally by several iterations. For every iteration, it will select a batch of data based on the sampling strategy.

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
`max_data_item_count` |
`int`
Max number of human labeled DataItems. This field is a member of `oneof` _ `human_labeling_budget` .
|
`max_data_item_percentage` |
`int`
Max percent of total DataItems for human labeling. This field is a member of `oneof` _ `human_labeling_budget` .
|
`sample_config` |
Active learning data sampling config. For every active learning labeling iteration, it will select a batch of data based on the sampling strategy. |
`training_config` |
CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems. |

## Methods

### ActiveLearningConfig

`ActiveLearningConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that configure the active learning pipeline. Active learning will label the data incrementally by several iterations. For every iteration, it will select a batch of data based on the sampling strategy.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PSCAutomationConfig -->

# Class PSCAutomationConfig (1.135.0)

`PSCAutomationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PSC config that is used to automatically create PSC endpoints in the user projects.

## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project id used to create forwarding rule. |
`network` |
`str`
Required. The full name of the Google Compute Engine `network ` __.
`Format ` __:
`projects/{project}/global/networks/{network}` .
|
`ip_address` |
`str`
Output only. IP address rule created by the PSC service automation. |
`forwarding_rule` |
`str`
Output only. Forwarding rule created by the PSC service automation. |
`state` |
Output only. The state of the PSC service automation. |
`error_message` |
`str`
Output only. Error message if the PSC service automation failed. |

## Methods

### PSCAutomationConfig

`PSCAutomationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PSC config that is used to automatically create PSC endpoints in the user projects.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssignNotebookRuntimeRequest -->

# Class AssignNotebookRuntimeRequest (1.135.0)

```
AssignNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.AssignNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to get the NotebookRuntime assignment. Format: `projects/{project}/locations/{location}`
|
`notebook_runtime_template` |
`str`
Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one). |
`notebook_runtime` |
Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. |
`notebook_runtime_id` |
`str`
Optional. User specified ID for the notebook runtime. |

## Methods

### AssignNotebookRuntimeRequest

```
AssignNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.AssignNotebookRuntime.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest.DeployConfig.SystemLabelsEntry -->

# Class SystemLabelsEntry (1.135.0)

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataConfig.DataItemLabelsEntry -->

# Class DataItemLabelsEntry (1.135.0)

`DataItemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardRequest -->

# Class UpdateTensorboardRequest (1.135.0)

`UpdateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboard.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the Tensorboard resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard` |
Required. The Tensorboard's `name` field is used to
identify the Tensorboard to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|

## Methods

### UpdateTensorboardRequest

`UpdateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboard.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LogprobsResult -->

# Class LogprobsResult (1.135.0)

`LogprobsResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Logprobs Result

## Attributes |
|
|---|---|
Name |
Description |
`top_candidates` |
`MutableSequence[`
Length = total number of decoding steps. |
`chosen_candidates` |
`MutableSequence[`
Length = total number of decoding steps. The chosen candidates may or may not be in top_candidates. |

## Classes

### Candidate

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidate for the logprobs token and score.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### TopCandidates

`TopCandidates(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidates with top log probabilities at each decoding step.

## Methods

### LogprobsResult

`LogprobsResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Logprobs Result

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardExperimentRequest -->

# Class CreateTensorboardExperimentRequest (1.135.0)

```
CreateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.CreateTensorboardExperiment.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Tensorboard to create the TensorboardExperiment in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`tensorboard_experiment` |
The TensorboardExperiment to create. |
`tensorboard_experiment_id` |
`str`
Required. The ID to use for the Tensorboard experiment, which becomes the final component of the Tensorboard experiment's resource name. This value should be 1-128 characters, and valid characters are `/` a-z][0-9]`-/` .
|

## Methods

### CreateTensorboardExperimentRequest

```
CreateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.CreateTensorboardExperiment.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceInput -->

# Class CoherenceInput (1.135.0)

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for coherence score metric. |
`instance` |
Required. Coherence instance. |

## Methods

### CoherenceInput

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpgradeNotebookRuntimeResponse -->

# Class UpgradeNotebookRuntimeResponse (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ActiveLearningConfig -->

# Class ActiveLearningConfig (1.135.0)

`ActiveLearningConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that configure the active learning pipeline. Active learning will label the data incrementally by several iterations. For every iteration, it will select a batch of data based on the sampling strategy.

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
`max_data_item_count` |
`int`
Max number of human labeled DataItems. This field is a member of `oneof` _ `human_labeling_budget` .
|
`max_data_item_percentage` |
`int`
Max percent of total DataItems for human labeling. This field is a member of `oneof` _ `human_labeling_budget` .
|
`sample_config` |
Active learning data sampling config. For every active learning labeling iteration, it will select a batch of data based on the sampling strategy. |
`training_config` |
CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems. |

## Methods

### ActiveLearningConfig

`ActiveLearningConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that configure the active learning pipeline. Active learning will label the data incrementally by several iterations. For every iteration, it will select a batch of data based on the sampling strategy.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchNearestEntitiesRequest -->

# Class SearchNearestEntitiesRequest (1.135.0)

```
SearchNearestEntitiesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The request message for FeatureOnlineStoreService.SearchNearestEntities.

## Attributes |
|
|---|---|
Name |
Description |
`feature_view` |
`str`
Required. FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`
|
`query` |
Required. The query. |
`return_full_entity` |
`bool`
Optional. If set to true, the full entities (including all vector values and metadata) of the nearest neighbors are returned; otherwise only entity id of the nearest neighbors will be returned. Note that returning full entities will significantly increase the latency and cost of the query. |

## Methods

### SearchNearestEntitiesRequest

```
SearchNearestEntitiesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The request message for FeatureOnlineStoreService.SearchNearestEntities.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresRequest -->

# Class ListMetadataStoresRequest (1.135.0)

`ListMetadataStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataStores.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The Location whose MetadataStores should be listed. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
The maximum number of Metadata Stores to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListMetadataStores call. Provide this to retrieve the subsequent page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID_ARGUMENT error.) |

## Methods

### ListMetadataStoresRequest

`ListMetadataStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataStores.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RaySpec -->

# Class RaySpec (1.135.0)

`RaySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration information for the Ray cluster. For experimental launch, Ray cluster creation and Persistent cluster creation are 1:1 mapping: We will provision all the nodes within the Persistent cluster as Ray nodes.

## Attributes |
|
|---|---|
Name |
Description |
`image_uri` |
`str`
Optional. Default image for user to choose a preferred ML framework (for example, TensorFlow or Pytorch) by choosing from `Vertex prebuilt images |
`nfs_mounts` |
`MutableSequence[`
Optional. Use if you want to mount to any NFS storages. |
`resource_pool_images` |
`MutableMapping[str, str]`
Optional. Required if image_uri isn't set. A map of resource_pool_id to prebuild Ray image if user need to use different images for different head/worker pools. This map needs to cover all the resource pool ids. Example: { "ray_head_node_pool": "head image" "ray_worker_node_pool1": "worker image" "ray_worker_node_pool2": "another worker image" } |
`head_node_resource_pool_id` |
`str`
Optional. This will be used to indicate which resource pool will serve as the Ray head node(the first node within that pool). Will use the machine from the first workerpool as the head node by default if this field isn't set. |
`ray_metric_spec` |
Optional. Ray metrics configurations. |
`ray_logs_spec` |
Optional. OSS Ray logging configurations. |

## Classes

### ResourcePoolImagesEntry

`ResourcePoolImagesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### RaySpec

`RaySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration information for the Ray cluster. For experimental launch, Ray cluster creation and Persistent cluster creation are 1:1 mapping: We will provision all the nodes within the Persistent cluster as Ray nodes.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FulfillmentInstance -->

# Class FulfillmentInstance (1.135.0)

`FulfillmentInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment instance.

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
`instruction` |
`str`
Required. Inference instruction prompt to compare prediction with. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### FulfillmentInstance

`FulfillmentInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceResult -->

# Class CoherenceResult (1.135.0)

`CoherenceResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Coherence score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for coherence score. |
`confidence` |
`float`
Output only. Confidence for coherence score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### CoherenceResult

`CoherenceResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EntityIdSelector -->

# Class EntityIdSelector (1.135.0)

`EntityIdSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for entityId. Getting ids from the given source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`csv_source` |
Source of Csv This field is a member of `oneof` _ `EntityIdsSource` .
|
`entity_id_field` |
`str`
Source column that holds entity IDs. If not provided, entity IDs are extracted from the column named entity_id. |

## Methods

### EntityIdSelector

`EntityIdSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for entityId. Getting ids from the given source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageClassificationPredictionInstance -->

# Class ImageClassificationPredictionInstance (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetricxResult -->

# Class MetricxResult (1.135.0)

`MetricxResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX result - calculates the MetricX score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. MetricX score. Range depends on version. This field is a member of `oneof` _ `_score` .
|

## Methods

### MetricxResult

`MetricxResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX result - calculates the MetricX score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig.RoutingConfig.ManualRoutingMode -->

# Class ManualRoutingMode (1.135.0)

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
The model name to use. Only the public LLM models are accepted. e.g. 'gemini-1.5-pro-001'. This field is a member of `oneof` _ `_model_name` .
|

## Methods

### ManualRoutingMode

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExactMatchResults -->

# Class ExactMatchResults (1.135.0)

`ExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for exact match metric.

## Attribute |
|
|---|---|
Name |
Description |
`exact_match_metric_values` |
`MutableSequence[`
Output only. Exact match metric values. |

## Methods

### ExactMatchResults

`ExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for exact match metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VeoHyperParameters.TuningTask -->

# Class TuningTask (1.135.0)

`TuningTask(value)`


An enum defining the tuning task used for Veo.

## Enums |
|
|---|---|
Name |
Description |
`TUNING_TASK_UNSPECIFIED` |
Default value. This value is unused. |
`TUNING_TASK_I2V` |
Tuning task for image to video. |
`TUNING_TASK_T2V` |
Tuning task for text to video. |

## Methods

### TuningTask

`TuningTask(value)`


An enum defining the tuning task used for Veo.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorRequest -->

# Class CreateFeatureMonitorRequest (1.135.0)

`CreateFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [FeatureRegistryService.CreateFeatureMonitorRequest][].

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of FeatureGroup to create FeatureMonitor. Format: `projects/{project}/locations/{location}/featureGroups/{featuregroup}`
|
`feature_monitor` |
Required. The Monitor to create. |
`feature_monitor_id` |
`str`
Required. The ID to use for this FeatureMonitor, which will become the final component of the FeatureGroup's resource name. This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within the FeatureGroup.
|

## Methods

### CreateFeatureMonitorRequest

`CreateFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [FeatureRegistryService.CreateFeatureMonitorRequest][].

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient -->

# Class GenAiTuningServiceClient (1.135.0)

```
GenAiTuningServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing GenAI Tuning Jobs.

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
`GenAiTuningServiceTransport` |
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

### GenAiTuningServiceClient

```
GenAiTuningServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the gen ai tuning service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,GenAiTuningServiceTransport,Callable[..., GenAiTuningServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the GenAiTuningServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### cancel_tuning_job

```
cancel_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.genai_tuning_service.CancelTuningJobRequest,
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


Cancels a TuningJob. Starts asynchronous cancellation on the
TuningJob. The server makes a best effort to cancel the job, but
success is not guaranteed. Clients can use
xref_GenAiTuningService.GetTuningJob
or other methods to check whether the cancellation succeeded or
whether the job completed despite cancellation. On successful
cancellation, the TuningJob is not deleted; instead it becomes a
job with a
xref_TuningJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_TuningJob.state is
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
def sample_cancel_tuning_job():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelTuningJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceClient_cancel_tuning_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.CancelTuningJob. |
`name` |
`str`
Required. The name of the TuningJob to cancel. Format: |
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

### create_tuning_job

```
create_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.genai_tuning_service.CreateTuningJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tuning_job: typing.Optional[
google.cloud.aiplatform_v1.types.tuning_job.TuningJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tuning_job.TuningJob
```


Creates a TuningJob. A created TuningJob right away will be attempted to be run.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_tuning_job():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
tuning_job = aiplatform_v1.[TuningJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TuningJob.html)()
tuning_job.base_model = "base_model_value"
tuning_job.supervised_tuning_spec.training_dataset_uri = "training_dataset_uri_value"
request = aiplatform_v1.[CreateTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTuningJobRequest.html)(
parent="parent_value",
tuning_job=tuning_job,
)
# Make the request
response = client.[create_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceClient_create_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.CreateTuningJob. |
`parent` |
`str`
Required. The resource name of the Location to create the TuningJob in. Format: |
`tuning_job` |
Required. The TuningJob to create. This corresponds to the |
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
Represents a TuningJob that runs with Google owned models. |

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
`GenAiTuningServiceClient` |
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
`GenAiTuningServiceClient` |
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
`GenAiTuningServiceClient` |
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

### get_tuning_job

```
get_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.genai_tuning_service.GetTuningJobRequest,
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
) -> google.cloud.aiplatform_v1.types.tuning_job.TuningJob
```


Gets a TuningJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_tuning_job():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTuningJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceClient_get_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.GetTuningJob. |
`name` |
`str`
Required. The name of the TuningJob resource. Format: |
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
Represents a TuningJob that runs with Google owned models. |

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

### list_tuning_jobs

```
list_tuning_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsRequest,
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
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers.ListTuningJobsPager
)
```


Lists TuningJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_tuning_jobs():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTuningJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tuning_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceClient_list_tuning_jobs)(request=request)
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
The request object. Request message for GenAiTuningService.ListTuningJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the TuningJobs from. Format: |
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
Response message for GenAiTuningService.ListTuningJobs Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_context_path

`parse_context_path(path: str) -> typing.Dict[str, str]`


Parses a context path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_tuning_job_path

`parse_tuning_job_path(path: str) -> typing.Dict[str, str]`


Parses a tuning_job path into its component segments.

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

### rebase_tuned_model

```
rebase_tuned_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.genai_tuning_service.RebaseTunedModelRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tuned_model_ref: typing.Optional[
google.cloud.aiplatform_v1.types.tuning_job.TunedModelRef
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


Rebase a TunedModel.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_rebase_tuned_model():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
tuned_model_ref = aiplatform_v1.[TunedModelRef](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TunedModelRef.html)()
tuned_model_ref.tuned_model = "tuned_model_value"
request = aiplatform_v1.[RebaseTunedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebaseTunedModelRequest.html)(
parent="parent_value",
tuned_model_ref=tuned_model_ref,
)
# Make the request
operation = client.[rebase_tuned_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceClient_rebase_tuned_model)(request=request)
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
The request object. Request message for GenAiTuningService.RebaseTunedModel. |
`parent` |
`str`
Required. The resource name of the Location into which to rebase the Model. Format: |
`tuned_model_ref` |
Required. TunedModel reference to retrieve the legacy model information. This corresponds to the |
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

### tuning_job_path

`tuning_job_path(project: str, location: str, tuning_job: str) -> str`


Returns a fully-qualified tuning_job string.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient -->

# Class NotebookServiceAsyncClient (1.135.0)

```
NotebookServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The interface for Vertex Notebook service (a.k.a. Colab on Workbench).

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
`NotebookServiceTransport` |
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

### NotebookServiceAsyncClient

```
NotebookServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the notebook service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,NotebookServiceTransport,Callable[..., NotebookServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the NotebookServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### assign_notebook_runtime

```
assign_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.AssignNotebookRuntimeRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_runtime_template: typing.Optional[str] = None,
notebook_runtime: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntime
] = None,
notebook_runtime_id: typing.Optional[str] = None,
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


Assigns a NotebookRuntime to a user for a particular Notebook file. This method will either returns an existing assignment or generates a new one.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_assign_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime = aiplatform_v1beta1.[NotebookRuntime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntime.html)()
notebook_runtime.runtime_user = "runtime_user_value"
notebook_runtime.display_name = "display_name_value"
request = aiplatform_v1beta1.[AssignNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssignNotebookRuntimeRequest.html)(
parent="parent_value",
notebook_runtime_template="notebook_runtime_template_value",
notebook_runtime=notebook_runtime,
)
# Make the request
operation = client.[assign_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_assign_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.AssignNotebookRuntime. |
`parent` |
Required. The resource name of the Location to get the NotebookRuntime assignment. Format: |
`notebook_runtime_template` |
Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one). This corresponds to the |
`notebook_runtime` |
Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. This corresponds to the |
`notebook_runtime_id` |
Optional. User specified ID for the notebook runtime. This corresponds to the |
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

### create_notebook_execution_job

```
create_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.CreateNotebookExecutionJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_execution_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_execution_job.NotebookExecutionJob
] = None,
notebook_execution_job_id: typing.Optional[str] = None,
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


Creates a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_execution_job = aiplatform_v1beta1.[NotebookExecutionJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.html)()
notebook_execution_job.notebook_runtime_template_resource_name = "notebook_runtime_template_resource_name_value"
notebook_execution_job.gcs_output_uri = "gcs_output_uri_value"
notebook_execution_job.execution_user = "execution_user_value"
request = aiplatform_v1beta1.[CreateNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookExecutionJobRequest.html)(
parent="parent_value",
notebook_execution_job=notebook_execution_job,
)
# Make the request
operation = client.[create_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_create_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.CreateNotebookExecutionJob] |
`parent` |
Required. The resource name of the Location to create the NotebookExecutionJob. Format: |
`notebook_execution_job` |
Required. The NotebookExecutionJob to create. This corresponds to the |
`notebook_execution_job_id` |
Optional. User specified ID for the NotebookExecutionJob. This corresponds to the |
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

### create_notebook_runtime_template

```
create_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.CreateNotebookRuntimeTemplateRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_runtime_template: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
] = None,
notebook_runtime_template_id: typing.Optional[str] = None,
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


Creates a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1beta1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookRuntimeTemplateRequest.html)(
parent="parent_value",
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
operation = client.[create_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_create_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.CreateNotebookRuntimeTemplate. |
`parent` |
Required. The resource name of the Location to create the NotebookRuntimeTemplate. Format: |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to create. This corresponds to the |
`notebook_runtime_template_id` |
Optional. User specified ID for the notebook runtime template. This corresponds to the |
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

### delete_notebook_execution_job

```
delete_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.DeleteNotebookExecutionJobRequest,
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


Deletes a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.DeleteNotebookExecutionJob] |
`name` |
Required. The name of the NotebookExecutionJob resource to be deleted. This corresponds to the |
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

### delete_notebook_runtime

```
delete_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.DeleteNotebookRuntimeRequest,
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


Deletes a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be deleted. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### delete_notebook_runtime_template

```
delete_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.DeleteNotebookRuntimeTemplateRequest,
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


Deletes a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntimeTemplate. |
`name` |
Required. The name of the NotebookRuntimeTemplate resource to be deleted. Format: |
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
`NotebookServiceAsyncClient` |
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
`NotebookServiceAsyncClient` |
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
`NotebookServiceAsyncClient` |
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

### get_notebook_execution_job

```
get_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.GetNotebookExecutionJobRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_execution_job.NotebookExecutionJob
```


Gets a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_execution_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [NotebookService.GetNotebookExecutionJob] |
`name` |
Required. The name of the NotebookExecutionJob resource. This corresponds to the |
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
NotebookExecutionJob represents an instance of a notebook execution. |

### get_notebook_runtime

```
get_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.GetNotebookRuntimeRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntime
```


Gets a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_runtime)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.GetNotebookRuntime |
`name` |
Required. The name of the NotebookRuntime resource. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade. |

### get_notebook_runtime_template

```
get_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.GetNotebookRuntimeTemplateRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
```


Gets a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.GetNotebookRuntimeTemplate |
`name` |
Required. The name of the NotebookRuntimeTemplate resource. Format: |
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
A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template. |

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
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport
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

### list_notebook_execution_jobs

```
list_notebook_execution_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookExecutionJobsAsyncPager
)
```


Lists NotebookExecutionJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_notebook_execution_jobs():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookExecutionJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_execution_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_execution_jobs)(request=request)
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
The request object. Request message for [NotebookService.ListNotebookExecutionJobs] |
`parent` |
Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: |
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
Response message for [NotebookService.CreateNotebookExecutionJob] Iterating over this object will yield results and resolve additional pages automatically. |

### list_notebook_runtime_templates

```
list_notebook_runtime_templates(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
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
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesAsyncPager
)
```


Lists NotebookRuntimeTemplates in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_notebook_runtime_templates():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookRuntimeTemplatesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtime_templates](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_runtime_templates)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimeTemplates. |
`parent` |
Required. The resource name of the Location from which to list the NotebookRuntimeTemplates. Format: |
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
Response message for NotebookService.ListNotebookRuntimeTemplates. Iterating over this object will yield results and resolve additional pages automatically. |

### list_notebook_runtimes

```
list_notebook_runtimes(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
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
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimesAsyncPager
)
```


Lists NotebookRuntimes in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_notebook_runtimes():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookRuntimesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtimes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_runtimes)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimes. |
`parent` |
Required. The resource name of the Location from which to list the NotebookRuntimes. Format: |
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
Response message for NotebookService.ListNotebookRuntimes. Iterating over this object will yield results and resolve additional pages automatically. |

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

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### notebook_execution_job_path

```
notebook_execution_job_path(
project: str, location: str, notebook_execution_job: str
) -> str
```


Returns a fully-qualified notebook_execution_job string.

### notebook_runtime_path

`notebook_runtime_path(project: str, location: str, notebook_runtime: str) -> str`


Returns a fully-qualified notebook_runtime string.

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

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_execution_job_path

`parse_notebook_execution_job_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_execution_job path into its component segments.

### parse_notebook_runtime_path

`parse_notebook_runtime_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_schedule_path

`parse_schedule_path(path: str) -> typing.Dict[str, str]`


Parses a schedule path into its component segments.

### parse_subnetwork_path

`parse_subnetwork_path(path: str) -> typing.Dict[str, str]`


Parses a subnetwork path into its component segments.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### schedule_path

`schedule_path(project: str, location: str, schedule: str) -> str`


Returns a fully-qualified schedule string.

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

### start_notebook_runtime

```
start_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.StartNotebookRuntimeRequest,
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


Starts a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_start_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StartNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[start_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_start_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StartNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be started. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### stop_notebook_runtime

```
stop_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.StopNotebookRuntimeRequest,
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


Stops a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_stop_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StopNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[stop_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_stop_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StopNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### subnetwork_path

`subnetwork_path(project: str, region: str, subnetwork: str) -> str`


Returns a fully-qualified subnetwork string.

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

### update_notebook_runtime_template

```
update_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.UpdateNotebookRuntimeTemplateRequest,
dict,
]
] = None,
*,
notebook_runtime_template: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
```


Updates a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1beta1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateNotebookRuntimeTemplateRequest.html)(
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
response = await client.[update_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_update_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.UpdateNotebookRuntimeTemplate. |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to update. This corresponds to the |
`update_mask` |
Required. The update mask applies to the resource. For the |
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
A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template. |

### upgrade_notebook_runtime

```
upgrade_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.UpgradeNotebookRuntimeRequest,
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


Upgrades a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_upgrade_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpgradeNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[upgrade_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_upgrade_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.UpgradeNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be upgrade. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient -->

# Class NotebookServiceAsyncClient (1.134.0)

```
NotebookServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The interface for Vertex Notebook service (a.k.a. Colab on Workbench).

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
`NotebookServiceTransport` |
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

### NotebookServiceAsyncClient

```
NotebookServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the notebook service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,NotebookServiceTransport,Callable[..., NotebookServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the NotebookServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### assign_notebook_runtime

```
assign_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.AssignNotebookRuntimeRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_runtime_template: typing.Optional[str] = None,
notebook_runtime: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntime
] = None,
notebook_runtime_id: typing.Optional[str] = None,
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


Assigns a NotebookRuntime to a user for a particular Notebook file. This method will either returns an existing assignment or generates a new one.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_assign_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime = aiplatform_v1beta1.[NotebookRuntime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntime.html)()
notebook_runtime.runtime_user = "runtime_user_value"
notebook_runtime.display_name = "display_name_value"
request = aiplatform_v1beta1.[AssignNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssignNotebookRuntimeRequest.html)(
parent="parent_value",
notebook_runtime_template="notebook_runtime_template_value",
notebook_runtime=notebook_runtime,
)
# Make the request
operation = client.[assign_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_assign_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.AssignNotebookRuntime. |
`parent` |
Required. The resource name of the Location to get the NotebookRuntime assignment. Format: |
`notebook_runtime_template` |
Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one). This corresponds to the |
`notebook_runtime` |
Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. This corresponds to the |
`notebook_runtime_id` |
Optional. User specified ID for the notebook runtime. This corresponds to the |
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

### create_notebook_execution_job

```
create_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.CreateNotebookExecutionJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_execution_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_execution_job.NotebookExecutionJob
] = None,
notebook_execution_job_id: typing.Optional[str] = None,
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


Creates a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_execution_job = aiplatform_v1beta1.[NotebookExecutionJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.html)()
notebook_execution_job.notebook_runtime_template_resource_name = "notebook_runtime_template_resource_name_value"
notebook_execution_job.gcs_output_uri = "gcs_output_uri_value"
notebook_execution_job.execution_user = "execution_user_value"
request = aiplatform_v1beta1.[CreateNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookExecutionJobRequest.html)(
parent="parent_value",
notebook_execution_job=notebook_execution_job,
)
# Make the request
operation = client.[create_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_create_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.CreateNotebookExecutionJob] |
`parent` |
Required. The resource name of the Location to create the NotebookExecutionJob. Format: |
`notebook_execution_job` |
Required. The NotebookExecutionJob to create. This corresponds to the |
`notebook_execution_job_id` |
Optional. User specified ID for the NotebookExecutionJob. This corresponds to the |
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

### create_notebook_runtime_template

```
create_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.CreateNotebookRuntimeTemplateRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_runtime_template: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
] = None,
notebook_runtime_template_id: typing.Optional[str] = None,
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


Creates a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1beta1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookRuntimeTemplateRequest.html)(
parent="parent_value",
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
operation = client.[create_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_create_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.CreateNotebookRuntimeTemplate. |
`parent` |
Required. The resource name of the Location to create the NotebookRuntimeTemplate. Format: |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to create. This corresponds to the |
`notebook_runtime_template_id` |
Optional. User specified ID for the notebook runtime template. This corresponds to the |
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

### delete_notebook_execution_job

```
delete_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.DeleteNotebookExecutionJobRequest,
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


Deletes a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.DeleteNotebookExecutionJob] |
`name` |
Required. The name of the NotebookExecutionJob resource to be deleted. This corresponds to the |
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

### delete_notebook_runtime

```
delete_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.DeleteNotebookRuntimeRequest,
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


Deletes a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be deleted. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### delete_notebook_runtime_template

```
delete_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.DeleteNotebookRuntimeTemplateRequest,
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


Deletes a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntimeTemplate. |
`name` |
Required. The name of the NotebookRuntimeTemplate resource to be deleted. Format: |
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
`NotebookServiceAsyncClient` |
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
`NotebookServiceAsyncClient` |
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
`NotebookServiceAsyncClient` |
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

### get_notebook_execution_job

```
get_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.GetNotebookExecutionJobRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_execution_job.NotebookExecutionJob
```


Gets a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_execution_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [NotebookService.GetNotebookExecutionJob] |
`name` |
Required. The name of the NotebookExecutionJob resource. This corresponds to the |
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
NotebookExecutionJob represents an instance of a notebook execution. |

### get_notebook_runtime

```
get_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.GetNotebookRuntimeRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntime
```


Gets a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_runtime)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.GetNotebookRuntime |
`name` |
Required. The name of the NotebookRuntime resource. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade. |

### get_notebook_runtime_template

```
get_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.GetNotebookRuntimeTemplateRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
```


Gets a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.GetNotebookRuntimeTemplate |
`name` |
Required. The name of the NotebookRuntimeTemplate resource. Format: |
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
A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template. |

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
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport
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

### list_notebook_execution_jobs

```
list_notebook_execution_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookExecutionJobsAsyncPager
)
```


Lists NotebookExecutionJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_notebook_execution_jobs():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookExecutionJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_execution_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_execution_jobs)(request=request)
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
The request object. Request message for [NotebookService.ListNotebookExecutionJobs] |
`parent` |
Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: |
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
Response message for [NotebookService.CreateNotebookExecutionJob] Iterating over this object will yield results and resolve additional pages automatically. |

### list_notebook_runtime_templates

```
list_notebook_runtime_templates(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
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
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesAsyncPager
)
```


Lists NotebookRuntimeTemplates in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_notebook_runtime_templates():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookRuntimeTemplatesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtime_templates](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_runtime_templates)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimeTemplates. |
`parent` |
Required. The resource name of the Location from which to list the NotebookRuntimeTemplates. Format: |
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
Response message for NotebookService.ListNotebookRuntimeTemplates. Iterating over this object will yield results and resolve additional pages automatically. |

### list_notebook_runtimes

```
list_notebook_runtimes(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
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
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimesAsyncPager
)
```


Lists NotebookRuntimes in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_notebook_runtimes():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookRuntimesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtimes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_runtimes)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimes. |
`parent` |
Required. The resource name of the Location from which to list the NotebookRuntimes. Format: |
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
Response message for NotebookService.ListNotebookRuntimes. Iterating over this object will yield results and resolve additional pages automatically. |

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

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### notebook_execution_job_path

```
notebook_execution_job_path(
project: str, location: str, notebook_execution_job: str
) -> str
```


Returns a fully-qualified notebook_execution_job string.

### notebook_runtime_path

`notebook_runtime_path(project: str, location: str, notebook_runtime: str) -> str`


Returns a fully-qualified notebook_runtime string.

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

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_execution_job_path

`parse_notebook_execution_job_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_execution_job path into its component segments.

### parse_notebook_runtime_path

`parse_notebook_runtime_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_schedule_path

`parse_schedule_path(path: str) -> typing.Dict[str, str]`


Parses a schedule path into its component segments.

### parse_subnetwork_path

`parse_subnetwork_path(path: str) -> typing.Dict[str, str]`


Parses a subnetwork path into its component segments.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### schedule_path

`schedule_path(project: str, location: str, schedule: str) -> str`


Returns a fully-qualified schedule string.

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

### start_notebook_runtime

```
start_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.StartNotebookRuntimeRequest,
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


Starts a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_start_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StartNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[start_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_start_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StartNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be started. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### stop_notebook_runtime

```
stop_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.StopNotebookRuntimeRequest,
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


Stops a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_stop_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StopNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[stop_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_stop_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StopNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### subnetwork_path

`subnetwork_path(project: str, region: str, subnetwork: str) -> str`


Returns a fully-qualified subnetwork string.

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

### update_notebook_runtime_template

```
update_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.UpdateNotebookRuntimeTemplateRequest,
dict,
]
] = None,
*,
notebook_runtime_template: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
```


Updates a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1beta1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateNotebookRuntimeTemplateRequest.html)(
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
response = await client.[update_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_update_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.UpdateNotebookRuntimeTemplate. |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to update. This corresponds to the |
`update_mask` |
Required. The update mask applies to the resource. For the |
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
A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template. |

### upgrade_notebook_runtime

```
upgrade_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.UpgradeNotebookRuntimeRequest,
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


Upgrades a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_upgrade_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpgradeNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[upgrade_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_upgrade_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.UpgradeNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be upgrade. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DataLabelingJob.AnnotationLabelsEntry -->

# Class AnnotationLabelsEntry (1.134.0)

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteFeatureValuesPayload.FeatureValuesEntry -->

# Class FeatureValuesEntry (1.134.0)

`FeatureValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### FeatureValuesEntry

`FeatureValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineJob.RuntimeConfig.InputArtifactsEntry -->

# Class InputArtifactsEntry (1.134.0)

`InputArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### InputArtifactsEntry

`InputArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsRequest -->

# Class ListDatasetVersionsRequest (1.134.0)

`ListDatasetVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasetVersions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Dataset to list DatasetVersions from. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`filter` |
`str`
Optional. The standard list filter. |
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. |

## Methods

### ListDatasetVersionsRequest

`ListDatasetVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasetVersions.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PSCAutomationConfig -->

# Class PSCAutomationConfig (1.134.0)

`PSCAutomationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PSC config that is used to automatically create PSC endpoints in the user projects.

## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project id used to create forwarding rule. |
`network` |
`str`
Required. The full name of the Google Compute Engine `network ` __.
`Format ` __:
`projects/{project}/global/networks/{network}` .
|
`ip_address` |
`str`
Output only. IP address rule created by the PSC service automation. |
`forwarding_rule` |
`str`
Output only. Forwarding rule created by the PSC service automation. |
`state` |
Output only. The state of the PSC service automation. |
`error_message` |
`str`
Output only. Error message if the PSC service automation failed. |

## Methods

### PSCAutomationConfig

`PSCAutomationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PSC config that is used to automatically create PSC endpoints in the user projects.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataConfig.AnnotationLabelsEntry -->

# Class AnnotationLabelsEntry (1.134.0)

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction -->

# Class CallToAction (1.134.0)

`CallToAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions could take on this Publisher Model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Classes

### Deploy

`Deploy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata that is needed for UploadModel or DeployModel/CreateEndpoint requests.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### DeployGke

`DeployGke(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations for PublisherModel GKE deployment

### OpenFineTuningPipelines

`OpenFineTuningPipelines(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open fine tuning pipelines.

### OpenNotebooks

`OpenNotebooks(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open notebooks.

### RegionalResourceReferences

`RegionalResourceReferences(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The regional resource name or the URI. Key is region, e.g., us-central1, europe-west2, global, etc..

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ViewRestApi

`ViewRestApi(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rest API docs.

## Methods

### CallToAction

`CallToAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions could take on this Publisher Model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluateInstancesRequest -->

# Class EvaluateInstancesRequest (1.134.0)

`EvaluateInstancesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EvaluationService.EvaluateInstances.

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
`exact_match_input` |
Auto metric instances. Instances and metric spec for exact match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`bleu_input` |
Instances and metric spec for bleu metric. This field is a member of `oneof` _ `metric_inputs` .
|
`rouge_input` |
Instances and metric spec for rouge metric. This field is a member of `oneof` _ `metric_inputs` .
|
`fluency_input` |
LLM-based metric instance. General text generation metrics, applicable to other categories. Input for fluency metric. This field is a member of `oneof` _ `metric_inputs` .
|
`coherence_input` |
Input for coherence metric. This field is a member of `oneof` _ `metric_inputs` .
|
`safety_input` |
Input for safety metric. This field is a member of `oneof` _ `metric_inputs` .
|
`groundedness_input` |
Input for groundedness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`fulfillment_input` |
Input for fulfillment metric. This field is a member of `oneof` _ `metric_inputs` .
|
`summarization_quality_input` |
Input for summarization quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pairwise_summarization_quality_input` |
Input for pairwise summarization quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`summarization_helpfulness_input` |
Input for summarization helpfulness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`summarization_verbosity_input` |
Input for summarization verbosity metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_quality_input` |
Input for question answering quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pairwise_question_answering_quality_input` |
Input for pairwise question answering quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_relevance_input` |
Input for question answering relevance metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_helpfulness_input` |
Input for question answering helpfulness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_correctness_input` |
Input for question answering correctness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pointwise_metric_input` |
Input for pointwise metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pairwise_metric_input` |
Input for pairwise metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_call_valid_input` |
Tool call metric instances. Input for tool call valid metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_name_match_input` |
Input for tool name match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_parameter_key_match_input` |
Input for tool parameter key match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_parameter_kv_match_input` |
Input for tool parameter key value match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`comet_input` |
Translation metrics. Input for Comet metric. This field is a member of `oneof` _ `metric_inputs` .
|
`metricx_input` |
Input for Metricx metric. This field is a member of `oneof` _ `metric_inputs` .
|
`location` |
`str`
Required. The resource name of the Location to evaluate the instances. Format: `projects/{project}/locations/{location}`
|

## Methods

### EvaluateInstancesRequest

`EvaluateInstancesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EvaluationService.EvaluateInstances.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Content -->

# Class Content (1.134.0)

`Content(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The base structured datatype containing multi-part content of a message.

A `Content`

includes a `role`

field designating the producer of
the `Content`

and a `parts`

field containing multi-part data
that contains the content of the message turn.

## Attributes |
|
|---|---|
Name |
Description |
`role` |
`str`
Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset. |
`parts` |
`MutableSequence[`
Required. Ordered `Parts` that constitute a single
message. Parts may have different IANA MIME types.
|

## Methods

### Content

`Content(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The base structured datatype containing multi-part content of a message.

A `Content`

includes a `role`

field designating the producer of
the `Content`

and a `parts`

field containing multi-part data
that contains the content of the message turn.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RaySpec.ResourcePoolImagesEntry -->

# Class ResourcePoolImagesEntry (1.134.0)

`ResourcePoolImagesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ResourcePoolImagesEntry

`ResourcePoolImagesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolCallValidInstance -->

# Class ToolCallValidInstance (1.134.0)

`ToolCallValidInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid instance.

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
Required. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|

## Methods

### ToolCallValidInstance

`ToolCallValidInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolNameMatchInstance -->

# Class ToolNameMatchInstance (1.134.0)

`ToolNameMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match instance.

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
Required. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|

## Methods

### ToolNameMatchInstance

`ToolNameMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.NumericTransformation -->

# Class NumericTransformation (1.134.0)

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

## Attribute |
|
|---|---|
Name |
Description |
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseChoice -->

# Class PairwiseChoice (1.134.0)

`PairwiseChoice(value)`


Pairwise prediction autorater preference.

## Enums |
|
|---|---|
Name |
Description |
`PAIRWISE_CHOICE_UNSPECIFIED` |
Unspecified prediction choice. |
`BASELINE` |
Baseline prediction wins |
`CANDIDATE` |
Candidate prediction wins |
`TIE` |
Winner cannot be determined |

## Methods

### PairwiseChoice

`PairwiseChoice(value)`


Pairwise prediction autorater preference.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardUsageResponse.PerMonthUsageData -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.RoutingConfig.ManualRoutingMode -->

# Class ManualRoutingMode (1.134.0)

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
The model name to use. Only the public LLM models are accepted. e.g. 'gemini-1.5-pro-001'. This field is a member of `oneof` _ `_model_name` .
|

## Methods

### ManualRoutingMode

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxResult -->

# Class MetricxResult (1.134.0)

`MetricxResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX result - calculates the MetricX score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. MetricX score. Range depends on version. This field is a member of `oneof` _ `_score` .
|

## Methods

### MetricxResult

`MetricxResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX result - calculates the MetricX score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EntityIdSelector -->

# Class EntityIdSelector (1.134.0)

`EntityIdSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for entityId. Getting ids from the given source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`csv_source` |
Source of Csv This field is a member of `oneof` _ `EntityIdsSource` .
|
`entity_id_field` |
`str`
Source column that holds entity IDs. If not provided, entity IDs are extracted from the column named entity_id. |

## Methods

### EntityIdSelector

`EntityIdSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for entityId. Getting ids from the given source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeArtifact.CustomPropertiesEntry -->

# Class CustomPropertiesEntry (1.134.0)

`CustomPropertiesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### CustomPropertiesEntry

`CustomPropertiesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadRagFileConfig -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringAlertConfig.EmailAlertConfig -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CopyModelRequest -->

# Class CopyModelRequest (1.134.0)

`CopyModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.CopyModel.

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
`model_id` |
`str`
Optional. Copy source_model into a new Model with this ID. The ID will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
This field is a member of `oneof` _ `destination_model` .
|
`parent_model` |
`str`
Optional. Specify this field to copy source_model into this existing Model as a new version. Format: `projects/{project}/locations/{location}/models/{model}`
This field is a member of `oneof` _ `destination_model` .
|
`parent` |
`str`
Required. The resource name of the Location into which to copy the Model. Format: `projects/{project}/locations/{location}`
|
`source_model` |
`str`
Required. The resource name of the Model to copy. That Model must be in the same Project. Format: `projects/{project}/locations/{location}/models/{model}`
|
`encryption_spec` |
Customer-managed encryption key options. If this is set, then the Model copy will be encrypted with the provided encryption key. |

## Methods

### CopyModelRequest

`CopyModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.CopyModel.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.InputArtifactsEntry -->

# Class InputArtifactsEntry (1.134.0)

`InputArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### InputArtifactsEntry

`InputArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DataLabelingJob.AnnotationLabelsEntry -->

# Class AnnotationLabelsEntry (1.134.0)

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineJob.RuntimeConfig.ParameterValuesEntry -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataConfig.AnnotationLabelsEntry -->

# Class AnnotationLabelsEntry (1.134.0)

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAlertCondition -->

# Class ModelMonitoringAlertCondition (1.134.0)

```
ModelMonitoringAlertCondition(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Monitoring alert triggered condition.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`threshold` |
`float`
A condition that compares a stats value against a threshold. Alert will be triggered if value above the threshold. This field is a member of `oneof` _ `condition` .
|

## Methods

### ModelMonitoringAlertCondition

```
ModelMonitoringAlertCondition(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Monitoring alert triggered condition.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsRequest -->

# Class ListDatasetVersionsRequest (1.134.0)

`ListDatasetVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasetVersions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Dataset to list DatasetVersions from. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`filter` |
`str`
Optional. The standard list filter. |
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. |

## Methods

### ListDatasetVersionsRequest

`ListDatasetVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasetVersions.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.dataset_service.pagers`

module.

## Classes

[ListAnnotationsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListAnnotationsAsyncPager)

```
ListAnnotationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse,
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


A pager for iterating through `list_annotations`

requests.

This class thinly wraps an initial
[ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse) object, and
provides an `__aiter__`

method to iterate through its
`annotations`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListAnnotations`

requests and continue to iterate
through the `annotations`

field on the
corresponding responses.

All the usual [ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListAnnotationsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListAnnotationsPager)

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

[ListDataItemsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDataItemsAsyncPager)

```
ListDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse,
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


A pager for iterating through `list_data_items`

requests.

This class thinly wraps an initial
[ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsResponse) object, and
provides an `__aiter__`

method to iterate through its
`data_items`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDataItems`

requests and continue to iterate
through the `data_items`

field on the
corresponding responses.

All the usual [ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDataItemsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDataItemsPager)

```
ListDataItemsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse,
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
[ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsResponse) object, and
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

All the usual [ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDatasetVersionsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetVersionsAsyncPager)

```
ListDatasetVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse,
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


A pager for iterating through `list_dataset_versions`

requests.

This class thinly wraps an initial
[ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`dataset_versions`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDatasetVersions`

requests and continue to iterate
through the `dataset_versions`

field on the
corresponding responses.

All the usual [ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDatasetVersionsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetVersionsPager)

```
ListDatasetVersionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse,
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse,
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


A pager for iterating through `list_dataset_versions`

requests.

This class thinly wraps an initial
[ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsResponse) object, and
provides an `__iter__`

method to iterate through its
`dataset_versions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDatasetVersions`

requests and continue to iterate
through the `dataset_versions`

field on the
corresponding responses.

All the usual [ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDatasetsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetsAsyncPager)

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

[ListDatasetsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetsPager)

```
ListDatasetsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse,
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
[ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsResponse) object, and
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

All the usual [ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListSavedQueriesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListSavedQueriesAsyncPager)

```
ListSavedQueriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse,
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


A pager for iterating through `list_saved_queries`

requests.

This class thinly wraps an initial
[ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSavedQueriesResponse) object, and
provides an `__aiter__`

method to iterate through its
`saved_queries`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSavedQueries`

requests and continue to iterate
through the `saved_queries`

field on the
corresponding responses.

All the usual [ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSavedQueriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListSavedQueriesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListSavedQueriesPager)

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

[SearchDataItemsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.SearchDataItemsAsyncPager)

```
SearchDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse,
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


A pager for iterating through `search_data_items`

requests.

This class thinly wraps an initial
[SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsResponse) object, and
provides an `__aiter__`

method to iterate through its
`data_item_views`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchDataItems`

requests and continue to iterate
through the `data_item_views`

field on the
corresponding responses.

All the usual [SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchDataItemsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.SearchDataItemsPager)

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CopyModelRequest -->

# Class CopyModelRequest (1.134.0)

`CopyModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.CopyModel.

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
`model_id` |
`str`
Optional. Copy source_model into a new Model with this ID. The ID will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
This field is a member of `oneof` _ `destination_model` .
|
`parent_model` |
`str`
Optional. Specify this field to copy source_model into this existing Model as a new version. Format: `projects/{project}/locations/{location}/models/{model}`
This field is a member of `oneof` _ `destination_model` .
|
`parent` |
`str`
Required. The resource name of the Location into which to copy the Model. Format: `projects/{project}/locations/{location}`
|
`source_model` |
`str`
Required. The resource name of the Model to copy. That Model must be in the same Project. Format: `projects/{project}/locations/{location}/models/{model}`
|
`encryption_spec` |
Customer-managed encryption key options. If this is set, then the Model copy will be encrypted with the provided encryption key. |

## Methods

### CopyModelRequest

`CopyModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.CopyModel.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Content -->

# Class Content (1.134.0)

`Content(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The base structured datatype containing multi-part content of a message.

A `Content`

includes a `role`

field designating the producer of
the `Content`

and a `parts`

field containing multi-part data
that contains the content of the message turn.

## Attributes |
|
|---|---|
Name |
Description |
`role` |
`str`
Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset. |
`parts` |
`MutableSequence[`
Required. Ordered `Parts` that constitute a single
message. Parts may have different IANA MIME types.
|

## Methods

### Content

`Content(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The base structured datatype containing multi-part content of a message.

A `Content`

includes a `role`

field designating the producer of
the `Content`

and a `parts`

field containing multi-part data
that contains the content of the message turn.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RaySpec.ResourcePoolImagesEntry -->

# Class ResourcePoolImagesEntry (1.134.0)

`ResourcePoolImagesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ResourcePoolImagesEntry

`ResourcePoolImagesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PartnerModelTuningSpec.HyperParametersEntry -->

# Class HyperParametersEntry (1.134.0)

`HyperParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### HyperParametersEntry

`HyperParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadFeatureValuesRequest -->

# Class ReadFeatureValuesRequest (1.134.0)

`ReadFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.ReadFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
Required. The resource name of the EntityType for the entity being read. Value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .
For example, for a machine learning model predicting user
clicks on a website, an EntityType ID could be `user` .
|
`entity_id` |
`str`
Required. ID for a specific entity. For example, for a machine learning model predicting user clicks on a website, an entity ID could be `user_123` .
|
`feature_selector` |
Required. Selector choosing Features of the target EntityType. |

## Methods

### ReadFeatureValuesRequest

`ReadFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.ReadFeatureValues.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchInstance -->

# Class ToolNameMatchInstance (1.134.0)

`ToolNameMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match instance.

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
Required. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|

## Methods

### ToolNameMatchInstance

`ToolNameMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidInstance -->

# Class ToolCallValidInstance (1.134.0)

`ToolCallValidInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid instance.

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
Required. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|

## Methods

### ToolCallValidInstance

`ToolCallValidInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.NumericTransformation -->

# Class NumericTransformation (1.134.0)

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

## Attribute |
|
|---|---|
Name |
Description |
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageClassificationPredictionInstance -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeResponse -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchResults -->

# Class ExactMatchResults (1.134.0)

`ExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for exact match metric.

## Attribute |
|
|---|---|
Name |
Description |
`exact_match_metric_values` |
`MutableSequence[`
Output only. Exact match metric values. |

## Methods

### ExactMatchResults

`ExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for exact match metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TuningJob -->

# Class TuningJob (1.134.0)

`TuningJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a TuningJob that runs with Google owned models.

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
`base_model` |
`str`
The base model that is being tuned. See `Supported models |
`pre_tuned_model` |
The pre-tuned model for continuous tuning. This field is a member of `oneof` _ `source_model` .
|
`supervised_tuning_spec` |
Tuning Spec for Supervised Fine Tuning. This field is a member of `oneof` _ `tuning_spec` .
|
`name` |
`str`
Output only. Identifier. Resource name of a TuningJob. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}`
|
`tuned_model_display_name` |
`str`
Optional. The display name of the TunedModel. The name can be up to 128 characters long and can consist of any UTF-8 characters. For continuous tuning, tuned_model_display_name will by default use the same display name as the pre-tuned model. If a new display name is provided, the tuning job will create a new model instead of a new version. |
`description` |
`str`
Optional. The description of the TuningJob. |
`state` |
Output only. The detailed state of the job. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TuningJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TuningJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TuningJob entered any of the following JobStates: `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` ,
`JOB_STATE_CANCELLED` , `JOB_STATE_EXPIRED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TuningJob was most recently updated. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .
|
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize TuningJob and generated resources such as Model and Endpoint. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`experiment` |
`str`
Output only. The Experiment associated with this TuningJob. |
`tuned_model` |
Output only. The tuned model resources associated with this TuningJob. |
`tuning_data_stats` |
Output only. The tuning data statistics associated with this TuningJob. |
`encryption_spec` |
Customer-managed encryption key options for a TuningJob. If this is set, then all resources created by the TuningJob will be encrypted with the provided encryption key. |
`service_account` |
`str`
The service account that the tuningJob workload runs as. If not specified, the Vertex AI Secure Fine-Tuned Service Agent in the project will be used. See https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-agent Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service
account.
|

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

### TuningJob

`TuningJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a TuningJob that runs with Google owned models.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient -->

# Class SpecialistPoolServiceClient (1.134.0)

```
SpecialistPoolServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Customer SpecialistPools. When customers start Data Labeling jobs, they can reuse/create Specialist Pools to bring their own Specialists to label the data. Customers can add/remove Managers for the Specialist Pool on Cloud console, then Managers will get email notifications to manage Specialists and tasks on CrowdCompute console.

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
`SpecialistPoolServiceTransport` |
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

### SpecialistPoolServiceClient

```
SpecialistPoolServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the specialist pool service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,SpecialistPoolServiceTransport,Callable[..., SpecialistPoolServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the SpecialistPoolServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_specialist_pool

```
create_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.specialist_pool_service.CreateSpecialistPoolRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
specialist_pool: typing.Optional[
google.cloud.aiplatform_v1.types.specialist_pool.SpecialistPool
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


Creates a SpecialistPool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
specialist_pool = aiplatform_v1.[SpecialistPool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpecialistPool.html)()
specialist_pool.name = "name_value"
specialist_pool.display_name = "display_name_value"
request = aiplatform_v1.[CreateSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateSpecialistPoolRequest.html)(
parent="parent_value",
specialist_pool=specialist_pool,
)
# Make the request
operation = client.[create_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceClient_create_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.CreateSpecialistPool. |
`parent` |
`str`
Required. The parent Project name for the new SpecialistPool. The form is |
`specialist_pool` |
Required. The SpecialistPool to create. This corresponds to the |
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

### delete_specialist_pool

```
delete_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.specialist_pool_service.DeleteSpecialistPoolRequest,
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


Deletes a SpecialistPool as well as all Specialists in the pool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteSpecialistPoolRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceClient_delete_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.DeleteSpecialistPool. |
`name` |
`str`
Required. The resource name of the SpecialistPool to delete. Format: |
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
`SpecialistPoolServiceClient` |
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
`SpecialistPoolServiceClient` |
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
`SpecialistPoolServiceClient` |
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

### get_specialist_pool

```
get_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.specialist_pool_service.GetSpecialistPoolRequest,
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
) -> google.cloud.aiplatform_v1.types.specialist_pool.SpecialistPool
```


Gets a SpecialistPool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetSpecialistPoolRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceClient_get_specialist_pool)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for SpecialistPoolService.GetSpecialistPool. |
`name` |
`str`
Required. The name of the SpecialistPool resource. The form is |
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
SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console. |

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

### list_specialist_pools

```
list_specialist_pools(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
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
google.cloud.aiplatform_v1.services.specialist_pool_service.pagers.ListSpecialistPoolsPager
)
```


Lists SpecialistPools in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_specialist_pools():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListSpecialistPoolsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_specialist_pools](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceClient_list_specialist_pools)(request=request)
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
The request object. Request message for SpecialistPoolService.ListSpecialistPools. |
`parent` |
`str`
Required. The name of the SpecialistPool's parent resource. Format: |
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
Response message for SpecialistPoolService.ListSpecialistPools. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_specialist_pool_path

`parse_specialist_pool_path(path: str) -> typing.Dict[str, str]`


Parses a specialist_pool path into its component segments.

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

### specialist_pool_path

`specialist_pool_path(project: str, location: str, specialist_pool: str) -> str`


Returns a fully-qualified specialist_pool string.

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

### update_specialist_pool

```
update_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.specialist_pool_service.UpdateSpecialistPoolRequest,
dict,
]
] = None,
*,
specialist_pool: typing.Optional[
google.cloud.aiplatform_v1.types.specialist_pool.SpecialistPool
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


Updates a SpecialistPool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
specialist_pool = aiplatform_v1.[SpecialistPool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpecialistPool.html)()
specialist_pool.name = "name_value"
specialist_pool.display_name = "display_name_value"
request = aiplatform_v1.[UpdateSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateSpecialistPoolRequest.html)(
specialist_pool=specialist_pool,
)
# Make the request
operation = client.[update_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceClient_update_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.UpdateSpecialistPool. |
`specialist_pool` |
Required. The SpecialistPool which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. This corresponds to the |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient -->

# Class GenAiTuningServiceClient (1.134.0)

```
GenAiTuningServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing GenAI Tuning Jobs.

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
`GenAiTuningServiceTransport` |
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

### GenAiTuningServiceClient

```
GenAiTuningServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the gen ai tuning service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,GenAiTuningServiceTransport,Callable[..., GenAiTuningServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the GenAiTuningServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### cancel_tuning_job

```
cancel_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.CancelTuningJobRequest,
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


Cancels a TuningJob. Starts asynchronous cancellation on the
TuningJob. The server makes a best effort to cancel the job, but
success is not guaranteed. Clients can use
xref_GenAiTuningService.GetTuningJob
or other methods to check whether the cancellation succeeded or
whether the job completed despite cancellation. On successful
cancellation, the TuningJob is not deleted; instead it becomes a
job with a
xref_TuningJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_TuningJob.state
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
def sample_cancel_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelTuningJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceClient_cancel_tuning_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.CancelTuningJob. |
`name` |
`str`
Required. The name of the TuningJob to cancel. Format: |
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

### create_tuning_job

```
create_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.CreateTuningJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tuning_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tuning_job.TuningJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.tuning_job.TuningJob
```


Creates a TuningJob. A created TuningJob right away will be attempted to be run.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
tuning_job = aiplatform_v1beta1.[TuningJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TuningJob.html)()
tuning_job.base_model = "base_model_value"
tuning_job.supervised_tuning_spec.training_dataset_uri = "training_dataset_uri_value"
request = aiplatform_v1beta1.[CreateTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTuningJobRequest.html)(
parent="parent_value",
tuning_job=tuning_job,
)
# Make the request
response = client.[create_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceClient_create_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.CreateTuningJob. |
`parent` |
`str`
Required. The resource name of the Location to create the TuningJob in. Format: |
`tuning_job` |
Required. The TuningJob to create. This corresponds to the |
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
Represents a TuningJob that runs with Google owned models. |

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
`GenAiTuningServiceClient` |
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
`GenAiTuningServiceClient` |
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
`GenAiTuningServiceClient` |
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

### get_tuning_job

```
get_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.GetTuningJobRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.tuning_job.TuningJob
```


Gets a TuningJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTuningJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceClient_get_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.GetTuningJob. |
`name` |
`str`
Required. The name of the TuningJob resource. Format: |
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
Represents a TuningJob that runs with Google owned models. |

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

### list_tuning_jobs

```
list_tuning_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.pagers.ListTuningJobsPager
)
```


Lists TuningJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_tuning_jobs():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTuningJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tuning_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceClient_list_tuning_jobs)(request=request)
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
The request object. Request message for GenAiTuningService.ListTuningJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the TuningJobs from. Format: |
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
Response message for GenAiTuningService.ListTuningJobs Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_context_path

`parse_context_path(path: str) -> typing.Dict[str, str]`


Parses a context path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_tuning_job_path

`parse_tuning_job_path(path: str) -> typing.Dict[str, str]`


Parses a tuning_job path into its component segments.

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

### rebase_tuned_model

```
rebase_tuned_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.RebaseTunedModelRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tuned_model_ref: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tuning_job.TunedModelRef
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


Rebase a TunedModel. Creates a LongRunningOperation that takes a legacy Tuned GenAI model Reference and creates a TuningJob based on newly available model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_rebase_tuned_model():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
tuned_model_ref = aiplatform_v1beta1.[TunedModelRef](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TunedModelRef.html)()
tuned_model_ref.tuned_model = "tuned_model_value"
request = aiplatform_v1beta1.[RebaseTunedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebaseTunedModelRequest.html)(
parent="parent_value",
tuned_model_ref=tuned_model_ref,
)
# Make the request
operation = client.[rebase_tuned_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceClient_rebase_tuned_model)(request=request)
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
The request object. Request message for GenAiTuningService.RebaseTunedModel. |
`parent` |
`str`
Required. The resource name of the Location into which to rebase the Model. Format: |
`tuned_model_ref` |
Required. TunedModel reference to retrieve the legacy model information. This corresponds to the |
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

### tuning_job_path

`tuning_job_path(project: str, location: str, tuning_job: str) -> str`


Returns a fully-qualified tuning_job string.

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service -->

# Package pipeline_service (1.134.0)

API documentation for `aiplatform_v1.services.pipeline_service`

package.

## Classes

[PipelineServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceAsyncClient)

A service for creating and managing Vertex AI's pipelines. This
includes both `TrainingPipeline`

resources (used for AutoML and
custom training) and `PipelineJob`

resources (used for Vertex AI
Pipelines).

[PipelineServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient)

A service for creating and managing Vertex AI's pipelines. This
includes both `TrainingPipeline`

resources (used for AutoML and
custom training) and `PipelineJob`

resources (used for Vertex AI
Pipelines).

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers)

API documentation for `aiplatform_v1.services.pipeline_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.RegionalResourceReferences.ReferencesEntry -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DistillationSpec -->

# Class DistillationSpec (1.134.0)

`DistillationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning Spec for Distillation.

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
`base_teacher_model` |
`str`
The base teacher model that is being distilled. See `Supported models |
`tuned_teacher_model_source` |
`str`
The resource name of the Tuned teacher model. Format: `projects/{project}/locations/{location}/models/{model}` .
This field is a member of `oneof` _ `teacher_model` .
|
`training_dataset_uri` |
`str`
Required. Cloud Storage path to file containing training dataset for tuning. The dataset must be formatted as a JSONL file. |
`validation_dataset_uri` |
`str`
Optional. Cloud Storage path to file containing validation dataset for tuning. The dataset must be formatted as a JSONL file. This field is a member of `oneof` _ `_validation_dataset_uri` .
|
`hyper_parameters` |
Optional. Hyperparameters for Distillation. |
`student_model` |
`str`
The student model that is being tuned, e.g., "google/gemma-2b-1.1-it". |
`pipeline_root_directory` |
`str`
Required. A path in a Cloud Storage bucket, which will be treated as the root output directory of the distillation pipeline. It is used by the system to generate the paths of output artifacts. |

## Methods

### DistillationSpec

`DistillationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning Spec for Distillation.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.DeploymentSpec.ResourceLimitsEntry -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.ParameterValuesEntry -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborSearchOperationMetadata.ContentValidationStats -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis.State -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig.RoutingConfig -->

# Class RoutingConfig (1.134.0)

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

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
`auto_mode` |
Automated routing. This field is a member of `oneof` _ `routing_config` .
|
`manual_mode` |
Manual routing. This field is a member of `oneof` _ `routing_config` .
|

## Classes

### AutoRoutingMode

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ManualRoutingMode

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RoutingConfig

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadFeatureValuesRequest -->

# Class ReadFeatureValuesRequest (1.134.0)

`ReadFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.ReadFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
Required. The resource name of the EntityType for the entity being read. Value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .
For example, for a machine learning model predicting user
clicks on a website, an EntityType ID could be `user` .
|
`entity_id` |
`str`
Required. ID for a specific entity. For example, for a machine learning model predicting user clicks on a website, an entity ID could be `user_123` .
|
`feature_selector` |
Required. Selector choosing Features of the target EntityType. |

## Methods

### ReadFeatureValuesRequest

`ReadFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.ReadFeatureValues.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageObjectDetectionPredictionInstance -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Presets.Modality -->

# Class Modality (1.134.0)

`Modality(value)`


Preset option controlling parameters for different modalities

## Enums |
|
|---|---|
Name |
Description |
`MODALITY_UNSPECIFIED` |
Should not be set. Added as a recommended best practice for enums |
`IMAGE` |
IMAGE modality |
`TEXT` |
TEXT modality |
`TABULAR` |
TABULAR modality |

## Methods

### Modality

`Modality(value)`


Preset option controlling parameters for different modalities

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesResponse -->

# Class BatchReadFeatureValuesResponse (1.134.0)

```
BatchReadFeatureValuesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeaturestoreService.BatchReadFeatureValues.

## Methods

### BatchReadFeatureValuesResponse

```
BatchReadFeatureValuesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeaturestoreService.BatchReadFeatureValues.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardUsageResponse.MonthlyUsageDataEntry -->

# Class MonthlyUsageDataEntry (1.134.0)

`MonthlyUsageDataEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### MonthlyUsageDataEntry

`MonthlyUsageDataEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Neighbor -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardUsageResponse.PerMonthUsageData -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.DeploymentSpec.ResourceLimitsEntry -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsRequest -->

# Class ListDeploymentResourcePoolsRequest (1.134.0)

```
ListDeploymentResourcePoolsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ListDeploymentResourcePools method.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent Location which owns this collection of DeploymentResourcePools. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
The maximum number of DeploymentResourcePools to return. The service may return fewer than this value. |
`page_token` |
`str`
A page token, received from a previous `ListDeploymentResourcePools` call. Provide this to
retrieve the subsequent page.
When paginating, all other parameters provided to
`ListDeploymentResourcePools` must match the call that
provided the page token.
|

## Methods

### ListDeploymentResourcePoolsRequest

```
ListDeploymentResourcePoolsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ListDeploymentResourcePools method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.RegionalResourceReferences.ReferencesEntry -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.RoutingConfig -->

# Class RoutingConfig (1.134.0)

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

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
`auto_mode` |
Automated routing. This field is a member of `oneof` _ `routing_config` .
|
`manual_mode` |
Manual routing. This field is a member of `oneof` _ `routing_config` .
|

## Classes

### AutoRoutingMode

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ManualRoutingMode

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RoutingConfig

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FulfillmentResult -->

# Class FulfillmentResult (1.134.0)

`FulfillmentResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Fulfillment score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for fulfillment score. |
`confidence` |
`float`
Output only. Confidence for fulfillment score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### FulfillmentResult

`FulfillmentResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportFeatureValuesResponse -->

# Class ImportFeatureValuesResponse (1.134.0)

`ImportFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ImportFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`imported_entity_count` |
`int`
Number of entities that have been imported by the operation. |
`imported_feature_value_count` |
`int`
Number of Feature values that have been imported by the operation. |
`invalid_row_count` |
`int`
The number of rows in input source that weren't imported due to either - Not having any featureValues. - Having a null entityId. - Having a null timestamp. - Not being parsable (applicable for CSV sources). |
`timestamp_outside_retention_rows_count` |
`int`
The number rows that weren't ingested due to having feature timestamps outside the retention boundary. |

## Methods

### ImportFeatureValuesResponse

`ImportFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ImportFeatureValues.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskRerunConfig.Inputs.ParameterValuesEntry -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis.State -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborSearchOperationMetadata.ContentValidationStats -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TabularClassificationPredictionResult -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Session -->

# Class Session (1.134.0)

`Session(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A session contains a set of actions between users and Vertex agents.

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
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Timestamp of when this session is considered expired. This is *always* provided on output, regardless of what was sent on input. This field is a member of `oneof` _ `expiration` .
|
`ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. Input only. The TTL for this session. This field is a member of `oneof` _ `expiration` .
|
`name` |
`str`
Identifier. The resource name of the session. Format: 'projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}'. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the session was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the session was updated. |
`display_name` |
`str`
Optional. The display name of the session. |
`session_state` |
`google.protobuf.struct_pb2.Struct`
Optional. Session specific memory which stores key conversation points. |
`user_id` |
`str`
Required. Immutable. String id provided by the user |

## Methods

### Session

`Session(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A session contains a set of actions between users and Vertex agents.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SharePointSources.SharePointSource -->

# Class SharePointSource (1.134.0)

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

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
`sharepoint_folder_path` |
`str`
The path of the SharePoint folder to download from. This field is a member of `oneof` _ `folder_source` .
|
`sharepoint_folder_id` |
`str`
The ID of the SharePoint folder to download from. This field is a member of `oneof` _ `folder_source` .
|
`drive_name` |
`str`
The name of the drive to download from. This field is a member of `oneof` _ `drive_source` .
|
`drive_id` |
`str`
The ID of the drive to download from. This field is a member of `oneof` _ `drive_source` .
|
`client_id` |
`str`
The Application ID for the app registered in Microsoft Azure Portal. The application must also be configured with MS Graph permissions "Files.ReadAll", "Sites.ReadAll" and BrowserSiteLists.Read.All. |
`client_secret` |
The application secret for the app registered in Azure. |
`tenant_id` |
`str`
Unique identifier of the Azure Active Directory Instance. |
`sharepoint_site_name` |
`str`
The name of the SharePoint site to download from. This can be the site name or the site id. |
`file_id` |
`str`
Output only. The SharePoint file id. Output only. |

## Methods

### SharePointSource

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAlertConfig.EmailAlertConfig -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Port -->

# Class Port (1.134.0)

`Port(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a network port in a container.

## Attribute |
|
|---|---|
Name |
Description |
`container_port` |
`int`
The number of the port to expose on the pod's IP address. Must be a valid port number, between 1 and 65535 inclusive. |

## Methods

### Port

`Port(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a network port in a container.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardTimeSeriesDataRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient -->

# Class ReasoningEngineServiceClient (1.134.0)

```
ReasoningEngineServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's Reasoning Engines.

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
`ReasoningEngineServiceTransport` |
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

### ReasoningEngineServiceClient

```
ReasoningEngineServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the reasoning engine service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ReasoningEngineServiceTransport,Callable[..., ReasoningEngineServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the ReasoningEngineServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_reasoning_engine

```
create_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_service.CreateReasoningEngineRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
reasoning_engine: typing.Optional[
google.cloud.aiplatform_v1.types.reasoning_engine.ReasoningEngine
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


Creates a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient.html)()
# Initialize request argument(s)
reasoning_engine = aiplatform_v1.[ReasoningEngine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngine.html)()
reasoning_engine.display_name = "display_name_value"
request = aiplatform_v1.[CreateReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateReasoningEngineRequest.html)(
parent="parent_value",
reasoning_engine=reasoning_engine,
)
# Make the request
operation = client.[create_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_service_ReasoningEngineServiceClient_create_reasoning_engine)(request=request)
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
The request object. Request message for ReasoningEngineService.CreateReasoningEngine. |
`parent` |
`str`
Required. The resource name of the Location to create the ReasoningEngine in. Format: |
`reasoning_engine` |
Required. The ReasoningEngine to create. This corresponds to the |
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

### delete_reasoning_engine

```
delete_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_service.DeleteReasoningEngineRequest,
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


Deletes a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_service_ReasoningEngineServiceClient_delete_reasoning_engine)(request=request)
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
The request object. Request message for ReasoningEngineService.DeleteReasoningEngine. |
`name` |
`str`
Required. The name of the ReasoningEngine resource to be deleted. Format: |
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
`ReasoningEngineServiceClient` |
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
`ReasoningEngineServiceClient` |
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
`ReasoningEngineServiceClient` |
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

### get_reasoning_engine

```
get_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_service.GetReasoningEngineRequest,
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
) -> google.cloud.aiplatform_v1.types.reasoning_engine.ReasoningEngine
```


Gets a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_service_ReasoningEngineServiceClient_get_reasoning_engine)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ReasoningEngineService.GetReasoningEngine. |
`name` |
`str`
Required. The name of the ReasoningEngine resource. Format: |
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
ReasoningEngine provides a customizable runtime for models to determine which actions to take and in which order. |

### git_repository_link_path

```
git_repository_link_path(
project: str, location: str, connection: str, git_repository_link: str
) -> str
```


Returns a fully-qualified git_repository_link string.

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

### list_reasoning_engines

```
list_reasoning_engines(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
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
google.cloud.aiplatform_v1.services.reasoning_engine_service.pagers.ListReasoningEnginesPager
)
```


Lists reasoning engines in a location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_reasoning_engines():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListReasoningEnginesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_reasoning_engines](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_service_ReasoningEngineServiceClient_list_reasoning_engines)(request=request)
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
The request object. Request message for ReasoningEngineService.ListReasoningEngines. |
`parent` |
`str`
Required. The resource name of the Location to list the ReasoningEngines from. Format: |
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
Response message for ReasoningEngineService.ListReasoningEngines Iterating over this object will yield results and resolve additional pages automatically. |

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

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

### parse_git_repository_link_path

`parse_git_repository_link_path(path: str) -> typing.Dict[str, str]`


Parses a git_repository_link path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### reasoning_engine_path

`reasoning_engine_path(project: str, location: str, reasoning_engine: str) -> str`


Returns a fully-qualified reasoning_engine string.

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

### update_reasoning_engine

```
update_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_service.UpdateReasoningEngineRequest,
dict,
]
] = None,
*,
reasoning_engine: typing.Optional[
google.cloud.aiplatform_v1.types.reasoning_engine.ReasoningEngine
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


Updates a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient.html)()
# Initialize request argument(s)
reasoning_engine = aiplatform_v1.[ReasoningEngine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngine.html)()
reasoning_engine.display_name = "display_name_value"
request = aiplatform_v1.[UpdateReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateReasoningEngineRequest.html)(
reasoning_engine=reasoning_engine,
)
# Make the request
operation = client.[update_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_service_ReasoningEngineServiceClient_update_reasoning_engine)(request=request)
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
The request object. Request message for ReasoningEngineService.UpdateReasoningEngine. |
`reasoning_engine` |
Required. The ReasoningEngine which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to update. This corresponds to the |
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
