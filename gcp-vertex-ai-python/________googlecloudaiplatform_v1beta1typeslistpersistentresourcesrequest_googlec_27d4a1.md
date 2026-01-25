---
merged_at: 2026-01-25T21:47:44.375886
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1beta1typeslistpersistentresourcesrequest_googlecl_2707a3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typeslistpersistentresourcesrequest_googleclo_8b1f01.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typeslistpersistentresourcesrequest_googleclou_8bf400.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typeslistpersistentresourcesrequest_googlecloud_d25b2e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistpersistentresourcesrequest_googleclouda_3831b0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistpersistentresourcesrequest_googlecloudai_068128.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistpersistentresourcesrequest_googlecloudaip_5ebafd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistpersistentresourcesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesRequest -->

# Class ListPersistentResourcesRequest (1.134.0)

```
ListPersistentResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [PersistentResourceService.ListPersistentResource][].

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the PersistentResources from. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via [ListPersistentResourceResponse.next_page_token][] of the previous [PersistentResourceService.ListPersistentResource][] call. |

## Methods

### ListPersistentResourcesRequest

```
ListPersistentResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [PersistentResourceService.ListPersistentResource][].


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfetchfeaturevaluesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FetchFeatureValuesRequest -->

# Class FetchFeatureValuesRequest (1.134.0)

`FetchFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreService.FetchFeatureValues. All the features under the requested feature view will be returned.

## Attributes |
|
|---|---|
Name |
Description |
`feature_view` |
`str`
Required. FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`
|
`data_key` |
Optional. The request key to fetch feature values for. |
`data_format` |
Optional. Response data format. If not set, FeatureViewDataFormat.KEY_VALUE will be used. |

## Methods

### FetchFeatureValuesRequest

`FetchFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreService.FetchFeatureValues. All the features under the requested feature view will be returned.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespipelinejobruntimeconfigdefaultruntime_google_242bfb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinejobruntimeconfigdefaultruntime.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.DefaultRuntime -->

# Class DefaultRuntime (1.134.0)

`DefaultRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The default runtime for the PipelineJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`persistent_resource_runtime_detail` |
Persistent resource based runtime detail. This field is a member of `oneof` _ `runtime_detail` .
|

## Methods

### DefaultRuntime

`DefaultRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The default runtime for the PipelineJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureonlinestorebigtableautoscaling.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.Bigtable.AutoScaling -->

# Class AutoScaling (1.134.0)

`AutoScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`min_node_count` |
`int`
Required. The minimum number of nodes to scale down to. Must be greater than or equal to 1. |
`max_node_count` |
`int`
Required. The maximum number of nodes to scale up to. Must be greater than or equal to min_node_count, and less than or equal to 10 times of 'min_node_count'. |
`cpu_utilization_target` |
`int`
Optional. A percentage of the cluster's CPU capacity. Can be from 10% to 80%. When a cluster's CPU utilization exceeds the target that you have set, Bigtable immediately adds nodes to the cluster. When CPU utilization is substantially lower than the target, Bigtable removes nodes. If not set will default to 50%. |

## Methods

### AutoScaling

`AutoScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesstreamingpredictrequest_googlecloudaiplatform_v1b_9b3b4e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstreamingpredictrequest_googlecloudaiplatform_v1be_b35605.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstreamingpredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamingPredictRequest -->

# Class StreamingPredictRequest (1.134.0)

`StreamingPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingPredict.

The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][].

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`inputs` |
`MutableSequence[`
The prediction input. |
`parameters` |
The parameters that govern the prediction. |

## Methods

### StreamingPredictRequest

`StreamingPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingPredict.

The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][].


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeswritefeaturevaluesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteFeatureValuesRequest -->

# Class WriteFeatureValuesRequest (1.134.0)

`WriteFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.WriteFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
Required. The resource name of the EntityType for the entities being written. Value format: `projects/{project}/locations/{location}/featurestores/ {featurestore}/entityTypes/{entityType}` .
For example, for a machine learning model predicting user
clicks on a website, an EntityType ID could be `user` .
|
`payloads` |
`MutableSequence[`
Required. The entities to be written. Up to 100,000 feature values can be written across all `payloads` .
|

## Methods

### WriteFeatureValuesRequest

`WriteFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.WriteFeatureValues.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlimageclassificationinputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationInputs -->

# Class AutoMlImageClassificationInputs (1.134.0)

```
AutoMlImageClassificationInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`base_model_id` |
`str`
The ID of the `base` model. If it is specified, the new
model will be trained based on the `base` model.
Otherwise, the new model will be trained from scratch. The
`base` model must be in the same Project and Location as
the new Model to train, and have the same modelType.
|
`budget_milli_node_hours` |
`int`
The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node_hour = actual_hour \*
number_of_nodes_involved. For modelType
`cloud` \ (default), the budget must be between 8,000 and
800,000 milli node hours, inclusive. The default value is
192,000 which represents one day in wall time, considering 8
nodes are used. For model types `mobile-tf-low-latency-1` ,
`mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` ,
the training budget must be between 1,000 and 100,000 milli
node hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.
|
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Classification might stop training before the entire training budget has been used. |
`multi_label` |
`bool`
If false, a single-label (multi-class) Model will be trained (i.e. assuming that for each image just up to one annotation may be applicable). If true, a multi-label Model will be trained (i.e. assuming that for each image multiple annotations may be applicable). |

## Classes

### ModelType

`ModelType(value)`


## Methods

### AutoMlImageClassificationInputs

```
AutoMlImageClassificationInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageClassificationInputs

```
AutoMlImageClassificationInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltable_e0ebe5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltablesinputstransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation -->

# Class Transformation (1.134.0)

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Classes

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

### TextArrayTransformation

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The text as is--no change to case, punctuation, spelling, tense, and so on.
- Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Tokenization is based on unicode script boundaries.
- Missing values get their own lookup index and resulting embedding.
- Stop-words receive no special treatment and are not removed.

### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- Apply the transformation functions for Numerical columns.
- Determine the year, month, day,and weekday. Treat each value from the
- timestamp as a Categorical column.
- Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

## Methods

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgroundingchunk__googlecloudaiplatform_v1typespersi_007282.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgroundingchunk.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingChunk -->

# Class GroundingChunk (1.134.0)

`GroundingChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Grounding chunk.

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
`web` |
Grounding chunk from the web. This field is a member of `oneof` _ `chunk_type` .
|
`retrieved_context` |
Grounding chunk from context retrieved by the retrieval tools. This field is a member of `oneof` _ `chunk_type` .
|
`maps` |
Grounding chunk from Google Maps. This field is a member of `oneof` _ `chunk_type` .
|

## Classes

### Maps

`Maps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from Google Maps.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### RetrievedContext

`RetrievedContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from context retrieved by the retrieval tools.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Web

`Web(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from the web.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### GroundingChunk

`GroundingChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Grounding chunk.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespersistentdiskspec_googlecloudaiplatform_v1typesli_94bec9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespersistentdiskspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PersistentDiskSpec -->

# Class PersistentDiskSpec (1.134.0)

`PersistentDiskSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of [persistent
disk][[https://cloud.google.com/compute/docs/disks/persistent-disks](https://cloud.google.com/compute/docs/disks/persistent-disks)]
options.

## Attributes |
|
|---|---|
Name |
Description |
`disk_type` |
`str`
Type of the disk (default is "pd-standard"). Valid values: "pd-ssd" (Persistent Disk Solid State Drive) "pd-standard" (Persistent Disk Hard Disk Drive) "pd-balanced" (Balanced Persistent Disk) "pd-extreme" (Extreme Persistent Disk) |
`disk_size_gb` |
`int`
Size in GB of the disk (default is 100GB). |

## Methods

### PersistentDiskSpec

`PersistentDiskSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of [persistent
disk][[https://cloud.google.com/compute/docs/disks/persistent-disks](https://cloud.google.com/compute/docs/disks/persistent-disks)]
options.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistsavedqueriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSavedQueriesRequest -->

# Class ListSavedQueriesRequest (1.134.0)

`ListSavedQueriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListSavedQueries.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Dataset to list SavedQueries from. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`filter` |
`str`
The standard list filter. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. |

## Methods

### ListSavedQueriesRequest

`ListSavedQueriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListSavedQueries.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesquerycontextlineagesubgraphrequest_googleclouda_ac13ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesquerycontextlineagesubgraphrequest_googlecloudai_29ea6f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesquerycontextlineagesubgraphrequest_googlecloudaip_277450.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesquerycontextlineagesubgraphrequest_googlecloudaipl_14e2e5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesquerycontextlineagesubgraphrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryContextLineageSubgraphRequest -->

# Class QueryContextLineageSubgraphRequest (1.134.0)

```
QueryContextLineageSubgraphRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryContextLineageSubgraph.

## Attribute |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the Context whose Artifacts and Executions should be retrieved as a LineageSubgraph. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
The request may error with FAILED_PRECONDITION if the number
of Artifacts, the number of Executions, or the number of
Events that would be returned for the Context exceeds 1000.
|

## Methods

### QueryContextLineageSubgraphRequest

```
QueryContextLineageSubgraphRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryContextLineageSubgraph.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typesimagesegmentationpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageSegmentationPredictionInstance -->

# Class ImageSegmentationPredictionInstance (1.134.0)

```
ImageSegmentationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Segmentation.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The image bytes to make the predictions on. |
`mime_type` |
`str`
The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/png |

## Methods

### ImageSegmentationPredictionInstance

```
ImageSegmentationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Segmentation.

### ImageSegmentationPredictionInstance

```
ImageSegmentationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Segmentation.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexportfeaturevaluesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesRequest -->

# Class ExportFeatureValuesRequest (1.134.0)

`ExportFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ExportFeatureValues.

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
`snapshot_export` |
Exports the latest Feature values of all entities of the EntityType within a time range. This field is a member of `oneof` _ `mode` .
|
`full_export` |
Exports all historical values of all entities of the EntityType within a time range This field is a member of `oneof` _ `mode` .
|
`entity_type` |
`str`
Required. The resource name of the EntityType from which to export Feature values. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
|
`destination` |
Required. Specifies destination location and format. |
`feature_selector` |
Required. Selects Features to export values of. |
`settings` |
`MutableSequence[`
Per-Feature export settings. |

## Classes

### FullExport

`FullExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting all historical Feature values of all entities of the EntityType between [start_time, end_time].

### SnapshotExport

`SnapshotExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting the latest Feature values of all entities of the EntityType between [start_time, snapshot_time].

## Methods

### ExportFeatureValuesRequest

`ExportFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ExportFeatureValues.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgroundingchunk_googlecloudaiplatform_v1typesm_a9e77e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgroundingchunk.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingChunk -->

# Class GroundingChunk (1.134.0)

`GroundingChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Grounding chunk.

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
`web` |
Grounding chunk from the web. This field is a member of `oneof` _ `chunk_type` .
|
`retrieved_context` |
Grounding chunk from context retrieved by the retrieval tools. This field is a member of `oneof` _ `chunk_type` .
|
`maps` |
Grounding chunk from Google Maps. This field is a member of `oneof` _ `chunk_type` .
|

## Classes

### Maps

`Maps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from Google Maps.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### RetrievedContext

`RetrievedContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from context retrieved by the retrieval tools.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Web

`Web(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from the web.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### GroundingChunk

`GroundingChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Grounding chunk.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigtrainingpredictionskewdetectionconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.TrainingPredictionSkewDetectionConfig -->

# Class TrainingPredictionSkewDetectionConfig (1.134.0)

```
TrainingPredictionSkewDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.

## Attributes |
|
|---|---|
Name |
Description |
`skew_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. If a feature needs to be monitored for skew, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between the training and prediction feature. |
`attribution_score_skew_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. The threshold here is against attribution score distance between the training and prediction feature. |
`default_skew_threshold` |
Skew anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features. |

## Classes

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

## Methods

### TrainingPredictionSkewDetectionConfig

```
TrainingPredictionSkewDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesdeployment_resource_pool_service_googlec_b46af9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesdeployment_resource_pool_service_googlecl_ce5660.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesdeployment_resource_pool_service_googleclo_40ba19.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdeployment_resource_pool_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service -->

# Package deployment_resource_pool_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.deployment_resource_pool_service`

package.

## Classes

[DeploymentResourcePoolServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient)

A service that manages the DeploymentResourcePool resource.

[DeploymentResourcePoolServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient)

A service that manages the DeploymentResourcePool resource.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers)

API documentation for `aiplatform_v1beta1.services.deployment_resource_pool_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryrecallmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryRecallMetricValue -->

# Class TrajectoryRecallMetricValue (1.134.0)

`TrajectoryRecallMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TrajectoryRecall metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. TrajectoryRecall score. This field is a member of `oneof` _ `_score` .
|

## Methods

### TrajectoryRecallMetricValue

`TrajectoryRecallMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TrajectoryRecall metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfetchfeaturevaluesresponsefeaturenamevaluepairlist_9169ba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfetchfeaturevaluesresponsefeaturenamevaluepairlist.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FetchFeatureValuesResponse.FeatureNameValuePairList -->

# Class FeatureNameValuePairList (1.134.0)

`FeatureNameValuePairList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response structure in the format of key (feature name) and (feature) value pair.

## Attribute |
|
|---|---|
Name |
Description |
`features` |
`MutableSequence[`
List of feature names and values. |

## Classes

### FeatureNameValuePair

`FeatureNameValuePair(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature name & value pair.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### FeatureNameValuePairList

`FeatureNameValuePairList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response structure in the format of key (feature name) and (feature) value pair.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltextsentimentinputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextSentimentInputs -->

# Class AutoMlTextSentimentInputs (1.134.0)

`AutoMlTextSentimentInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attribute |
|
|---|---|
Name |
Description |
`sentiment_max` |
`int`
A sentiment is expressed as an integer ordinal, where higher value means a more positive sentiment. The range of sentiments that will be used is between 0 and sentimentMax (inclusive on both ends), and all the values in the range must be represented in the dataset before a model can be created. Only the Annotations with this sentimentMax will be used for training. sentimentMax value must be between 1 and 10 (inclusive). |

## Methods

### AutoMlTextSentimentInputs

`AutoMlTextSentimentInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### AutoMlTextSentimentInputs

`AutoMlTextSentimentInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeseventlabelsentry_googlecloudaiplatform_v1beta1typ_2b097c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeseventlabelsentry_googlecloudaiplatform_v1beta1type_5df33d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeseventlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Event.LabelsEntry -->

# Class LabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmemoryscopeentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Memory.ScopeEntry -->

# Class ScopeEntry (1.134.0)

`ScopeEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ScopeEntry

`ScopeEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfindneighborsrequestquery.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FindNeighborsRequest.Query -->

# Class Query (1.134.0)

`Query(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A query to find a number of the nearest neighbors (most similar vectors) of a vector.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`rrf` |
Optional. Represents RRF algorithm that combines search results. This field is a member of `oneof` _ `ranking` .
|
`datapoint` |
Required. The datapoint/vector whose nearest neighbors should be searched for. |
`neighbor_count` |
`int`
The number of nearest neighbors to be retrieved from database for each query. If not set, will use the default from the service configuration (https://cloud.google.com/vertex-ai/docs/matching-engine/configuring-indexes#nearest-neighbor-search-config). |
`per_crowding_attribute_neighbor_count` |
`int`
Crowding is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than some value k' of the k neighbors returned have the same value of crowding_attribute. It's used for improving result diversity. This field is the maximum number of matches with the same crowding tag. |
`approximate_neighbor_count` |
`int`
The number of neighbors to find via approximate search before exact reordering is performed. If not set, the default value from scam config is used; if set, this value must be > 0. |
`fraction_leaf_nodes_to_search_override` |
`float`
The fraction of the number of leaves to search, set at query time allows user to tune search performance. This value increase result in both search accuracy and latency increase. The value should be between 0.0 and 1.0. If not set or set to 0.0, query uses the default value specified in NearestNeighborSearchConfig.TreeAHConfig.fraction_leaf_nodes_to_search. |

## Classes

### RRF

`RRF(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for RRF algorithm that combines search results.

## Methods

### Query

`Query(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A query to find a number of the nearest neighbors (most similar vectors) of a vector.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesindex_endpoint_serviceindexendpointserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient -->

# Class IndexEndpointServiceClient (1.134.0)

```
IndexEndpointServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's IndexEndpoints.

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
`IndexEndpointServiceTransport` |
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

### IndexEndpointServiceClient

```
IndexEndpointServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the index endpoint service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,IndexEndpointServiceTransport,Callable[..., IndexEndpointServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the IndexEndpointServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_index_endpoint

```
create_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.CreateIndexEndpointRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
index_endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.index_endpoint.IndexEndpoint
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


Creates an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_index_endpoint():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
index_endpoint = aiplatform_v1.[IndexEndpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexEndpoint.html)()
index_endpoint.display_name = "display_name_value"
request = aiplatform_v1.[CreateIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateIndexEndpointRequest.html)(
parent="parent_value",
index_endpoint=index_endpoint,
)
# Make the request
operation = client.[create_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_create_index_endpoint)(request=request)
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
The request object. Request message for IndexEndpointService.CreateIndexEndpoint. |
`parent` |
`str`
Required. The resource name of the Location to create the IndexEndpoint in. Format: |
`index_endpoint` |
Required. The IndexEndpoint to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_index_endpoint

```
delete_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.DeleteIndexEndpointRequest,
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


Deletes an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_index_endpoint():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteIndexEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_delete_index_endpoint)(request=request)
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
The request object. Request message for IndexEndpointService.DeleteIndexEndpoint. |
`name` |
`str`
Required. The name of the IndexEndpoint resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### deploy_index

```
deploy_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.DeployIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index: typing.Optional[
google.cloud.aiplatform_v1.types.index_endpoint.DeployedIndex
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


Deploys an Index into this IndexEndpoint, creating a DeployedIndex within it. Only non-empty Indexes can be deployed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_deploy_index():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
deployed_index = aiplatform_v1.[DeployedIndex](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedIndex.html)()
deployed_index.id = "id_value"
deployed_index.index = "index_value"
request = aiplatform_v1.[DeployIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index=deployed_index,
)
# Make the request
operation = client.[deploy_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_deploy_index)(request=request)
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
The request object. Request message for IndexEndpointService.DeployIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: |
`deployed_index` |
Required. The DeployedIndex to be created within the IndexEndpoint. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`IndexEndpointServiceClient` |
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
`IndexEndpointServiceClient` |
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
`IndexEndpointServiceClient` |
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

### get_index_endpoint

```
get_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.GetIndexEndpointRequest,
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
) -> google.cloud.aiplatform_v1.types.index_endpoint.IndexEndpoint
```


Gets an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_index_endpoint():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetIndexEndpointRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_get_index_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexEndpointService.GetIndexEndpoint |
`name` |
`str`
Required. The name of the IndexEndpoint resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes. |

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

### index_endpoint_path

`index_endpoint_path(project: str, location: str, index_endpoint: str) -> str`


Returns a fully-qualified index_endpoint string.

### index_path

`index_path(project: str, location: str, index: str) -> str`


Returns a fully-qualified index string.

### list_index_endpoints

```
list_index_endpoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsRequest,
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
google.cloud.aiplatform_v1.services.index_endpoint_service.pagers.ListIndexEndpointsPager
)
```


Lists IndexEndpoints in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_index_endpoints():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListIndexEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_index_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_list_index_endpoints)(request=request)
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
The request object. Request message for IndexEndpointService.ListIndexEndpoints. |
`parent` |
`str`
Required. The resource name of the Location from which to list the IndexEndpoints. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for IndexEndpointService.ListIndexEndpoints. Iterating over this object will yield results and resolve additional pages automatically. |

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

### mutate_deployed_index

```
mutate_deployed_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.MutateDeployedIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index: typing.Optional[
google.cloud.aiplatform_v1.types.index_endpoint.DeployedIndex
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


Update an existing DeployedIndex under an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_mutate_deployed_index():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
deployed_index = aiplatform_v1.[DeployedIndex](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedIndex.html)()
deployed_index.id = "id_value"
deployed_index.index = "index_value"
request = aiplatform_v1.[MutateDeployedIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index=deployed_index,
)
# Make the request
operation = client.[mutate_deployed_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_mutate_deployed_index)(request=request)
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
The request object. Request message for IndexEndpointService.MutateDeployedIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: |
`deployed_index` |
Required. The DeployedIndex to be updated within the IndexEndpoint. Currently, the updatable fields are DeployedIndex.automatic_resources and DeployedIndex.dedicated_resources This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### undeploy_index

```
undeploy_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.UndeployIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index_id: typing.Optional[str] = None,
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


Undeploys an Index from an IndexEndpoint, removing a DeployedIndex from it, and freeing all resources it's using.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_undeploy_index():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UndeployIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index_id="deployed_index_id_value",
)
# Make the request
operation = client.[undeploy_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_undeploy_index)(request=request)
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
The request object. Request message for IndexEndpointService.UndeployIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource from which to undeploy an Index. Format: |
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to be undeployed from the IndexEndpoint. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### update_index_endpoint

```
update_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.UpdateIndexEndpointRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.index_endpoint.IndexEndpoint
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
) -> google.cloud.aiplatform_v1.types.index_endpoint.IndexEndpoint
```


Updates an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_index_endpoint():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
index_endpoint = aiplatform_v1.[IndexEndpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexEndpoint.html)()
index_endpoint.display_name = "display_name_value"
request = aiplatform_v1.[UpdateIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateIndexEndpointRequest.html)(
index_endpoint=index_endpoint,
)
# Make the request
response = client.[update_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_update_index_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexEndpointService.UpdateIndexEndpoint. |
`index_endpoint` |
Required. The IndexEndpoint which replaces the resource on the server. This corresponds to the |
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
Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes. |

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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualization__de47d3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualization_g_577994.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualization_go_e3b1f0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualization_goo_8477ef.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualization_goog_00179f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualization.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata.Visualization -->

# Class Visualization (1.134.0)

`Visualization(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Visualization configurations for image explanation.

## Attributes |
|
|---|---|
Name |
Description |
`type_` |
Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1.ExplanationParameters.integrated_gradients_attribution]. OUTLINES shows regions of attribution, while PIXELS shows per-pixel attribution. Defaults to OUTLINES. |
`polarity` |
Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE. |
`color_map` |
The color scheme used for the highlighted areas. Defaults to PINK_GREEN for [Integrated Gradients attribution][google.cloud.aiplatform.v1.ExplanationParameters.integrated_gradients_attribution], which shows positive attributions in green and negative in pink. Defaults to VIRIDIS for [XRAI attribution][google.cloud.aiplatform.v1.ExplanationParameters.xrai_attribution], which highlights the most influential regions in yellow and the least influential in blue. |
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


Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1.ExplanationParameters.integrated_gradients_attribution].

## Methods

### Visualization

`Visualization(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Visualization configurations for image explanation.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfindneighborsrequestquery.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsRequest.Query -->

# Class Query (1.134.0)

`Query(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A query to find a number of the nearest neighbors (most similar vectors) of a vector.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`rrf` |
Optional. Represents RRF algorithm that combines search results. This field is a member of `oneof` _ `ranking` .
|
`datapoint` |
Required. The datapoint/vector whose nearest neighbors should be searched for. |
`neighbor_count` |
`int`
The number of nearest neighbors to be retrieved from database for each query. If not set, will use the default from the service configuration (https://cloud.google.com/vertex-ai/docs/matching-engine/configuring-indexes#nearest-neighbor-search-config). |
`per_crowding_attribute_neighbor_count` |
`int`
Crowding is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than some value k' of the k neighbors returned have the same value of crowding_attribute. It's used for improving result diversity. This field is the maximum number of matches with the same crowding tag. |
`approximate_neighbor_count` |
`int`
The number of neighbors to find via approximate search before exact reordering is performed. If not set, the default value from scam config is used; if set, this value must be > 0. |
`fraction_leaf_nodes_to_search_override` |
`float`
The fraction of the number of leaves to search, set at query time allows user to tune search performance. This value increase result in both search accuracy and latency increase. The value should be between 0.0 and 1.0. If not set or set to 0.0, query uses the default value specified in NearestNeighborSearchConfig.TreeAHConfig.fraction_leaf_nodes_to_search. |

## Classes

### RRF

`RRF(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for RRF algorithm that combines search results.

## Methods

### Query

`Query(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A query to find a number of the nearest neighbors (most similar vectors) of a vector.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodelmonitoringalert_googlecloudaiplatform_v_ae0623.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringalert_googlecloudaiplatform_v1_d88bb2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringalert.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAlert -->

# Class ModelMonitoringAlert (1.134.0)

`ModelMonitoringAlert(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single monitoring alert. This is currently used in the SearchModelMonitoringAlerts api, thus the alert wrapped in this message belongs to the resource asked in the request.

## Attributes |
|
|---|---|
Name |
Description |
`stats_name` |
`str`
The stats name. |
`objective_type` |
`str`
One of the supported monitoring objectives: `raw-feature-drift` `prediction-output-drift`
`feature-attribution`
|
`alert_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Alert creation time. |
`anomaly` |
Anomaly details. |

## Methods

### ModelMonitoringAlert

`ModelMonitoringAlert(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single monitoring alert. This is currently used in the SearchModelMonitoringAlerts api, thus the alert wrapped in this message belongs to the resource asked in the request.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatefeaturestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeaturestoreRequest -->

# Class CreateFeaturestoreRequest (1.134.0)

`CreateFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateFeaturestore.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create Featurestores. Format: `projects/{project}/locations/{location}`
|
`featurestore` |
Required. The Featurestore to create. |
`featurestore_id` |
`str`
Required. The ID to use for this Featurestore, which will become the final component of the Featurestore's resource name. This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within the project and location.
|

## Methods

### CreateFeaturestoreRequest

`CreateFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateFeaturestore.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfetchfeaturevaluesresponsefeaturenamevaluepai_64759a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfetchfeaturevaluesresponsefeaturenamevaluepairlistfeaturenamevaluepair.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchFeatureValuesResponse.FeatureNameValuePairList.FeatureNameValuePair -->

# Class FeatureNameValuePair (1.134.0)

`FeatureNameValuePair(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature name & value pair.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`value` |
Feature value. This field is a member of `oneof` _ `data` .
|
`name` |
`str`
Feature short name. |

## Methods

### FeatureNameValuePair

`FeatureNameValuePair(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature name & value pair.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquerycontextlineagesubgraphrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryContextLineageSubgraphRequest -->

# Class QueryContextLineageSubgraphRequest (1.134.0)

```
QueryContextLineageSubgraphRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryContextLineageSubgraph.

## Attribute |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the Context whose Artifacts and Executions should be retrieved as a LineageSubgraph. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
The request may error with FAILED_PRECONDITION if the number
of Artifacts, the number of Executions, or the number of
Events that would be returned for the Context exceeds 1000.
|

## Methods

### QueryContextLineageSubgraphRequest

```
QueryContextLineageSubgraphRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryContextLineageSubgraph.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesupsertexamplesrequest_googlecloudaiplatform_a6c82e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupsertexamplesrequest_googlecloudaiplatform__2c20a4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupsertexamplesrequest_googlecloudaiplatform_v_b9129f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupsertexamplesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertExamplesRequest -->

# Class UpsertExamplesRequest (1.134.0)

`UpsertExamplesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.UpsertExamples.

## Attributes |
|
|---|---|
Name |
Description |
`example_store` |
`str`
Required. The name of the ExampleStore resource that examples are added to or updated in. Format: `projects/{project}/locations/{location}/exampleStores/{example_store}`
|
`examples` |
`MutableSequence[`
Required. A list of examples to be created/updated. |
`overwrite` |
`bool`
Optional. A flag indicating whether an example can be overwritten if it already exists. If False (default) and the example already exists, the example will not be updated. This does not affect behavior if the example does not exist already. |

## Methods

### UpsertExamplesRequest

`UpsertExamplesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.UpsertExamples.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespointwisemetricresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PointwiseMetricResult -->

# Class PointwiseMetricResult (1.134.0)

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

## Methods

### PointwiseMetricResult

`PointwiseMetricResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfunctionresponseblob_googlecloudaiplatform_v1_87098b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfunctionresponseblob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionResponseBlob -->

# Class FunctionResponseBlob (1.134.0)

`FunctionResponseBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Raw media bytes for function response.

Text should not be sent as raw bytes, use the 'text' field.

## Attributes |
|
|---|---|
Name |
Description |
`mime_type` |
`str`
Required. The IANA standard MIME type of the source data. |
`data` |
`bytes`
Required. Raw bytes. |
`display_name` |
`str`
Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. |

## Methods

### FunctionResponseBlob

`FunctionResponseBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Raw media bytes for function response.

Text should not be sent as raw bytes, use the 'text' field.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstreamingfetchfeaturevaluesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingFetchFeatureValuesResponse -->

# Class StreamingFetchFeatureValuesResponse (1.134.0)

```
StreamingFetchFeatureValuesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreService.StreamingFetchFeatureValues.

## Attribute |
|
|---|---|
Name |
Description |
`status` |
`google.rpc.status_pb2.Status`
Response status. If OK, then StreamingFetchFeatureValuesResponse.data will be populated. Otherwise StreamingFetchFeatureValuesResponse.data_keys_with_error will be populated with the appropriate data keys. The error only applies to the listed data keys - the stream will remain open for further [FeatureOnlineStoreService.StreamingFetchFeatureValuesRequest][] requests. |

## Methods

### StreamingFetchFeatureValuesResponse

```
StreamingFetchFeatureValuesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreService.StreamingFetchFeatureValues.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexplanationmetadataoutputmetadata__googlecloudaipl_1d6dd8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanationmetadataoutputmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.OutputMetadata -->

# Class OutputMetadata (1.134.0)

`OutputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the prediction output to be explained.

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
`index_display_name_mapping` |
`google.protobuf.struct_pb2.Value`
Static mapping between the index and display name. Use this if the outputs are a deterministic n-dimensional array, e.g. a list of scores of all the classes in a pre-defined order for a multi-classification Model. It's not feasible if the outputs are non-deterministic, e.g. the Model produces top-k classes or sort the outputs by their values. The shape of the value must be an n-dimensional array of strings. The number of dimensions must match that of the outputs to be explained. The Attribution.output_display_name is populated by locating in the mapping with Attribution.output_index. This field is a member of `oneof` _ `display_name_mapping` .
|
`display_name_mapping_key` |
`str`
Specify a field name in the prediction to look for the display name. Use this if the prediction contains the display names for the outputs. The display names in the prediction must have the same shape of the outputs, so that it can be located by Attribution.output_index for a specific output. This field is a member of `oneof` _ `display_name_mapping` .
|
`output_tensor_name` |
`str`
Name of the output tensor. Required and is only applicable to Vertex AI provided images for Tensorflow. |

## Methods

### OutputMetadata

`OutputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the prediction output to be explained.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeatureviewdirectwriterequestdatakeyandfeaturevalu_ccfe2f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureviewdirectwriterequestdatakeyandfeaturevaluesfeature.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureViewDirectWriteRequest.DataKeyAndFeatureValues.Feature -->

# Class Feature (1.134.0)

`Feature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature name & value pair.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`value` |
Feature value. A user provided timestamp may be set in the `FeatureValue.metadata.generate_time` field.
This field is a member of `oneof` _ `data_oneof` .
|
`name` |
`str`
Feature short name. |

## Methods

### Feature

`Feature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature name & value pair.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetmodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetModelRequest -->

# Class GetModelRequest (1.134.0)

`GetModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.GetModel.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Model resource. Format: `projects/{project}/locations/{location}/models/{model}`
In order to retrieve a specific version of the model, also
provide the version ID or version alias. Example:
`projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
If no version ID or alias is specified, the "default"
version will be returned. The "default" version alias is
created for the first version of the model, and can be moved
to other versions later on. There will be exactly one
default version.
|

## Methods

### GetModelRequest

`GetModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.GetModel.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigtrainingpredi_952396.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigtrainingpredic_55510f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigtrainingpredict_4e15d7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigtrainingpredictionskewdetectionconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.TrainingPredictionSkewDetectionConfig -->

# Class TrainingPredictionSkewDetectionConfig (1.134.0)

```
TrainingPredictionSkewDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.

## Attributes |
|
|---|---|
Name |
Description |
`skew_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. If a feature needs to be monitored for skew, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between the training and prediction feature. |
`attribution_score_skew_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. The threshold here is against attribution score distance between the training and prediction feature. |
`default_skew_threshold` |
Skew anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features. |

## Classes

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

## Methods

### TrainingPredictionSkewDetectionConfig

```
TrainingPredictionSkewDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesbleuinstance_googlecloudaiplatform_v1beta1typessch_c7a3fa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbleuinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BleuInstance -->

# Class BleuInstance (1.134.0)

`BleuInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for bleu instance.

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

### BleuInstance

`BleuInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for bleu instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesschemadefsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schema.DefsEntry -->

# Class DefsEntry (1.134.0)

`DefsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### DefsEntry

`DefsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstra_2c5666.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstransformationtimestamptransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.TimestampTransformation -->

# Class TimestampTransformation (1.134.0)

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- Apply the transformation functions for Numerical columns.
- Determine the year, month, day,and weekday. Treat each value from the
- timestamp as a Categorical column.
- Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

## Attributes |
|
|---|---|
Name |
Description |
`time_format` |
`str`
The format in which that time field is expressed. The time_format must either be one of: - `unix-seconds`
- `unix-milliseconds`
- `unix-microseconds`
- `unix-nanoseconds` (for respectively number of seconds,
milliseconds, microseconds and nanoseconds since start of
the Unix epoch); or be written in `strftime` syntax. If
time_format is not set, then the default format is RFC
3339 `date-time` format, where `time-offset` = `"Z"`
(e.g. 1985-04-12T23:20:50.52Z)
|
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- Apply the transformation functions for Numerical columns.
- Determine the year, month, day,and weekday. Treat each value from the
- timestamp as a Categorical column.
- Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- Apply the transformation functions for Numerical columns.
- Determine the year, month, day,and weekday. Treat each value from the
- timestamp as a Categorical column.
- Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstudy_googlecloudaiplatform_v1beta1typeslistsavedq_7f4363.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstudy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Study -->

# Class Study (1.134.0)

`Study(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Study.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The name of a study. The study's globally unique identifier. Format: `projects/{project}/locations/{location}/studies/{study}`
|
`display_name` |
`str`
Required. Describes the Study, default value is empty string. |
`study_spec` |
Required. Configuration of the Study. |
`state` |
Output only. The detailed state of a Study. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time at which the study was created. |
`inactive_reason` |
`str`
Output only. A human readable reason why the Study is inactive. This should be empty if a study is ACTIVE or COMPLETED. |

## Classes

### State

`State(value)`


Describes the Study state.

## Methods

### Study

`Study(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Study.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistsavedqueriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesRequest -->

# Class ListSavedQueriesRequest (1.134.0)

`ListSavedQueriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListSavedQueries.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Dataset to list SavedQueries from. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`filter` |
`str`
The standard list filter. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. |

## Methods

### ListSavedQueriesRequest

`ListSavedQueriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListSavedQueries.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesqueryreasoningenginerequest_googlecloudaipl_cad796.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesqueryreasoningenginerequest_googlecloudaipla_4f4638.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesqueryreasoningenginerequest_googlecloudaiplat_d0ee86.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesqueryreasoningenginerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryReasoningEngineRequest -->

# Class QueryReasoningEngineRequest (1.134.0)

`QueryReasoningEngineRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [ReasoningEngineExecutionService.Query][].

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ReasoningEngine resource to use. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`input` |
`google.protobuf.struct_pb2.Struct`
Optional. Input content provided by users in JSON object format. Examples include text query, function calling parameters, media bytes, etc. |
`class_method` |
`str`
Optional. Class method to be used for the query. It is optional and defaults to "query" if unspecified. |

## Methods

### QueryReasoningEngineRequest

`QueryReasoningEngineRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [ReasoningEngineExecutionService.Query][].


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimageclassificationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata -->

# Class AutoMlImageClassificationMetadata (1.134.0)

```
AutoMlImageClassificationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`cost_milli_node_hours` |
`int`
The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours. |
`successful_stop_reason` |
For successful job completions, this is the reason why the job has finished. |

## Classes

### SuccessfulStopReason

`SuccessfulStopReason(value)`


## Methods

### AutoMlImageClassificationMetadata

```
AutoMlImageClassificationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageClassificationMetadata

```
AutoMlImageClassificationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodellabelsentry_googlecloudaiplatform_v1typesinde_366798.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodellabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model.LabelsEntry -->

# Class LabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesindexlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Index.LabelsEntry -->

# Class LabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesevaluatedatasetrequest_googlecloudaiplatform_bae098.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesevaluatedatasetrequest_googlecloudaiplatform__47b22e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesevaluatedatasetrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateDatasetRequest -->

# Class EvaluateDatasetRequest (1.134.0)

`EvaluateDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EvaluationService.EvaluateDataset.

## Attributes |
|
|---|---|
Name |
Description |
`location` |
`str`
Required. The resource name of the Location to evaluate the dataset. Format: `projects/{project}/locations/{location}`
|
`dataset` |
Required. The dataset used for evaluation. |
`metrics` |
`MutableSequence[`
Required. The metrics used for evaluation. |
`output_config` |
Required. Config for evaluation output. |
`autorater_config` |
Optional. Autorater config used for evaluation. Currently only publisher Gemini models are supported. Format: `projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL}.`
|

## Methods

### EvaluateDatasetRequest

`EvaluateDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EvaluationService.EvaluateDataset.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatetensorboardrunrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardRunRequest -->

# Class CreateTensorboardRunRequest (1.134.0)

`CreateTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.CreateTensorboardRun.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the TensorboardExperiment to create the TensorboardRun in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|
`tensorboard_run` |
Required. The TensorboardRun to create. |
`tensorboard_run_id` |
`str`
Required. The ID to use for the Tensorboard run, which becomes the final component of the Tensorboard run's resource name. This value should be 1-128 characters, and valid characters are `/` a-z][0-9]`-/` .
|

## Methods

### CreateTensorboardRunRequest

`CreateTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.CreateTensorboardRun.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeatureviewdirectwriterequest_googlecloudaiplatfor_441fcb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureviewdirectwriterequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureViewDirectWriteRequest -->

# Class FeatureViewDirectWriteRequest (1.134.0)

```
FeatureViewDirectWriteRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreService.FeatureViewDirectWrite.

## Attributes |
|
|---|---|
Name |
Description |
`feature_view` |
`str`
FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`
|
`data_key_and_feature_values` |
`MutableSequence[`
Required. The data keys and associated feature values. |

## Classes

### DataKeyAndFeatureValues

`DataKeyAndFeatureValues(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A data key and associated feature values to write to the feature view.

## Methods

### FeatureViewDirectWriteRequest

```
FeatureViewDirectWriteRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreService.FeatureViewDirectWrite.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespersistentdiskspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PersistentDiskSpec -->

# Class PersistentDiskSpec (1.134.0)

`PersistentDiskSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of [persistent
disk][[https://cloud.google.com/compute/docs/disks/persistent-disks](https://cloud.google.com/compute/docs/disks/persistent-disks)]
options.

## Attributes |
|
|---|---|
Name |
Description |
`disk_type` |
`str`
Type of the disk (default is "pd-standard"). Valid values: "pd-ssd" (Persistent Disk Solid State Drive) "pd-standard" (Persistent Disk Hard Disk Drive) "pd-balanced" (Balanced Persistent Disk) "pd-extreme" (Extreme Persistent Disk) |
`disk_size_gb` |
`int`
Size in GB of the disk (default is 100GB). |

## Methods

### PersistentDiskSpec

`PersistentDiskSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of [persistent
disk][[https://cloud.google.com/compute/docs/disks/persistent-disks](https://cloud.google.com/compute/docs/disks/persistent-disks)]
options.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesindex_endpoint_serviceindexendpointserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient -->

# Class IndexEndpointServiceClient (1.134.0)

```
IndexEndpointServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's IndexEndpoints.

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
`IndexEndpointServiceTransport` |
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

### IndexEndpointServiceClient

```
IndexEndpointServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the index endpoint service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,IndexEndpointServiceTransport,Callable[..., IndexEndpointServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the IndexEndpointServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_index_endpoint

```
create_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.CreateIndexEndpointRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
index_endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.index_endpoint.IndexEndpoint
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


Creates an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
index_endpoint = aiplatform_v1beta1.[IndexEndpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexEndpoint.html)()
index_endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexEndpointRequest.html)(
parent="parent_value",
index_endpoint=index_endpoint,
)
# Make the request
operation = client.[create_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_create_index_endpoint)(request=request)
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
The request object. Request message for IndexEndpointService.CreateIndexEndpoint. |
`parent` |
`str`
Required. The resource name of the Location to create the IndexEndpoint in. Format: |
`index_endpoint` |
Required. The IndexEndpoint to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_index_endpoint

```
delete_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.DeleteIndexEndpointRequest,
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


Deletes an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteIndexEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_delete_index_endpoint)(request=request)
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
The request object. Request message for IndexEndpointService.DeleteIndexEndpoint. |
`name` |
`str`
Required. The name of the IndexEndpoint resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### deploy_index

```
deploy_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.DeployIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index: typing.Optional[
google.cloud.aiplatform_v1beta1.types.index_endpoint.DeployedIndex
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


Deploys an Index into this IndexEndpoint, creating a DeployedIndex within it. Only non-empty Indexes can be deployed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_deploy_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
deployed_index = aiplatform_v1beta1.[DeployedIndex](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndex.html)()
deployed_index.id = "id_value"
deployed_index.index = "index_value"
request = aiplatform_v1beta1.[DeployIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index=deployed_index,
)
# Make the request
operation = client.[deploy_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_deploy_index)(request=request)
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
The request object. Request message for IndexEndpointService.DeployIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: |
`deployed_index` |
Required. The DeployedIndex to be created within the IndexEndpoint. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`IndexEndpointServiceClient` |
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
`IndexEndpointServiceClient` |
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
`IndexEndpointServiceClient` |
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

### get_index_endpoint

```
get_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.GetIndexEndpointRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.index_endpoint.IndexEndpoint
```


Gets an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetIndexEndpointRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_get_index_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexEndpointService.GetIndexEndpoint |
`name` |
`str`
Required. The name of the IndexEndpoint resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes. |

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

### index_endpoint_path

`index_endpoint_path(project: str, location: str, index_endpoint: str) -> str`


Returns a fully-qualified index_endpoint string.

### index_path

`index_path(project: str, location: str, index: str) -> str`


Returns a fully-qualified index string.

### list_index_endpoints

```
list_index_endpoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
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
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers.ListIndexEndpointsPager
)
```


Lists IndexEndpoints in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_index_endpoints():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListIndexEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_index_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_list_index_endpoints)(request=request)
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
The request object. Request message for IndexEndpointService.ListIndexEndpoints. |
`parent` |
`str`
Required. The resource name of the Location from which to list the IndexEndpoints. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for IndexEndpointService.ListIndexEndpoints. Iterating over this object will yield results and resolve additional pages automatically. |

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

### mutate_deployed_index

```
mutate_deployed_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.MutateDeployedIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index: typing.Optional[
google.cloud.aiplatform_v1beta1.types.index_endpoint.DeployedIndex
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


Update an existing DeployedIndex under an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_mutate_deployed_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
deployed_index = aiplatform_v1beta1.[DeployedIndex](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndex.html)()
deployed_index.id = "id_value"
deployed_index.index = "index_value"
request = aiplatform_v1beta1.[MutateDeployedIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index=deployed_index,
)
# Make the request
operation = client.[mutate_deployed_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_mutate_deployed_index)(request=request)
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
The request object. Request message for IndexEndpointService.MutateDeployedIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: |
`deployed_index` |
Required. The DeployedIndex to be updated within the IndexEndpoint. Currently, the updatable fields are |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### undeploy_index

```
undeploy_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.UndeployIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index_id: typing.Optional[str] = None,
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


Undeploys an Index from an IndexEndpoint, removing a DeployedIndex from it, and freeing all resources it's using.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_undeploy_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UndeployIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index_id="deployed_index_id_value",
)
# Make the request
operation = client.[undeploy_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_undeploy_index)(request=request)
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
The request object. Request message for IndexEndpointService.UndeployIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource from which to undeploy an Index. Format: |
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to be undeployed from the IndexEndpoint. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### update_index_endpoint

```
update_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.UpdateIndexEndpointRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.index_endpoint.IndexEndpoint
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
) -> google.cloud.aiplatform_v1beta1.types.index_endpoint.IndexEndpoint
```


Updates an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
index_endpoint = aiplatform_v1beta1.[IndexEndpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexEndpoint.html)()
index_endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexEndpointRequest.html)(
index_endpoint=index_endpoint,
)
# Make the request
response = client.[update_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_update_index_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexEndpointService.UpdateIndexEndpoint. |
`index_endpoint` |
Required. The IndexEndpoint which replaces the resource on the server. This corresponds to the |
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
Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes. |

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformtimeseriesdenseencoderforecastingtrainingjob_____googlec_ecc75f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformtimeseriesdenseencoderforecastingtrainingjob_____googlecl_67cf13.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformtimeseriesdenseencoderforecastingtrainingjob_____googleclo_b90fec.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformtimeseriesdenseencoderforecastingtrainingjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TimeSeriesDenseEncoderForecastingTrainingJob -->

# Class TimeSeriesDenseEncoderForecastingTrainingJob (1.134.0)

```
TimeSeriesDenseEncoderForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Class to train Time series Dense Encoder (TiDE) forecasting models.

The `TimeSeriesDenseEncoderForecastingTrainingJob`

class uses the
Time-series Dense Encoder (TiDE) training method to train and run a
forecasting model. TiDE uses a
[multi-layer perceptron](https://arxiv.org/abs/2304.08424) (MLP) to provide
the speed of forecasting linear models with covariates and non-linear
dependencies. For more information about TiDE, see
[Recent advances in deep long-horizon forecasting](https://blog.research.google/2023/04/recent-advances-in-deep-long-horizon.html)
and this
[TiDE blog post](https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-forecasting).

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Optional. The time when the training job entered the
`PIPELINE_STATE_SUCCEEDED`

, `PIPELINE_STATE_FAILED`

, or
`PIPELINE_STATE_CANCELLED`

state.

### error

Optional. Detailed error information for this training job resource.
Error information is created only when the state of the training job is
`PIPELINE_STATE_FAILED`

or `PIPELINE_STATE_CANCELLED`

.

### evaluated_data_items_bigquery_uri

BigQuery location of exported evaluated examples from the Training Job

Returns |
|
|---|---|
Type |
Description |
`str` |
BigQuery uri for the exported evaluated examples if the export feature is enabled for training. None: If the export feature was not enabled for training. |

### gca_resource

The underlying resource proto representation.

### has_failed

Returns `true`

if the training job failed, otherwise `false`

.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### start_time

Optional. The time when the training job first entered the
`PIPELINE_STATE_RUNNING`

state.

### state

Current training state.

### update_time

Time this resource was last updated.

## Methods

### TimeSeriesDenseEncoderForecastingTrainingJob

```
TimeSeriesDenseEncoderForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Constructs a Forecasting Training Job.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of this TrainingPipeline. |
`optimization_objective` |
`str`
Optional. Objective function the model is to be optimized towards. The training process creates a Model that optimizes the value of the objective function over the validation set. The supported optimization objectives: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE). "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE). "minimize-quantile-loss" - Minimize the quantile loss at the defined quantiles. (Set this objective to build quantile forecasts.) |
`column_specs` |
`Dict[str, str]`
Optional. Alternative to column_transformations where the keys of the dict are column names and their respective values are one of AutoMLTabularTrainingJob.column_data_types. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. |
`column_transformations` |
`List[Dict[str, Dict[str, str]]]`
Optional. Transformations to apply to the input columns (i.e. columns other than the targetColumn). Each transformation may produce multiple result values from the column's value, and all are used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. Consider using column_specs as column_transformations will be deprecated eventually. |
`project` |
`str`
Optional. Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both column_transformations and column_specs were provided. |

### cancel

`cancel() -> None`


Asynchronously attempts to cancel a training job.

The server makes a best effort to cancel the job, but the training job
can't always be cancelled. If the training job is canceled, its state
transitions to `CANCELLED`

and it's not deleted.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If this training job isn't running, then a runtime error is raised. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.training_jobs._TrainingJob
```


Gets a training job using the `resource_name`

that's passed in.

Parameters |
|
|---|---|
Name |
Description |
`resource_name` |
`str`
Required. A fully-qualified resource name or ID. |
`project` |
`str`
Optional. The name of the Google Cloud project to retrieve the training job from. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job is retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload this model. These credentials override the credentials set by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A `ValueError` is raised if the task definition of the retrieved training job doesn't match the custom training task definition. |

### get_model

`get_model(sync=True) -> google.cloud.aiplatform.models.Model`


Returns the Vertex AI model produced by this training job.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
If set to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
A runtime error is raised if the training job failed or if a model wasn't produced by the training job. |

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


Lists all instances of this training job resource.

The following shows an example of how to call `CustomTrainingJob.list`

:

```
aiplatform.CustomTrainingJob.list(
filter='display_name="experiment_a27"',
order_by='create_time desc'
)
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names, snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields used to sort the returned traing job resources. The defauilt sorting order is ascending. To sort by a field name in descending order, use |
`project` |
`str`
Optional. The name of the Google Cloud project to which to retrieve the list of training job resources. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job resources are retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to retrieve list. These credentials override the credentials set by |

Returns |
|
|---|---|
Type |
Description |
`List[VertexAiResourceNoun]` |
A list of training job resources. |

### run

```
run(
dataset: google.cloud.aiplatform.datasets.time_series_dataset.TimeSeriesDataset,
target_column: str,
time_column: str,
time_series_identifier_column: str,
unavailable_at_forecast_columns: typing.List[str],
available_at_forecast_columns: typing.List[str],
forecast_horizon: int,
data_granularity_unit: str,
data_granularity_count: int,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
predefined_split_column_name: typing.Optional[str] = None,
timestamp_split_column_name: typing.Optional[str] = None,
weight_column: typing.Optional[str] = None,
time_series_attribute_columns: typing.Optional[typing.List[str]] = None,
context_window: typing.Optional[int] = None,
export_evaluated_data_items: bool = False,
export_evaluated_data_items_bigquery_destination_uri: typing.Optional[str] = None,
export_evaluated_data_items_override_destination: bool = False,
quantiles: typing.Optional[typing.List[float]] = None,
validation_options: typing.Optional[str] = None,
budget_milli_node_hours: int = 1000,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
additional_experiments: typing.Optional[typing.List[str]] = None,
hierarchy_group_columns: typing.Optional[typing.List[str]] = None,
hierarchy_group_total_weight: typing.Optional[float] = None,
hierarchy_temporal_total_weight: typing.Optional[float] = None,
hierarchy_group_temporal_total_weight: typing.Optional[float] = None,
window_column: typing.Optional[str] = None,
window_stride_length: typing.Optional[int] = None,
window_max_count: typing.Optional[int] = None,
holiday_regions: typing.Optional[typing.List[str]] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
enable_probabilistic_inference: bool = False,
) -> google.cloud.aiplatform.models.Model
```


Runs the training job and returns a model.

If training on a Vertex AI dataset, you can use one of the following split configurations:
Data fraction splits:
Any of `training_fraction_split`

, `validation_fraction_split`

and
`test_fraction_split`

may optionally be provided, they must sum to up to 1. If
the provided ones sum to less than 1, the remainder is assigned to sets as
decided by Vertex AI. If none of the fractions are set, by default roughly 80%
of data will be used for training, 10% for validation, and 10% for test.

```
Predefined splits:
Assigns input data to training, validation, and test sets based on the value of a provided key.
If using predefined splits, `predefined_split_column_name` must be provided.
Supported only for tabular Datasets.
Timestamp splits:
Assigns input data to training, validation, and test sets
based on a provided timestamps. The youngest data pieces are
assigned to training set, next to validation set, and the oldest
to the test set.
Supported only for tabular Datasets.
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TimeSeriesDataset`
Required. The dataset within the same Project from which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. For time series Datasets, all their data is exported to training, to pick and choose from. |
`target_column` |
`str`
Required. Name of the column that the Model is to predict values for. This column must be unavailable at forecast. |
`time_column` |
`str`
Required. Name of the column that identifies time order in the time series. This column must be available at forecast. |
`time_series_identifier_column` |
`str`
Required. Name of the column that identifies the time series. |
`unavailable_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are unavailable at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is unknown before the forecast (e.g. population of a city in a given year, or weather on a given day). |
`available_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are available at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is known at forecast. |
`data_granularity_unit` |
`str`
Required. The data granularity unit. Accepted values are |
`data_granularity_count` |
`int`
Required. The number of data granularity units between data points in the training data. If [data_granularity_unit] is |
`predefined_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { |
`timestamp_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key values of the key (the values in the column) must be in RFC 3339 |
`weight_column` |
`str`
Optional. Name of the column that should be used as the weight column. Higher values in this column give more importance to the row during Model training. The column must have numeric values between 0 and 10000 inclusively, and 0 value means that the row is ignored. If the weight column field is not set, then all rows are assumed to have equal weight of 1. |
`time_series_attribute_columns` |
`List[str]`
Optional. Column names that should be used as attribute columns. Each column is constant within a time series. |
`context_window` |
`int`
Optional. The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the [data_granularity_unit] and [data_granularity_count] fields. When not provided uses the default value of 0 which means the model sets each series context window to be 0 (also known as "cold start"). Inclusive. |
`export_evaluated_data_items` |
`bool`
Whether to export the test set predictions to a BigQuery table. If False, then the export is not performed. |
`export_evaluated_data_items_bigquery_destination_uri` |
`string`
Optional. URI of desired destination BigQuery table for exported test set predictions. Expected format: `<project_id>:export_evaluated_examples_<model_name>_<yyyy_MM_dd'T'HH_mm_ss_SSS'Z'>.evaluated_examples` Applies only if [export_evaluated_data_items] is True.
|
`export_evaluated_data_items_override_destination` |
`bool`
Whether to override the contents of [export_evaluated_data_items_bigquery_destination_uri], if the table exists, for exported test set predictions. If False, and the table exists, then the training job will fail. Applies only if [export_evaluated_data_items] is True and [export_evaluated_data_items_bigquery_destination_uri] is specified. |
`quantiles` |
`List[float]`
Quantiles to use for the |
`validation_options` |
`str`
Validation options for the data validation component. The available options are: "fail-pipeline" - (default), will validate against the validation and fail the pipeline if it fails. "ignore-validation" - ignore the results of the validation and continue the pipeline |
`budget_milli_node_hours` |
`int`
Optional. The train budget of creating this Model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a Model for the given training set, the training won't be attempted and will error. The minimum value is 1000 and the maximum is 72000. |
`model_display_name` |
`str`
Optional. If the script produces a managed Vertex AI Model. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
`model_labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`model_id` |
`str`
Optional. The ID to use for the Model produced by this job, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model. The new model uploaded by this job will be a version of |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of the model produced by this job without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the model version produced by this job will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`model_version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that the model version uploaded by this job can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`model_version_description` |
`str`
Optional. The description of the model version being uploaded by this job. |
`additional_experiments` |
`List[str]`
Optional. Additional experiment flags for the time series forcasting training. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`hierarchy_group_columns` |
`List[str]`
Optional. A list of time series attribute column names that define the time series hierarchy. Only one level of hierarchy is supported, ex. |
`hierarchy_group_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over time series in the same hierarchy group. |
`hierarchy_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over the horizon for a single time series. |
`hierarchy_group_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over both the horizon and time series in the same hierarchy group. |
`window_column` |
`str`
Optional. Name of the column that should be used to filter input rows. The column should contain either booleans or string booleans; if the value of the row is True, generate a sliding window from that row. |
`window_stride_length` |
`int`
Optional. Step length used to generate input examples. Every |
`window_max_count` |
`int`
Optional. Number of rows that should be used to generate input examples. If the total row count is larger than this number, the input data will be randomly sampled to hit the count. |
`holiday_regions` |
`List[str]`
Optional. The geographical regions to use when creating holiday features. This option is only allowed when data_granularity_unit is |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_probabilistic_inference` |
`bool`
If probabilistic inference is enabled, the model will fit a distribution that captures the uncertainty of a prediction. At inference time, the predictive distribution is used to make a point prediction that minimizes the optimization objective. For example, the mean of a predictive distribution is the point prediction that minimizes RMSE loss. If quantiles are specified, then the quantiles of the distribution are also returned. The optimization objective cannot be minimize-quantile-loss. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run or is waiting to run. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource or None if training did not produce a Vertex AI Model. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until the resource has been created.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesdataitemlabelsentry_googlecloudaiplatform_v1typ_16f894.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesdataitemlabelsentry_googlecloudaiplatform_v1type_8c2c29.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesdataitemlabelsentry_googlecloudaiplatform_v1types_6c3fec.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdataitemlabelsentry_googlecloudaiplatform_v1typest_f14f97.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdataitemlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DataItem.LabelsEntry -->

# Class LabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestuningjoblabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TuningJob.LabelsEntry -->

# Class LabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanationmetadataoutputmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.OutputMetadata -->

# Class OutputMetadata (1.134.0)

`OutputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the prediction output to be explained.

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
`index_display_name_mapping` |
`google.protobuf.struct_pb2.Value`
Static mapping between the index and display name. Use this if the outputs are a deterministic n-dimensional array, e.g. a list of scores of all the classes in a pre-defined order for a multi-classification Model. It's not feasible if the outputs are non-deterministic, e.g. the Model produces top-k classes or sort the outputs by their values. The shape of the value must be an n-dimensional array of strings. The number of dimensions must match that of the outputs to be explained. The Attribution.output_display_name is populated by locating in the mapping with Attribution.output_index. This field is a member of `oneof` _ `display_name_mapping` .
|
`display_name_mapping_key` |
`str`
Specify a field name in the prediction to look for the display name. Use this if the prediction contains the display names for the outputs. The display names in the prediction must have the same shape of the outputs, so that it can be located by Attribution.output_index for a specific output. This field is a member of `oneof` _ `display_name_mapping` .
|
`output_tensor_name` |
`str`
Name of the output tensor. Required and is only applicable to Vertex AI provided images for Tensorflow. |

## Methods

### OutputMetadata

`OutputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the prediction output to be explained.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesslacksourceslackchannels_googlecloudaiplatformv1s_9d7c18.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesslacksourceslackchannels_googlecloudaiplatformv1sc_1aaced.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesslacksourceslackchannels.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SlackSource.SlackChannels -->

# Class SlackChannels (1.134.0)

`SlackChannels(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannels contains the Slack channels and corresponding access token.

## Attributes |
|
|---|---|
Name |
Description |
`channels` |
`MutableSequence[`
Required. The Slack channel IDs. |
`api_key_config` |
Required. The SecretManager secret version resource name (e.g. projects/{project}/secrets/{secret}/versions/{version}) storing the Slack channel access token that has access to the slack channel IDs. See: https://api.slack.com/tutorials/tracks/getting-a-token. |

## Classes

### SlackChannel

`SlackChannel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannel contains the Slack channel ID and the time range to import.

## Methods

### SlackChannels

`SlackChannels(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannels contains the Slack channels and corresponding access token.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimageobjectdetectionmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata -->

# Class AutoMlImageObjectDetectionMetadata (1.134.0)

```
AutoMlImageObjectDetectionMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`cost_milli_node_hours` |
`int`
The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours. |
`successful_stop_reason` |
For successful job completions, this is the reason why the job has finished. |

## Classes

### SuccessfulStopReason

`SuccessfulStopReason(value)`


## Methods

### AutoMlImageObjectDetectionMetadata

```
AutoMlImageObjectDetectionMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageObjectDetectionMetadata

```
AutoMlImageObjectDetectionMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesrougeinstance_googlecloudaiplatform_v1typesartifac_ba112c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesrougeinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RougeInstance -->

# Class RougeInstance (1.134.0)

`RougeInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge instance.

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

### RougeInstance

`RougeInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesartifactlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Artifact.LabelsEntry -->

# Class LabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesstudy_googlecloudaiplatform_v1typesimportra_45a94e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesstudy_googlecloudaiplatform_v1typesimportrag_634db7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstudy_googlecloudaiplatform_v1typesimportragf_a27bfa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Study -->

# Class Study (1.134.0)

`Study(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Study.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The name of a study. The study's globally unique identifier. Format: `projects/{project}/locations/{location}/studies/{study}`
|
`display_name` |
`str`
Required. Describes the Study, default value is empty string. |
`study_spec` |
Required. Configuration of the Study. |
`state` |
Output only. The detailed state of a Study. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time at which the study was created. |
`inactive_reason` |
`str`
Output only. A human readable reason why the Study is inactive. This should be empty if a study is ACTIVE or COMPLETED. |

## Classes

### State

`State(value)`


Describes the Study state.

## Methods

### Study

`Study(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Study.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesimportragfilesoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportRagFilesOperationMetadata -->

# Class ImportRagFilesOperationMetadata (1.134.0)

```
ImportRagFilesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for VertexRagDataService.ImportRagFiles.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`rag_corpus_id` |
`int`
The resource ID of RagCorpus that this operation is executed on. |
`import_rag_files_config` |
Output only. The config that was passed in the ImportRagFilesRequest. |
`progress_percentage` |
`int`
The progress percentage of the operation. Value is in the range [0, 100]. This percentage is calculated as follows: progress_percentage = 100 \* (successes + failures + skips) / total |

## Methods

### ImportRagFilesOperationMetadata

```
ImportRagFilesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for VertexRagDataService.ImportRagFiles.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesretrievalconfig_googlecloudaiplatform_v1beta1types_b0c9e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesretrievalconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrievalConfig -->

# Class RetrievalConfig (1.134.0)

`RetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Retrieval config.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`lat_lng` |
`google.type.latlng_pb2.LatLng`
The location of the user. This field is a member of `oneof` _ `_lat_lng` .
|
`language_code` |
`str`
The language code of the user. This field is a member of `oneof` _ `_language_code` .
|

## Methods

### RetrievalConfig

`RetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Retrieval config.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringstatsdatapointtypedvaluedistributiondatavalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringStatsDataPoint.TypedValue.DistributionDataValue -->

# Class DistributionDataValue (1.134.0)

`DistributionDataValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary statistics for a population of values.

## Attributes |
|
|---|---|
Name |
Description |
`distribution` |
`google.protobuf.struct_pb2.Value`
Predictive monitoring drift distribution in `tensorflow.metadata.v0.DatasetFeatureStatistics` format.
|
`distribution_deviation` |
`float`
Distribution distance deviation from the current dataset's statistics to baseline dataset's statistics. - For categorical feature, the distribution distance is calculated by L-inifinity norm or Jensen–Shannon divergence. - For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. |

## Methods

### DistributionDataValue

`DistributionDataValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary statistics for a population of values.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltable_5d61ce.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltablesinputstransformationtimestamptransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.TimestampTransformation -->

# Class TimestampTransformation (1.134.0)

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- Apply the transformation functions for Numerical columns.
- Determine the year, month, day,and weekday. Treat each value from the
- timestamp as a Categorical column.
- Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

## Attributes |
|
|---|---|
Name |
Description |
`time_format` |
`str`
The format in which that time field is expressed. The time_format must either be one of: - `unix-seconds`
- `unix-milliseconds`
- `unix-microseconds`
- `unix-nanoseconds` (for respectively number of seconds,
milliseconds, microseconds and nanoseconds since start of
the Unix epoch); or be written in `strftime` syntax. If
time_format is not set, then the default format is RFC
3339 `date-time` format, where `time-offset` = `"Z"`
(e.g. 1985-04-12T23:20:50.52Z)
|
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- Apply the transformation functions for Numerical columns.
- Determine the year, month, day,and weekday. Treat each value from the
- timestamp as a Categorical column.
- Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- Apply the transformation functions for Numerical columns.
- Determine the year, month, day,and weekday. Treat each value from the
- timestamp as a Categorical column.
- Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgetmodelrequest_googlecloudaiplatform_v1beta1_cafceb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetmodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelRequest -->

# Class GetModelRequest (1.134.0)

`GetModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.GetModel.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Model resource. Format: `projects/{project}/locations/{location}/models/{model}`
In order to retrieve a specific version of the model, also
provide the version ID or version alias. Example:
`projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
If no version ID or alias is specified, the "default"
version will be returned. The "default" version alias is
created for the first version of the model, and can be moved
to other versions later on. There will be exactly one
default version.
|

## Methods

### GetModelRequest

`GetModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.GetModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescustomoutputformatconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomOutputFormatConfig -->

# Class CustomOutputFormatConfig (1.134.0)

`CustomOutputFormatConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for custom output format configuration.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`return_raw_output` |
`bool`
Optional. Whether to return raw output. This field is a member of `oneof` _ `custom_output_format_config` .
|

## Methods

### CustomOutputFormatConfig

`CustomOutputFormatConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for custom output format configuration.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformtemporalfusiontransformerforecastingtrainingjob___googlecl_f0e6bb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformtemporalfusiontransformerforecastingtrainingjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob -->

# Class TemporalFusionTransformerForecastingTrainingJob (1.134.0)

```
TemporalFusionTransformerForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Class to train Temporal Fusion Transformer (TFT) forecasting models.

The `TemporalFusionTransformerForecastingTrainingJob`

class uses the
Temporal Fusion Transformer (TFT) training method to train and run a
forecasting model. The TFT training method implements an attention-based
deep neural network (DNN) model that uses a multi-horizon forecasting task
to produce predictions.

For sample code that shows you how to use
`TemporalFusionTransformerForecastingTrainingJob, see the
[Create a training pipeline forecasting temporal fusion transformer
sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_tft_sample.py)
on GitHub.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Optional. The time when the training job entered the
`PIPELINE_STATE_SUCCEEDED`

, `PIPELINE_STATE_FAILED`

, or
`PIPELINE_STATE_CANCELLED`

state.

### error

Optional. Detailed error information for this training job resource.
Error information is created only when the state of the training job is
`PIPELINE_STATE_FAILED`

or `PIPELINE_STATE_CANCELLED`

.

### evaluated_data_items_bigquery_uri

BigQuery location of exported evaluated examples from the Training Job

Returns |
|
|---|---|
Type |
Description |
`str` |
BigQuery uri for the exported evaluated examples if the export feature is enabled for training. None: If the export feature was not enabled for training. |

### gca_resource

The underlying resource proto representation.

### has_failed

Returns `true`

if the training job failed, otherwise `false`

.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### start_time

Optional. The time when the training job first entered the
`PIPELINE_STATE_RUNNING`

state.

### state

Current training state.

### update_time

Time this resource was last updated.

## Methods

### TemporalFusionTransformerForecastingTrainingJob

```
TemporalFusionTransformerForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Constructs a Forecasting Training Job.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of this TrainingPipeline. |
`optimization_objective` |
`str`
Optional. Objective function the model is to be optimized towards. The training process creates a Model that optimizes the value of the objective function over the validation set. The supported optimization objectives: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE). "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE). "minimize-quantile-loss" - Minimize the quantile loss at the defined quantiles. (Set this objective to build quantile forecasts.) |
`column_specs` |
`Dict[str, str]`
Optional. Alternative to column_transformations where the keys of the dict are column names and their respective values are one of AutoMLTabularTrainingJob.column_data_types. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. |
`column_transformations` |
`List[Dict[str, Dict[str, str]]]`
Optional. Transformations to apply to the input columns (i.e. columns other than the targetColumn). Each transformation may produce multiple result values from the column's value, and all are used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. Consider using column_specs as column_transformations will be deprecated eventually. |
`project` |
`str`
Optional. Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both column_transformations and column_specs were provided. |

### cancel

`cancel() -> None`


Asynchronously attempts to cancel a training job.

The server makes a best effort to cancel the job, but the training job
can't always be cancelled. If the training job is canceled, its state
transitions to `CANCELLED`

and it's not deleted.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If this training job isn't running, then a runtime error is raised. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.training_jobs._TrainingJob
```


Gets a training job using the `resource_name`

that's passed in.

Parameters |
|
|---|---|
Name |
Description |
`resource_name` |
`str`
Required. A fully-qualified resource name or ID. |
`project` |
`str`
Optional. The name of the Google Cloud project to retrieve the training job from. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job is retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload this model. These credentials override the credentials set by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A `ValueError` is raised if the task definition of the retrieved training job doesn't match the custom training task definition. |

### get_model

`get_model(sync=True) -> google.cloud.aiplatform.models.Model`


Returns the Vertex AI model produced by this training job.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
If set to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
A runtime error is raised if the training job failed or if a model wasn't produced by the training job. |

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


Lists all instances of this training job resource.

The following shows an example of how to call `CustomTrainingJob.list`

:

```
aiplatform.CustomTrainingJob.list(
filter='display_name="experiment_a27"',
order_by='create_time desc'
)
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names, snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields used to sort the returned traing job resources. The defauilt sorting order is ascending. To sort by a field name in descending order, use |
`project` |
`str`
Optional. The name of the Google Cloud project to which to retrieve the list of training job resources. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job resources are retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to retrieve list. These credentials override the credentials set by |

Returns |
|
|---|---|
Type |
Description |
`List[VertexAiResourceNoun]` |
A list of training job resources. |

### run

```
run(
dataset: google.cloud.aiplatform.datasets.time_series_dataset.TimeSeriesDataset,
target_column: str,
time_column: str,
time_series_identifier_column: str,
unavailable_at_forecast_columns: typing.List[str],
available_at_forecast_columns: typing.List[str],
forecast_horizon: int,
data_granularity_unit: str,
data_granularity_count: int,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
predefined_split_column_name: typing.Optional[str] = None,
timestamp_split_column_name: typing.Optional[str] = None,
weight_column: typing.Optional[str] = None,
time_series_attribute_columns: typing.Optional[typing.List[str]] = None,
context_window: typing.Optional[int] = None,
export_evaluated_data_items: bool = False,
export_evaluated_data_items_bigquery_destination_uri: typing.Optional[str] = None,
export_evaluated_data_items_override_destination: bool = False,
quantiles: typing.Optional[typing.List[float]] = None,
validation_options: typing.Optional[str] = None,
budget_milli_node_hours: int = 1000,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
additional_experiments: typing.Optional[typing.List[str]] = None,
hierarchy_group_columns: typing.Optional[typing.List[str]] = None,
hierarchy_group_total_weight: typing.Optional[float] = None,
hierarchy_temporal_total_weight: typing.Optional[float] = None,
hierarchy_group_temporal_total_weight: typing.Optional[float] = None,
window_column: typing.Optional[str] = None,
window_stride_length: typing.Optional[int] = None,
window_max_count: typing.Optional[int] = None,
holiday_regions: typing.Optional[typing.List[str]] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
enable_probabilistic_inference: bool = False,
) -> google.cloud.aiplatform.models.Model
```


Runs the training job and returns a model.

If training on a Vertex AI dataset, you can use one of the following split configurations:
Data fraction splits:
Any of `training_fraction_split`

, `validation_fraction_split`

and
`test_fraction_split`

may optionally be provided, they must sum to up to 1. If
the provided ones sum to less than 1, the remainder is assigned to sets as
decided by Vertex AI. If none of the fractions are set, by default roughly 80%
of data will be used for training, 10% for validation, and 10% for test.

```
Predefined splits:
Assigns input data to training, validation, and test sets based on the value of a provided key.
If using predefined splits, `predefined_split_column_name` must be provided.
Supported only for tabular Datasets.
Timestamp splits:
Assigns input data to training, validation, and test sets
based on a provided timestamps. The youngest data pieces are
assigned to training set, next to validation set, and the oldest
to the test set.
Supported only for tabular Datasets.
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TimeSeriesDataset`
Required. The dataset within the same Project from which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. For time series Datasets, all their data is exported to training, to pick and choose from. |
`target_column` |
`str`
Required. Name of the column that the Model is to predict values for. This column must be unavailable at forecast. |
`time_column` |
`str`
Required. Name of the column that identifies time order in the time series. This column must be available at forecast. |
`time_series_identifier_column` |
`str`
Required. Name of the column that identifies the time series. |
`unavailable_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are unavailable at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is unknown before the forecast (e.g. population of a city in a given year, or weather on a given day). |
`available_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are available at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is known at forecast. |
`data_granularity_unit` |
`str`
Required. The data granularity unit. Accepted values are |
`data_granularity_count` |
`int`
Required. The number of data granularity units between data points in the training data. If [data_granularity_unit] is |
`predefined_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { |
`timestamp_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key values of the key (the values in the column) must be in RFC 3339 |
`weight_column` |
`str`
Optional. Name of the column that should be used as the weight column. Higher values in this column give more importance to the row during Model training. The column must have numeric values between 0 and 10000 inclusively, and 0 value means that the row is ignored. If the weight column field is not set, then all rows are assumed to have equal weight of 1. |
`time_series_attribute_columns` |
`List[str]`
Optional. Column names that should be used as attribute columns. Each column is constant within a time series. |
`context_window` |
`int`
Optional. The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the [data_granularity_unit] and [data_granularity_count] fields. When not provided uses the default value of 0 which means the model sets each series context window to be 0 (also known as "cold start"). Inclusive. |
`export_evaluated_data_items` |
`bool`
Whether to export the test set predictions to a BigQuery table. If False, then the export is not performed. |
`export_evaluated_data_items_bigquery_destination_uri` |
`string`
Optional. URI of desired destination BigQuery table for exported test set predictions. Expected format: `<project_id>:export_evaluated_examples_<model_name>_<yyyy_MM_dd'T'HH_mm_ss_SSS'Z'>.evaluated_examples` Applies only if [export_evaluated_data_items] is True.
|
`export_evaluated_data_items_override_destination` |
`bool`
Whether to override the contents of [export_evaluated_data_items_bigquery_destination_uri], if the table exists, for exported test set predictions. If False, and the table exists, then the training job will fail. Applies only if [export_evaluated_data_items] is True and [export_evaluated_data_items_bigquery_destination_uri] is specified. |
`quantiles` |
`List[float]`
Quantiles to use for the |
`validation_options` |
`str`
Validation options for the data validation component. The available options are: "fail-pipeline" - (default), will validate against the validation and fail the pipeline if it fails. "ignore-validation" - ignore the results of the validation and continue the pipeline |
`budget_milli_node_hours` |
`int`
Optional. The train budget of creating this Model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a Model for the given training set, the training won't be attempted and will error. The minimum value is 1000 and the maximum is 72000. |
`model_display_name` |
`str`
Optional. If the script produces a managed Vertex AI Model. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
`model_labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`model_id` |
`str`
Optional. The ID to use for the Model produced by this job, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model. The new model uploaded by this job will be a version of |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of the model produced by this job without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the model version produced by this job will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`model_version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that the model version uploaded by this job can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`model_version_description` |
`str`
Optional. The description of the model version being uploaded by this job. |
`additional_experiments` |
`List[str]`
Optional. Additional experiment flags for the time series forcasting training. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`hierarchy_group_columns` |
`List[str]`
Optional. A list of time series attribute column names that define the time series hierarchy. Only one level of hierarchy is supported, ex. |
`hierarchy_group_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over time series in the same hierarchy group. |
`hierarchy_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over the horizon for a single time series. |
`hierarchy_group_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over both the horizon and time series in the same hierarchy group. |
`window_column` |
`str`
Optional. Name of the column that should be used to filter input rows. The column should contain either booleans or string booleans; if the value of the row is True, generate a sliding window from that row. |
`window_stride_length` |
`int`
Optional. Step length used to generate input examples. Every |
`window_max_count` |
`int`
Optional. Number of rows that should be used to generate input examples. If the total row count is larger than this number, the input data will be randomly sampled to hit the count. |
`holiday_regions` |
`List[str]`
Optional. The geographical regions to use when creating holiday features. This option is only allowed when data_granularity_unit is |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_probabilistic_inference` |
`bool`
If probabilistic inference is enabled, the model will fit a distribution that captures the uncertainty of a prediction. At inference time, the predictive distribution is used to make a point prediction that minimizes the optimization objective. For example, the mean of a predictive distribution is the point prediction that minimizes RMSE loss. If quantiles are specified, then the quantiles of the distribution are also returned. The optimization objective cannot be minimize-quantile-loss. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run or is waiting to run. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource or None if training did not produce a Vertex AI Model. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until the resource has been created.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesnotebookruntime_googlecloudaiplatform_v1typesinpu_8b62be.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnotebookruntime_googlecloudaiplatform_v1typesinput_ef3506.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnotebookruntime.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntime -->

# Class NotebookRuntime (1.134.0)

`NotebookRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the NotebookRuntime. |
`runtime_user` |
`str`
Required. The user email of the NotebookRuntime. |
`notebook_runtime_template_ref` |
Output only. The pointer to NotebookRuntimeTemplate this NotebookRuntime is created from. |
`proxy_uri` |
`str`
Output only. The proxy endpoint used to access the NotebookRuntime. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookRuntime was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookRuntime was most recently updated. |
`health_state` |
Output only. The health state of the NotebookRuntime. |
`display_name` |
`str`
Required. The display name of the NotebookRuntime. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the NotebookRuntime. |
`service_account` |
`str`
Output only. Deprecated: This field is no longer used and the "Vertex AI Notebook Service Account" (service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com) is used for the runtime workload identity. See https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account for more details. The service account that the NotebookRuntime workload runs as. |
`runtime_state` |
Output only. The runtime (instance) state of the NotebookRuntime. |
`is_upgradable` |
`bool`
Output only. Whether NotebookRuntime is upgradable. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your NotebookRuntime. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one NotebookRuntime (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for NotebookRuntime: - "aiplatform.googleapis.com/notebook_runtime_gce_instance_id": output only, its value is the Compute Engine instance id. - "aiplatform.googleapis.com/colab_enterprise_entry_service": its value is either "bigquery" or "vertex"; if absent, it should be "vertex". This is to describe the entry service, either BigQuery or Vertex. |
`expiration_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookRuntime will be expired: 1. System Predefined NotebookRuntime: 24 hours after creation. After expiration, system predifined runtime will be deleted. 2. User created NotebookRuntime: 6 months after last upgrade. After expiration, user created runtime will be stopped and allowed for upgrade. |
`version` |
`str`
Output only. The VM os image version of NotebookRuntime. |
`notebook_runtime_type` |
Output only. The type of the notebook runtime. |
`machine_spec` |
Output only. The specification of a single machine used by the notebook runtime. |
`data_persistent_disk_spec` |
Output only. The specification of [persistent disk][https://cloud.google.com/compute/docs/disks/persistent-disks] attached to the notebook runtime as data disk storage. |
`network_spec` |
Output only. Network spec of the notebook runtime. |
`idle_shutdown_config` |
Output only. The idle shutdown configuration of the notebook runtime. |
`euc_config` |
Output only. EUC configuration of the notebook runtime. |
`shielded_vm_config` |
Output only. Runtime Shielded VM spec. |
`network_tags` |
`MutableSequence[str]`
Optional. The Compute Engine tags to add to runtime (see `Tagging instances |
`software_config` |
Output only. Software config of the notebook runtime. |
`encryption_spec` |
Output only. Customer-managed encryption key spec for the notebook runtime. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### HealthState

`HealthState(value)`


The substate of the NotebookRuntime to display health information.

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

### RuntimeState

`RuntimeState(value)`


The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

## Methods

### NotebookRuntime

`NotebookRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesinputdataconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.InputDataConfig -->

# Class InputDataConfig (1.134.0)

`InputDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies Vertex AI owned input data to be used for training, and possibly evaluating, the Model.

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
`fraction_split` |
Split based on fractions defining the size of each set. This field is a member of `oneof` _ `split` .
|
`filter_split` |
Split based on the provided filters for each set. This field is a member of `oneof` _ `split` .
|
`predefined_split` |
Supported only for tabular Datasets. Split based on a predefined key. This field is a member of `oneof` _ `split` .
|
`timestamp_split` |
Supported only for tabular Datasets. Split based on the timestamp of the input data pieces. This field is a member of `oneof` _ `split` .
|
`stratified_split` |
Supported only for tabular Datasets. Split based on the distribution of the specified column. This field is a member of `oneof` _ `split` .
|
`gcs_destination` |
The Cloud Storage location where the training data is to be written to. In the given directory a new directory is created with name: `dataset-`
where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601
format. All training input data is written into that
directory.
The Vertex AI environment variables representing Cloud
Storage data URIs are represented in the Cloud Storage
wildcard format to support sharded data. e.g.:
"gs://.../training-\*.jsonl"
- AIP_DATA_FORMAT = "jsonl" for non-tabular data, "csv" for
tabular data
- AIP_TRAINING_DATA_URI =
"gcs_destination/dataset---/training-\*.${AIP_DATA_FORMAT}"
- AIP_VALIDATION_DATA_URI =
"gcs_destination/dataset---/validation-\*.${AIP_DATA_FORMAT}"
- AIP_TEST_DATA_URI =
"gcs_destination/dataset---/test-\*.${AIP_DATA_FORMAT}".
This field is a member of `oneof` _ `destination` .
|
`bigquery_destination` |
Only applicable to custom training with tabular Dataset with BigQuery source. The BigQuery project location where the training data is to be written to. In the given project a new dataset is created with name `dataset_`
where timestamp is in YYYY_MM_DDThh_mm_ss_sssZ format. All
training input data is written into that dataset. In the
dataset three tables are created, `training` ,
`validation` and `test` .
- AIP_DATA_FORMAT = "bigquery".
- AIP_TRAINING_DATA_URI =
"bigquery_destination.dataset\_\ **\ .training"
- AIP_VALIDATION_DATA_URI =
"bigquery_destination.dataset\_\ **\ .validation"
- AIP_TEST_DATA_URI =
"bigquery_destination.dataset\_\ **\ .test".
This field is a member of `oneof` _ `destination` .
|
`dataset_id` |
`str`
Required. The ID of the Dataset in the same Project and Location which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1.TrainingPipeline.training_task_definition]. For tabular Datasets, all their data is exported to training, to pick and choose from. |
`annotations_filter` |
`str`
Applicable only to Datasets that have DataItems and Annotations. A filter on Annotations of the Dataset. Only Annotations that both match this filter and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on (for the auto-assigned that role is decided by Vertex AI). A filter with same syntax as the one used in ListAnnotations may be used, but note here it filters across all Annotations of the Dataset, and not just within a single DataItem. |
`annotation_schema_uri` |
`str`
Applicable only to custom training with Datasets that have DataItems and Annotations. Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`saved_query_id` |
`str`
Only applicable to Datasets that have SavedQueries. The ID of a SavedQuery (annotation set) under the Dataset specified by dataset_id used for filtering Annotations for training. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`persist_ml_use_assignment` |
`bool`
Whether to persist the ML use assignment to data item system labels. |

## Methods

### InputDataConfig

`InputDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies Vertex AI owned input data to be used for training, and possibly evaluating, the Model.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typescreateentitytyperequest_googlecloudaiplatfo_744795.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescreateentitytyperequest_googlecloudaiplatfor_19d1a0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreateentitytyperequest_googlecloudaiplatform_7e50b4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreateentitytyperequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEntityTypeRequest -->

# Class CreateEntityTypeRequest (1.134.0)

`CreateEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateEntityType.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Featurestore to create EntityTypes. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`entity_type` |
The EntityType to create. |
`entity_type_id` |
`str`
Required. The ID to use for the EntityType, which will become the final component of the EntityType's resource name. This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within a featurestore.
|

## Methods

### CreateEntityTypeRequest

`CreateEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateEntityType.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictparams_v1typesimagesegmentationpredictionparams.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.ImageSegmentationPredictionParams -->

# Class ImageSegmentationPredictionParams (1.134.0)

```
ImageSegmentationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Segmentation.

## Attribute |
|
|---|---|
Name |
Description |
`confidence_threshold` |
`float`
When the model predicts category of pixels of the image, it will only provide predictions for pixels that it is at least this much confident about. All other pixels will be classified as background. Default value is 0.5. |

## Methods

### ImageSegmentationPredictionParams

```
ImageSegmentationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Segmentation.

### ImageSegmentationPredictionParams

```
ImageSegmentationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Segmentation.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestrialcontext_googlecloudaiplatform_v1typesbatchcre_4c7009.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestrialcontext.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TrialContext -->

# Class TrialContext (1.134.0)

`TrialContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`description` |
`str`
A human-readable field which can store a description of this context. This will become part of the resulting Trial's description field. |
`parameters` |
`MutableSequence[`
If/when a Trial is generated or selected from this Context, its Parameters will match any parameters specified here. (I.e. if this context specifies parameter name:'a' int_value:3, then a resulting Trial will have int_value:3 for its parameter named 'a'.) Note that we first attempt to match existing REQUESTED Trials with contexts, and if there are no matches, we generate suggestions in the subspace defined by the parameters specified here. NOTE: a Context without any Parameters matches the entire feasible search space. |

## Methods

### TrialContext

`TrialContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchcreatetensorboardrunsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateTensorboardRunsRequest -->

# Class BatchCreateTensorboardRunsRequest (1.134.0)

```
BatchCreateTensorboardRunsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchCreateTensorboardRuns.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the TensorboardExperiment to create the TensorboardRuns in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
The parent field in the CreateTensorboardRunRequest messages
must match this field.
|
`requests` |
`MutableSequence[`
Required. The request message specifying the TensorboardRuns to create. A maximum of 1000 TensorboardRuns can be created in a batch. |

## Methods

### BatchCreateTensorboardRunsRequest

```
BatchCreateTensorboardRunsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchCreateTensorboardRuns.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistannotationsrequest_googlecloudaiplatform_v1ty_0b388c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistannotationsrequest_googlecloudaiplatform_v1typ_5fb435.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistannotationsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsRequest -->

# Class ListAnnotationsRequest (1.134.0)

`ListAnnotationsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListAnnotations.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the DataItem to list Annotations from. Format: `projects/{project}/locations/{location}/datasets/{dataset}/dataItems/{data_item}`
|
`filter` |
`str`
The standard list filter. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. |

## Methods

### ListAnnotationsRequest

`ListAnnotationsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListAnnotations.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesendpointlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.LabelsEntry -->

# Class LabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistspecialistpoolsrequest_googlecloudaiplatform_v_68e135.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistspecialistpoolsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsRequest -->

# Class ListSpecialistPoolsRequest (1.134.0)

`ListSpecialistPoolsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.ListSpecialistPools.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the SpecialistPool's parent resource. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained by ListSpecialistPoolsResponse.next_page_token of the previous SpecialistPoolService.ListSpecialistPools call. Return first page if empty. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. FieldMask represents a set of |

## Methods

### ListSpecialistPoolsRequest

`ListSpecialistPoolsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.ListSpecialistPools.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmodelevaluationsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationsRequest -->

# Class ListModelEvaluationsRequest (1.134.0)

`ListModelEvaluationsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModelEvaluations.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Model to list the ModelEvaluations from. Format: `projects/{project}/locations/{location}/models/{model}`
|
`filter` |
`str`
The standard list filter. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListModelEvaluationsResponse.next_page_token of the previous ModelService.ListModelEvaluations call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListModelEvaluationsRequest

`ListModelEvaluationsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModelEvaluations.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesschedule_servicescheduleserviceclient__goo_f384ef.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesschedule_servicescheduleserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient -->

# Class ScheduleServiceClient (1.134.0)

```
ScheduleServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.schedule_service.transports.base.ScheduleServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.schedule_service.transports.base.ScheduleServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's Schedule resources to periodically launch shceudled runs to make API calls.

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
`ScheduleServiceTransport` |
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

### ScheduleServiceClient

```
ScheduleServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.schedule_service.transports.base.ScheduleServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.schedule_service.transports.base.ScheduleServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the schedule service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ScheduleServiceTransport,Callable[..., ScheduleServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the ScheduleServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### batch_prediction_job_path

```
batch_prediction_job_path(
project: str, location: str, batch_prediction_job: str
) -> str
```


Returns a fully-qualified batch_prediction_job string.

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

### create_schedule

```
create_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.CreateScheduleRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
schedule: typing.Optional[
google.cloud.aiplatform_v1beta1.types.schedule.Schedule
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.schedule.Schedule
```


Creates a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
schedule = aiplatform_v1beta1.[Schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schedule.html)()
schedule.cron = "cron_value"
schedule.create_pipeline_job_request.parent = "parent_value"
schedule.display_name = "display_name_value"
schedule.max_concurrent_run_count = 2596
request = aiplatform_v1beta1.[CreateScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateScheduleRequest.html)(
parent="parent_value",
schedule=schedule,
)
# Make the request
response = client.[create_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_create_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.CreateSchedule. |
`parent` |
`str`
Required. The resource name of the Location to create the Schedule in. Format: |
`schedule` |
Required. The Schedule to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

### custom_job_path

`custom_job_path(project: str, location: str, custom_job: str) -> str`


Returns a fully-qualified custom_job string.

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

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

### delete_schedule

```
delete_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.DeleteScheduleRequest,
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


Deletes a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteScheduleRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_delete_schedule)(request=request)
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
The request object. Request message for ScheduleService.DeleteSchedule. |
`name` |
`str`
Required. The name of the Schedule resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`ScheduleServiceClient` |
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
`ScheduleServiceClient` |
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
`ScheduleServiceClient` |
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

### get_schedule

```
get_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.GetScheduleRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.schedule.Schedule
```


Gets a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetScheduleRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_get_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.GetSchedule. |
`name` |
`str`
Required. The name of the Schedule resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

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

### list_schedules

```
list_schedules(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
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
google.cloud.aiplatform_v1beta1.services.schedule_service.pagers.ListSchedulesPager
)
```


Lists Schedules in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_schedules():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListSchedulesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_schedules](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_list_schedules)(request=request)
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
The request object. Request message for ScheduleService.ListSchedules. |
`parent` |
`str`
Required. The resource name of the Location to list the Schedules from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ScheduleService.ListSchedules Iterating over this object will yield results and resolve additional pages automatically. |

### model_monitor_path

`model_monitor_path(project: str, location: str, model_monitor: str) -> str`


Returns a fully-qualified model_monitor string.

### model_monitoring_job_path

```
model_monitoring_job_path(
project: str, location: str, model_monitor: str, model_monitoring_job: str
) -> str
```


Returns a fully-qualified model_monitoring_job string.

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

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

### notebook_runtime_template_path

```
notebook_runtime_template_path(
project: str, location: str, notebook_runtime_template: str
) -> str
```


Returns a fully-qualified notebook_runtime_template string.

### parse_artifact_path

`parse_artifact_path(path: str) -> typing.Dict[str, str]`


Parses a artifact path into its component segments.

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

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_model_monitor_path

`parse_model_monitor_path(path: str) -> typing.Dict[str, str]`


Parses a model_monitor path into its component segments.

### parse_model_monitoring_job_path

`parse_model_monitoring_job_path(path: str) -> typing.Dict[str, str]`


Parses a model_monitoring_job path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_execution_job_path

`parse_notebook_execution_job_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_execution_job path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_schedule_path

`parse_schedule_path(path: str) -> typing.Dict[str, str]`


Parses a schedule path into its component segments.

### parse_subnetwork_path

`parse_subnetwork_path(path: str) -> typing.Dict[str, str]`


Parses a subnetwork path into its component segments.

### pause_schedule

```
pause_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.PauseScheduleRequest,
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


Pauses a Schedule. Will mark xref_Schedule.state to 'PAUSED'. If the schedule is paused, no new runs will be created. Already created runs will NOT be paused or canceled.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_pause_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[PauseScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PauseScheduleRequest.html)(
name="name_value",
)
# Make the request
client.[pause_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_pause_schedule)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.PauseSchedule. |
`name` |
`str`
Required. The name of the Schedule resource to be paused. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### resume_schedule

```
resume_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.ResumeScheduleRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
catch_up: typing.Optional[bool] = None,
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


Resumes a paused Schedule to start scheduling new runs. Will mark xref_Schedule.state to 'ACTIVE'. Only paused Schedule can be resumed.

When the Schedule is resumed, new runs will be scheduled starting from the next execution time after the current time based on the time_specification in the Schedule. If [Schedule.catchUp][] is set up true, all missed runs will be scheduled for backfill first.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_resume_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ResumeScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResumeScheduleRequest.html)(
name="name_value",
)
# Make the request
client.[resume_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_resume_schedule)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.ResumeSchedule. |
`name` |
`str`
Required. The name of the Schedule resource to be resumed. Format: |
`catch_up` |
`bool`
Optional. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. This will also update Schedule.catch_up field. Default to false. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

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

### update_schedule

```
update_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.UpdateScheduleRequest,
dict,
]
] = None,
*,
schedule: typing.Optional[
google.cloud.aiplatform_v1beta1.types.schedule.Schedule
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
) -> google.cloud.aiplatform_v1beta1.types.schedule.Schedule
```


Updates an active or paused Schedule.

When the Schedule is updated, new runs will be scheduled starting from the updated next execution time after the update time based on the time_specification in the updated Schedule. All unstarted runs before the update time will be skipped while already created runs will NOT be paused or canceled.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
schedule = aiplatform_v1beta1.[Schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schedule.html)()
schedule.cron = "cron_value"
schedule.create_pipeline_job_request.parent = "parent_value"
schedule.display_name = "display_name_value"
schedule.max_concurrent_run_count = 2596
request = aiplatform_v1beta1.[UpdateScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateScheduleRequest.html)(
schedule=schedule,
)
# Make the request
response = client.[update_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_update_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.UpdateSchedule. |
`schedule` |
Required. The Schedule which replaces the resource on the server. The following restrictions will be applied: - The scheduled request type cannot be changed. - The non-empty fields cannot be unset. - The output_only fields will be ignored if specified. This corresponds to the |
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
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformsequencetosequenceplusforecastingtrainingjob_____googleclo_3b9357.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformsequencetosequenceplusforecastingtrainingjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.SequenceToSequencePlusForecastingTrainingJob -->

# Class SequenceToSequencePlusForecastingTrainingJob (1.134.0)

```
SequenceToSequencePlusForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Class to train Sequence to Sequence (Seq2Seq) forecasting models.

The `SequenceToSequencePlusForecastingTrainingJob`

class uses the `Seq2seq+`

training method to train and run a forecasting model. The `Seq2seq+`

training method is a good choice for experimentation. Its algorithm is
simpler and uses a smaller search space than the `AutoML`

option. `Seq2seq+`

is a good option if you want fast results and your datasets are smaller than
1 GB.

For sample code that shows you how to use
`SequenceToSequencePlusForecastingTrainingJob`

, see the [Create a training
pipeline forecasting Seq2seq
sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_seq2seq_sample.py)
on GitHub.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Optional. The time when the training job entered the
`PIPELINE_STATE_SUCCEEDED`

, `PIPELINE_STATE_FAILED`

, or
`PIPELINE_STATE_CANCELLED`

state.

### error

Optional. Detailed error information for this training job resource.
Error information is created only when the state of the training job is
`PIPELINE_STATE_FAILED`

or `PIPELINE_STATE_CANCELLED`

.

### evaluated_data_items_bigquery_uri

BigQuery location of exported evaluated examples from the Training Job

Returns |
|
|---|---|
Type |
Description |
`str` |
BigQuery uri for the exported evaluated examples if the export feature is enabled for training. None: If the export feature was not enabled for training. |

### gca_resource

The underlying resource proto representation.

### has_failed

Returns `true`

if the training job failed, otherwise `false`

.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### start_time

Optional. The time when the training job first entered the
`PIPELINE_STATE_RUNNING`

state.

### state

Current training state.

### update_time

Time this resource was last updated.

## Methods

### SequenceToSequencePlusForecastingTrainingJob

```
SequenceToSequencePlusForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Constructs a Forecasting Training Job.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of this TrainingPipeline. |
`optimization_objective` |
`str`
Optional. Objective function the model is to be optimized towards. The training process creates a Model that optimizes the value of the objective function over the validation set. The supported optimization objectives: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE). "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE). "minimize-quantile-loss" - Minimize the quantile loss at the defined quantiles. (Set this objective to build quantile forecasts.) |
`column_specs` |
`Dict[str, str]`
Optional. Alternative to column_transformations where the keys of the dict are column names and their respective values are one of AutoMLTabularTrainingJob.column_data_types. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. |
`column_transformations` |
`List[Dict[str, Dict[str, str]]]`
Optional. Transformations to apply to the input columns (i.e. columns other than the targetColumn). Each transformation may produce multiple result values from the column's value, and all are used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. Consider using column_specs as column_transformations will be deprecated eventually. |
`project` |
`str`
Optional. Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both column_transformations and column_specs were provided. |

### cancel

`cancel() -> None`


Asynchronously attempts to cancel a training job.

The server makes a best effort to cancel the job, but the training job
can't always be cancelled. If the training job is canceled, its state
transitions to `CANCELLED`

and it's not deleted.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If this training job isn't running, then a runtime error is raised. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.training_jobs._TrainingJob
```


Gets a training job using the `resource_name`

that's passed in.

Parameters |
|
|---|---|
Name |
Description |
`resource_name` |
`str`
Required. A fully-qualified resource name or ID. |
`project` |
`str`
Optional. The name of the Google Cloud project to retrieve the training job from. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job is retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload this model. These credentials override the credentials set by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A `ValueError` is raised if the task definition of the retrieved training job doesn't match the custom training task definition. |

### get_model

`get_model(sync=True) -> google.cloud.aiplatform.models.Model`


Returns the Vertex AI model produced by this training job.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
If set to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
A runtime error is raised if the training job failed or if a model wasn't produced by the training job. |

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


Lists all instances of this training job resource.

The following shows an example of how to call `CustomTrainingJob.list`

:

```
aiplatform.CustomTrainingJob.list(
filter='display_name="experiment_a27"',
order_by='create_time desc'
)
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names, snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields used to sort the returned traing job resources. The defauilt sorting order is ascending. To sort by a field name in descending order, use |
`project` |
`str`
Optional. The name of the Google Cloud project to which to retrieve the list of training job resources. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job resources are retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to retrieve list. These credentials override the credentials set by |

Returns |
|
|---|---|
Type |
Description |
`List[VertexAiResourceNoun]` |
A list of training job resources. |

### run

```
run(
dataset: google.cloud.aiplatform.datasets.time_series_dataset.TimeSeriesDataset,
target_column: str,
time_column: str,
time_series_identifier_column: str,
unavailable_at_forecast_columns: typing.List[str],
available_at_forecast_columns: typing.List[str],
forecast_horizon: int,
data_granularity_unit: str,
data_granularity_count: int,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
predefined_split_column_name: typing.Optional[str] = None,
timestamp_split_column_name: typing.Optional[str] = None,
weight_column: typing.Optional[str] = None,
time_series_attribute_columns: typing.Optional[typing.List[str]] = None,
context_window: typing.Optional[int] = None,
export_evaluated_data_items: bool = False,
export_evaluated_data_items_bigquery_destination_uri: typing.Optional[str] = None,
export_evaluated_data_items_override_destination: bool = False,
quantiles: typing.Optional[typing.List[float]] = None,
validation_options: typing.Optional[str] = None,
budget_milli_node_hours: int = 1000,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
additional_experiments: typing.Optional[typing.List[str]] = None,
hierarchy_group_columns: typing.Optional[typing.List[str]] = None,
hierarchy_group_total_weight: typing.Optional[float] = None,
hierarchy_temporal_total_weight: typing.Optional[float] = None,
hierarchy_group_temporal_total_weight: typing.Optional[float] = None,
window_column: typing.Optional[str] = None,
window_stride_length: typing.Optional[int] = None,
window_max_count: typing.Optional[int] = None,
holiday_regions: typing.Optional[typing.List[str]] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
enable_probabilistic_inference: bool = False,
) -> google.cloud.aiplatform.models.Model
```


Runs the training job and returns a model.

If training on a Vertex AI dataset, you can use one of the following split configurations:
Data fraction splits:
Any of `training_fraction_split`

, `validation_fraction_split`

and
`test_fraction_split`

may optionally be provided, they must sum to up to 1. If
the provided ones sum to less than 1, the remainder is assigned to sets as
decided by Vertex AI. If none of the fractions are set, by default roughly 80%
of data will be used for training, 10% for validation, and 10% for test.

```
Predefined splits:
Assigns input data to training, validation, and test sets based on the value of a provided key.
If using predefined splits, `predefined_split_column_name` must be provided.
Supported only for tabular Datasets.
Timestamp splits:
Assigns input data to training, validation, and test sets
based on a provided timestamps. The youngest data pieces are
assigned to training set, next to validation set, and the oldest
to the test set.
Supported only for tabular Datasets.
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TimeSeriesDataset`
Required. The dataset within the same Project from which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. For time series Datasets, all their data is exported to training, to pick and choose from. |
`target_column` |
`str`
Required. Name of the column that the Model is to predict values for. This column must be unavailable at forecast. |
`time_column` |
`str`
Required. Name of the column that identifies time order in the time series. This column must be available at forecast. |
`time_series_identifier_column` |
`str`
Required. Name of the column that identifies the time series. |
`unavailable_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are unavailable at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is unknown before the forecast (e.g. population of a city in a given year, or weather on a given day). |
`available_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are available at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is known at forecast. |
`data_granularity_unit` |
`str`
Required. The data granularity unit. Accepted values are |
`data_granularity_count` |
`int`
Required. The number of data granularity units between data points in the training data. If [data_granularity_unit] is |
`predefined_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { |
`timestamp_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key values of the key (the values in the column) must be in RFC 3339 |
`weight_column` |
`str`
Optional. Name of the column that should be used as the weight column. Higher values in this column give more importance to the row during Model training. The column must have numeric values between 0 and 10000 inclusively, and 0 value means that the row is ignored. If the weight column field is not set, then all rows are assumed to have equal weight of 1. |
`time_series_attribute_columns` |
`List[str]`
Optional. Column names that should be used as attribute columns. Each column is constant within a time series. |
`context_window` |
`int`
Optional. The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the [data_granularity_unit] and [data_granularity_count] fields. When not provided uses the default value of 0 which means the model sets each series context window to be 0 (also known as "cold start"). Inclusive. |
`export_evaluated_data_items` |
`bool`
Whether to export the test set predictions to a BigQuery table. If False, then the export is not performed. |
`export_evaluated_data_items_bigquery_destination_uri` |
`string`
Optional. URI of desired destination BigQuery table for exported test set predictions. Expected format: `<project_id>:export_evaluated_examples_<model_name>_<yyyy_MM_dd'T'HH_mm_ss_SSS'Z'>.evaluated_examples` Applies only if [export_evaluated_data_items] is True.
|
`export_evaluated_data_items_override_destination` |
`bool`
Whether to override the contents of [export_evaluated_data_items_bigquery_destination_uri], if the table exists, for exported test set predictions. If False, and the table exists, then the training job will fail. Applies only if [export_evaluated_data_items] is True and [export_evaluated_data_items_bigquery_destination_uri] is specified. |
`quantiles` |
`List[float]`
Quantiles to use for the |
`validation_options` |
`str`
Validation options for the data validation component. The available options are: "fail-pipeline" - (default), will validate against the validation and fail the pipeline if it fails. "ignore-validation" - ignore the results of the validation and continue the pipeline |
`budget_milli_node_hours` |
`int`
Optional. The train budget of creating this Model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a Model for the given training set, the training won't be attempted and will error. The minimum value is 1000 and the maximum is 72000. |
`model_display_name` |
`str`
Optional. If the script produces a managed Vertex AI Model. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
`model_labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`model_id` |
`str`
Optional. The ID to use for the Model produced by this job, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model. The new model uploaded by this job will be a version of |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of the model produced by this job without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the model version produced by this job will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`model_version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that the model version uploaded by this job can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`model_version_description` |
`str`
Optional. The description of the model version being uploaded by this job. |
`additional_experiments` |
`List[str]`
Optional. Additional experiment flags for the time series forcasting training. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`hierarchy_group_columns` |
`List[str]`
Optional. A list of time series attribute column names that define the time series hierarchy. Only one level of hierarchy is supported, ex. |
`hierarchy_group_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over time series in the same hierarchy group. |
`hierarchy_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over the horizon for a single time series. |
`hierarchy_group_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over both the horizon and time series in the same hierarchy group. |
`window_column` |
`str`
Optional. Name of the column that should be used to filter input rows. The column should contain either booleans or string booleans; if the value of the row is True, generate a sliding window from that row. |
`window_stride_length` |
`int`
Optional. Step length used to generate input examples. Every |
`window_max_count` |
`int`
Optional. Number of rows that should be used to generate input examples. If the total row count is larger than this number, the input data will be randomly sampled to hit the count. |
`holiday_regions` |
`List[str]`
Optional. The geographical regions to use when creating holiday features. This option is only allowed when data_granularity_unit is |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_probabilistic_inference` |
`bool`
If probabilistic inference is enabled, the model will fit a distribution that captures the uncertainty of a prediction. At inference time, the predictive distribution is used to make a point prediction that minimizes the optimization objective. For example, the mean of a predictive distribution is the point prediction that minimizes RMSE loss. If quantiles are specified, then the quantiles of the distribution are also returned. The optimization objective cannot be minimize-quantile-loss. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run or is waiting to run. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource or None if training did not produce a Vertex AI Model. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until the resource has been created.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesentitytypelabelsentry_googlecloudaiplatform_v1b_b922d2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesentitytypelabelsentry_googlecloudaiplatform_v1be_ea46af.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesentitytypelabelsentry_googlecloudaiplatform_v1bet_243358.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesentitytypelabelsentry_googlecloudaiplatform_v1beta_179aac.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesentitytypelabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EntityType.LabelsEntry -->

# Class LabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrialcontext.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrialContext -->

# Class TrialContext (1.134.0)

`TrialContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`description` |
`str`
A human-readable field which can store a description of this context. This will become part of the resulting Trial's description field. |
`parameters` |
`MutableSequence[`
If/when a Trial is generated or selected from this Context, its Parameters will match any parameters specified here. (I.e. if this context specifies parameter name:'a' int_value:3, then a resulting Trial will have int_value:3 for its parameter named 'a'.) Note that we first attempt to match existing REQUESTED Trials with contexts, and if there are no matches, we generate suggestions in the subspace defined by the parameters specified here. NOTE: a Context without any Parameters matches the entire feasible search space. |

## Methods

### TrialContext

`TrialContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexecutionlabelsentry_googlecloudaiplatform_v1types_fad03d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexecutionlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Execution.LabelsEntry -->

# Class LabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescustomjoblabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CustomJob.LabelsEntry -->

# Class LabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesnasjoblabelsentry_googlecloudaiplatform_v1typesmo_9c9b60.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnasjoblabelsentry_googlecloudaiplatform_v1typesmod_5ef197.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnasjoblabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJob.LabelsEntry -->

# Class LabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringstatsanomalies.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringStatsAnomalies -->

# Class ModelMonitoringStatsAnomalies (1.134.0)

```
ModelMonitoringStatsAnomalies(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Statistics and anomalies generated by Model Monitoring.

## Attributes |
|
|---|---|
Name |
Description |
`objective` |
Model Monitoring Objective those stats and anomalies belonging to. |
`deployed_model_id` |
`str`
Deployed Model ID. |
`anomaly_count` |
`int`
Number of anomalies within all stats. |
`feature_stats` |
`MutableSequence[`
A list of historical Stats and Anomalies generated for all Features. |

## Classes

### FeatureHistoricStatsAnomalies

```
FeatureHistoricStatsAnomalies(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Historical Stats (and Anomalies) for a specific Feature.

## Methods

### ModelMonitoringStatsAnomalies

```
ModelMonitoringStatsAnomalies(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Statistics and anomalies generated by Model Monitoring.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesbleuinstance_googlecloudaiplatform_v1beta1typ_059e9d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbleuinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BleuInstance -->

# Class BleuInstance (1.134.0)

`BleuInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for bleu instance.

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

### BleuInstance

`BleuInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for bleu instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistspecialistpoolsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsRequest -->

# Class ListSpecialistPoolsRequest (1.134.0)

`ListSpecialistPoolsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.ListSpecialistPools.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the SpecialistPool's parent resource. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained by ListSpecialistPoolsResponse.next_page_token of the previous SpecialistPoolService.ListSpecialistPools call. Return first page if empty. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. FieldMask represents a set of |

## Methods

### ListSpecialistPoolsRequest

`ListSpecialistPoolsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.ListSpecialistPools.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesinputdataconfig_googlecloudaiplatform_v1beta1_64627a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesinputdataconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.InputDataConfig -->

# Class InputDataConfig (1.134.0)

`InputDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies Vertex AI owned input data to be used for training, and possibly evaluating, the Model.

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
`fraction_split` |
Split based on fractions defining the size of each set. This field is a member of `oneof` _ `split` .
|
`filter_split` |
Split based on the provided filters for each set. This field is a member of `oneof` _ `split` .
|
`predefined_split` |
Supported only for tabular Datasets. Split based on a predefined key. This field is a member of `oneof` _ `split` .
|
`timestamp_split` |
Supported only for tabular Datasets. Split based on the timestamp of the input data pieces. This field is a member of `oneof` _ `split` .
|
`stratified_split` |
Supported only for tabular Datasets. Split based on the distribution of the specified column. This field is a member of `oneof` _ `split` .
|
`gcs_destination` |
The Cloud Storage location where the training data is to be written to. In the given directory a new directory is created with name: `dataset-`
where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601
format. All training input data is written into that
directory.
The Vertex AI environment variables representing Cloud
Storage data URIs are represented in the Cloud Storage
wildcard format to support sharded data. e.g.:
"gs://.../training-\*.jsonl"
- AIP_DATA_FORMAT = "jsonl" for non-tabular data, "csv" for
tabular data
- AIP_TRAINING_DATA_URI =
"gcs_destination/dataset---/training-\*.${AIP_DATA_FORMAT}"
- AIP_VALIDATION_DATA_URI =
"gcs_destination/dataset---/validation-\*.${AIP_DATA_FORMAT}"
- AIP_TEST_DATA_URI =
"gcs_destination/dataset---/test-\*.${AIP_DATA_FORMAT}".
This field is a member of `oneof` _ `destination` .
|
`bigquery_destination` |
Only applicable to custom training with tabular Dataset with BigQuery source. The BigQuery project location where the training data is to be written to. In the given project a new dataset is created with name `dataset_`
where timestamp is in YYYY_MM_DDThh_mm_ss_sssZ format. All
training input data is written into that dataset. In the
dataset three tables are created, `training` ,
`validation` and `test` .
- AIP_DATA_FORMAT = "bigquery".
- AIP_TRAINING_DATA_URI =
"bigquery_destination.dataset\_\ **\ .training"
- AIP_VALIDATION_DATA_URI =
"bigquery_destination.dataset\_\ **\ .validation"
- AIP_TEST_DATA_URI =
"bigquery_destination.dataset\_\ **\ .test".
This field is a member of `oneof` _ `destination` .
|
`dataset_id` |
`str`
Required. The ID of the Dataset in the same Project and Location which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. For tabular Datasets, all their data is exported to training, to pick and choose from. |
`annotations_filter` |
`str`
Applicable only to Datasets that have DataItems and Annotations. A filter on Annotations of the Dataset. Only Annotations that both match this filter and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on (for the auto-assigned that role is decided by Vertex AI). A filter with same syntax as the one used in ListAnnotations may be used, but note here it filters across all Annotations of the Dataset, and not just within a single DataItem. |
`annotation_schema_uri` |
`str`
Applicable only to custom training with Datasets that have DataItems and Annotations. Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`saved_query_id` |
`str`
Only applicable to Datasets that have SavedQueries. The ID of a SavedQuery (annotation set) under the Dataset specified by dataset_id used for filtering Annotations for training. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`persist_ml_use_assignment` |
`bool`
Whether to persist the ML use assignment to data item system labels. |

## Methods

### InputDataConfig

`InputDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies Vertex AI owned input data to be used for training, and possibly evaluating, the Model.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinejob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob -->

# Class PipelineJob (1.134.0)

`PipelineJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An instance of a machine learning PipelineJob.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the PipelineJob. |
`display_name` |
`str`
The display name of the Pipeline. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Pipeline creation time. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Pipeline start time. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Pipeline end time. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this PipelineJob was most recently updated. |
`pipeline_spec` |
`google.protobuf.struct_pb2.Struct`
The spec of the pipeline. |
`state` |
Output only. The detailed state of the job. |
`job_detail` |
Output only. The details of pipeline run. Not available in the list view. |
`error` |
`google.rpc.status_pb2.Status`
Output only. The error that occurred during pipeline execution. Only populated when the pipeline's state is FAILED or CANCELLED. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize PipelineJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. Note there is some reserved label key for Vertex AI Pipelines. - `vertex-ai-pipelines-run-billing-id` , user set value
will get overrided.
|
`runtime_config` |
Runtime config of the pipeline. |
`encryption_spec` |
Customer-managed encryption key spec for a pipelineJob. If set, this PipelineJob and all of its sub-resources will be secured by this key. |
`service_account` |
`str`
The service account that the pipeline workload runs as. If not specified, the Compute Engine default service account in the project will be used. See https://cloud.google.com/compute/docs/access/service-accounts#default_service_account Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service
account.
|
`network` |
`str`
The full name of the Compute Engine `network ` __
to which the Pipeline Job's workload should be peered. For
example, `projects/12345/global/networks/myVPC` .
`Format ` __
is of the form
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in `12345` , and
{network} is a network name.
Private services access must already be configured for the
network. Pipeline job will apply the network configuration
to the Google Cloud resources being launched, if applied,
such as Vertex AI Training or Dataflow job. If left
unspecified, the workload is not peered with any network.
|
`reserved_ip_ranges` |
`MutableSequence[str]`
A list of names for the reserved ip ranges under the VPC network that can be used for this Pipeline Job's workload. If set, we will deploy the Pipeline Job's workload within the provided ip ranges. Otherwise, the job will be deployed to any ip ranges under the provided VPC network. Example: ['vertex-ai-ip-range']. |
`psc_interface_config` |
Optional. Configuration for PSC-I for PipelineJob. |
`template_uri` |
`str`
A template uri from where the PipelineJob.pipeline_spec, if empty, will be downloaded. Currently, only uri from Vertex Template Registry & Gallery is supported. Reference to https://cloud.google.com/vertex-ai/docs/pipelines/create-pipeline-template. |
`template_metadata` |
Output only. Pipeline template metadata. Will fill up fields if PipelineJob.template_uri is from supported template registry. |
`schedule_name` |
`str`
Output only. The schedule resource name. Only returned if the Pipeline is created by Schedule API. |
`preflight_validations` |
`bool`
Optional. Whether to do component level validations before job creation. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`original_pipeline_job_id` |
`int`
Optional. The original pipeline job id if this pipeline job is a rerun of a previous pipeline job. |
`pipeline_task_rerun_configs` |
`MutableSequence[`
Optional. The rerun configs for each task in the pipeline job. By default, the rerun will: 1. Use the same input artifacts as the original run. 2. Use the same input parameters as the original run. 3. Skip all the tasks that are already succeeded in the original run. 4. Rerun all the tasks that are not succeeded in the original run. By providing this field, users can override the default behavior and specify the rerun config for each task. |

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

### RuntimeConfig

`RuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime config of a PipelineJob.

## Methods

### PipelineJob

`PipelineJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An instance of a machine learning PipelineJob.
