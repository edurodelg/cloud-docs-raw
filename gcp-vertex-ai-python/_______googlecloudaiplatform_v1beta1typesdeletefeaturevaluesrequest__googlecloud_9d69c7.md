---
merged_at: 2026-01-25T21:47:44.381997
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typesdeletefeaturevaluesrequest__googleclouda_05fb14.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesdeletefeaturevaluesrequest__googlecloudai_f38441.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesdeletefeaturevaluesrequest__googlecloudaip_3d2dbe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesdeletefeaturevaluesrequest__googlecloudaipl_56f9bb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesdeletefeaturevaluesrequest__googlecloudaipla_e54a70.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeletefeaturevaluesrequest__googlecloudaiplat_cdc186.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletefeaturevaluesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesRequest -->

# Class DeleteFeatureValuesRequest (1.134.0)

`DeleteFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeatureValues.

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
`select_entity` |
Select feature values to be deleted by specifying entities. This field is a member of `oneof` _ `DeleteOption` .
|
`select_time_range_and_feature` |
Select feature values to be deleted by specifying time range and features. This field is a member of `oneof` _ `DeleteOption` .
|
`entity_type` |
`str`
Required. The resource name of the EntityType grouping the Features for which values are being deleted from. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}`
|

## Classes

### SelectEntity

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select entity. If an entity id is selected, all the feature values corresponding to the entity id will be deleted, including the entityId.

### SelectTimeRangeAndFeature

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select time range and feature. Values of the selected feature generated within an inclusive time range will be deleted. Using this option permanently deletes the feature values from the specified feature IDs within the specified time range. This might include data from the online storage. If you want to retain any deleted historical data in the online storage, you must re-ingest it.

## Methods

### DeleteFeatureValuesRequest

`DeleteFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeatureValues.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesquerydeployedmodelsresponse_googlecloudaiplatform__616a71.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesquerydeployedmodelsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse -->

# Class QueryDeployedModelsResponse (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeploymodelrequesttrafficsplitentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelRequest.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforecastinginputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs -->

# Class AutoMlForecastingInputs (1.134.0)

`AutoMlForecastingInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`target_column` |
`str`
The name of the column that the model is to predict. |
`time_series_identifier_column` |
`str`
The name of the column that identifies the time series. |
`time_column` |
`str`
The name of the column that identifies time order in the time series. |
`transformations` |
`MutableSequence[`
Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. |
`optimization_objective` |
`str`
Objective function the model is optimizing towards. The training process creates a model that optimizes the value of the objective function over the validation set. The supported optimization objectives: - "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). - "minimize-mae" - Minimize mean-absolute error (MAE). - "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). - "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE). - "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE). - "minimize-quantile-loss" - Minimize the quantile loss at the quantiles defined in `quantiles` .
|
`train_budget_milli_node_hours` |
`int`
Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won't be attempted and will error. The train budget must be between 1,000 and 72,000 milli node hours, inclusive. |
`weight_column` |
`str`
Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1. |
`time_series_attribute_columns` |
`MutableSequence[str]`
Column names that should be used as attribute columns. The value of these columns does not vary as a function of time. For example, store ID or item color. |
`unavailable_at_forecast_columns` |
`MutableSequence[str]`
Names of columns that are unavailable when a forecast is requested. This column contains information for the given entity (identified by the time_series_identifier_column) that is unknown before the forecast For example, actual weather on a given day. |
`available_at_forecast_columns` |
`MutableSequence[str]`
Names of columns that are available and provided when a forecast is requested. These columns contain information for the given entity (identified by the time_series_identifier_column column) that is known at forecast. For example, predicted weather for a specific day. |
`data_granularity` |
Expected difference in time granularity between rows in the data. |
`forecast_horizon` |
`int`
The amount of time into the future for which forecasted values for the target are returned. Expressed in number of units defined by the `data_granularity` field.
|
`context_window` |
`int`
The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the `data_granularity` field.
|
`export_evaluated_data_items_config` |
Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed. |
`quantiles` |
`MutableSequence[float]`
Quantiles to use for minimize-quantile-loss `optimization_objective` . Up to 5 quantiles are allowed of
values between 0 and 1, exclusive. Required if the value of
optimization_objective is minimize-quantile-loss. Represents
the percent quantiles to use for that objective. Quantiles
must be unique.
|
`validation_options` |
`str`
Validation options for the data validation component. The available options are: - "fail-pipeline" - default, will validate against the validation and fail the pipeline if it fails. - "ignore-validation" - ignore the results of the validation and continue |
`additional_experiments` |
`MutableSequence[str]`
Additional experiment flags for the time series forcasting training. |

## Classes

### Granularity

`Granularity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A duration of time expressed in time granularity units.

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### AutoMlForecastingInputs

`AutoMlForecastingInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### AutoMlForecastingInputs

`AutoMlForecastingInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesundeploymodelrequesttrafficsplitentry_googl_40e3af.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesundeploymodelrequesttrafficsplitentry_google_f81315.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesundeploymodelrequesttrafficsplitentry_googlec_5e37ce.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesundeploymodelrequesttrafficsplitentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelRequest.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolparameterkvmatchmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchMetricValue -->

# Class ToolParameterKVMatchMetricValue (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployRequest -->

# Class DeployRequest (1.134.0)

`DeployRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.Deploy.

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
`publisher_model_name` |
`str`
The Model Garden model to deploy. Format: `publishers/{publisher}/models/{publisher_model}@{version_id}` ,
or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001` .
This field is a member of `oneof` _ `artifacts` .
|
`hugging_face_model_id` |
`str`
The Hugging Face model to deploy. Format: Hugging Face model ID like `google/gemma-2-2b-it` .
This field is a member of `oneof` _ `artifacts` .
|
`destination` |
`str`
Required. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`
|
`model_config` |
Optional. The model config to use for the deployment. If not specified, the default model config will be used. |
`endpoint_config` |
Optional. The endpoint config to use for the deployment. If not specified, the default endpoint config will be used. |
`deploy_config` |
Optional. The deploy config to use for the deployment. If not specified, the default deploy config will be used. |

## Classes

### DeployConfig

`DeployConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The deploy config to use for the deployment.

### EndpointConfig

`EndpointConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The endpoint config to use for the deployment.

### ModelConfig

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

## Methods

### DeployRequest

`DeployRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.Deploy.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfulfillmentinstance_googlecloudaiplatform_v1_686ad0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfulfillmentinstance_googlecloudaiplatform_v1b_9e7977.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfulfillmentinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FulfillmentInstance -->

# Class FulfillmentInstance (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescoherenceresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceResult -->

# Class CoherenceResult (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescometresult__googlecloudaiplatform_v1beta1typ_4754dd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescometresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CometResult -->

# Class CometResult (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragvectordbconfigragmanageddbknn_googleclouda_5e5351.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragvectordbconfigragmanageddbknn.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig.RagManagedDb.KNN -->

# Class KNN (1.134.0)

`KNN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for KNN search.

## Methods

### KNN

`KNN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for KNN search.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesurlcontext.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UrlContext -->

# Class UrlContext (1.134.0)

`UrlContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support URL context.

## Methods

### UrlContext

`UrlContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support URL context.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesvizier_servicepagerslisttrialspager_googleclo_4036da.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesvizier_servicepagerslisttrialspager_googleclou_97cbfb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesvizier_servicepagerslisttrialspager_googlecloud_6e3fb6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvizier_servicepagerslisttrialspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsPager -->

# Class ListTrialsPager (1.134.0)

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse) object, and
provides an `__iter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__iter__`

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

### ListTrialsPager

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslistnasjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasJobsPager -->

# Class ListNasJobsPager (1.134.0)

```
ListNasJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse,
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


A pager for iterating through `list_nas_jobs`

requests.

This class thinly wraps an initial
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`nas_jobs`

field.

If there are more pages, the `__iter__`

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

### ListNasJobsPager

```
ListNasJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespscautomationconfig_googlecloudaiplatform_v1beta1_168329.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespscautomationconfig_googlecloudaiplatform_v1beta1t_84a074.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespscautomationconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PSCAutomationConfig -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesassignnotebookruntimerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssignNotebookRuntimeRequest -->

# Class AssignNotebookRuntimeRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreatetensorboardexperimentrequest_googlecloudaipl_2c8c42.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatetensorboardexperimentrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardExperimentRequest -->

# Class CreateTensorboardExperimentRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespointwisemetricresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricResult -->

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
`custom_output` |
Output only. Spec for custom output. |

## Methods

### PointwiseMetricResult

`PointwiseMetricResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesassignnotebookruntimerequest_googlecloudaiplatfo_5d777b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesassignnotebookruntimerequest_googlecloudaiplatfor_74f043.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesassignnotebookruntimerequest_googlecloudaiplatform_f341cb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesassignnotebookruntimerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AssignNotebookRuntimeRequest -->

# Class AssignNotebookRuntimeRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesimportdataconfigdataitemlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataConfig.DataItemLabelsEntry -->

# Class DataItemLabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessearchnearestentitiesrequest_googlecloudaiplatform_4ab132.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessearchnearestentitiesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchNearestEntitiesRequest -->

# Class SearchNearestEntitiesRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureonlinestorebigtable.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.Bigtable -->

# Class Bigtable (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesrayspecresourcepoolimagesentry_googlecloudaiplatf_b55d92.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesrayspecresourcepoolimagesentry_googlecloudaiplatfo_6572a5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesrayspecresourcepoolimagesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RaySpec.ResourcePoolImagesEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolcallvalidinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolCallValidInstance -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelsPager -->

# Class ListModelsPager (1.134.0)

```
ListModelsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.model_service.ListModelsResponse
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelsResponse,
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


A pager for iterating through `list_models`

requests.

This class thinly wraps an initial
[ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`models`

field.

If there are more pages, the `__iter__`

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

### ListModelsPager

```
ListModelsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.model_service.ListModelsResponse
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelsResponse,
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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typescoherenceresult_googlecloudaiplatform_v1typesw_9e93fb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typescoherenceresult_googlecloudaiplatform_v1typeswr_77b197.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typescoherenceresult_googlecloudaiplatform_v1typeswri_da3390.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescoherenceresult_googlecloudaiplatform_v1typeswrit_72c744.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescoherenceresult_googlecloudaiplatform_v1typeswrite_b2eaa6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescoherenceresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CoherenceResult -->

# Class CoherenceResult (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeswritefeaturevaluespayloadfeaturevaluesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteFeatureValuesPayload.FeatureValuesEntry -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmetricxresult_googlecloudaiplatform_v1beta1ty_6bb070.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmetricxresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxResult -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesentityidselector.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EntityIdSelector -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesimportdataconfigannotationlabelsentry_googlecloud_172b0f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesimportdataconfigannotationlabelsentry_googleclouda_6fdeaa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesimportdataconfigannotationlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataConfig.AnnotationLabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescontent.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Content -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeployrequestdeployconfigsystemlabelsentry_googlec_155642.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployrequestdeployconfigsystemlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployRequest.DeployConfig.SystemLabelsEntry -->

# Class SystemLabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatetensorboardrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardRequest -->

# Class UpdateTensorboardRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typestoolparameterkvmatchmetricvalue_googlecloudaipla_8e9623.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typestoolparameterkvmatchmetricvalue_googlecloudaiplat_a5bd5d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestoolparameterkvmatchmetricvalue_googlecloudaiplatf_ba021d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolparameterkvmatchmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKVMatchMetricValue -->

# Class ToolParameterKVMatchMetricValue (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexportfeaturevaluesrequestsnapshotexport.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesRequest.SnapshotExport -->

# Class SnapshotExport (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestrajectorysingletoolusemetricvalue_googleclou_596c89.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectorysingletoolusemetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseMetricValue -->

# Class TrajectorySingleToolUseMetricValue (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryanyordermatchmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchMetricValue -->

# Class TrajectoryAnyOrderMatchMetricValue (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespipelinetaskrerunconfiginputsartifactsentry__efb576.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespipelinetaskrerunconfiginputsartifactsentry_g_4f2e3e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinetaskrerunconfiginputsartifactsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskRerunConfig.Inputs.ArtifactsEntry -->

# Class ArtifactsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistcachedcontentsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsRequest -->

# Class ListCachedContentsRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespublishermodelcalltoactiondeploydeploymetadatalabe_5d9992.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespublishermodelcalltoactiondeploydeploymetadatalabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.Deploy.DeployMetadata.LabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexactmatchinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchInstance -->

# Class ExactMatchInstance (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typestrainingpipeline___googlecloudaiplatform_v1beta1t_a4c893.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestrainingpipeline___googlecloudaiplatform_v1beta1ty_7b402d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestrainingpipeline.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TrainingPipeline -->

# Class TrainingPipeline (1.134.0)

`TrainingPipeline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the TrainingPipeline. |
`display_name` |
`str`
Required. The user-defined name of this TrainingPipeline. |
`input_data_config` |
Specifies Vertex AI owned input data that may be used for training the Model. The TrainingPipeline's training_task_definition should make clear whether this config is used and if there are any special requirements on how it should be filled. If nothing about this config is mentioned in the training_task_definition, then it should be assumed that the TrainingPipeline does not depend on this configuration. |
`training_task_definition` |
`str`
Required. A Google Cloud Storage path to the YAML file that defines the training task which is responsible for producing the model artifact, and may also include additional auxiliary work. The definition files that can be used here are found in gs://google-cloud-aiplatform/schema/trainingjob/definition/. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access. |
`training_task_inputs` |
`google.protobuf.struct_pb2.Value`
Required. The training task's parameter(s), as specified in the training_task_definition's `inputs` .
|
`training_task_metadata` |
`google.protobuf.struct_pb2.Value`
Output only. The metadata information as specified in the training_task_definition's `metadata` . This metadata is an auxiliary runtime and
final information about the training task. While the
pipeline is running this information is populated only at a
best effort basis. Only present if the pipeline's
training_task_definition
contains `metadata` object.
|
`model_to_upload` |
Describes the Model that may be uploaded (via ModelService.UploadModel) by this TrainingPipeline. The TrainingPipeline's training_task_definition should make clear whether this Model description should be populated, and if there are any special requirements regarding how it should be filled. If nothing is mentioned in the training_task_definition, then it should be assumed that this field should not be filled and the training task either uploads the Model without a need of this information, or that training task does not support uploading a Model as part of the pipeline. When the Pipeline's state becomes `PIPELINE_STATE_SUCCEEDED` and the trained Model had been
uploaded into Vertex AI, then the model_to_upload's resource
name is populated.
The Model is always uploaded into the Project and Location
in which this pipeline is.
|
`model_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
|
`parent_model` |
`str`
Optional. When specify this field, the `model_to_upload`
will not be uploaded as a new model, instead, it will become
a new version of this `parent_model` .
|
`state` |
Output only. The detailed state of the pipeline. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when the pipeline's state is `PIPELINE_STATE_FAILED` or `PIPELINE_STATE_CANCELLED` .
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline for the first time entered the `PIPELINE_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline entered any of the following states: `PIPELINE_STATE_SUCCEEDED` ,
`PIPELINE_STATE_FAILED` , `PIPELINE_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline was most recently updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key spec for a TrainingPipeline. If set, this TrainingPipeline will be secured by this key. Note: Model trained by this TrainingPipeline is also secured by this key if model_to_upload is not set separately. |

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

### TrainingPipeline

`TrainingPipeline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessearchnearestentitiesrequest_googlecloudaipl_0a3611.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessearchnearestentitiesrequest_googlecloudaipla_4b81bd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchnearestentitiesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchNearestEntitiesRequest -->

# Class SearchNearestEntitiesRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmetadatastoresrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresRequest -->

# Class ListMetadataStoresRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestoolcallvalidinstance_googlecloudaiplatform_v_dfb22f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolcallvalidinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidInstance -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicespipeline_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typespipelinejobruntimeconfigparametersentry_goo_b155b3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespipelinejobruntimeconfigparametersentry_goog_337149.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespipelinejobruntimeconfigparametersentry_googl_588ab2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinejobruntimeconfigparametersentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.ParametersEntry -->

# Class ParametersEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesundeploymodelrequesttrafficsplitentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployModelRequest.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistdatasetversionsrequest_googlecloudaiplatform_v_209e4b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistdatasetversionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespscautomationconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PSCAutomationConfig -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslogprobsresult_googlecloudaiplatform_v1beta1_e1a871.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslogprobsresult_googlecloudaiplatform_v1beta1t_182cb7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslogprobsresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LogprobsResult -->

# Class LogprobsResult (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatetensorboardexperimentrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardExperimentRequest -->

# Class CreateTensorboardExperimentRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexportfeaturevaluesrequestsnapshotexport_googleclo_40a591.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportfeaturevaluesrequestsnapshotexport.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFeatureValuesRequest.SnapshotExport -->

# Class SnapshotExport (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelevaluationslicesliceslicespecconfigsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluationSlice.Slice.SliceSpec.ConfigsEntry -->

# Class ConfigsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typestensorboardexperiment__googlecloudaiplatform_v_0fb39c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typestensorboardexperiment__googlecloudaiplatform_v1_6e1e37.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typestensorboardexperiment__googlecloudaiplatform_v1b_ae2558.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typestensorboardexperiment__googlecloudaiplatform_v1be_88506f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestensorboardexperiment__googlecloudaiplatform_v1bet_a98542.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestensorboardexperiment.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardExperiment -->

# Class TensorboardExperiment (1.134.0)

`TensorboardExperiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the TensorboardExperiment. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|
`display_name` |
`str`
User provided name of this TensorboardExperiment. |
`description` |
`str`
Description of this TensorboardExperiment. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardExperiment was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardExperiment was last updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your TensorboardExperiment. Label keys and values cannot be longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Dataset (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with `aiplatform.googleapis.com/` and are immutable. The
following system labels exist for each Dataset:
- `aiplatform.googleapis.com/dataset_metadata_schema` :
output only. Its value is the
[metadata_schema's][google.cloud.aiplatform.v1.Dataset.metadata_schema_uri]
title.
|
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`source` |
`str`
Immutable. Source of the TensorboardExperiment. Example: a custom training job. |

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

### TensorboardExperiment

`TensorboardExperiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatetensorboardrequest__googlecloudaiplatfo_d18259.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatetensorboardrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardRequest -->

# Class UpdateTensorboardRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeatureonlinestoreoptimized_googlecloudaiplatform__0679a5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureonlinestoreoptimized.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.Optimized -->

# Class Optimized (1.134.0)

`Optimized(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Optimized storage type

## Methods

### Optimized

`Optimized(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Optimized storage type


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesurlcontext.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UrlContext -->

# Class UrlContext (1.134.0)

`UrlContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support URL context.

## Methods

### UrlContext

`UrlContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support URL context.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrainingpipeline.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrainingPipeline -->

# Class TrainingPipeline (1.134.0)

`TrainingPipeline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the TrainingPipeline. |
`display_name` |
`str`
Required. The user-defined name of this TrainingPipeline. |
`input_data_config` |
Specifies Vertex AI owned input data that may be used for training the Model. The TrainingPipeline's training_task_definition should make clear whether this config is used and if there are any special requirements on how it should be filled. If nothing about this config is mentioned in the training_task_definition, then it should be assumed that the TrainingPipeline does not depend on this configuration. |
`training_task_definition` |
`str`
Required. A Google Cloud Storage path to the YAML file that defines the training task which is responsible for producing the model artifact, and may also include additional auxiliary work. The definition files that can be used here are found in gs://google-cloud-aiplatform/schema/trainingjob/definition/. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access. |
`training_task_inputs` |
`google.protobuf.struct_pb2.Value`
Required. The training task's parameter(s), as specified in the training_task_definition's `inputs` .
|
`training_task_metadata` |
`google.protobuf.struct_pb2.Value`
Output only. The metadata information as specified in the training_task_definition's `metadata` . This metadata is an auxiliary runtime and
final information about the training task. While the
pipeline is running this information is populated only at a
best effort basis. Only present if the pipeline's
training_task_definition
contains `metadata` object.
|
`model_to_upload` |
Describes the Model that may be uploaded (via ModelService.UploadModel) by this TrainingPipeline. The TrainingPipeline's training_task_definition should make clear whether this Model description should be populated, and if there are any special requirements regarding how it should be filled. If nothing is mentioned in the training_task_definition, then it should be assumed that this field should not be filled and the training task either uploads the Model without a need of this information, or that training task does not support uploading a Model as part of the pipeline. When the Pipeline's state becomes `PIPELINE_STATE_SUCCEEDED` and the trained Model had been
uploaded into Vertex AI, then the model_to_upload's resource
name is
populated. The Model is always uploaded into the Project and
Location in which this pipeline is.
|
`model_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
|
`parent_model` |
`str`
Optional. When specify this field, the `model_to_upload`
will not be uploaded as a new model, instead, it will become
a new version of this `parent_model` .
|
`state` |
Output only. The detailed state of the pipeline. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when the pipeline's state is `PIPELINE_STATE_FAILED` or `PIPELINE_STATE_CANCELLED` .
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline for the first time entered the `PIPELINE_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline entered any of the following states: `PIPELINE_STATE_SUCCEEDED` ,
`PIPELINE_STATE_FAILED` , `PIPELINE_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline was most recently updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key spec for a TrainingPipeline. If set, this TrainingPipeline will be secured by this key. Note: Model trained by this TrainingPipeline is also secured by this key if model_to_upload is not set separately. |

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

### TrainingPipeline

`TrainingPipeline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typespipelinejobruntimeconfigparametersentry_googlecl_aacf4d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespipelinejobruntimeconfigparametersentry_googleclo_8e919d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespipelinejobruntimeconfigparametersentry_googleclou_4a55b2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespipelinejobruntimeconfigparametersentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineJob.RuntimeConfig.ParametersEntry -->

# Class ParametersEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictprediction_v1typestextsentimentpredictionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TextSentimentPredictionResult -->

# Class TextSentimentPredictionResult (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistdatasetversionsrequest_googlecloudaiplatf_86351a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistdatasetversionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescontent.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Content -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmetricxresult_googlecloudaiplatform_v1typesgenera_79c972.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmetricxresult_googlecloudaiplatform_v1typesgenerat_cc6aef.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmetricxresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetricxResult -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgenerationconfigroutingconfigmanualroutingmode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig.RoutingConfig.ManualRoutingMode -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesquerydeployedmodelsresponse_googlecloudaiplat_2cf22d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquerydeployedmodelsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse -->

# Class QueryDeployedModelsResponse (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatedeploymentresourcepoolrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDeploymentResourcePoolRequest -->

# Class CreateDeploymentResourcePoolRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesendpoint__googlecloudaiplatform_v1beta1servicesmo_6fce21.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesendpoint__googlecloudaiplatform_v1beta1servicesmod_cb746f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesendpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint -->

# Class Endpoint (1.134.0)

`Endpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Endpoint. |
`display_name` |
`str`
Required. The display name of the Endpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Endpoint. |
`deployed_models` |
`MutableSequence[`
Output only. The models deployed in this Endpoint. To add or remove DeployedModels use EndpointService.DeployModel and EndpointService.UndeployModel respectively. |
`traffic_split` |
`MutableMapping[str, int]`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If a DeployedModel's ID is not listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Endpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Endpoint was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Endpoint was last updated. |
`encryption_spec` |
Customer-managed encryption key spec for an Endpoint. If set, this Endpoint and all sub-resources of this Endpoint will be secured by this key. |
`network` |
`str`
Optional. The full name of the Google Compute Engine `network ` __
to which the Endpoint should be peered.
Private services access must already be configured for the
network. If left unspecified, the Endpoint is not peered
with any network.
Only one of the fields,
network or
enable_private_service_connect,
can be set.
`Format ` __:
`projects/{project}/global/networks/{network}` . Where
`{project}` is a project number, as in `12345` , and
`{network}` is network name.
|
`enable_private_service_connect` |
`bool`
Deprecated: If true, expose the Endpoint via private service connect. Only one of the fields, network or enable_private_service_connect, can be set. |
`private_service_connect_config` |
Optional. Configuration for private service connect. network and private_service_connect_config are mutually exclusive. |
`model_deployment_monitoring_job` |
`str`
Output only. Resource name of the Model Monitoring job associated with this Endpoint if monitoring is enabled by JobService.CreateModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|
`predict_request_response_logging_config` |
Configures the request-response logging for online prediction. |
`dedicated_endpoint_enabled` |
`bool`
If true, the endpoint will be exposed through a dedicated DNS [Endpoint.dedicated_endpoint_dns]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitation will be removed soon. |
`dedicated_endpoint_dns` |
`str`
Output only. DNS of the dedicated endpoint. Will only be populated if dedicated_endpoint_enabled is true. Depending on the features enabled, uid might be a random number or a string. For example, if fast_tryout is enabled, uid will be fasttryout. Format: `https://{endpoint_id}.{region}-{uid}.prediction.vertexai.goog` .
|
`client_connection_config` |
Configurations that are applied to the endpoint for online prediction. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`gen_ai_advanced_features_config` |
Optional. Configuration for GenAiAdvancedFeatures. If the endpoint is serving GenAI models, advanced features like native RAG integration can be configured. Currently, only Model Garden models are supported. |
`private_model_server_enabled` |
`bool`
If true, the model server will be isolated from the external internet. |

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

## Methods

### Endpoint

`Endpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelspager_googlec_a8405e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelsPager -->

# Class ListModelsPager (1.134.0)

```
ListModelsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse,
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


A pager for iterating through `list_models`

requests.

This class thinly wraps an initial
[ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`models`

field.

If there are more pages, the `__iter__`

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

### ListModelsPager

```
ListModelsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescontext.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Context -->

# Class Context (1.134.0)

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general context.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. The resource name of the Context. |
`display_name` |
`str`
User provided display name of the Context. May be up to 128 Unicode characters. |
`etag` |
`str`
An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Contexts. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Context (System labels are excluded). |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Context was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Context was last updated. |
`parent_contexts` |
`MutableSequence[str]`
Output only. A list of resource names of Contexts that are parents of this Context. A Context may have at most 10 parent_contexts. |
`schema_title` |
`str`
The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`schema_version` |
`str`
The version of the schema in schema_name to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Context. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB. |
`description` |
`str`
Description of the Context |

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

### Context

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general context.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesendpoint__googlecloudaiplatform_v1servicesviz_75eb0d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesendpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint -->

# Class Endpoint (1.134.0)

`Endpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Endpoint. |
`display_name` |
`str`
Required. The display name of the Endpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Endpoint. |
`deployed_models` |
`MutableSequence[`
Output only. The models deployed in this Endpoint. To add or remove DeployedModels use EndpointService.DeployModel and EndpointService.UndeployModel respectively. |
`traffic_split` |
`MutableMapping[str, int]`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If a DeployedModel's ID is not listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Endpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Endpoint was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Endpoint was last updated. |
`encryption_spec` |
Customer-managed encryption key spec for an Endpoint. If set, this Endpoint and all sub-resources of this Endpoint will be secured by this key. |
`network` |
`str`
Optional. The full name of the Google Compute Engine `network ` __
to which the Endpoint should be peered.
Private services access must already be configured for the
network. If left unspecified, the Endpoint is not peered
with any network.
Only one of the fields,
network
or
enable_private_service_connect,
can be set.
`Format ` __:
`projects/{project}/global/networks/{network}` . Where
`{project}` is a project number, as in `12345` , and
`{network}` is network name.
|
`enable_private_service_connect` |
`bool`
Deprecated: If true, expose the Endpoint via private service connect. Only one of the fields, network or enable_private_service_connect, can be set. |
`private_service_connect_config` |
Optional. Configuration for private service connect. network and private_service_connect_config are mutually exclusive. |
`model_deployment_monitoring_job` |
`str`
Output only. Resource name of the Model Monitoring job associated with this Endpoint if monitoring is enabled by JobService.CreateModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|
`predict_request_response_logging_config` |
Configures the request-response logging for online prediction. |
`dedicated_endpoint_enabled` |
`bool`
If true, the endpoint will be exposed through a dedicated DNS [Endpoint.dedicated_endpoint_dns]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitation will be removed soon. |
`dedicated_endpoint_dns` |
`str`
Output only. DNS of the dedicated endpoint. Will only be populated if dedicated_endpoint_enabled is true. Depending on the features enabled, uid might be a random number or a string. For example, if fast_tryout is enabled, uid will be fasttryout. Format: `https://{endpoint_id}.{region}-{uid}.prediction.vertexai.goog` .
|
`client_connection_config` |
Configurations that are applied to the endpoint for online prediction. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`gen_ai_advanced_features_config` |
Optional. Configuration for GenAiAdvancedFeatures. If the endpoint is serving GenAI models, advanced features like native RAG integration can be configured. Currently, only Model Garden models are supported. |
`private_model_server_enabled` |
`bool`
If true, the model server will be isolated from the external internet. |

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

## Methods

### Endpoint

`Endpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesvizier_servicepagersliststudiespager__googleclo_c6fb57.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvizier_servicepagersliststudiespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListStudiesPager -->

# Class ListStudiesPager (1.134.0)

```
ListStudiesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse,
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


A pager for iterating through `list_studies`

requests.

This class thinly wraps an initial
[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse) object, and
provides an `__iter__`

method to iterate through its
`studies`

field.

If there are more pages, the `__iter__`

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

### ListStudiesPager

```
ListStudiesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespublishermodelcalltoactiondeploydeploymetadat_2bcd7e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelcalltoactiondeploydeploymetadatalabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.Deploy.DeployMetadata.LabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeminitemplateconfigfieldmappingentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GeminiTemplateConfig.FieldMappingEntry -->

# Class FieldMappingEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesreadfeaturevaluesrequest_googlecloudaiplatform_c522ba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesreadfeaturevaluesrequest_googlecloudaiplatform__f68aed.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesreadfeaturevaluesrequest_googlecloudaiplatform_v_796622.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesreadfeaturevaluesrequest_googlecloudaiplatform_v1_1eaa1b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreadfeaturevaluesrequest_googlecloudaiplatform_v1b_c6cdcc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadfeaturevaluesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadFeatureValuesRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolnamematchinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchInstance -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatefeaturemonitorrequest_googlecloudaiplat_2b50cf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatefeaturemonitorrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorRequest -->

# Class CreateFeatureMonitorRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdatalabelingjobannotationlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DataLabelingJob.AnnotationLabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesindex_servicepagerslistindexespager__googleclou_c61c60.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesindex_servicepagerslistindexespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.pagers.ListIndexesPager -->

# Class ListIndexesPager (1.134.0)

```
ListIndexesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse
],
request: google.cloud.aiplatform_v1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse,
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


A pager for iterating through `list_indexes`

requests.

This class thinly wraps an initial
[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesResponse) object, and
provides an `__iter__`

method to iterate through its
`indexes`

field.

If there are more pages, the `__iter__`

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

### ListIndexesPager

```
ListIndexesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse
],
request: google.cloud.aiplatform_v1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeployrequestdeployconfigsystemlabelsentry_go_4d9745.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployrequestdeployconfigsystemlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest.DeployConfig.SystemLabelsEntry -->

# Class SystemLabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportdataconfigdataitemlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataConfig.DataItemLabelsEntry -->

# Class DataItemLabelsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesfulfillmentresult_googlecloudaiplatform_v1typesi_da08f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfulfillmentresult_googlecloudaiplatform_v1typesim_65cac2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfulfillmentresult_googlecloudaiplatform_v1typesimp_aa513e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfulfillmentresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FulfillmentResult -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesimportfeaturevaluesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportFeatureValuesResponse -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesentityidselector_googlecloudaiplatformv1schemapred_b654e8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesentityidselector.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EntityIdSelector -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictinstance_v1typesimageclassificationpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageClassificationPredictionInstance -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestensorboardexperiment__googlecloudaiplatform__d3aa0e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestensorboardexperiment.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardExperiment -->

# Class TensorboardExperiment (1.134.0)

`TensorboardExperiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the TensorboardExperiment. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|
`display_name` |
`str`
User provided name of this TensorboardExperiment. |
`description` |
`str`
Description of this TensorboardExperiment. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardExperiment was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardExperiment was last updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your TensorboardExperiment. Label keys and values cannot be longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Dataset (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with `aiplatform.googleapis.com/` and are immutable. The
following system labels exist for each Dataset:
- `aiplatform.googleapis.com/dataset_metadata_schema` :
output only. Its value is the
[metadata_schema's][google.cloud.aiplatform.v1beta1.Dataset.metadata_schema_uri]
title.
|
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`source` |
`str`
Immutable. Source of the TensorboardExperiment. Example: a custom training job. |

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

### TensorboardExperiment

`TensorboardExperiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeswritefeaturevaluespayloadfeaturevaluesentry_g_3c3a2b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeswritefeaturevaluespayloadfeaturevaluesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteFeatureValuesPayload.FeatureValuesEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespipelinejobruntimeconfiginputartifactsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineJob.RuntimeConfig.InputArtifactsEntry -->

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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesreadtensorboardusageresponsemonthlyusageda_62d3f2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesreadtensorboardusageresponsemonthlyusagedat_42fe9a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesreadtensorboardusageresponsemonthlyusagedata_063dfc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesreadtensorboardusageresponsemonthlyusagedatae_205989.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadtensorboardusageresponsemonthlyusagedataentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardUsageResponse.MonthlyUsageDataEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgroundednessinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundednessInstance -->

# Class GroundednessInstance (1.134.0)

`GroundednessInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness instance.

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
`context` |
`str`
Required. Background information provided in context used to compare against the prediction. This field is a member of `oneof` _ `_context` .
|

## Methods

### GroundednessInstance

`GroundednessInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescontext.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Context -->

# Class Context (1.134.0)

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general context.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. The resource name of the Context. |
`display_name` |
`str`
User provided display name of the Context. May be up to 128 Unicode characters. |
`etag` |
`str`
An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Contexts. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Context (System labels are excluded). |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Context was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Context was last updated. |
`parent_contexts` |
`MutableSequence[str]`
Output only. A list of resource names of Contexts that are parents of this Context. A Context may have at most 10 parent_contexts. |
`schema_title` |
`str`
The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`schema_version` |
`str`
The version of the schema in schema_name to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Context. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB. |
`description` |
`str`
Description of the Context |

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

### Context

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general context.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnotebookexecutionjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJob -->

# Class NotebookExecutionJob (1.134.0)

`NotebookExecutionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


NotebookExecutionJob represents an instance of a notebook execution.

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
`dataform_repository_source` |
The Dataform Repository pointing to a single file notebook repository. This field is a member of `oneof` _ `notebook_source` .
|
`gcs_notebook_source` |
The Cloud Storage url pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`
This field is a member of `oneof` _ `notebook_source` .
|
`direct_notebook_source` |
The contents of an input notebook file. This field is a member of `oneof` _ `notebook_source` .
|
`notebook_runtime_template_resource_name` |
`str`
The NotebookRuntimeTemplate to source compute configuration from. This field is a member of `oneof` _ `environment_spec` .
|
`custom_environment_spec` |
The custom compute configuration for an execution job. This field is a member of `oneof` _ `environment_spec` .
|
`gcs_output_uri` |
`str`
The Cloud Storage location to upload the result to. Format: `gs://bucket-name`
This field is a member of `oneof` _ `execution_sink` .
|
`execution_user` |
`str`
The user email to run the execution as. Only supported by Colab runtimes. This field is a member of `oneof` _ `execution_identity` .
|
`service_account` |
`str`
The service account to run the execution as. This field is a member of `oneof` _ `execution_identity` .
|
`workbench_runtime` |
The Workbench runtime configuration to use for the notebook execution. This field is a member of `oneof` _ `runtime_environment` .
|
`name` |
`str`
Output only. The resource name of this NotebookExecutionJob. Format: `projects/{project_id}/locations/{location}/notebookExecutionJobs/{job_id}`
|
`display_name` |
`str`
The display name of the NotebookExecutionJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`execution_timeout` |
`google.protobuf.duration_pb2.Duration`
Max running time of the execution job in seconds (default 86400s / 24 hrs). |
`schedule_resource_name` |
`str`
The Schedule resource name if this job is triggered by one. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`
|
`job_state` |
Output only. The state of the NotebookExecutionJob. |
`status` |
`google.rpc.status_pb2.Status`
Output only. Populated when the NotebookExecutionJob is completed. When there is an error during notebook execution, the error details are populated. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookExecutionJob was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookExecutionJob was most recently updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize NotebookExecutionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`kernel_name` |
`str`
The name of the kernel to use during notebook execution. If unset, the default kernel is used. |
`encryption_spec` |
Customer-managed encryption key spec for the notebook execution job. This field is auto-populated if the NotebookRuntimeTemplate has an encryption spec. |

## Classes

### CustomEnvironmentSpec

`CustomEnvironmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Compute configuration to use for an execution job.

### DataformRepositorySource

`DataformRepositorySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Dataform Repository containing the input notebook.

### DirectNotebookSource

`DirectNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The content of the input notebook in ipynb format.

### GcsNotebookSource

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

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

### WorkbenchRuntime

`WorkbenchRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a Workbench Instances-based environment.

## Methods

### NotebookExecutionJob

`NotebookExecutionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


NotebookExecutionJob represents an instance of a notebook execution.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typestoolnamematchinstance_googlecloudaiplatform_v1be_514c8d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typestoolnamematchinstance_googlecloudaiplatform_v1bet_227fe9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestoolnamematchinstance_googlecloudaiplatform_v1beta_08b855.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolnamematchinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolNameMatchInstance -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgenerationconfigroutingconfigmanualroutingmode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.RoutingConfig.ManualRoutingMode -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typestextsentimentpr_157a8c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typestextsentimentpredictionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TextSentimentPredictionResult -->

# Class TextSentimentPredictionResult (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookruntimeruntimestate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntime.RuntimeState -->

# Class RuntimeState (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfulfillmentresult_googlecloudaiplatform_v1ty_5ba04e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfulfillmentresult_googlecloudaiplatform_v1typ_d7f1c3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfulfillmentresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FulfillmentResult -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesprivateserviceconnectconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PrivateServiceConnectConfig -->

# Class PrivateServiceConnectConfig (1.134.0)

`PrivateServiceConnectConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents configuration for private service connect.

## Attributes |
|
|---|---|
Name |
Description |
`enable_private_service_connect` |
`bool`
Required. If true, expose the IndexEndpoint via private service connect. |
`project_allowlist` |
`MutableSequence[str]`
A list of Projects from which the forwarding rule will target the service attachment. |
`psc_automation_configs` |
`MutableSequence[`
Optional. List of projects and networks where the PSC endpoints will be created. This field is used by Online Inference(Prediction) only. |
`service_attachment` |
`str`
Output only. The name of the generated service attachment resource. This is only populated if the endpoint is deployed with PrivateServiceConnect. |

## Methods

### PrivateServiceConnectConfig

`PrivateServiceConnectConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents configuration for private service connect.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesimportdataconfigannotationlabelsentry_googlec_6c6948.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportdataconfigannotationlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataConfig.AnnotationLabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringalertcondition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAlertCondition -->

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

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1servicesdataset_servicepagerslistdatasetspager_goo_fc4aec.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1servicesdataset_servicepagerslistdatasetspager_goog_ee2132.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1servicesdataset_servicepagerslistdatasetspager_googl_a71b61.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesdataset_servicepagerslistdatasetspager_google_2ea6c3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesdataset_servicepagerslistdatasetspager_googlec_957688.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdataset_servicepagerslistdatasetspager_googlecl_4af564.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerslistdatasetspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetsPager -->

# Class ListDatasetsPager (1.134.0)

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

## Methods

### ListDatasetsPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvizier_servicepagerslisttrialspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListTrialsPager -->

# Class ListTrialsPager (1.134.0)

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse,
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


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsResponse) object, and
provides an `__iter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__iter__`

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

### ListTrialsPager

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookexecutionjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob -->

# Class NotebookExecutionJob (1.134.0)

`NotebookExecutionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


NotebookExecutionJob represents an instance of a notebook execution.

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
`dataform_repository_source` |
The Dataform Repository pointing to a single file notebook repository. This field is a member of `oneof` _ `notebook_source` .
|
`gcs_notebook_source` |
The Cloud Storage url pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`
This field is a member of `oneof` _ `notebook_source` .
|
`direct_notebook_source` |
The contents of an input notebook file. This field is a member of `oneof` _ `notebook_source` .
|
`notebook_runtime_template_resource_name` |
`str`
The NotebookRuntimeTemplate to source compute configuration from. This field is a member of `oneof` _ `environment_spec` .
|
`custom_environment_spec` |
The custom compute configuration for an execution job. This field is a member of `oneof` _ `environment_spec` .
|
`gcs_output_uri` |
`str`
The Cloud Storage location to upload the result to. Format: `gs://bucket-name`
This field is a member of `oneof` _ `execution_sink` .
|
`execution_user` |
`str`
The user email to run the execution as. Only supported by Colab runtimes. This field is a member of `oneof` _ `execution_identity` .
|
`service_account` |
`str`
The service account to run the execution as. This field is a member of `oneof` _ `execution_identity` .
|
`workbench_runtime` |
The Workbench runtime configuration to use for the notebook execution. This field is a member of `oneof` _ `runtime_environment` .
|
`name` |
`str`
Output only. The resource name of this NotebookExecutionJob. Format: `projects/{project_id}/locations/{location}/notebookExecutionJobs/{job_id}`
|
`display_name` |
`str`
The display name of the NotebookExecutionJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`execution_timeout` |
`google.protobuf.duration_pb2.Duration`
Max running time of the execution job in seconds (default 86400s / 24 hrs). |
`schedule_resource_name` |
`str`
The Schedule resource name if this job is triggered by one. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`
|
`job_state` |
Output only. The state of the NotebookExecutionJob. |
`status` |
`google.rpc.status_pb2.Status`
Output only. Populated when the NotebookExecutionJob is completed. When there is an error during notebook execution, the error details are populated. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookExecutionJob was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookExecutionJob was most recently updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize NotebookExecutionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`kernel_name` |
`str`
The name of the kernel to use during notebook execution. If unset, the default kernel is used. |
`encryption_spec` |
Customer-managed encryption key spec for the notebook execution job. This field is auto-populated if the NotebookRuntimeTemplate has an encryption spec. |

## Classes

### CustomEnvironmentSpec

`CustomEnvironmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Compute configuration to use for an execution job.

### DataformRepositorySource

`DataformRepositorySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Dataform Repository containing the input notebook.

### DirectNotebookSource

`DirectNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The content of the input notebook in ipynb format.

### GcsNotebookSource

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

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

### WorkbenchRuntime

`WorkbenchRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a Workbench Instances-based environment.

## Methods

### NotebookExecutionJob

`NotebookExecutionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


NotebookExecutionJob represents an instance of a notebook execution.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typespublishermodellaunchstage_googlecloudaiplat_116cce.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespublishermodellaunchstage_googlecloudaiplatf_0ffb05.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespublishermodellaunchstage_googlecloudaiplatfo_10184b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodellaunchstage.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.LaunchStage -->

# Class LaunchStage (1.134.0)

`LaunchStage(value)`


An enum representing the launch stage of a PublisherModel.

## Enums |
|
|---|---|
Name |
Description |
`LAUNCH_STAGE_UNSPECIFIED` |
The model launch stage is unspecified. |
`EXPERIMENTAL` |
Used to indicate the PublisherModel is at Experimental launch stage, available to a small set of customers. |
`PRIVATE_PREVIEW` |
Used to indicate the PublisherModel is at Private Preview launch stage, only available to a small set of customers, although a larger set of customers than an Experimental launch. Previews are the first launch stage used to get feedback from customers. |
`PUBLIC_PREVIEW` |
Used to indicate the PublisherModel is at Public Preview launch stage, available to all customers, although not supported for production workloads. |
`GA` |
Used to indicate the PublisherModel is at GA launch stage, available to all customers and ready for production workload. |

## Methods

### LaunchStage

`LaunchStage(value)`


An enum representing the launch stage of a PublisherModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgroundednessresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundednessResult -->

# Class GroundednessResult (1.134.0)

`GroundednessResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Groundedness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for groundedness score. |
`confidence` |
`float`
Output only. Confidence for groundedness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### GroundednessResult

`GroundednessResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdatalabelingjobannotationlabelsentry_googlecl_865b07.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdatalabelingjobannotationlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DataLabelingJob.AnnotationLabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespipelinejobruntimeconfigparametervaluesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineJob.RuntimeConfig.ParameterValuesEntry -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesrayspecresourcepoolimagesentry_googlecloudai_0df012.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesrayspecresourcepoolimagesentry_googlecloudaip_abb330.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrayspecresourcepoolimagesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RaySpec.ResourcePoolImagesEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespartnermodeltuningspechyperparametersentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PartnerModelTuningSpec.HyperParametersEntry -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesruntimeartifactcustompropertiesentry_googlecl_a9a2d7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesruntimeartifactcustompropertiesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeArtifact.CustomPropertiesEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinejobruntimeconfiginputartifactsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.InputArtifactsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesevaluation_serviceevaluationserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service.EvaluationServiceAsyncClient -->

# Class EvaluationServiceAsyncClient (1.134.0)

```
EvaluationServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Vertex AI Online Evaluation Service.

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
`EvaluationServiceTransport` |
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

### EvaluationServiceAsyncClient

```
EvaluationServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the evaluation service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,EvaluationServiceTransport,Callable[..., EvaluationServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the EvaluationServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### evaluate_instances

```
evaluate_instances(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.evaluation_service.EvaluateInstancesRequest,
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
) -> google.cloud.aiplatform_v1.types.evaluation_service.EvaluateInstancesResponse
```


Evaluates instances based on a given metric.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_evaluate_instances():
# Create a client
client = aiplatform_v1.
```[EvaluationServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service.EvaluationServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[EvaluateInstancesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluateInstancesRequest.html)(
location="location_value",
)
# Make the request
response = await client.[evaluate_instances](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service.EvaluationServiceAsyncClient.html#google_cloud_aiplatform_v1_services_evaluation_service_EvaluationServiceAsyncClient_evaluate_instances)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EvaluationService.EvaluateInstances. |
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
Response message for EvaluationService.EvaluateInstances. |

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
`EvaluationServiceAsyncClient` |
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
`EvaluationServiceAsyncClient` |
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
`EvaluationServiceAsyncClient` |
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
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdata_foundry_servicedatafoundryserviceclient____599d31.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdata_foundry_servicedatafoundryserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceClient -->

# Class DataFoundryServiceClient (1.134.0)

```
DataFoundryServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### DataFoundryServiceClient

```
DataFoundryServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the data foundry service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the DataFoundryServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
`DataFoundryServiceClient` |
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
`DataFoundryServiceClient` |
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
`DataFoundryServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_generate_synthetic_data():
# Create a client
client = aiplatform_v1.
```[DataFoundryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceClient.html)()
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
response = client.[generate_synthetic_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceClient.html#google_cloud_aiplatform_v1_services_data_foundry_service_DataFoundryServiceClient_generate_synthetic_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DataFoundryService.GenerateSyntheticData. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesimportfeaturevaluesresponse_googlecloudaip_d44ebc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesimportfeaturevaluesresponse_googlecloudaipl_89b59f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesimportfeaturevaluesresponse_googlecloudaipla_0b0831.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesimportfeaturevaluesresponse_googlecloudaiplat_b49c5c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportfeaturevaluesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesResponse -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureonlinestorebigtable.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.Bigtable -->

# Class Bigtable (1.134.0)

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
Optional. Whether direct access to the Bigtable instance is enabled or not. |
`bigtable_metadata` |
Output only. Metadata of the Bigtable instance. Output only. |
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespublishermodellaunchstage_googlecloudaiplatform_v1_1a80a5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespublishermodellaunchstage.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.LaunchStage -->

# Class LaunchStage (1.134.0)

`LaunchStage(value)`


An enum representing the launch stage of a PublisherModel.

## Enums |
|
|---|---|
Name |
Description |
`LAUNCH_STAGE_UNSPECIFIED` |
The model launch stage is unspecified. |
`EXPERIMENTAL` |
Used to indicate the PublisherModel is at Experimental launch stage, available to a small set of customers. |
`PRIVATE_PREVIEW` |
Used to indicate the PublisherModel is at Private Preview launch stage, only available to a small set of customers, although a larger set of customers than an Experimental launch. Previews are the first launch stage used to get feedback from customers. |
`PUBLIC_PREVIEW` |
Used to indicate the PublisherModel is at Public Preview launch stage, available to all customers, although not supported for production workloads. |
`GA` |
Used to indicate the PublisherModel is at GA launch stage, available to all customers and ready for production workload. |

## Methods

### LaunchStage

`LaunchStage(value)`


An enum representing the launch stage of a PublisherModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistdeploymentresourcepoolsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsRequest -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesjob_servicepagerslistnasjobspager__googlec_4a7376.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslistnasjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasJobsPager -->

# Class ListNasJobsPager (1.134.0)

```
ListNasJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse,
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


A pager for iterating through `list_nas_jobs`

requests.

This class thinly wraps an initial
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`nas_jobs`

field.

If there are more pages, the `__iter__`

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

### ListNasJobsPager

```
ListNasJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreadtensorboardusageresponsemonthlyusagedataentry__c4cdf8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadtensorboardusageresponsemonthlyusagedataentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardUsageResponse.MonthlyUsageDataEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistdeploymentresourcepoolsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsRequest -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesmetadata_servicepagerslistcontextspager__googl_32e3cb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmetadata_servicepagerslistcontextspager__google_d13556.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicepagerslistcontextspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListContextsPager -->

# Class ListContextsPager (1.134.0)

```
ListContextsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse,
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
[ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse) object, and
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

All the usual [ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListContextsPager

```
ListContextsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestrajectorysingletooluseinstance_googlecloudai_4f706f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectorysingletooluseinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseInstance -->

# Class TrajectorySingleToolUseInstance (1.134.0)

```
TrajectorySingleToolUseInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectorySingleToolUse instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`predicted_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for predicted tool call trajectory. This field is a member of `oneof` _ `_predicted_trajectory` .
|

## Methods

### TrajectorySingleToolUseInstance

```
TrajectorySingleToolUseInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectorySingleToolUse instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgroundednessresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundednessResult -->

# Class GroundednessResult (1.134.0)

`GroundednessResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Groundedness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for groundedness score. |
`confidence` |
`float`
Output only. Confidence for groundedness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### GroundednessResult

`GroundednessResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesresourceruntime_googlecloudaiplatform_v1beta1serv_541318.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesresourceruntime_googlecloudaiplatform_v1beta1servi_1a4aaf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesresourceruntime.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResourceRuntime -->

# Class ResourceRuntime (1.134.0)

`ResourceRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Persistent Cluster runtime information as output

## Attribute |
|
|---|---|
Name |
Description |
`access_uris` |
`MutableMapping[str, str]`
Output only. URIs for user to connect to the Cluster. Example: { "RAY_HEAD_NODE_INTERNAL_IP": "head-node-IP:10001" "RAY_DASHBOARD_URI": "ray-dashboard-address:8888" } |

## Classes

### AccessUrisEntry

`AccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ResourceRuntime

`ResourceRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Persistent Cluster runtime information as output


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicespipeline_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service -->

# Package pipeline_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.pipeline_service`

package.

## Classes

[PipelineServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient)

A service for creating and managing Vertex AI's pipelines. This
includes both `TrainingPipeline`

resources (used for AutoML and
custom training) and `PipelineJob`

resources (used for Vertex AI
Pipelines).

[PipelineServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient)

A service for creating and managing Vertex AI's pipelines. This
includes both `TrainingPipeline`

resources (used for AutoML and
custom training) and `PipelineJob`

resources (used for Vertex AI
Pipelines).

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers)

API documentation for `aiplatform_v1beta1.services.pipeline_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesindex_servicepagerslistindexespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.pagers.ListIndexesPager -->

# Class ListIndexesPager (1.134.0)

```
ListIndexesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse
],
request: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse,
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


A pager for iterating through `list_indexes`

requests.

This class thinly wraps an initial
[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse) object, and
provides an `__iter__`

method to iterate through its
`indexes`

field.

If there are more pages, the `__iter__`

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

### ListIndexesPager

```
ListIndexesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse
],
request: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse,
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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformmodeldeploymentmonitoringjob___googlecloudaiplatform_v1b_a1c596.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformmodeldeploymentmonitoringjob___googlecloudaiplatform_v1be_e3e9a3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformmodeldeploymentmonitoringjob___googlecloudaiplatform_v1bet_27cf95.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformmodeldeploymentmonitoringjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelDeploymentMonitoringJob -->

# Class ModelDeploymentMonitoringJob (1.134.0)

```
ModelDeploymentMonitoringJob(
model_deployment_monitoring_job_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Vertex AI Model Deployment Monitoring Job.

This class should be used in conjunction with the Endpoint class in order to configure model monitoring for deployed models.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Time when the Job resource entered the `JOB_STATE_SUCCEEDED`

,
`JOB_STATE_FAILED`

, or `JOB_STATE_CANCELLED`

state.

### error

Detailed error info for this Job resource. Only populated when the
Job's state is `JOB_STATE_FAILED`

or `JOB_STATE_CANCELLED`

.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### start_time

Time when the Job resource entered the `JOB_STATE_RUNNING`

for the
first time.

### state

Fetch Job again and return the current JobState.

Returns |
|
|---|---|
Type |
Description |
`state (job_state.JobState)` |
Enum that describes the state of a Vertex AI job. |

### update_time

Time this resource was last updated.

## Methods

### ModelDeploymentMonitoringJob

```
ModelDeploymentMonitoringJob(
model_deployment_monitoring_job_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Initializer for ModelDeploymentMonitoringJob.

Parameter |
|
|---|---|
Name |
Description |
`model_deployment_monitoring_job_name` |
`str`
Required. A fully-qualified ModelDeploymentMonitoringJob resource name or ID. Example: "projects/.../locations/.../modelDeploymentMonitoringJobs/456" or "456" when project and location are initialized or passed. |

### cancel

`cancel()`


Cancels this Job.

Success of cancellation is not guaranteed. Use `Job.state`

property to verify if cancellation was successful.

### create

```
create(
endpoint: typing.Union[str, google.cloud.aiplatform.models.Endpoint],
objective_configs: typing.Optional[
typing.Union[
google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig,
typing.Dict[
str, google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig
],
]
] = None,
logging_sampling_strategy: typing.Optional[
google.cloud.aiplatform.model_monitoring.sampling.RandomSampleConfig
] = None,
schedule_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.schedule.ScheduleConfig
] = None,
display_name: typing.Optional[str] = None,
deployed_model_ids: typing.Optional[typing.List[str]] = None,
alert_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.alert.EmailAlertConfig
] = None,
predict_instance_schema_uri: typing.Optional[str] = None,
sample_predict_instance: typing.Optional[str] = None,
analysis_instance_schema_uri: typing.Optional[str] = None,
bigquery_tables_log_ttl: typing.Optional[int] = None,
stats_anomalies_base_directory: typing.Optional[str] = None,
enable_monitoring_pipeline_logs: typing.Optional[bool] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.jobs.ModelDeploymentMonitoringJob
```


Creates and launches a model monitoring job.

Parameters |
|
|---|---|
Name |
Description |
`endpoint` |
`Union[str, "aiplatform.Endpoint"]`
Required. Endpoint resource name or an instance of |
`logging_sampling_strategy` |
`model_monitoring.sampling.RandomSampleConfig`
Optional. Sample Strategy for logging. |
`schedule_config` |
`model_monitoring.schedule.ScheduleConfig`
Optional. Configures model monitoring job scheduling interval in hours. This defines how often the monitoring jobs are triggered. |
`display_name` |
`str`
Optional. The user-defined name of the ModelDeploymentMonitoringJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. Display name of a ModelDeploymentMonitoringJob. |
`deployed_model_ids` |
`List[str]`
Optional. Use this argument to specify which deployed models to apply the objective config to. If left unspecified, the same config will be applied to all deployed models. |
`alert_config` |
`model_monitoring.alert.EmailAlertConfig`
Optional. Configures how alerts are sent to the user. Right now only email alert is supported. |
`predict_instance_schema_uri` |
`str`
Optional. YAML schema file uri describing the format of a single instance, which are given to format the Endpoint's prediction (and explanation). If not set, the schema will be generated from collected predict requests. |
`sample_predict_instance` |
`str`
Optional. Sample Predict instance, same format as PredictionRequest.instances, this can be set as a replacement of predict_instance_schema_uri If not set, the schema will be generated from collected predict requests. |
`analysis_instance_schema_uri` |
`str`
Optional. YAML schema file uri describing the format of a single instance that you want Tensorflow Data Validation (TFDV) to analyze. If this field is empty, all the feature data types are inferred from predict_instance_schema_uri, meaning that TFDV will use the data in the exact format as prediction request/response. If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Vertex AI, this field must be set as all the fields in predict instance formatted as string. |
`bigquery_tables_log_ttl` |
`int`
Optional. The TTL(time to live) of BigQuery tables in user projects which stores logs. A day is the basic unit of the TTL and we take the ceil of TTL/86400(a day). e.g. { second: 3600} indicates ttl = 1 day. |
`stats_anomalies_base_directory` |
`str`
Optional. Stats anomalies base folder path. |
`enable_monitoring_pipeline_logs` |
`bool`
Optional. If true, the scheduled monitoring pipeline logs are sent to Google Cloud Logging, including pipeline status and anomalies detected. Please note the logs incur cost, which are subject to |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize the ModelDeploymentMonitoringJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`str`
Optional. Customer-managed encryption key spec for a ModelDeploymentMonitoringJob. If set, this ModelDeploymentMonitoringJob and all sub-resources of this ModelDeploymentMonitoringJob will be secured by this key. |
`create_request_timeout` |
`int`
Optional. Timeout in seconds for the model monitoring job creation request. |

### delete

`delete() -> None`


Deletes an MDM job.

### done

`done() -> bool`


Method indicating whether a job has completed.

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


List all instances of this Job Resource.

Example Usage:

aiplatform.BatchPredictionJobs.list( filter='state="JOB_STATE_SUCCEEDED" AND display_name="my_job"', )

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

### pause

`pause() -> google.cloud.aiplatform.jobs.ModelDeploymentMonitoringJob`


Pause a running MDM job.

### resume

`resume() -> google.cloud.aiplatform.jobs.ModelDeploymentMonitoringJob`


Resumes a paused MDM job.

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
*,
display_name: typing.Optional[str] = None,
schedule_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.schedule.ScheduleConfig
] = None,
alert_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.alert.EmailAlertConfig
] = None,
logging_sampling_strategy: typing.Optional[
google.cloud.aiplatform.model_monitoring.sampling.RandomSampleConfig
] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
bigquery_tables_log_ttl: typing.Optional[int] = None,
enable_monitoring_pipeline_logs: typing.Optional[bool] = None,
objective_configs: typing.Optional[
typing.Union[
google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig,
typing.Dict[
str, google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig
],
]
] = None,
deployed_model_ids: typing.Optional[typing.List[str]] = None,
update_request_timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.jobs.ModelDeploymentMonitoringJob
```


Updates an existing ModelDeploymentMonitoringJob.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the ModelDeploymentMonitoringJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. Display name of a ModelDeploymentMonitoringJob. |
`schedule_config` |
`model_monitoring.schedule.ScheduleConfig`
Required. Configures model monitoring job scheduling interval in hours. This defines how often the monitoring jobs are triggered. |
`alert_config` |
`model_monitoring.alert.EmailAlertConfig`
Optional. Configures how alerts are sent to the user. Right now only email alert is supported. |
`logging_sampling_strategy` |
`model_monitoring.sampling.RandomSampleConfig`
Required. Sample Strategy for logging. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize the ModelDeploymentMonitoringJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`bigquery_tables_log_ttl` |
`int`
Optional. The number of days for which the logs are stored. The TTL(time to live) of BigQuery tables in user projects which stores logs. A day is the basic unit of the TTL and we take the ceil of TTL/86400(a day). e.g. { second: 3600} indicates ttl = 1 day. |
`enable_monitoring_pipeline_logs` |
`bool`
Optional. If true, the scheduled monitoring pipeline logs are sent to Google Cloud Logging, including pipeline status and anomalies detected. Please note the logs incur cost, which are subject to |
`deployed_model_ids` |
`List[str]`
Optional. Use this argument to specify which deployed models to apply the updated objective config to. If left unspecified, the same config will be applied to all deployed models. |
`upate_request_timeout` |
`float`
Optional. Timeout in seconds for the model monitoring job update request. |

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_completion

`wait_for_completion() -> None`


Waits for job to complete.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If job failed or cancelled. |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesdeployrequestendpointconfig__googlecloudaipl_5262c6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeployrequestendpointconfig__googlecloudaipla_62f7d2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployrequestendpointconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest.EndpointConfig -->

# Class EndpointConfig (1.134.0)

`EndpointConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The endpoint config to use for the deployment.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint_display_name` |
`str`
Optional. The user-specified display name of the endpoint. If not set, a default name will be used. |
`dedicated_endpoint_enabled` |
`bool`
Optional. Deprecated. Use dedicated_endpoint_disabled instead. If true, the endpoint will be exposed through a dedicated DNS [Endpoint.dedicated_endpoint_dns]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitations will be removed soon. |
`dedicated_endpoint_disabled` |
`bool`
Optional. By default, if dedicated endpoint is enabled and private service connect config is not set, the endpoint will be exposed through a dedicated DNS [Endpoint.dedicated_endpoint_dns]. If private service connect config is set, the endpoint will be exposed through private service connect. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitations will be removed soon. If this field is set to true, the dedicated endpoint will be disabled and the deployed model will be exposed through the shared DNS {region}-aiplatform.googleapis.com. |
`private_service_connect_config` |
Optional. Configuration for private service connect. If set, the endpoint will be exposed through private service connect. |
`endpoint_user_id` |
`str`
Optional. Immutable. The ID to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Vertex AI will generate a value for this ID. If the first character is a letter, this value may be up to 63 characters, and valid characters are `[a-z0-9-]` . The
last character must be a letter or number.
If the first character is a number, this value may be up to
9 characters, and valid characters are `[0-9]` with no
leading zeros.
When using HTTP/JSON, this field is populated based on a
query string argument, such as `?endpoint_id=12345` . This
is the fallback for fields that are not included in either
the URI or the body.
|

## Methods

### EndpointConfig

`EndpointConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The endpoint config to use for the deployment.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessupervisedhyperparameters_googlecloudaiplatfo_6ca636.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessupervisedhyperparameters.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SupervisedHyperParameters -->

# Class SupervisedHyperParameters (1.134.0)

`SupervisedHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for SFT.

## Attributes |
|
|---|---|
Name |
Description |
`epoch_count` |
`int`
Optional. Number of complete passes the model makes over the entire training dataset during training. |
`learning_rate_multiplier` |
`float`
Optional. Multiplier for adjusting the default learning rate. Mutually exclusive with `learning_rate` .
|
`learning_rate` |
`float`
Optional. Learning rate for tuning. Mutually exclusive with `learning_rate_multiplier` . This feature is only available
for open source models.
|
`adapter_size` |
Optional. Adapter size for tuning. |
`batch_size` |
`int`
Optional. Batch size for tuning. This feature is only available for open source models. |

## Classes

### AdapterSize

`AdapterSize(value)`


Supported adapter sizes for tuning.

## Methods

### SupervisedHyperParameters

`SupervisedHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for SFT.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesjirasourcejiraqueries.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.JiraSource.JiraQueries -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesreasoningenginespecdeploymentspecresourcelimitsen_9c0de8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreasoningenginespecdeploymentspecresourcelimitsent_4304e7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreasoningenginespecdeploymentspecresourcelimitsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.DeploymentSpec.ResourceLimitsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinejobruntimeconfigparametervaluesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.ParameterValuesEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslistcustomjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListCustomJobsPager -->

# Class ListCustomJobsPager (1.134.0)

```
ListCustomJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse,
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
[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse) object, and
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

All the usual [ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListCustomJobsPager

```
ListCustomJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadatacontentva_f07eff.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadatacontentval_645cec.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadatacontentvali_da4a9b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadatacontentvalid_50d022.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadatacontentvalidationstats.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborSearchOperationMetadata.ContentValidationStats -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturestoremonitoringconfigimportfeaturesanalysisstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis.State -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragfile.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagFile -->

# Class RagFile (1.134.0)

`RagFile(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagFile contains user data for chunking, embedding and indexing.

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
Output only. Google Cloud Storage location of the RagFile. It does not support wildcards in the Cloud Storage uri for now. This field is a member of `oneof` _ `rag_file_source` .
|
`google_drive_source` |
Output only. Google Drive location. Supports importing individual files as well as Google Drive folders. This field is a member of `oneof` _ `rag_file_source` .
|
`direct_upload_source` |
Output only. The RagFile is encapsulated and uploaded in the UploadRagFile request. This field is a member of `oneof` _ `rag_file_source` .
|
`slack_source` |
The RagFile is imported from a Slack channel. This field is a member of `oneof` _ `rag_file_source` .
|
`jira_source` |
The RagFile is imported from a Jira query. This field is a member of `oneof` _ `rag_file_source` .
|
`share_point_sources` |
The RagFile is imported from a SharePoint source. This field is a member of `oneof` _ `rag_file_source` .
|
`name` |
`str`
Output only. The resource name of the RagFile. |
`display_name` |
`str`
Required. The display name of the RagFile. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the RagFile. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagFile was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagFile was last updated. |
`file_status` |
Output only. State of the RagFile. |

## Methods

### RagFile

`RagFile(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagFile contains user data for chunking, embedding and indexing.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesreadfeaturevaluesrequest_googlecloudaiplatfo_4117a5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesreadfeaturevaluesrequest_googlecloudaiplatfor_ee2a75.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadfeaturevaluesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadFeatureValuesRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictinstance_v1typesimageobjectdetectionpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageObjectDetectionPredictionInstance -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreatetensorboardtimeseriesrequest_googlecloudaipl_0764b9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatetensorboardtimeseriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardTimeSeriesRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescometspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CometSpec -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesdataset_servicepagerslistdataitemspager_google_f43536.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdataset_servicepagerslistdataitemspager_googlec_f4a7f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerslistdataitemspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDataItemsPager -->

# Class ListDataItemsPager (1.134.0)

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

## Methods

### ListDataItemsPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicessession_servicepagerslisteventspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListEventsPager -->

# Class ListEventsPager (1.134.0)

```
ListEventsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse,
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


A pager for iterating through `list_events`

requests.

This class thinly wraps an initial
[ListEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse) object, and
provides an `__iter__`

method to iterate through its
`session_events`

field.

If there are more pages, the `__iter__`

method will make additional
`ListEvents`

requests and continue to iterate
through the `session_events`

field on the
corresponding responses.

All the usual [ListEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEventsPager

```
ListEventsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnearestneighborquerynumericfilter__googlecloudaipl_92b272.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnearestneighborquerynumericfilter.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborQuery.NumericFilter -->

# Class NumericFilter (1.134.0)

`NumericFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Numeric filter is used to search a subset of the entities by using boolean rules on numeric columns. For example: Database Point 0: {name: "a" value_int: 42} {name: "b" value_float: 1.0} Database Point 1: {name: "a" value_int: 10} {name: "b" value_float: 2.0} Database Point 2: {name: "a" value_int: -1} {name: "b" value_float: 3.0} Query: {name: "a" value_int: 12 operator: LESS} // Matches Point 1, 2 {name: "b" value_float: 2.0 operator: EQUAL} // Matches Point 1

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


Datapoints for which Operator is true relative to the query's Value field will be allowlisted.

## Methods

### NumericFilter

`NumericFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Numeric filter is used to search a subset of the entities by using boolean rules on numeric columns. For example: Database Point 0: {name: "a" value_int: 42} {name: "b" value_float: 1.0} Database Point 1: {name: "a" value_int: 10} {name: "b" value_float: 2.0} Database Point 2: {name: "a" value_int: -1} {name: "b" value_float: 3.0} Query: {name: "a" value_int: 12 operator: LESS} // Matches Point 1, 2 {name: "b" value_float: 2.0 operator: EQUAL} // Matches Point 1

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreadtensorboardtimeseriesdatarequest_googlecloudai_b328c8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadtensorboardtimeseriesdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardTimeSeriesDataRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringjobexecutiondetailobjectivestatusentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringJobExecutionDetail.ObjectiveStatusEntry -->

# Class ObjectiveStatusEntry (1.134.0)

`ObjectiveStatusEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ObjectiveStatusEntry

`ObjectiveStatusEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1servicesschedule_servicepagerslistschedulespager_goo_65468f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesschedule_servicepagerslistschedulespager_goog_0e0b96.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesschedule_servicepagerslistschedulespager_googl_70d0ac.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesschedule_servicepagerslistschedulespager_google_51988f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesschedule_servicepagerslistschedulespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.pagers.ListSchedulesPager -->

# Class ListSchedulesPager (1.134.0)

```
ListSchedulesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse
],
request: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse,
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
[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesResponse) object, and
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

All the usual [ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSchedulesPager

```
ListSchedulesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse
],
request: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicepagerslistartifactspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListArtifactsPager -->

# Class ListArtifactsPager (1.134.0)

```
ListArtifactsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse,
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
[ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse) object, and
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

All the usual [ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListArtifactsPager

```
ListArtifactsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesannotation_googlecloudaiplatform_v1servicesfeature_5306e4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesannotation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Annotation -->

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
Optional. The labels with user-defined metadata to organize your Annotations. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Annotation(System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each Annotation: - "aiplatform.googleapis.com/annotation_set_name": optional, name of the UI's annotation set this Annotation belongs to. If not set, the Annotation is not visible in the UI. - "aiplatform.googleapis.com/payload_schema": output only, its value is the [payload_schema's][google.cloud.aiplatform.v1.Annotation.payload_schema_uri] title. |

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_registry_servicepagerslistfeaturespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeaturesPager -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesvizier_servicepagersliststudiespager__goo_18cd1d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesvizier_servicepagersliststudiespager__goog_c9e1bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvizier_servicepagersliststudiespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListStudiesPager -->

# Class ListStudiesPager (1.134.0)

```
ListStudiesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse,
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


A pager for iterating through `list_studies`

requests.

This class thinly wraps an initial
[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesResponse) object, and
provides an `__iter__`

method to iterate through its
`studies`

field.

If there are more pages, the `__iter__`

method will make additional
`ListStudies`

requests and continue to iterate
through the `studies`

field on the
corresponding responses.

All the usual [ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListStudiesPager

```
ListStudiesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schemapredictparams_v1typesimageclassificationprediction_31fbf2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictparams_v1typesimageclassificationpredictionparams.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.ImageClassificationPredictionParams -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgroundednessinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundednessInstance -->

# Class GroundednessInstance (1.134.0)

`GroundednessInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness instance.

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
`context` |
`str`
Required. Background information provided in context used to compare against the prediction. This field is a member of `oneof` _ `_context` .
|

## Methods

### GroundednessInstance

`GroundednessInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmigrateresourcerequestmigratemlenginemodelversion_7b8ef6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmigrateresourcerequestmigratemlenginemodelversionc_9d2aa9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmigrateresourcerequestmigratemlenginemodelversionconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest.MigrateMlEngineModelVersionConfig -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescontentmap.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ContentMap -->

# Class ContentMap (1.134.0)

`ContentMap(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Map of placeholder in metric prompt template to contents of model input.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableMapping[str, `
Optional. Map of placeholder to contents. |

## Classes

### Contents

`Contents(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Repeated Content type.

### ValuesEntry

`ValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ContentMap

`ContentMap(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Map of placeholder in metric prompt template to contents of model input.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesendpoint_servicepagerslistendpointspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.pagers.ListEndpointsPager -->

# Class ListEndpointsPager (1.134.0)

```
ListEndpointsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse
],
request: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse,
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
[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsResponse) object, and
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

All the usual [ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEndpointsPager

```
ListEndpointsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse
],
request: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesllm_utility_servicellmutilityserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceClient -->

# Class LlmUtilityServiceClient (1.134.0)

```
LlmUtilityServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### LlmUtilityServiceClient

```
LlmUtilityServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the llm utility service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the LlmUtilityServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_compute_tokens():
# Create a client
client = aiplatform_v1beta1.
```[LlmUtilityServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ComputeTokensRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ComputeTokensRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[compute_tokens](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceClient.html#google_cloud_aiplatform_v1beta1_services_llm_utility_service_LlmUtilityServiceClient_compute_tokens)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ComputeTokens RPC call. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to get lists of tokens and token ids. This corresponds to the |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Optional. The instances that are the input to token computing API call. Schema is identical to the prediction schema of the text model, even for the non-text models, like chat models, or Codey models. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
`LlmUtilityServiceClient` |
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
`LlmUtilityServiceClient` |
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
`LlmUtilityServiceClient` |
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
