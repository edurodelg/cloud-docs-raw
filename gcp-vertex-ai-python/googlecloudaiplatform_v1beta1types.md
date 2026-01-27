---
source_url: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types
fetched_at: 2026-01-27T03:19:48.046372
---

# Package types (1.134.0)

API documentation for `aiplatform_v1beta1.types`

package.

## Classes

[AcceleratorType](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AcceleratorType)

Represents a hardware accelerator type.

[AcceptPublisherModelEulaRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AcceptPublisherModelEulaRequest)

Request message for ModelGardenService.AcceptPublisherModelEula.

[ActiveLearningConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ActiveLearningConfig)

Parameters that configure the active learning pipeline. Active learning will label the data incrementally by several iterations. For every iteration, it will select a batch of data based on the sampling strategy.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[AddContextArtifactsAndExecutionsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddContextArtifactsAndExecutionsRequest)

Request message for MetadataService.AddContextArtifactsAndExecutions.

[AddContextArtifactsAndExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddContextArtifactsAndExecutionsResponse)

Response message for MetadataService.AddContextArtifactsAndExecutions.

[AddContextChildrenRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddContextChildrenRequest)

Request message for MetadataService.AddContextChildren.

[AddContextChildrenResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddContextChildrenResponse)

Response message for MetadataService.AddContextChildren.

[AddExecutionEventsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddExecutionEventsRequest)

Request message for MetadataService.AddExecutionEvents.

[AddExecutionEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddExecutionEventsResponse)

Response message for MetadataService.AddExecutionEvents.

[AddTrialMeasurementRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddTrialMeasurementRequest)

Request message for VizierService.AddTrialMeasurement.

[AggregationOutput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AggregationOutput)

The aggregation result for the entire dataset and all metrics.

[AggregationResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AggregationResult)

The aggregation result for a single metric.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[Annotation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Annotation)

Used to assign specific AnnotationSpec to a particular area of a DataItem or the whole part of the DataItem.

[AnnotationSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AnnotationSpec)

Identifies a concept with which DataItems may be annotated with.

[ApiAuth](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ApiAuth)

The generic reusable api auth config.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[AppendEventRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AppendEventRequest)

Request message for SessionService.AppendEvent.

[AppendEventResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AppendEventResponse)

Response message for SessionService.AppendEvent.

[Artifact](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Artifact)

Instance of a general artifact.

[ArtifactTypeSchema](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ArtifactTypeSchema)

The definition of a artifact type in MLMD.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[AssembleDataOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssembleDataOperationMetadata)

Runtime operation information for DatasetService.AssembleData.

[AssembleDataRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssembleDataRequest)

Request message for DatasetService.AssembleData. Used only for MULTIMODAL datasets.

[AssembleDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssembleDataResponse)

Response message for DatasetService.AssembleData.

[AssessDataOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataOperationMetadata)

Runtime operation information for DatasetService.AssessData.

[AssessDataRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest)

Request message for DatasetService.AssessData. Used only for MULTIMODAL datasets.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[AssessDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataResponse)

Response message for DatasetService.AssessData.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[AssignNotebookRuntimeOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssignNotebookRuntimeOperationMetadata)

Metadata information for NotebookService.AssignNotebookRuntime.

[AssignNotebookRuntimeRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssignNotebookRuntimeRequest)

Request message for NotebookService.AssignNotebookRuntime.

[Attribution](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Attribution)

Attribution that explains a particular prediction output.

[AugmentPromptRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AugmentPromptRequest)

Request message for AugmentPrompt.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[AugmentPromptResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AugmentPromptResponse)

Response message for AugmentPrompt.

[AuthConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AuthConfig)

Auth configuration to run the extension.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[AuthType](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AuthType)

Type of Auth.

[AutomaticResources](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AutomaticResources)

A description of resources that to large degree are decided by Vertex AI, and require only a modest additional configuration. Each Model supporting these resources documents its specific guidelines.

[AutoraterConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AutoraterConfig)

The configs for autorater. This is applicable to both EvaluateInstances and EvaluateDataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[AutoscalingMetricSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AutoscalingMetricSpec)

The metric specification that defines the target resource utilization (CPU utilization, accelerator's duty cycle, and so on) for calculating the desired replica count.

[AvroSource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AvroSource)

The storage details for Avro input content.

[BatchCancelPipelineJobsOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsOperationMetadata)

Runtime operation information for PipelineService.BatchCancelPipelineJobs.

[BatchCancelPipelineJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsRequest)

Request message for PipelineService.BatchCancelPipelineJobs.

[BatchCancelPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsResponse)

Response message for PipelineService.BatchCancelPipelineJobs.

[BatchCreateFeaturesOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesOperationMetadata)

Details of operations that perform batch create Features.

[BatchCreateFeaturesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesRequest)

Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures.

[BatchCreateFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesResponse)

Response message for FeaturestoreService.BatchCreateFeatures.

[BatchCreateTensorboardRunsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateTensorboardRunsRequest)

Request message for TensorboardService.BatchCreateTensorboardRuns.

[BatchCreateTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateTensorboardRunsResponse)

Response message for TensorboardService.BatchCreateTensorboardRuns.

[BatchCreateTensorboardTimeSeriesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateTensorboardTimeSeriesRequest)

Request message for TensorboardService.BatchCreateTensorboardTimeSeries.

[BatchCreateTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateTensorboardTimeSeriesResponse)

Response message for TensorboardService.BatchCreateTensorboardTimeSeries.

[BatchDedicatedResources](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchDedicatedResources)

A description of resources that are used for performing batch operations, are dedicated to a Model, and need manual configuration.

[BatchDeletePipelineJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchDeletePipelineJobsRequest)

Request message for PipelineService.BatchDeletePipelineJobs.

[BatchDeletePipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchDeletePipelineJobsResponse)

Response message for PipelineService.BatchDeletePipelineJobs.

[BatchImportEvaluatedAnnotationsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportEvaluatedAnnotationsRequest)

Request message for ModelService.BatchImportEvaluatedAnnotations

[BatchImportEvaluatedAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportEvaluatedAnnotationsResponse)

Response message for ModelService.BatchImportEvaluatedAnnotations

[BatchImportModelEvaluationSlicesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportModelEvaluationSlicesRequest)

Request message for ModelService.BatchImportModelEvaluationSlices

[BatchImportModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportModelEvaluationSlicesResponse)

Response message for ModelService.BatchImportModelEvaluationSlices

[BatchMigrateResourcesOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesOperationMetadata)

Runtime operation information for MigrationService.BatchMigrateResources.

[BatchMigrateResourcesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesRequest)

Request message for MigrationService.BatchMigrateResources.

[BatchMigrateResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesResponse)

Response message for MigrationService.BatchMigrateResources.

[BatchPredictionJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchPredictionJob)

A job that uses a Model to produce predictions on multiple [input instances][google.cloud.aiplatform.v1beta1.BatchPredictionJob.input_config]. If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances.

[BatchReadFeatureValuesOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesOperationMetadata)

Details of operations that batch reads Feature values.

[BatchReadFeatureValuesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesRequest)

Request message for FeaturestoreService.BatchReadFeatureValues.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[BatchReadFeatureValuesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesResponse)

Response message for FeaturestoreService.BatchReadFeatureValues.

[BatchReadTensorboardTimeSeriesDataRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadTensorboardTimeSeriesDataRequest)

Request message for TensorboardService.BatchReadTensorboardTimeSeriesData.

[BatchReadTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadTensorboardTimeSeriesDataResponse)

Response message for TensorboardService.BatchReadTensorboardTimeSeriesData.

[BigQueryDestination](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BigQueryDestination)

The BigQuery location for the output content.

[BigQuerySource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BigQuerySource)

The BigQuery location for the input content.

[BleuInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BleuInput)

Input for bleu metric.

[BleuInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BleuInstance)

Spec for bleu instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[BleuMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BleuMetricValue)

Bleu metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[BleuResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BleuResults)

Results for bleu metric.

[BleuSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BleuSpec)

Spec for bleu score metric - calculates the precision of n-grams in the prediction as compared to reference - returns a score ranging between 0 to 1.

[Blob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Blob)

Content blob.

It's preferred to send as text directly rather than raw bytes.

[BlurBaselineConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BlurBaselineConfig)

Config for blur baseline.

When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here:

[BoolArray](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BoolArray)

A list of boolean values.

[CachedContent](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CachedContent)

A resource used in LLM queries for users to explicitly specify what to cache and how to cache.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CancelBatchPredictionJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelBatchPredictionJobRequest)

Request message for JobService.CancelBatchPredictionJob.

[CancelCustomJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelCustomJobRequest)

Request message for JobService.CancelCustomJob.

[CancelDataLabelingJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelDataLabelingJobRequest)

Request message for JobService.CancelDataLabelingJob.

[CancelHyperparameterTuningJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelHyperparameterTuningJobRequest)

Request message for JobService.CancelHyperparameterTuningJob.

[CancelNasJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelNasJobRequest)

Request message for JobService.CancelNasJob.

[CancelPipelineJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelPipelineJobRequest)

Request message for PipelineService.CancelPipelineJob.

[CancelTrainingPipelineRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelTrainingPipelineRequest)

Request message for PipelineService.CancelTrainingPipeline.

[CancelTuningJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelTuningJobRequest)

Request message for GenAiTuningService.CancelTuningJob.

[Candidate](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Candidate)

A response candidate generated from the model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ChatCompletionsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ChatCompletionsRequest)

Request message for [PredictionService.ChatCompletions]

[CheckPublisherModelEulaAcceptanceRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckPublisherModelEulaAcceptanceRequest)

Request message for [ModelGardenService.CheckPublisherModelEula][].

[CheckTrialEarlyStoppingStateMetatdata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckTrialEarlyStoppingStateMetatdata)

This message will be placed in the metadata field of a google.longrunning.Operation associated with a CheckTrialEarlyStoppingState request.

[CheckTrialEarlyStoppingStateRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckTrialEarlyStoppingStateRequest)

Request message for VizierService.CheckTrialEarlyStoppingState.

[CheckTrialEarlyStoppingStateResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckTrialEarlyStoppingStateResponse)

Response message for VizierService.CheckTrialEarlyStoppingState.

[Checkpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Checkpoint)

Describes the machine learning model version checkpoint.

[Citation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Citation)

Source attributions for content.

[CitationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CitationMetadata)

A collection of source attributions for a piece of content.

[Claim](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Claim)

Claim that is extracted from the input text and facts that support it.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ClientConnectionConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ClientConnectionConfig)

Configurations (e.g. inference timeout) that are applied on your endpoints.

[CodeExecutionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CodeExecutionResult)

Result of executing the [ExecutableCode].

Always follows a `part`

containing the [ExecutableCode].

[CoherenceInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceInput)

Input for coherence metric.

[CoherenceInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceInstance)

Spec for coherence instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CoherenceResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceResult)

Spec for coherence result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CoherenceSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceSpec)

Spec for coherence score metric.

[ColabImage](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ColabImage)

Colab image of the runtime.

[CometInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CometInput)

Input for Comet metric.

[CometInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CometInstance)

Spec for Comet instance - The fields used for evaluation are dependent on the comet version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CometResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CometResult)

Spec for Comet result - calculates the comet score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CometSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CometSpec)

Spec for Comet metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CompleteTrialRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CompleteTrialRequest)

Request message for VizierService.CompleteTrial.

[CompletionStats](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CompletionStats)

Success and error statistics of processing multiple entities (for example, DataItems or structured data rows) in batch.

[ComputeTokensRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ComputeTokensRequest)

Request message for ComputeTokens RPC call.

[ComputeTokensResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ComputeTokensResponse)

Response message for ComputeTokens RPC call.

[ContainerRegistryDestination](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ContainerRegistryDestination)

The Container Registry location for the container image.

[ContainerSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ContainerSpec)

The spec of a Container.

[Content](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Content)

The base structured datatype containing multi-part content of a message.

A `Content`

includes a `role`

field designating the producer of
the `Content`

and a `parts`

field containing multi-part data
that contains the content of the message turn.

[ContentMap](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ContentMap)

Map of placeholder in metric prompt template to contents of model input.

[ContentsExample](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ContentsExample)

A single example of a conversation with the model.

[Context](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Context)

Instance of a general context.

[CopyModelOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CopyModelOperationMetadata)

Details of ModelService.CopyModel operation.

[CopyModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CopyModelRequest)

Request message for ModelService.CopyModel.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CopyModelResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CopyModelResponse)

Response message of ModelService.CopyModel operation.

[CorpusStatus](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorpusStatus)

RagCorpus status.

[CorroborateContentRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentRequest)

Request message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CorroborateContentResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentResponse)

Response message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CountTokensRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CountTokensRequest)

Request message for PredictionService.CountTokens.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CountTokensResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CountTokensResponse)

Response message for PredictionService.CountTokens.

[CreateArtifactRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateArtifactRequest)

Request message for MetadataService.CreateArtifact.

[CreateBatchPredictionJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateBatchPredictionJobRequest)

Request message for JobService.CreateBatchPredictionJob.

[CreateCachedContentRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateCachedContentRequest)

Request message for GenAiCacheService.CreateCachedContent.

[CreateContextRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateContextRequest)

Request message for MetadataService.CreateContext.

[CreateCustomJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateCustomJobRequest)

Request message for JobService.CreateCustomJob.

[CreateDataLabelingJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDataLabelingJobRequest)

Request message for JobService.CreateDataLabelingJob.

[CreateDatasetOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetOperationMetadata)

Runtime operation information for DatasetService.CreateDataset.

[CreateDatasetRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetRequest)

Request message for DatasetService.CreateDataset.

[CreateDatasetVersionOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetVersionOperationMetadata)

Runtime operation information for DatasetService.CreateDatasetVersion.

[CreateDatasetVersionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetVersionRequest)

Request message for DatasetService.CreateDatasetVersion.

[CreateDeploymentResourcePoolOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDeploymentResourcePoolOperationMetadata)

Runtime operation information for CreateDeploymentResourcePool method.

[CreateDeploymentResourcePoolRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDeploymentResourcePoolRequest)

Request message for CreateDeploymentResourcePool method.

[CreateEndpointOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEndpointOperationMetadata)

Runtime operation information for EndpointService.CreateEndpoint.

[CreateEndpointRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEndpointRequest)

Request message for EndpointService.CreateEndpoint.

[CreateEntityTypeOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEntityTypeOperationMetadata)

Details of operations that perform create EntityType.

[CreateEntityTypeRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEntityTypeRequest)

Request message for FeaturestoreService.CreateEntityType.

[CreateExampleStoreOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateExampleStoreOperationMetadata)

Details of ExampleStoreService.CreateExampleStore operation.

[CreateExampleStoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateExampleStoreRequest)

Request message for ExampleStoreService.CreateExampleStore.

[CreateExecutionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateExecutionRequest)

Request message for MetadataService.CreateExecution.

[CreateFeatureGroupOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureGroupOperationMetadata)

Details of operations that perform create FeatureGroup.

[CreateFeatureGroupRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureGroupRequest)

Request message for FeatureRegistryService.CreateFeatureGroup.

[CreateFeatureMonitorJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorJobRequest)

Request message for [FeatureRegistryService.CreateFeatureMonitorJobRequest][].

[CreateFeatureMonitorOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorOperationMetadata)

Details of operations that perform create FeatureMonitor.

[CreateFeatureMonitorRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorRequest)

Request message for [FeatureRegistryService.CreateFeatureMonitorRequest][].

[CreateFeatureOnlineStoreOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureOnlineStoreOperationMetadata)

Details of operations that perform create FeatureOnlineStore.

[CreateFeatureOnlineStoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureOnlineStoreRequest)

Request message for FeatureOnlineStoreAdminService.CreateFeatureOnlineStore.

[CreateFeatureOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureOperationMetadata)

Details of operations that perform create Feature.

[CreateFeatureRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest)

Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature.

[CreateFeatureViewOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureViewOperationMetadata)

Details of operations that perform create FeatureView.

[CreateFeatureViewRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureViewRequest)

Request message for FeatureOnlineStoreAdminService.CreateFeatureView.

[CreateFeaturestoreOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeaturestoreOperationMetadata)

Details of operations that perform create Featurestore.

[CreateFeaturestoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeaturestoreRequest)

Request message for FeaturestoreService.CreateFeaturestore.

[CreateHyperparameterTuningJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateHyperparameterTuningJobRequest)

Request message for JobService.CreateHyperparameterTuningJob.

[CreateIndexEndpointOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexEndpointOperationMetadata)

Runtime operation information for IndexEndpointService.CreateIndexEndpoint.

[CreateIndexEndpointRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexEndpointRequest)

Request message for IndexEndpointService.CreateIndexEndpoint.

[CreateIndexOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexOperationMetadata)

Runtime operation information for IndexService.CreateIndex.

[CreateIndexRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexRequest)

Request message for IndexService.CreateIndex.

[CreateMemoryOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMemoryOperationMetadata)

Details of MemoryBankService.CreateMemory operation.

[CreateMemoryRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMemoryRequest)

Request message for MemoryBankService.CreateMemory.

[CreateMetadataSchemaRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMetadataSchemaRequest)

Request message for MetadataService.CreateMetadataSchema.

[CreateMetadataStoreOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMetadataStoreOperationMetadata)

Details of operations that perform MetadataService.CreateMetadataStore.

[CreateMetadataStoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMetadataStoreRequest)

Request message for MetadataService.CreateMetadataStore.

[CreateModelDeploymentMonitoringJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateModelDeploymentMonitoringJobRequest)

Request message for JobService.CreateModelDeploymentMonitoringJob.

[CreateModelMonitorOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateModelMonitorOperationMetadata)

Runtime operation information for ModelMonitoringService.CreateModelMonitor.

[CreateModelMonitorRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateModelMonitorRequest)

Request message for ModelMonitoringService.CreateModelMonitor.

[CreateModelMonitoringJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateModelMonitoringJobRequest)

Request message for ModelMonitoringService.CreateModelMonitoringJob.

[CreateNasJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNasJobRequest)

Request message for JobService.CreateNasJob.

[CreateNotebookExecutionJobOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookExecutionJobOperationMetadata)

Metadata information for NotebookService.CreateNotebookExecutionJob.

[CreateNotebookExecutionJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookExecutionJobRequest)

Request message for [NotebookService.CreateNotebookExecutionJob]

[CreateNotebookRuntimeTemplateOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookRuntimeTemplateOperationMetadata)

Metadata information for NotebookService.CreateNotebookRuntimeTemplate.

[CreateNotebookRuntimeTemplateRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookRuntimeTemplateRequest)

Request message for NotebookService.CreateNotebookRuntimeTemplate.

[CreatePersistentResourceOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePersistentResourceOperationMetadata)

Details of operations that perform create PersistentResource.

[CreatePersistentResourceRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePersistentResourceRequest)

Request message for PersistentResourceService.CreatePersistentResource.

[CreatePipelineJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePipelineJobRequest)

Request message for PipelineService.CreatePipelineJob.

[CreateRagCorpusOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateRagCorpusOperationMetadata)

Runtime operation information for VertexRagDataService.CreateRagCorpus.

[CreateRagCorpusRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateRagCorpusRequest)

Request message for VertexRagDataService.CreateRagCorpus.

[CreateReasoningEngineOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateReasoningEngineOperationMetadata)

Details of ReasoningEngineService.CreateReasoningEngine operation.

[CreateReasoningEngineRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateReasoningEngineRequest)

Request message for ReasoningEngineService.CreateReasoningEngine.

[CreateRegistryFeatureOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateRegistryFeatureOperationMetadata)

Details of operations that perform create FeatureGroup.

[CreateScheduleRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateScheduleRequest)

Request message for ScheduleService.CreateSchedule.

[CreateSessionOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSessionOperationMetadata)

Metadata associated with the SessionService.CreateSession operation.

[CreateSessionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSessionRequest)

Request message for SessionService.CreateSession.

[CreateSpecialistPoolOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSpecialistPoolOperationMetadata)

Runtime operation information for SpecialistPoolService.CreateSpecialistPool.

[CreateSpecialistPoolRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSpecialistPoolRequest)

Request message for SpecialistPoolService.CreateSpecialistPool.

[CreateStudyRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateStudyRequest)

Request message for VizierService.CreateStudy.

[CreateTensorboardExperimentRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardExperimentRequest)

Request message for TensorboardService.CreateTensorboardExperiment.

[CreateTensorboardOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardOperationMetadata)

Details of operations that perform create Tensorboard.

[CreateTensorboardRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardRequest)

Request message for TensorboardService.CreateTensorboard.

[CreateTensorboardRunRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardRunRequest)

Request message for TensorboardService.CreateTensorboardRun.

[CreateTensorboardTimeSeriesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardTimeSeriesRequest)

Request message for TensorboardService.CreateTensorboardTimeSeries.

[CreateTrainingPipelineRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTrainingPipelineRequest)

Request message for PipelineService.CreateTrainingPipeline.

[CreateTrialRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTrialRequest)

Request message for VizierService.CreateTrial.

[CreateTuningJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTuningJobRequest)

Request message for GenAiTuningService.CreateTuningJob.

[CsvDestination](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CsvDestination)

The storage details for CSV output content.

[CsvSource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CsvSource)

The storage details for CSV input content.

[CustomJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomJob)

Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded).

[CustomJobSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomJobSpec)

Represents the spec of a CustomJob.

[CustomOutput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomOutput)

Spec for custom output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CustomOutputFormatConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomOutputFormatConfig)

Spec for custom output format configuration.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[DataItem](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DataItem)

A piece of data in a Dataset. Could be an image, a video, a document or plain text.

[DataItemView](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DataItemView)

A container for a single DataItem and Annotations on it.

[DataLabelingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DataLabelingJob)

DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset:

[Dataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Dataset)

A collection of DataItems and Annotations on them.

[DatasetDistribution](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetDistribution)

Distribution computed over a tuning dataset.

[DatasetStats](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetStats)

Statistics computed over a tuning dataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[DatasetVersion](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetVersion)

Describes the dataset version.

[DedicatedResources](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DedicatedResources)

A description of resources that are dedicated to a DeployedModel or DeployedIndex, and that need a higher degree of manual configuration.

[DeleteArtifactRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteArtifactRequest)

Request message for MetadataService.DeleteArtifact.

[DeleteBatchPredictionJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteBatchPredictionJobRequest)

Request message for JobService.DeleteBatchPredictionJob.

[DeleteCachedContentRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteCachedContentRequest)

Request message for GenAiCacheService.DeleteCachedContent.

[DeleteContextRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteContextRequest)

Request message for MetadataService.DeleteContext.

[DeleteCustomJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteCustomJobRequest)

Request message for JobService.DeleteCustomJob.

[DeleteDataLabelingJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDataLabelingJobRequest)

Request message for JobService.DeleteDataLabelingJob.

[DeleteDatasetRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetRequest)

Request message for DatasetService.DeleteDataset.

[DeleteDatasetVersionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetVersionRequest)

Request message for DatasetService.DeleteDatasetVersion.

[DeleteDeploymentResourcePoolRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDeploymentResourcePoolRequest)

Request message for DeleteDeploymentResourcePool method.

[DeleteEndpointRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteEndpointRequest)

Request message for EndpointService.DeleteEndpoint.

[DeleteEntityTypeRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteEntityTypeRequest)

Request message for [FeaturestoreService.DeleteEntityTypes][].

[DeleteExampleStoreOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteExampleStoreOperationMetadata)

Details of ExampleStoreService.DeleteExampleStore operation.

[DeleteExampleStoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteExampleStoreRequest)

Request message for ExampleStoreService.DeleteExampleStore.

[DeleteExecutionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteExecutionRequest)

Request message for MetadataService.DeleteExecution.

[DeleteExtensionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteExtensionRequest)

Request message for ExtensionRegistryService.DeleteExtension.

[DeleteFeatureGroupRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureGroupRequest)

Request message for FeatureRegistryService.DeleteFeatureGroup.

[DeleteFeatureMonitorRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureMonitorRequest)

Request message for FeatureRegistryService.DeleteFeatureMonitor.

[DeleteFeatureOnlineStoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureOnlineStoreRequest)

Request message for FeatureOnlineStoreAdminService.DeleteFeatureOnlineStore.

[DeleteFeatureRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureRequest)

Request message for FeaturestoreService.DeleteFeature. Request message for FeatureRegistryService.DeleteFeature.

[DeleteFeatureValuesOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesOperationMetadata)

Details of operations that delete Feature values.

[DeleteFeatureValuesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesRequest)

Request message for FeaturestoreService.DeleteFeatureValues.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[DeleteFeatureValuesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesResponse)

Response message for FeaturestoreService.DeleteFeatureValues.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[DeleteFeatureViewRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureViewRequest)

Request message for [FeatureOnlineStoreAdminService.DeleteFeatureViews][].

[DeleteFeaturestoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeaturestoreRequest)

Request message for FeaturestoreService.DeleteFeaturestore.

[DeleteHyperparameterTuningJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteHyperparameterTuningJobRequest)

Request message for JobService.DeleteHyperparameterTuningJob.

[DeleteIndexEndpointRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteIndexEndpointRequest)

Request message for IndexEndpointService.DeleteIndexEndpoint.

[DeleteIndexRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteIndexRequest)

Request message for IndexService.DeleteIndex.

[DeleteMemoryOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteMemoryOperationMetadata)

Details of MemoryBankService.DeleteMemory operation.

[DeleteMemoryRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteMemoryRequest)

Request message for MemoryBankService.DeleteMemory.

[DeleteMetadataStoreOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteMetadataStoreOperationMetadata)

Details of operations that perform MetadataService.DeleteMetadataStore.

[DeleteMetadataStoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteMetadataStoreRequest)

Request message for MetadataService.DeleteMetadataStore.

[DeleteModelDeploymentMonitoringJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelDeploymentMonitoringJobRequest)

Request message for JobService.DeleteModelDeploymentMonitoringJob.

[DeleteModelMonitorRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelMonitorRequest)

Request message for ModelMonitoringService.DeleteModelMonitor.

[DeleteModelMonitoringJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelMonitoringJobRequest)

Request message for ModelMonitoringService.DeleteModelMonitoringJob.

[DeleteModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelRequest)

Request message for ModelService.DeleteModel.

[DeleteModelVersionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelVersionRequest)

Request message for ModelService.DeleteModelVersion.

[DeleteNasJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNasJobRequest)

Request message for JobService.DeleteNasJob.

[DeleteNotebookExecutionJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookExecutionJobRequest)

Request message for [NotebookService.DeleteNotebookExecutionJob]

[DeleteNotebookRuntimeRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeRequest)

Request message for NotebookService.DeleteNotebookRuntime.

[DeleteNotebookRuntimeTemplateRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeTemplateRequest)

Request message for NotebookService.DeleteNotebookRuntimeTemplate.

[DeleteOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteOperationMetadata)

Details of operations that perform deletes of any entities.

[DeletePersistentResourceRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePersistentResourceRequest)

Request message for PersistentResourceService.DeletePersistentResource.

[DeletePipelineJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePipelineJobRequest)

Request message for PipelineService.DeletePipelineJob.

[DeleteRagCorpusRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagCorpusRequest)

Request message for VertexRagDataService.DeleteRagCorpus.

[DeleteRagFileRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagFileRequest)

Request message for VertexRagDataService.DeleteRagFile.

[DeleteReasoningEngineRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteReasoningEngineRequest)

Request message for ReasoningEngineService.DeleteReasoningEngine.

[DeleteSavedQueryRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSavedQueryRequest)

Request message for DatasetService.DeleteSavedQuery.

[DeleteScheduleRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteScheduleRequest)

Request message for ScheduleService.DeleteSchedule.

[DeleteSessionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSessionRequest)

Request message for SessionService.DeleteSession.

[DeleteSpecialistPoolRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSpecialistPoolRequest)

Request message for SpecialistPoolService.DeleteSpecialistPool.

[DeleteStudyRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteStudyRequest)

Request message for VizierService.DeleteStudy.

[DeleteTensorboardExperimentRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardExperimentRequest)

Request message for TensorboardService.DeleteTensorboardExperiment.

[DeleteTensorboardRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardRequest)

Request message for TensorboardService.DeleteTensorboard.

[DeleteTensorboardRunRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardRunRequest)

Request message for TensorboardService.DeleteTensorboardRun.

[DeleteTensorboardTimeSeriesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardTimeSeriesRequest)

Request message for TensorboardService.DeleteTensorboardTimeSeries.

[DeleteTrainingPipelineRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTrainingPipelineRequest)

Request message for PipelineService.DeleteTrainingPipeline.

[DeleteTrialRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTrialRequest)

Request message for VizierService.DeleteTrial.

[DeployIndexOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployIndexOperationMetadata)

Runtime operation information for IndexEndpointService.DeployIndex.

[DeployIndexRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployIndexRequest)

Request message for IndexEndpointService.DeployIndex.

[DeployIndexResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployIndexResponse)

Response message for IndexEndpointService.DeployIndex.

[DeployModelOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelOperationMetadata)

Runtime operation information for EndpointService.DeployModel.

[DeployModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelRequest)

Request message for EndpointService.DeployModel.

[DeployModelResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelResponse)

Response message for EndpointService.DeployModel.

[DeployOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployOperationMetadata)

Runtime operation information for ModelGardenService.Deploy.

[DeployPublisherModelOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployPublisherModelOperationMetadata)

Runtime operation information for ModelGardenService.DeployPublisherModel.

[DeployPublisherModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployPublisherModelRequest)

Request message for ModelGardenService.DeployPublisherModel.

[DeployPublisherModelResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployPublisherModelResponse)

Response message for ModelGardenService.DeployPublisherModel.

[DeployRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest)

Request message for ModelGardenService.Deploy.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[DeployResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployResponse)

Response message for ModelGardenService.Deploy.

[DeployedIndex](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndex)

A deployment of an Index. IndexEndpoints contain one or more DeployedIndexes.

[DeployedIndexAuthConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndexAuthConfig)

Used to set up the auth on the DeployedIndex's private endpoint.

[DeployedIndexRef](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndexRef)

Points to a DeployedIndex.

[DeployedModel](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel)

A deployment of a Model. Endpoints contain one or more DeployedModels.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[DeployedModelRef](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModelRef)

Points to a DeployedModel.

[DeploymentResourcePool](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeploymentResourcePool)

A description of resources that can be shared by multiple DeployedModels, whose underlying specification consists of a DedicatedResources.

[DeploymentStage](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeploymentStage)

Stage field indicating the current progress of a deployment.

[DestinationFeatureSetting](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DestinationFeatureSetting)

[DirectPredictRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectPredictRequest)

Request message for PredictionService.DirectPredict.

[DirectPredictResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectPredictResponse)

Response message for PredictionService.DirectPredict.

[DirectRawPredictRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectRawPredictRequest)

Request message for PredictionService.DirectRawPredict.

[DirectRawPredictResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectRawPredictResponse)

Response message for PredictionService.DirectRawPredict.

[DirectUploadSource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectUploadSource)

The input content is encapsulated and uploaded in the request.

[DiskSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DiskSpec)

Represents the spec of disk options.

[DistillationDataStats](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DistillationDataStats)

Statistics computed for datasets used for distillation.

[DistillationHyperParameters](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DistillationHyperParameters)

Hyperparameters for Distillation.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[DistillationSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DistillationSpec)

Tuning Spec for Distillation.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[DnsPeeringConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DnsPeeringConfig)

DNS peering configuration. These configurations are used to create DNS peering zones in the Vertex tenant project VPC, enabling resolution of records within the specified domain hosted in the target network's Cloud DNS.

[DoubleArray](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DoubleArray)

A list of double values.

[DynamicRetrievalConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DynamicRetrievalConfig)

Describes the options to customize dynamic retrieval.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[EmbedContentRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EmbedContentRequest)

Request message for PredictionService.EmbedContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[EmbedContentResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EmbedContentResponse)

Response message for PredictionService.EmbedContent.

[EncryptionSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EncryptionSpec)

Represents a customer-managed encryption key spec that can be applied to a top-level resource.

[Endpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint)

Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations.

[EnterpriseWebSearch](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EnterpriseWebSearch)

Tool to search public web data, powered by Vertex AI Search and Sec4 compliance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[EntityIdSelector](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EntityIdSelector)

Selector for entityId. Getting ids from the given source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[EntityType](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EntityType)

An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver.

[EnvVar](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EnvVar)

Represents an environment variable present in a Container or Python Module.

[ErrorAnalysisAnnotation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ErrorAnalysisAnnotation)

Model error analysis for each annotation.

[EvaluateDatasetOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateDatasetOperationMetadata)

Operation metadata for Dataset Evaluation.

[EvaluateDatasetRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateDatasetRequest)

Request message for EvaluationService.EvaluateDataset.

[EvaluateDatasetResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateDatasetResponse)

Response in LRO for EvaluationService.EvaluateDataset.

[EvaluateDatasetRun](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateDatasetRun)

Evaluate Dataset Run Result for Tuning Job.

[EvaluateInstancesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateInstancesRequest)

Request message for EvaluationService.EvaluateInstances.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[EvaluateInstancesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateInstancesResponse)

Response message for EvaluationService.EvaluateInstances.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[EvaluatedAnnotation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluatedAnnotation)

True positive, false positive, or false negative.

EvaluatedAnnotation is only available under ModelEvaluationSlice
with slice of `annotationSpec`

dimension.

[EvaluatedAnnotationExplanation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluatedAnnotationExplanation)

Explanation result of the prediction produced by the Model.

[EvaluationConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluationConfig)

Evaluation Config for Tuning Job.

[EvaluationDataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluationDataset)

The dataset used for evaluation.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[Event](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Event)

An edge describing the relationship between an Artifact and an Execution in a lineage graph.

[EventActions](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EventActions)

Actions are parts of events that are executed by the agent.

[EventMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EventMetadata)

Metadata relating to a LLM response event.

[ExactMatchInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchInput)

Input for exact match metric.

[ExactMatchInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchInstance)

Spec for exact match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ExactMatchMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchMetricValue)

Exact match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ExactMatchResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchResults)

Results for exact match metric.

[ExactMatchSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchSpec)

Spec for exact match metric - returns 1 if prediction and reference exactly matches, otherwise 0.

[Example](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Example)

A single example to upload or read from the Example Store.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ExampleStore](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExampleStore)

Represents an executable service to manage and retrieve examples.

[ExampleStoreConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExampleStoreConfig)

Configuration for the Example Store.

[Examples](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Examples)

Example-based explainability that returns the nearest neighbors from the provided dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ExamplesArrayFilter](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExamplesArrayFilter)

Filters for examples' array metadata fields. An array field is example metadata where multiple values are attributed to a single example.

[ExamplesOverride](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExamplesOverride)

Overrides for example-based explanations.

[ExamplesRestrictionsNamespace](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExamplesRestrictionsNamespace)

Restrictions namespace for example-based explanations overrides.

[ExecutableCode](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExecutableCode)

Code generated by the model that is meant to be executed, and the result returned to the model.

Generated when using the [FunctionDeclaration] tool and [FunctionCallingConfig] mode is set to [Mode.CODE].

[ExecuteExtensionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExecuteExtensionRequest)

Request message for ExtensionExecutionService.ExecuteExtension.

[ExecuteExtensionResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExecuteExtensionResponse)

Response message for ExtensionExecutionService.ExecuteExtension.

[Execution](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Execution)

Instance of a general execution.

[ExplainRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplainRequest)

Request message for PredictionService.Explain.

[ExplainResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplainResponse)

Response message for PredictionService.Explain.

[Explanation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Explanation)

Explanation of a prediction (provided in PredictResponse.predictions) produced by the Model on a given instance.

[ExplanationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata)

Metadata describing the Model's input and output for explanation.

[ExplanationMetadataOverride](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadataOverride)

The ExplanationMetadata entries that can be overridden at [online explanation][google.cloud.aiplatform.v1beta1.PredictionService.Explain] time.

[ExplanationParameters](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationParameters)

Parameters to configure explaining for Model's predictions.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ExplanationSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationSpec)

Specification of Model explanation.

[ExplanationSpecOverride](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationSpecOverride)

The ExplanationSpec entries that can be overridden at [online explanation][google.cloud.aiplatform.v1beta1.PredictionService.Explain] time.

[ExportDataConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataConfig)

Describes what part of the Dataset is to be exported, the destination of the export and how to export.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ExportDataOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataOperationMetadata)

Runtime operation information for DatasetService.ExportData.

[ExportDataRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataRequest)

Request message for DatasetService.ExportData.

[ExportDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataResponse)

Response message for DatasetService.ExportData.

[ExportFeatureValuesOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesOperationMetadata)

Details of operations that exports Features values.

[ExportFeatureValuesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesRequest)

Request message for FeaturestoreService.ExportFeatureValues.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ExportFeatureValuesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesResponse)

Response message for FeaturestoreService.ExportFeatureValues.

[ExportFractionSplit](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFractionSplit)

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

[ExportModelOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportModelOperationMetadata)

Details of ModelService.ExportModel operation.

[ExportModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportModelRequest)

Request message for ModelService.ExportModel.

[ExportModelResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportModelResponse)

Response message of ModelService.ExportModel operation.

[ExportPublisherModelOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportPublisherModelOperationMetadata)

Runtime operation information for ModelGardenService.ExportPublisherModel.

[ExportPublisherModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportPublisherModelRequest)

Request message for ModelGardenService.ExportPublisherModel.

[ExportPublisherModelResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportPublisherModelResponse)

Response message for ModelGardenService.ExportPublisherModel.

[ExportTensorboardTimeSeriesDataRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataRequest)

Request message for TensorboardService.ExportTensorboardTimeSeriesData.

[ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataResponse)

Response message for TensorboardService.ExportTensorboardTimeSeriesData.

[Extension](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Extension)

Extensions are tools for large language models to access external data, run computations, etc.

[ExtensionManifest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExtensionManifest)

Manifest spec of an Extension needed for runtime execution.

[ExtensionOperation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExtensionOperation)

Operation of an extension.

[ExtensionPrivateServiceConnectConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExtensionPrivateServiceConnectConfig)

PrivateExtensionConfig configuration for the extension.

[Fact](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Fact)

The fact used in grounding.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FasterDeploymentConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FasterDeploymentConfig)

Configuration for faster model deployment.

[Feature](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Feature)

Feature Metadata information. For example, color is a feature that describes an apple.

[FeatureGroup](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup)

Vertex AI Feature Group.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FeatureMonitor](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureMonitor)

Vertex AI Feature Monitor.

[FeatureMonitorJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureMonitorJob)

Vertex AI Feature Monitor Job.

[FeatureNoiseSigma](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureNoiseSigma)

Noise sigma by features. Noise sigma represents the standard deviation of the gaussian kernel that will be used to add noise to interpolated inputs prior to computing gradients.

[FeatureOnlineStore](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore)

Vertex AI Feature Online Store provides a centralized repository for serving ML features and embedding indexes at low latency. The Feature Online Store is a top-level container.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FeatureSelectionConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureSelectionConfig)

Feature selection configuration for the FeatureMonitor.

[FeatureSelector](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureSelector)

Selector for Features of an EntityType.

[FeatureStatsAndAnomaly](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureStatsAndAnomaly)

Stats and Anomaly generated by FeatureMonitorJobs. Anomaly only includes Drift.

[FeatureStatsAndAnomalySpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureStatsAndAnomalySpec)

Defines how to select FeatureStatsAndAnomaly to be populated in response. If set, retrieves FeatureStatsAndAnomaly generated by FeatureMonitors based on this spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FeatureStatsAnomaly](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureStatsAnomaly)

Stats and Anomaly generated at specific timestamp for specific Feature. The start_time and end_time are used to define the time range of the dataset that current stats belongs to, e.g. prediction traffic is bucketed into prediction datasets by time window. If the Dataset is not defined by time window, start_time = end_time. Timestamp of the stats and anomalies always refers to end_time. Raw stats and anomalies are stored in stats_uri or anomaly_uri in the tensorflow defined protos. Field data_stats contains almost identical information with the raw stats in Vertex AI defined proto, for UI to display.

[FeatureValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValue)

Value for a feature.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FeatureValueDestination](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValueDestination)

A destination location for Feature values and format.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FeatureValueList](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValueList)

Container for list of values.

[FeatureView](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView)

FeatureView is representation of values that the FeatureOnlineStore will serve based on its syncConfig.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FeatureViewDataFormat](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDataFormat)

Format of the data in the Feature View.

[FeatureViewDataKey](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDataKey)

Lookup key for a feature view.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FeatureViewDirectWriteRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDirectWriteRequest)

Request message for FeatureOnlineStoreService.FeatureViewDirectWrite.

[FeatureViewDirectWriteResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDirectWriteResponse)

Response message for FeatureOnlineStoreService.FeatureViewDirectWrite.

[FeatureViewSync](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewSync)

FeatureViewSync is a representation of sync operation which copies data from data source to Feature View in Online Store.

[Featurestore](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Featurestore)

Vertex AI Feature Store provides a centralized repository for organizing, storing, and serving ML features. The Featurestore is a top-level container for your features and their values.

[FeaturestoreMonitoringConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeaturestoreMonitoringConfig)

Configuration of how features in Featurestore are monitored.

[FetchExamplesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesRequest)

Request message for ExampleStoreService.FetchExamples.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FetchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse)

Response message for ExampleStoreService.FetchExamples.

[FetchFeatureValuesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchFeatureValuesRequest)

Request message for FeatureOnlineStoreService.FetchFeatureValues. All the features under the requested feature view will be returned.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FetchFeatureValuesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchFeatureValuesResponse)

Response message for FeatureOnlineStoreService.FetchFeatureValues

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FetchPublisherModelConfigRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchPublisherModelConfigRequest)

Request message for EndpointService.FetchPublisherModelConfig.

[FileData](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FileData)

URI based data.

[FileStatus](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FileStatus)

RagFile status.

[FilterSplit](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FilterSplit)

Assigns input data to training, validation, and test sets based on the given filters, data pieces not matched by any filter are ignored. Currently only supported for Datasets containing DataItems. If any of the filters in this message are to match nothing, then they can be set as '-' (the minus sign).

Supported only for unstructured Datasets.

[FindNeighborsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsRequest)

The request message for MatchService.FindNeighbors.

[FindNeighborsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsResponse)

The response message for MatchService.FindNeighbors.

[FlexStart](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FlexStart)

FlexStart is used to schedule the deployment workload on DWS resource. It contains the max duration of the deployment.

[FluencyInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FluencyInput)

Input for fluency metric.

[FluencyInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FluencyInstance)

Spec for fluency instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FluencyResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FluencyResult)

Spec for fluency result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FluencySpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FluencySpec)

Spec for fluency score metric.

[FractionSplit](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FractionSplit)

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

[FulfillmentInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FulfillmentInput)

Input for fulfillment metric.

[FulfillmentInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FulfillmentInstance)

Spec for fulfillment instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FulfillmentResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FulfillmentResult)

Spec for fulfillment result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FulfillmentSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FulfillmentSpec)

Spec for fulfillment metric.

[FullFineTunedResources](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FullFineTunedResources)

Resources for an fft model.

[FunctionCall](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionCall)

A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing the parameters and their values.

[FunctionCallingConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionCallingConfig)

Function calling config.

[FunctionDeclaration](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionDeclaration)

Structured representation of a function declaration as defined by
the ```
OpenAPI 3.0
specification <https://spec.openapis.org/oas/v3.0.3>
```

__. Included in
this declaration are the function name, description, parameters and
response type. This FunctionDeclaration is a representation of a
block of code that can be used as a `Tool`

by the model and
executed by the client.

[FunctionResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionResponse)

The result output from a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function is used as context to the model. This should contain the result of a [FunctionCall] made based on model prediction.

[FunctionResponseBlob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionResponseBlob)

Raw media bytes for function response.

Text should not be sent as raw bytes, use the 'text' field.

[FunctionResponseFileData](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionResponseFileData)

URI based data for function response.

[FunctionResponsePart](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionResponsePart)

A datatype containing media that is part of a `FunctionResponse`

message.

A `FunctionResponsePart`

consists of data which has an associated
datatype. A `FunctionResponsePart`

can only contain one of the
accepted types in `FunctionResponsePart.data`

.

A `FunctionResponsePart`

must have a fixed IANA MIME type
identifying the type and subtype of the media if the `inline_data`

field is filled with raw bytes.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[GcsDestination](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GcsDestination)

The Google Cloud Storage location where the output is to be written to.

[GcsSource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GcsSource)

The Google Cloud Storage location for the input content.

[GeminiExample](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GeminiExample)

Format for Gemini examples used for Vertex Multimodal datasets.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[GeminiRequestReadConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GeminiRequestReadConfig)

Configuration for how to read Gemini requests from a multimodal dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[GeminiTemplateConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GeminiTemplateConfig)

Template configuration to create Gemini examples from a multimodal dataset.

[GenAiAdvancedFeaturesConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenAiAdvancedFeaturesConfig)

Configuration for GenAiAdvancedFeatures.

[GenerateContentRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentRequest)

Request message for [PredictionService.GenerateContent].

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[GenerateContentResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentResponse)

Response message for [PredictionService.GenerateContent].

[GenerateFetchAccessTokenRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateFetchAccessTokenRequest)

Request message for [FeatureOnlineStoreService.GenerateFetchAccessToken][].

[GenerateFetchAccessTokenResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateFetchAccessTokenResponse)

Response message for [FeatureOnlineStoreService.GenerateFetchAccessToken][].

[GenerateMemoriesOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesOperationMetadata)

Details of MemoryBankService.GenerateMemories operation.

[GenerateMemoriesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest)

Request message for MemoryBankService.GenerateMemories.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[GenerateMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesResponse)

Response message for MemoryBankService.GenerateMemories.

[GenerateVideoResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateVideoResponse)

Generate video response.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[GenerationConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig)

Generation config.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[GenericOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenericOperationMetadata)

Generic Metadata shared by all operations.

[GenieSource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenieSource)

Contains information about the source of the models generated from Generative AI Studio.

[GetAnnotationSpecRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetAnnotationSpecRequest)

Request message for DatasetService.GetAnnotationSpec.

[GetArtifactRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetArtifactRequest)

Request message for MetadataService.GetArtifact.

[GetBatchPredictionJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetBatchPredictionJobRequest)

Request message for JobService.GetBatchPredictionJob.

[GetCachedContentRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetCachedContentRequest)

Request message for GenAiCacheService.GetCachedContent.

[GetContextRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetContextRequest)

Request message for MetadataService.GetContext.

[GetCustomJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetCustomJobRequest)

Request message for JobService.GetCustomJob.

[GetDataLabelingJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDataLabelingJobRequest)

Request message for JobService.GetDataLabelingJob.

[GetDatasetRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetRequest)

Request message for DatasetService.GetDataset.

[GetDatasetVersionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetVersionRequest)

Request message for DatasetService.GetDatasetVersion.

[GetDeploymentResourcePoolRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDeploymentResourcePoolRequest)

Request message for GetDeploymentResourcePool method.

[GetEndpointRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetEndpointRequest)

Request message for EndpointService.GetEndpoint

[GetEntityTypeRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetEntityTypeRequest)

Request message for FeaturestoreService.GetEntityType.

[GetExampleStoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetExampleStoreRequest)

Request message for ExampleStoreService.GetExampleStore.

[GetExecutionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetExecutionRequest)

Request message for MetadataService.GetExecution.

[GetExtensionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetExtensionRequest)

Request message for ExtensionRegistryService.GetExtension.

[GetFeatureGroupRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureGroupRequest)

Request message for FeatureRegistryService.GetFeatureGroup.

[GetFeatureMonitorJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorJobRequest)

Request message for FeatureRegistryService.GetFeatureMonitorJob.

[GetFeatureMonitorRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorRequest)

Request message for FeatureRegistryService.GetFeatureMonitor.

[GetFeatureOnlineStoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureOnlineStoreRequest)

Request message for FeatureOnlineStoreAdminService.GetFeatureOnlineStore.

[GetFeatureRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureRequest)

Request message for FeaturestoreService.GetFeature. Request message for FeatureRegistryService.GetFeature.

[GetFeatureViewRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureViewRequest)

Request message for FeatureOnlineStoreAdminService.GetFeatureView.

[GetFeatureViewSyncRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureViewSyncRequest)

Request message for FeatureOnlineStoreAdminService.GetFeatureViewSync.

[GetFeaturestoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeaturestoreRequest)

Request message for FeaturestoreService.GetFeaturestore.

[GetHyperparameterTuningJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetHyperparameterTuningJobRequest)

Request message for JobService.GetHyperparameterTuningJob.

[GetIndexEndpointRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetIndexEndpointRequest)

Request message for IndexEndpointService.GetIndexEndpoint

[GetIndexRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetIndexRequest)

Request message for IndexService.GetIndex

[GetMemoryRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetMemoryRequest)

Request message for MemoryBankService.GetMemory.

[GetMetadataSchemaRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetMetadataSchemaRequest)

Request message for MetadataService.GetMetadataSchema.

[GetMetadataStoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetMetadataStoreRequest)

Request message for MetadataService.GetMetadataStore.

[GetModelDeploymentMonitoringJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelDeploymentMonitoringJobRequest)

Request message for JobService.GetModelDeploymentMonitoringJob.

[GetModelEvaluationRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelEvaluationRequest)

Request message for ModelService.GetModelEvaluation.

[GetModelEvaluationSliceRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelEvaluationSliceRequest)

Request message for ModelService.GetModelEvaluationSlice.

[GetModelMonitorRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelMonitorRequest)

Request message for ModelMonitoringService.GetModelMonitor.

[GetModelMonitoringJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelMonitoringJobRequest)

Request message for ModelMonitoringService.GetModelMonitoringJob.

[GetModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelRequest)

Request message for ModelService.GetModel.

[GetNasJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNasJobRequest)

Request message for JobService.GetNasJob.

[GetNasTrialDetailRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNasTrialDetailRequest)

Request message for JobService.GetNasTrialDetail.

[GetNotebookExecutionJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookExecutionJobRequest)

Request message for [NotebookService.GetNotebookExecutionJob]

[GetNotebookRuntimeRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeRequest)

Request message for NotebookService.GetNotebookRuntime

[GetNotebookRuntimeTemplateRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeTemplateRequest)

Request message for NotebookService.GetNotebookRuntimeTemplate

[GetPersistentResourceRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPersistentResourceRequest)

Request message for PersistentResourceService.GetPersistentResource.

[GetPipelineJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPipelineJobRequest)

Request message for PipelineService.GetPipelineJob.

[GetPublisherModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPublisherModelRequest)

Request message for ModelGardenService.GetPublisherModel

[GetRagCorpusRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagCorpusRequest)

Request message for VertexRagDataService.GetRagCorpus

[GetRagEngineConfigRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagEngineConfigRequest)

Request message for VertexRagDataService.GetRagEngineConfig

[GetRagFileRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagFileRequest)

Request message for VertexRagDataService.GetRagFile

[GetReasoningEngineRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetReasoningEngineRequest)

Request message for ReasoningEngineService.GetReasoningEngine.

[GetScheduleRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetScheduleRequest)

Request message for ScheduleService.GetSchedule.

[GetSessionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetSessionRequest)

Request message for SessionService.GetSession.

[GetSpecialistPoolRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetSpecialistPoolRequest)

Request message for SpecialistPoolService.GetSpecialistPool.

[GetStudyRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetStudyRequest)

Request message for VizierService.GetStudy.

[GetTensorboardExperimentRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardExperimentRequest)

Request message for TensorboardService.GetTensorboardExperiment.

[GetTensorboardRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardRequest)

Request message for TensorboardService.GetTensorboard.

[GetTensorboardRunRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardRunRequest)

Request message for TensorboardService.GetTensorboardRun.

[GetTensorboardTimeSeriesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardTimeSeriesRequest)

Request message for TensorboardService.GetTensorboardTimeSeries.

[GetTrainingPipelineRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTrainingPipelineRequest)

Request message for PipelineService.GetTrainingPipeline.

[GetTrialRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTrialRequest)

Request message for VizierService.GetTrial.

[GetTuningJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTuningJobRequest)

Request message for GenAiTuningService.GetTuningJob.

[GoogleDriveSource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GoogleDriveSource)

The Google Drive location for the input content.

[GoogleMaps](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GoogleMaps)

Tool to retrieve public maps data for grounding, powered by Google.

[GoogleSearchRetrieval](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GoogleSearchRetrieval)

Tool to retrieve public web data for grounding, powered by Google.

[GroundednessInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundednessInput)

Input for groundedness metric.

[GroundednessInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundednessInstance)

Spec for groundedness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[GroundednessResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundednessResult)

Spec for groundedness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[GroundednessSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundednessSpec)

Spec for groundedness metric.

[GroundingChunk](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingChunk)

Grounding chunk.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[GroundingMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingMetadata)

Metadata returned to client when grounding is enabled.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[GroundingSupport](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingSupport)

Grounding support.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[HarmCategory](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.HarmCategory)

Harm categories that will block the content.

[HttpElementLocation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.HttpElementLocation)

Enum of location an HTTP element can be.

[HyperparameterTuningJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.HyperparameterTuningJob)

Represents a HyperparameterTuningJob. A HyperparameterTuningJob has a Study specification and multiple CustomJobs with identical CustomJob specification.

[IdMatcher](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IdMatcher)

Matcher for Features of an EntityType by Feature ID.

[ImageConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImageConfig)

Config for image generation features.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ImportDataConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataConfig)

Describes the location from where we import data into a Dataset, together with the labels that will be applied to the DataItems and the Annotations.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ImportDataOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataOperationMetadata)

Runtime operation information for DatasetService.ImportData.

[ImportDataRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataRequest)

Request message for DatasetService.ImportData.

[ImportDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataResponse)

Response message for DatasetService.ImportData.

[ImportExtensionOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportExtensionOperationMetadata)

Details of ExtensionRegistryService.ImportExtension operation.

[ImportExtensionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportExtensionRequest)

Request message for ExtensionRegistryService.ImportExtension.

[ImportFeatureValuesOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesOperationMetadata)

Details of operations that perform import Feature values.

[ImportFeatureValuesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesRequest)

Request message for FeaturestoreService.ImportFeatureValues.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ImportFeatureValuesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesResponse)

Response message for FeaturestoreService.ImportFeatureValues.

[ImportIndexOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexOperationMetadata)

Runtime operation information for IndexService.ImportIndex.

[ImportIndexRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest)

Request message for IndexService.ImportIndex.

[ImportModelEvaluationRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportModelEvaluationRequest)

Request message for ModelService.ImportModelEvaluation

[ImportRagFilesConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesConfig)

Config for importing RagFiles.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ImportRagFilesOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesOperationMetadata)

Runtime operation information for VertexRagDataService.ImportRagFiles.

[ImportRagFilesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesRequest)

Request message for VertexRagDataService.ImportRagFiles.

[ImportRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesResponse)

Response message for VertexRagDataService.ImportRagFiles.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[Index](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Index)

A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search.

[IndexDatapoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexDatapoint)

A datapoint of Index.

[IndexEndpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexEndpoint)

Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes.

[IndexPrivateEndpoints](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexPrivateEndpoints)

IndexPrivateEndpoints proto is used to provide paths for users to send requests via private endpoints (e.g. private service access, private service connect). To send request via private service access, use match_grpc_address. To send request via private service connect, use service_attachment.

[IndexStats](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexStats)

Stats of the Index.

[InputDataConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.InputDataConfig)

Specifies Vertex AI owned input data to be used for training, and possibly evaluating, the Model.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[Int64Array](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Int64Array)

A list of int64 values.

[IntegratedGradientsAttribution](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IntegratedGradientsAttribution)

An attribution method that computes the Aumann-Shapley value
taking advantage of the model's fully differentiable structure.
Refer to this paper for more details:
[https://arxiv.org/abs/1703.01365](https://arxiv.org/abs/1703.01365)

[JiraSource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.JiraSource)

The Jira source for the ImportRagFilesRequest.

[JobState](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.JobState)

Describes the state of a job.

[LargeModelReference](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LargeModelReference)

Contains information about the Large Model.

[LineageSubgraph](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LineageSubgraph)

A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes.

[ListAnnotationsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsRequest)

Request message for DatasetService.ListAnnotations.

[ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsResponse)

Response message for DatasetService.ListAnnotations.

[ListArtifactsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListArtifactsRequest)

Request message for MetadataService.ListArtifacts.

[ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListArtifactsResponse)

Response message for MetadataService.ListArtifacts.

[ListBatchPredictionJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsRequest)

Request message for JobService.ListBatchPredictionJobs.

[ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse)

Response message for JobService.ListBatchPredictionJobs

[ListCachedContentsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsRequest)

Request to list CachedContents.

[ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse)

Response with a list of CachedContents.

[ListContextsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListContextsRequest)

Request message for MetadataService.ListContexts

[ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListContextsResponse)

Response message for MetadataService.ListContexts.

[ListCustomJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsRequest)

Request message for JobService.ListCustomJobs.

[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse)

Response message for JobService.ListCustomJobs

[ListDataItemsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsRequest)

Request message for DatasetService.ListDataItems.

[ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsResponse)

Response message for DatasetService.ListDataItems.

[ListDataLabelingJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsRequest)

Request message for JobService.ListDataLabelingJobs.

[ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse)

Response message for JobService.ListDataLabelingJobs.

[ListDatasetVersionsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsRequest)

Request message for DatasetService.ListDatasetVersions.

[ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsResponse)

Response message for DatasetService.ListDatasetVersions.

[ListDatasetsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsRequest)

Request message for DatasetService.ListDatasets.

[ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsResponse)

Response message for DatasetService.ListDatasets.

[ListDeploymentResourcePoolsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsRequest)

Request message for ListDeploymentResourcePools method.

[ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsResponse)

Response message for ListDeploymentResourcePools method.

[ListEndpointsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsRequest)

Request message for EndpointService.ListEndpoints.

[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse)

Response message for EndpointService.ListEndpoints.

[ListEntityTypesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesRequest)

Request message for FeaturestoreService.ListEntityTypes.

[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse)

Response message for FeaturestoreService.ListEntityTypes.

[ListEventsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsRequest)

Request message for SessionService.ListEvents.

[ListEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse)

Response message for SessionService.ListEvents.

[ListExampleStoresRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresRequest)

Request message for ExampleStoreService.ListExampleStores.

[ListExampleStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresResponse)

Response message for ExampleStoreService.ListExampleStores.

[ListExecutionsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsRequest)

Request message for MetadataService.ListExecutions.

[ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsResponse)

Response message for MetadataService.ListExecutions.

[ListExtensionsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsRequest)

Request message for ExtensionRegistryService.ListExtensions.

[ListExtensionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsResponse)

Response message for ExtensionRegistryService.ListExtensions

[ListFeatureGroupsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsRequest)

Request message for FeatureRegistryService.ListFeatureGroups.

[ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse)

Response message for FeatureRegistryService.ListFeatureGroups.

[ListFeatureMonitorJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsRequest)

Request message for FeatureRegistryService.ListFeatureMonitorJobs.

[ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse)

Response message for FeatureRegistryService.ListFeatureMonitorJobs.

[ListFeatureMonitorsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsRequest)

Request message for FeatureRegistryService.ListFeatureMonitors.

[ListFeatureMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse)

Response message for FeatureRegistryService.ListFeatureMonitors.

[ListFeatureOnlineStoresRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresRequest)

Request message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse)

Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

[ListFeatureViewSyncsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsRequest)

Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse)

Response message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

[ListFeatureViewsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsRequest)

Request message for FeatureOnlineStoreAdminService.ListFeatureViews.

[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse)

Response message for FeatureOnlineStoreAdminService.ListFeatureViews.

[ListFeaturesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesRequest)

Request message for FeaturestoreService.ListFeatures. Request message for FeatureRegistryService.ListFeatures.

[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse)

Response message for FeaturestoreService.ListFeatures. Response message for FeatureRegistryService.ListFeatures.

[ListFeaturestoresRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresRequest)

Request message for FeaturestoreService.ListFeaturestores.

[ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse)

Response message for FeaturestoreService.ListFeaturestores.

[ListHyperparameterTuningJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsRequest)

Request message for JobService.ListHyperparameterTuningJobs.

[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse)

Response message for JobService.ListHyperparameterTuningJobs

[ListIndexEndpointsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsRequest)

Request message for IndexEndpointService.ListIndexEndpoints.

[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse)

Response message for IndexEndpointService.ListIndexEndpoints.

[ListIndexesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesRequest)

Request message for IndexService.ListIndexes.

[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse)

Response message for IndexService.ListIndexes.

[ListMemoriesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesRequest)

Request message for MemoryBankService.ListMemories.

[ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse)

Response message for MemoryBankService.ListMemories.

[ListMetadataSchemasRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasRequest)

Request message for MetadataService.ListMetadataSchemas.

[ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasResponse)

Response message for MetadataService.ListMetadataSchemas.

[ListMetadataStoresRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresRequest)

Request message for MetadataService.ListMetadataStores.

[ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresResponse)

Response message for MetadataService.ListMetadataStores.

[ListModelDeploymentMonitoringJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsRequest)

Request message for JobService.ListModelDeploymentMonitoringJobs.

[ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse)

Response message for JobService.ListModelDeploymentMonitoringJobs.

[ListModelEvaluationSlicesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationSlicesRequest)

Request message for ModelService.ListModelEvaluationSlices.

[ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationSlicesResponse)

Response message for ModelService.ListModelEvaluationSlices.

[ListModelEvaluationsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsRequest)

Request message for ModelService.ListModelEvaluations.

[ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsResponse)

Response message for ModelService.ListModelEvaluations.

[ListModelMonitoringJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsRequest)

Request message for ModelMonitoringService.ListModelMonitoringJobs.

[ListModelMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse)

Response message for ModelMonitoringService.ListModelMonitoringJobs.

[ListModelMonitorsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsRequest)

Request message for ModelMonitoringService.ListModelMonitors.

[ListModelMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsResponse)

Response message for ModelMonitoringService.ListModelMonitors

[ListModelVersionCheckpointsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsRequest)

Request message for ModelService.ListModelVersionCheckpoints.

[ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsResponse)

Response message for ModelService.ListModelVersionCheckpoints

[ListModelVersionsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsRequest)

Request message for ModelService.ListModelVersions.

[ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsResponse)

Response message for ModelService.ListModelVersions

[ListModelsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsRequest)

Request message for ModelService.ListModels.

[ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsResponse)

Response message for ModelService.ListModels

[ListNasJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsRequest)

Request message for JobService.ListNasJobs.

[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse)

Response message for JobService.ListNasJobs

[ListNasTrialDetailsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsRequest)

Request message for JobService.ListNasTrialDetails.

[ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsResponse)

Response message for JobService.ListNasTrialDetails

[ListNotebookExecutionJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsRequest)

Request message for [NotebookService.ListNotebookExecutionJobs]

[ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse)

Response message for [NotebookService.CreateNotebookExecutionJob]

[ListNotebookRuntimeTemplatesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesRequest)

Request message for NotebookService.ListNotebookRuntimeTemplates.

[ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse)

Response message for NotebookService.ListNotebookRuntimeTemplates.

[ListNotebookRuntimesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesRequest)

Request message for NotebookService.ListNotebookRuntimes.

[ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse)

Response message for NotebookService.ListNotebookRuntimes.

[ListOptimalTrialsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListOptimalTrialsRequest)

Request message for VizierService.ListOptimalTrials.

[ListOptimalTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListOptimalTrialsResponse)

Response message for VizierService.ListOptimalTrials.

[ListPersistentResourcesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesRequest)

Request message for [PersistentResourceService.ListPersistentResource][].

[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse)

Response message for PersistentResourceService.ListPersistentResources

[ListPipelineJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsRequest)

Request message for PipelineService.ListPipelineJobs.

[ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsResponse)

Response message for PipelineService.ListPipelineJobs

[ListPublisherModelsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsRequest)

Request message for ModelGardenService.ListPublisherModels.

[ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse)

Response message for ModelGardenService.ListPublisherModels.

[ListRagCorporaRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaRequest)

Request message for VertexRagDataService.ListRagCorpora.

[ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaResponse)

Response message for VertexRagDataService.ListRagCorpora.

[ListRagFilesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesRequest)

Request message for VertexRagDataService.ListRagFiles.

[ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse)

Response message for VertexRagDataService.ListRagFiles.

[ListReasoningEnginesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesRequest)

Request message for ReasoningEngineService.ListReasoningEngines.

[ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesResponse)

Response message for ReasoningEngineService.ListReasoningEngines

[ListSavedQueriesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesRequest)

Request message for DatasetService.ListSavedQueries.

[ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesResponse)

Response message for DatasetService.ListSavedQueries.

[ListSchedulesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesRequest)

Request message for ScheduleService.ListSchedules.

[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse)

Response message for ScheduleService.ListSchedules

[ListSessionsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsRequest)

Request message for SessionService.ListSessions.

[ListSessionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse)

Response message for SessionService.ListSessions.

[ListSpecialistPoolsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsRequest)

Request message for SpecialistPoolService.ListSpecialistPools.

[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse)

Response message for SpecialistPoolService.ListSpecialistPools.

[ListStudiesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesRequest)

Request message for VizierService.ListStudies.

[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesResponse)

Response message for VizierService.ListStudies.

[ListTensorboardExperimentsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsRequest)

Request message for TensorboardService.ListTensorboardExperiments.

[ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsResponse)

Response message for TensorboardService.ListTensorboardExperiments.

[ListTensorboardRunsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsRequest)

Request message for TensorboardService.ListTensorboardRuns.

[ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsResponse)

Response message for TensorboardService.ListTensorboardRuns.

[ListTensorboardTimeSeriesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesRequest)

Request message for TensorboardService.ListTensorboardTimeSeries.

[ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse)

Response message for TensorboardService.ListTensorboardTimeSeries.

[ListTensorboardsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsRequest)

Request message for TensorboardService.ListTensorboards.

[ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsResponse)

Response message for TensorboardService.ListTensorboards.

[ListTrainingPipelinesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesRequest)

Request message for PipelineService.ListTrainingPipelines.

[ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse)

Response message for PipelineService.ListTrainingPipelines

[ListTrialsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsRequest)

Request message for VizierService.ListTrials.

[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsResponse)

Response message for VizierService.ListTrials.

[ListTuningJobsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsRequest)

Request message for GenAiTuningService.ListTuningJobs.

[ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsResponse)

Response message for GenAiTuningService.ListTuningJobs

[LogprobsResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LogprobsResult)

Logprobs Result

[LookupStudyRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LookupStudyRequest)

Request message for VizierService.LookupStudy.

[LustreMount](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LustreMount)

Represents a mount configuration for Lustre file system.

[MachineSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MachineSpec)

Specification of a single machine.

[ManualBatchTuningParameters](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ManualBatchTuningParameters)

Manual batch tuning parameters.

[Measurement](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Measurement)

A message representing a Measurement of a Trial. A Measurement contains the Metrics got by executing a Trial using suggested hyperparameter values.

[Memory](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Memory)

A memory.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[MergeVersionAliasesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MergeVersionAliasesRequest)

Request message for ModelService.MergeVersionAliases.

[MetadataSchema](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetadataSchema)

Instance of a general MetadataSchema.

[MetadataStore](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetadataStore)

Instance of a metadata store. Contains a set of metadata that can be queried.

[Metric](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Metric)

The metric used for dataset level evaluation.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[MetricxInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxInput)

Input for MetricX metric.

[MetricxInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxInstance)

Spec for MetricX instance - The fields used for evaluation are dependent on the MetricX version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[MetricxResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxResult)

Spec for MetricX result - calculates the MetricX score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[MetricxSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxSpec)

Spec for MetricX metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[MigratableResource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigratableResource)

Represents one resource that exists in automl.googleapis.com, datalabeling.googleapis.com or ml.googleapis.com.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[MigrateResourceRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest)

Config of migrating one resource from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[MigrateResourceResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceResponse)

Describes a successfully migrated resource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[Modality](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Modality)

Content Part modality

[ModalityTokenCount](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModalityTokenCount)

Represents token counting info for a single modality.

[Model](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model)

A trained machine learning Model.

[ModelArmorConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelArmorConfig)

Configuration for Model Armor integrations of prompt and responses.

[ModelContainerSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelContainerSpec)

Specification of a container for serving predictions. Some fields in
this message correspond to fields in the ```
Kubernetes Container v1
core
specification <https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core>
```

__.

[ModelDeploymentMonitoringBigQueryTable](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringBigQueryTable)

ModelDeploymentMonitoringBigQueryTable specifies the BigQuery table name as well as some information of the logs stored in this table.

[ModelDeploymentMonitoringJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringJob)

Represents a job that runs periodically to monitor the deployed models in an endpoint. It will analyze the logged training & prediction data to detect any abnormal behaviors.

[ModelDeploymentMonitoringObjectiveConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringObjectiveConfig)

ModelDeploymentMonitoringObjectiveConfig contains the pair of deployed_model_id to ModelMonitoringObjectiveConfig.

[ModelDeploymentMonitoringObjectiveType](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringObjectiveType)

The Model Monitoring Objective types.

[ModelDeploymentMonitoringScheduleConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringScheduleConfig)

The config for scheduling monitoring job.

[ModelEvaluation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluation)

A collection of metrics calculated by comparing Model's predictions on all of the test data against annotations from the test data.

[ModelEvaluationSlice](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluationSlice)

A collection of metrics calculated by comparing Model's predictions on a slice of the test data against ground truth annotations.

[ModelExplanation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelExplanation)

Aggregated explanation metrics for a Model over a set of instances.

[ModelGardenSource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelGardenSource)

Contains information about the source of the models generated from Model Garden.

[ModelMonitor](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitor)

Vertex AI Model Monitoring Service serves as a central hub for the analysis and visualization of data quality and performance related to models. ModelMonitor stands as a top level resource for overseeing your model monitoring tasks.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ModelMonitoringAlert](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAlert)

Represents a single monitoring alert. This is currently used in the SearchModelMonitoringAlerts api, thus the alert wrapped in this message belongs to the resource asked in the request.

[ModelMonitoringAlertCondition](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAlertCondition)

Monitoring alert triggered condition.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ModelMonitoringAlertConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAlertConfig)

The alert config for model monitoring.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ModelMonitoringAnomaly](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAnomaly)

Represents a single model monitoring anomaly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ModelMonitoringConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringConfig)

The model monitoring configuration used for Batch Prediction Job.

[ModelMonitoringInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput)

Model monitoring data input spec.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ModelMonitoringJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringJob)

Represents a model monitoring job that analyze dataset using different monitoring algorithm.

[ModelMonitoringJobExecutionDetail](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringJobExecutionDetail)

Represent the execution details of the job.

[ModelMonitoringNotificationSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringNotificationSpec)

Notification spec(email, notification channel) for model monitoring statistics/alerts.

[ModelMonitoringObjectiveConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig)

The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.

[ModelMonitoringObjectiveSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveSpec)

Monitoring objectives spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ModelMonitoringOutputSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringOutputSpec)

Specification for the export destination of monitoring results, including metrics, logs, etc.

[ModelMonitoringSchema](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringSchema)

The Model Monitoring Schema definition.

[ModelMonitoringSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringSpec)

Monitoring monitoring job spec. It outlines the specifications for monitoring objectives, notifications, and result exports.

[ModelMonitoringStats](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringStats)

Represents the collection of statistics for a metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ModelMonitoringStatsAnomalies](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringStatsAnomalies)

Statistics and anomalies generated by Model Monitoring.

[ModelMonitoringStatsDataPoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringStatsDataPoint)

Represents a single statistics data point.

[ModelMonitoringTabularStats](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringTabularStats)

A collection of data points that describes the time-varying values of a tabular metric.

[ModelSourceInfo](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelSourceInfo)

Detail description of the source information of the model.

[ModelVersionCheckpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelVersionCheckpoint)

A proto representation of a Spanner-stored ModelVersionCheckpoint. The meaning of the fields is equivalent to their in-Spanner counterparts.

[MultiSpeakerVoiceConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MultiSpeakerVoiceConfig)

Configuration for a multi-speaker text-to-speech request.

[MutateDeployedIndexOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedIndexOperationMetadata)

Runtime operation information for IndexEndpointService.MutateDeployedIndex.

[MutateDeployedIndexRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedIndexRequest)

Request message for IndexEndpointService.MutateDeployedIndex.

[MutateDeployedIndexResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedIndexResponse)

Response message for IndexEndpointService.MutateDeployedIndex.

[MutateDeployedModelOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedModelOperationMetadata)

Runtime operation information for EndpointService.MutateDeployedModel.

[MutateDeployedModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedModelRequest)

Request message for EndpointService.MutateDeployedModel.

[MutateDeployedModelResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedModelResponse)

Response message for EndpointService.MutateDeployedModel.

[NasJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJob)

Represents a Neural Architecture Search (NAS) job.

[NasJobOutput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobOutput)

Represents a uCAIP NasJob output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[NasJobSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobSpec)

Represents the spec of a NasJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[NasTrial](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasTrial)

Represents a uCAIP NasJob trial.

[NasTrialDetail](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasTrialDetail)

Represents a NasTrial details along with its parameters. If there is a corresponding train NasTrial, the train NasTrial is also returned.

[NearestNeighborQuery](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborQuery)

A query to find a number of similar entities.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[NearestNeighborSearchOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborSearchOperationMetadata)

Runtime operation metadata with regard to Matching Engine Index.

[NearestNeighbors](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighbors)

Nearest neighbors for one query.

[Neighbor](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Neighbor)

Neighbors for example-based explanations.

[NetworkSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NetworkSpec)

Network spec.

[NfsMount](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NfsMount)

Represents a mount configuration for Network File System (NFS) to mount.

[NotebookEucConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookEucConfig)

The euc configuration of NotebookRuntimeTemplate.

[NotebookExecutionJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob)

NotebookExecutionJob represents an instance of a notebook execution.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[NotebookExecutionJobView](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJobView)

Views for Get/List NotebookExecutionJob

[NotebookIdleShutdownConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookIdleShutdownConfig)

The idle shutdown configuration of NotebookRuntimeTemplate, which contains the idle_timeout as required field.

[NotebookRuntime](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntime)

A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade.

[NotebookRuntimeTemplate](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplate)

A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template.

[NotebookRuntimeTemplateRef](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplateRef)

Points to a NotebookRuntimeTemplateRef.

[NotebookRuntimeType](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeType)

Represents a notebook runtime type.

[NotebookSoftwareConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookSoftwareConfig)

Notebook Software Config. This is passed to the backend when user makes software configurations in UI.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[OutputConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.OutputConfig)

Config for evaluation output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[OutputInfo](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.OutputInfo)

Describes the info for output of EvaluationService.EvaluateDataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PSCAutomationConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PSCAutomationConfig)

PSC config that is used to automatically create PSC endpoints in the user projects.

[PSCAutomationState](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PSCAutomationState)

The state of the PSC service automation.

[PairwiseChoice](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseChoice)

Pairwise prediction autorater preference.

[PairwiseMetricInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseMetricInput)

Input for pairwise metric.

[PairwiseMetricInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseMetricInstance)

Pairwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PairwiseMetricResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseMetricResult)

Spec for pairwise metric result.

[PairwiseMetricSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseMetricSpec)

Spec for pairwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PairwiseQuestionAnsweringQualityInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualityInput)

Input for pairwise question answering quality metric.

[PairwiseQuestionAnsweringQualityInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualityInstance)

Spec for pairwise question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PairwiseQuestionAnsweringQualityResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualityResult)

Spec for pairwise question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PairwiseQuestionAnsweringQualitySpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualitySpec)

Spec for pairwise question answering quality score metric.

[PairwiseSummarizationQualityInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseSummarizationQualityInput)

Input for pairwise summarization quality metric.

[PairwiseSummarizationQualityInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseSummarizationQualityInstance)

Spec for pairwise summarization quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PairwiseSummarizationQualityResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseSummarizationQualityResult)

Spec for pairwise summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PairwiseSummarizationQualitySpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseSummarizationQualitySpec)

Spec for pairwise summarization quality score metric.

[Part](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Part)

A datatype containing media that is part of a multi-part `Content`

message.

A `Part`

consists of data which has an associated datatype. A
`Part`

can only contain one of the accepted types in
`Part.data`

.

A `Part`

must have a fixed IANA MIME type identifying the type and
subtype of the media if `inline_data`

or `file_data`

field is
filled with raw bytes.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PartnerModelTuningSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PartnerModelTuningSpec)

Tuning spec for Partner models.

[PauseModelDeploymentMonitoringJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PauseModelDeploymentMonitoringJobRequest)

Request message for JobService.PauseModelDeploymentMonitoringJob.

[PauseScheduleRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PauseScheduleRequest)

Request message for ScheduleService.PauseSchedule.

[PersistentDiskSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PersistentDiskSpec)

Represents the spec of [persistent
disk][[https://cloud.google.com/compute/docs/disks/persistent-disks](https://cloud.google.com/compute/docs/disks/persistent-disks)]
options.

[PersistentResource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PersistentResource)

Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec.

[PipelineFailurePolicy](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineFailurePolicy)

Represents the failure policy of a pipeline. Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE_FAILURE_POLICY_FAIL_SLOW. However, if a pipeline is set to PIPELINE_FAILURE_POLICY_FAIL_FAST, it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion.

[PipelineJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob)

An instance of a machine learning PipelineJob.

[PipelineJobDetail](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJobDetail)

The runtime detail of PipelineJob.

[PipelineState](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineState)

Describes the state of a pipeline.

[PipelineTaskDetail](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskDetail)

The runtime detail of a task execution.

[PipelineTaskExecutorDetail](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskExecutorDetail)

The runtime detail of a pipeline executor.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PipelineTaskRerunConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskRerunConfig)

User provided rerun config to submit a rerun pipelinejob. This includes

- Which task to rerun
- User override input parameters and artifacts.

[PipelineTemplateMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTemplateMetadata)

Pipeline template metadata if PipelineJob.template_uri is from supported template registry. Currently, the only supported registry is Artifact Registry.

[PointwiseMetricInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricInput)

Input for pointwise metric.

[PointwiseMetricInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricInstance)

Pointwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PointwiseMetricResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricResult)

Spec for pointwise metric result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PointwiseMetricSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricSpec)

Spec for pointwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[Port](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Port)

Represents a network port in a container.

[PostStartupScriptConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PostStartupScriptConfig)

Post-startup script config.

[PreTunedModel](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PreTunedModel)

A pre-tuned model for continuous tuning.

[PrebuiltVoiceConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PrebuiltVoiceConfig)

The configuration for the prebuilt speaker to use.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PredefinedSplit](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredefinedSplit)

Assigns input data to training, validation, and test sets based on the value of a provided key.

Supported only for tabular Datasets.

[PredictLongRunningMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictLongRunningMetadata)

Metadata for PredictLongRunning long running operations.

[PredictLongRunningResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictLongRunningResponse)

Response message for [PredictionService.PredictLongRunning]

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PredictRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictRequest)

Request message for PredictionService.Predict.

[PredictRequestResponseLoggingConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictRequestResponseLoggingConfig)

Configuration for logging request-response to a BigQuery table.

[PredictResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictResponse)

Response message for PredictionService.Predict.

[PredictSchemata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictSchemata)

Contains the schemata used in Model's predictions and explanations via PredictionService.Predict, PredictionService.Explain and BatchPredictionJob.

[Presets](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Presets)

Preset configuration for example-based explanations

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PrivateEndpoints](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PrivateEndpoints)

PrivateEndpoints proto is used to provide paths for users to send requests privately. To send request via private service access, use predict_http_uri, explain_http_uri or health_http_uri. To send request via private service connect, use service_attachment.

[PrivateServiceConnectConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PrivateServiceConnectConfig)

Represents configuration for private service connect.

[Probe](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Probe)

Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[PscAutomatedEndpoints](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PscAutomatedEndpoints)

PscAutomatedEndpoints defines the output of the forwarding rule automatically created by each PscAutomationConfig.

[PscInterfaceConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PscInterfaceConfig)

Configuration for PSC-I.

[PublisherModel](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel)

A Model Garden Publisher Model.

[PublisherModelConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModelConfig)

This message contains configs of a publisher model.

[PublisherModelEulaAcceptance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModelEulaAcceptance)

Response message for [ModelGardenService.UpdatePublisherModelEula][].

[PublisherModelView](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModelView)

View enumeration of PublisherModel.

[PurgeArtifactsMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeArtifactsMetadata)

Details of operations that perform MetadataService.PurgeArtifacts.

[PurgeArtifactsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeArtifactsRequest)

Request message for MetadataService.PurgeArtifacts.

[PurgeArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeArtifactsResponse)

Response message for MetadataService.PurgeArtifacts.

[PurgeContextsMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeContextsMetadata)

Details of operations that perform MetadataService.PurgeContexts.

[PurgeContextsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeContextsRequest)

Request message for MetadataService.PurgeContexts.

[PurgeContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeContextsResponse)

Response message for MetadataService.PurgeContexts.

[PurgeExecutionsMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeExecutionsMetadata)

Details of operations that perform MetadataService.PurgeExecutions.

[PurgeExecutionsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeExecutionsRequest)

Request message for MetadataService.PurgeExecutions.

[PurgeExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeExecutionsResponse)

Response message for MetadataService.PurgeExecutions.

[PythonPackageSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PythonPackageSpec)

The spec of a Python packaged code.

[QueryArtifactLineageSubgraphRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryArtifactLineageSubgraphRequest)

Request message for MetadataService.QueryArtifactLineageSubgraph.

[QueryContextLineageSubgraphRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryContextLineageSubgraphRequest)

Request message for MetadataService.QueryContextLineageSubgraph.

[QueryDeployedModelsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsRequest)

Request message for QueryDeployedModels method.

[QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse)

Response message for QueryDeployedModels method.

[QueryExecutionInputsAndOutputsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryExecutionInputsAndOutputsRequest)

Request message for MetadataService.QueryExecutionInputsAndOutputs.

[QueryExtensionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryExtensionRequest)

Request message for ExtensionExecutionService.QueryExtension.

[QueryExtensionResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryExtensionResponse)

Response message for ExtensionExecutionService.QueryExtension.

[QueryReasoningEngineRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryReasoningEngineRequest)

Request message for [ReasoningEngineExecutionService.Query][].

[QueryReasoningEngineResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryReasoningEngineResponse)

Response message for [ReasoningEngineExecutionService.Query][]

[QuestionAnsweringCorrectnessInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringCorrectnessInput)

Input for question answering correctness metric.

[QuestionAnsweringCorrectnessInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringCorrectnessInstance)

Spec for question answering correctness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[QuestionAnsweringCorrectnessResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringCorrectnessResult)

Spec for question answering correctness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[QuestionAnsweringCorrectnessSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringCorrectnessSpec)

Spec for question answering correctness metric.

[QuestionAnsweringHelpfulnessInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringHelpfulnessInput)

Input for question answering helpfulness metric.

[QuestionAnsweringHelpfulnessInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringHelpfulnessInstance)

Spec for question answering helpfulness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[QuestionAnsweringHelpfulnessResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringHelpfulnessResult)

Spec for question answering helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[QuestionAnsweringHelpfulnessSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringHelpfulnessSpec)

Spec for question answering helpfulness metric.

[QuestionAnsweringQualityInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringQualityInput)

Input for question answering quality metric.

[QuestionAnsweringQualityInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringQualityInstance)

Spec for question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[QuestionAnsweringQualityResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringQualityResult)

Spec for question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[QuestionAnsweringQualitySpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringQualitySpec)

Spec for question answering quality score metric.

[QuestionAnsweringRelevanceInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringRelevanceInput)

Input for question answering relevance metric.

[QuestionAnsweringRelevanceInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringRelevanceInstance)

Spec for question answering relevance instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[QuestionAnsweringRelevanceResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringRelevanceResult)

Spec for question answering relevance result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[QuestionAnsweringRelevanceSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringRelevanceSpec)

Spec for question answering relevance metric.

[RagChunk](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagChunk)

A RagChunk includes the content of a chunk of a RagFile, and associated metadata.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RagContexts](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagContexts)

Relevant contexts for one query.

[RagCorpus](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus)

A RagCorpus is a RagFile container and a project can have multiple RagCorpora.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RagEmbeddingModelConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagEmbeddingModelConfig)

Config for the embedding model to use for RAG.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RagEngineConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagEngineConfig)

Config for RagEngine.

[RagFile](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFile)

A RagFile contains user data for chunking, embedding and indexing.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RagFileChunkingConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileChunkingConfig)

Specifies the size and overlap of chunks for RagFiles.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RagFileMetadataConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileMetadataConfig)

Metadata config for RagFile.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RagFileParsingConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileParsingConfig)

Specifies the parsing config for RagFiles.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RagFileTransformationConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileTransformationConfig)

Specifies the transformation config for RagFiles.

[RagManagedDbConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagManagedDbConfig)

Configuration message for RagManagedDb used by RagEngine.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RagQuery](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagQuery)

A query to retrieve relevant contexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RagRetrievalConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagRetrievalConfig)

Specifies the context retrieval config.

[RagVectorDbConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig)

Config for the Vector DB to use for RAG.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RawOutput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RawOutput)

Raw output.

[RawPredictRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RawPredictRequest)

Request message for PredictionService.RawPredict.

[RayLogsSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RayLogsSpec)

Configuration for the Ray OSS Logs.

[RayMetricSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RayMetricSpec)

Configuration for the Ray metrics.

[RaySpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RaySpec)

Configuration information for the Ray cluster. For experimental launch, Ray cluster creation and Persistent cluster creation are 1:1 mapping: We will provision all the nodes within the Persistent cluster as Ray nodes.

[ReadFeatureValuesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadFeatureValuesRequest)

Request message for FeaturestoreOnlineServingService.ReadFeatureValues.

[ReadFeatureValuesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadFeatureValuesResponse)

Response message for FeaturestoreOnlineServingService.ReadFeatureValues.

[ReadIndexDatapointsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadIndexDatapointsRequest)

The request message for MatchService.ReadIndexDatapoints.

[ReadIndexDatapointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadIndexDatapointsResponse)

The response message for MatchService.ReadIndexDatapoints.

[ReadTensorboardBlobDataRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardBlobDataRequest)

Request message for TensorboardService.ReadTensorboardBlobData.

[ReadTensorboardBlobDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardBlobDataResponse)

Response message for TensorboardService.ReadTensorboardBlobData.

[ReadTensorboardSizeRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardSizeRequest)

Request message for TensorboardService.ReadTensorboardSize.

[ReadTensorboardSizeResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardSizeResponse)

Response message for TensorboardService.ReadTensorboardSize.

[ReadTensorboardTimeSeriesDataRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardTimeSeriesDataRequest)

Request message for TensorboardService.ReadTensorboardTimeSeriesData.

[ReadTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardTimeSeriesDataResponse)

Response message for TensorboardService.ReadTensorboardTimeSeriesData.

[ReadTensorboardUsageRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardUsageRequest)

Request message for TensorboardService.ReadTensorboardUsage.

[ReadTensorboardUsageResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardUsageResponse)

Response message for TensorboardService.ReadTensorboardUsage.

[ReasoningEngine](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngine)

ReasoningEngine provides a customizable runtime for models to determine which actions to take and in which order.

[ReasoningEngineContextSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineContextSpec)

Configuration for how Agent Engine sub-resources should manage context.

[ReasoningEngineSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec)

ReasoningEngine configurations

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RebaseTunedModelOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebaseTunedModelOperationMetadata)

Runtime operation information for GenAiTuningService.RebaseTunedModel.

[RebaseTunedModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebaseTunedModelRequest)

Request message for GenAiTuningService.RebaseTunedModel.

[RebootPersistentResourceOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebootPersistentResourceOperationMetadata)

Details of operations that perform reboot PersistentResource.

[RebootPersistentResourceRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebootPersistentResourceRequest)

Request message for PersistentResourceService.RebootPersistentResource.

[RecommendSpecRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecRequest)

Request message for ModelService.RecommendSpec.

[RecommendSpecResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecResponse)

Response message for ModelService.RecommendSpec.

[RemoveContextChildrenRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveContextChildrenRequest)

Request message for [MetadataService.DeleteContextChildrenRequest][].

[RemoveContextChildrenResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveContextChildrenResponse)

Response message for MetadataService.RemoveContextChildren.

[RemoveDatapointsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveDatapointsRequest)

Request message for IndexService.RemoveDatapoints

[RemoveDatapointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveDatapointsResponse)

Response message for IndexService.RemoveDatapoints

[RemoveExamplesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveExamplesRequest)

Request message for ExampleStoreService.RemoveExamples.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RemoveExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveExamplesResponse)

Response message for ExampleStoreService.RemoveExamples.

[ReplicatedVoiceConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReplicatedVoiceConfig)

The configuration for the replicated voice to use.

[ReservationAffinity](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReservationAffinity)

A ReservationAffinity can be used to configure a Vertex AI resource (e.g., a DeployedModel) to draw its Compute Engine resources from a Shared Reservation, or exclusively from on-demand capacity.

[ResourcePool](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResourcePool)

Represents the spec of a group of resources of the same type, for example machine type, disk, and accelerators, in a PersistentResource.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ResourceRuntime](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResourceRuntime)

Persistent Cluster runtime information as output

[ResourceRuntimeSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResourceRuntimeSpec)

Configuration for the runtime on a PersistentResource instance, including but not limited to:

- Service accounts used to run the workloads.
- Whether to make it a dedicated Ray Cluster.

[ResourcesConsumed](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResourcesConsumed)

Statistics information about resource consumption.

[RestoreDatasetVersionOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RestoreDatasetVersionOperationMetadata)

Runtime operation information for DatasetService.RestoreDatasetVersion.

[RestoreDatasetVersionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RestoreDatasetVersionRequest)

Request message for DatasetService.RestoreDatasetVersion.

[ResumeModelDeploymentMonitoringJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResumeModelDeploymentMonitoringJobRequest)

Request message for JobService.ResumeModelDeploymentMonitoringJob.

[ResumeScheduleRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResumeScheduleRequest)

Request message for ScheduleService.ResumeSchedule.

[Retrieval](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Retrieval)

Defines a retrieval tool that model can call to access external knowledge.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RetrievalConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrievalConfig)

Retrieval config.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RetrievalMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrievalMetadata)

Metadata related to retrieval in the grounding flow.

[RetrieveContextsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsRequest)

Request message for VertexRagService.RetrieveContexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RetrieveContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsResponse)

Response message for VertexRagService.RetrieveContexts.

[RetrieveMemoriesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest)

Request message for MemoryBankService.RetrieveMemories.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RetrieveMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesResponse)

Response message for MemoryBankService.RetrieveMemories.

[RolloutOptions](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RolloutOptions)

Configuration for rolling deployments.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RougeInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RougeInput)

Input for rouge metric.

[RougeInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RougeInstance)

Spec for rouge instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RougeMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RougeMetricValue)

Rouge metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RougeResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RougeResults)

Results for rouge metric.

[RougeSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RougeSpec)

Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.

[RubricBasedInstructionFollowingInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RubricBasedInstructionFollowingInput)

Instance and metric spec for RubricBasedInstructionFollowing metric.

[RubricBasedInstructionFollowingInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RubricBasedInstructionFollowingInstance)

Instance for RubricBasedInstructionFollowing metric - one instance corresponds to one row in an evaluation dataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RubricBasedInstructionFollowingResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RubricBasedInstructionFollowingResult)

Result for RubricBasedInstructionFollowing metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RubricBasedInstructionFollowingSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RubricBasedInstructionFollowingSpec)

Spec for RubricBasedInstructionFollowing metric - returns rubrics and verdicts corresponding to rubrics along with overall score.

[RubricCritiqueResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RubricCritiqueResult)

Rubric critique result.

[RuntimeArtifact](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeArtifact)

The definition of a runtime artifact.

[RuntimeConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeConfig)

Runtime configuration to run the extension.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SafetyInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetyInput)

Input for safety metric.

[SafetyInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetyInstance)

Spec for safety instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SafetyRating](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetyRating)

Safety rating corresponding to the generated content.

[SafetyResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetyResult)

Spec for safety result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SafetySetting](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetySetting)

Safety settings.

[SafetySpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetySpec)

Spec for safety metric.

[SampleConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SampleConfig)

Active learning data sampling config. For every active learning labeling iteration, it will select a batch of data based on the sampling strategy.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SampledShapleyAttribution](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SampledShapleyAttribution)

An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features.

[SamplingStrategy](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SamplingStrategy)

Sampling Strategy for logging, can be for both training and prediction dataset.

[SavedQuery](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SavedQuery)

A SavedQuery is a view of the dataset. It references a subset of annotations by problem type and filters.

[Scalar](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Scalar)

One point viewable on a scalar metric plot.

[Schedule](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schedule)

An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ScheduleConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ScheduleConfig)

Schedule configuration for the FeatureMonitor.

[Scheduling](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Scheduling)

All parameters related to queuing and scheduling of custom jobs.

[Schema](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schema)

Schema is used to define the format of input/output data. Represents
a select subset of an ```
OpenAPI 3.0 schema
object <https://spec.openapis.org/oas/v3.0.3#schema-object>
```

__. More
fields may be added in the future as needed.

[SearchDataItemsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsRequest)

Request message for DatasetService.SearchDataItems.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsResponse)

Response message for DatasetService.SearchDataItems.

[SearchEntryPoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchEntryPoint)

Google search entry point.

[SearchExamplesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchExamplesRequest)

Request message for ExampleStoreService.SearchExamples.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SearchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchExamplesResponse)

Response message for ExampleStoreService.SearchExamples.

[SearchFeaturesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesRequest)

Request message for FeaturestoreService.SearchFeatures.

[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse)

Response message for FeaturestoreService.SearchFeatures.

[SearchMigratableResourcesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesRequest)

Request message for MigrationService.SearchMigratableResources.

[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse)

Response message for MigrationService.SearchMigratableResources.

[SearchModelDeploymentMonitoringStatsAnomaliesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesRequest)

Request message for JobService.SearchModelDeploymentMonitoringStatsAnomalies.

[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)

Response message for JobService.SearchModelDeploymentMonitoringStatsAnomalies.

[SearchModelMonitoringAlertsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringAlertsRequest)

Request message for ModelMonitoringService.SearchModelMonitoringAlerts.

[SearchModelMonitoringAlertsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringAlertsResponse)

Response message for ModelMonitoringService.SearchModelMonitoringAlerts.

[SearchModelMonitoringStatsFilter](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsFilter)

Filter for searching ModelMonitoringStats.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SearchModelMonitoringStatsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsRequest)

Request message for ModelMonitoringService.SearchModelMonitoringStats.

[SearchModelMonitoringStatsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsResponse)

Response message for ModelMonitoringService.SearchModelMonitoringStats.

[SearchNearestEntitiesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchNearestEntitiesRequest)

The request message for FeatureOnlineStoreService.SearchNearestEntities.

[SearchNearestEntitiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchNearestEntitiesResponse)

Response message for FeatureOnlineStoreService.SearchNearestEntities

[SecretEnvVar](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SecretEnvVar)

Represents an environment variable where the value is a secret in Cloud Secret Manager.

[SecretRef](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SecretRef)

Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable.

[Segment](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Segment)

Segment of the content.

[ServiceAccountSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ServiceAccountSpec)

Configuration for the use of custom service account to run the workloads.

[Session](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Session)

A session contains a set of actions between users and Vertex agents.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SessionEvent](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SessionEvent)

An event represents a message from either the user or agent.

[SetPublisherModelConfigOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SetPublisherModelConfigOperationMetadata)

Runtime operation information for EndpointService.SetPublisherModelConfig.

[SetPublisherModelConfigRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SetPublisherModelConfigRequest)

Request message for EndpointService.SetPublisherModelConfig.

[SharePointSources](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SharePointSources)

The SharePointSources to pass to ImportRagFiles.

[ShieldedVmConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ShieldedVmConfig)

A set of Shielded Instance options. See ```
Images using supported
Shielded VM
features <https://cloud.google.com/compute/docs/instances/modifying-shielded-vm>
```

__.

[SlackSource](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SlackSource)

The Slack source for the ImportRagFilesRequest.

[SmoothGradConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SmoothGradConfig)

Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details:

[https://arxiv.org/pdf/1706.03825.pdf](https://arxiv.org/pdf/1706.03825.pdf)

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SpeakerVoiceConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpeakerVoiceConfig)

Configuration for a single speaker in a multi-speaker setup.

[SpecialistPool](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpecialistPool)

SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

[SpeculativeDecodingSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpeculativeDecodingSpec)

Configuration for Speculative Decoding.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SpeechConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpeechConfig)

Configuration for speech generation.

[StartNotebookRuntimeOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeOperationMetadata)

Metadata information for NotebookService.StartNotebookRuntime.

[StartNotebookRuntimeRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeRequest)

Request message for NotebookService.StartNotebookRuntime.

[StartNotebookRuntimeResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeResponse)

Response message for NotebookService.StartNotebookRuntime.

[StopNotebookRuntimeOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopNotebookRuntimeOperationMetadata)

Metadata information for NotebookService.StopNotebookRuntime.

[StopNotebookRuntimeRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopNotebookRuntimeRequest)

Request message for NotebookService.StopNotebookRuntime.

[StopNotebookRuntimeResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopNotebookRuntimeResponse)

Response message for NotebookService.StopNotebookRuntime.

[StopTrialRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopTrialRequest)

Request message for VizierService.StopTrial.

[StoredContentsExample](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExample)

A ContentsExample to be used with GenerateContent alongside information required for storage and retrieval with Example Store.

[StoredContentsExampleFilter](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExampleFilter)

The metadata filters that will be used to remove or fetch StoredContentsExamples. If a field is unspecified, then no filtering for that field will be applied.

[StoredContentsExampleParameters](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExampleParameters)

The metadata filters that will be used to search StoredContentsExamples. If a field is unspecified, then no filtering for that field will be applied

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[StratifiedSplit](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StratifiedSplit)

Assigns input data to the training, validation, and test sets so
that the distribution of values found in the categorical column (as
specified by the `key`

field) is mirrored within each split. The
fraction values determine the relative sizes of the splits.

For example, if the specified column has three values, with 50% of the rows having value "A", 25% value "B", and 25% value "C", and the split fractions are specified as 80/10/10, then the training set will constitute 80% of the training data, with about 50% of the training set rows having the value "A" for the specified column, about 25% having the value "B", and about 25% having the value "C".

Only the top 500 occurring values are used; any values not in the top 500 values are randomly assigned to a split. If less than three rows contain a specific value, those rows are randomly assigned.

Supported only for tabular Datasets.

[StreamDirectPredictRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamDirectPredictRequest)

Request message for PredictionService.StreamDirectPredict.

The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][].

[StreamDirectPredictResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamDirectPredictResponse)

Response message for PredictionService.StreamDirectPredict.

[StreamDirectRawPredictRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamDirectRawPredictRequest)

Request message for PredictionService.StreamDirectRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.

[StreamDirectRawPredictResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamDirectRawPredictResponse)

Response message for PredictionService.StreamDirectRawPredict.

[StreamQueryReasoningEngineRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamQueryReasoningEngineRequest)

Request message for [ReasoningEngineExecutionService.StreamQuery][].

[StreamRawPredictRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamRawPredictRequest)

Request message for PredictionService.StreamRawPredict.

[StreamingFetchFeatureValuesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingFetchFeatureValuesRequest)

Request message for FeatureOnlineStoreService.StreamingFetchFeatureValues. For the entities requested, all features under the requested feature view will be returned.

[StreamingFetchFeatureValuesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingFetchFeatureValuesResponse)

Response message for FeatureOnlineStoreService.StreamingFetchFeatureValues.

[StreamingPredictRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingPredictRequest)

Request message for PredictionService.StreamingPredict.

The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][].

[StreamingPredictResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingPredictResponse)

Response message for PredictionService.StreamingPredict.

[StreamingRawPredictRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingRawPredictRequest)

Request message for PredictionService.StreamingRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.

[StreamingRawPredictResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingRawPredictResponse)

Response message for PredictionService.StreamingRawPredict.

[StreamingReadFeatureValuesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingReadFeatureValuesRequest)

Request message for FeaturestoreOnlineServingService.StreamingReadFeatureValues.

[StringArray](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StringArray)

A list of string values.

[StructFieldValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StructFieldValue)

One field of a Struct (or object) type feature value.

[StructValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StructValue)

Struct (or object) type feature value.

[Study](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Study)

A message representing a Study.

[StudySpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec)

Represents specification of a Study.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[StudyTimeConstraint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudyTimeConstraint)

Time-based Constraint for Study

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SuggestTrialsMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SuggestTrialsMetadata)

Details of operations that perform Trials suggestion.

[SuggestTrialsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SuggestTrialsRequest)

Request message for VizierService.SuggestTrials.

[SuggestTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SuggestTrialsResponse)

Response message for VizierService.SuggestTrials.

[SummarizationHelpfulnessInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationHelpfulnessInput)

Input for summarization helpfulness metric.

[SummarizationHelpfulnessInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationHelpfulnessInstance)

Spec for summarization helpfulness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SummarizationHelpfulnessResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationHelpfulnessResult)

Spec for summarization helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SummarizationHelpfulnessSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationHelpfulnessSpec)

Spec for summarization helpfulness score metric.

[SummarizationQualityInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationQualityInput)

Input for summarization quality metric.

[SummarizationQualityInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationQualityInstance)

Spec for summarization quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SummarizationQualityResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationQualityResult)

Spec for summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SummarizationQualitySpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationQualitySpec)

Spec for summarization quality score metric.

[SummarizationVerbosityInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationVerbosityInput)

Input for summarization verbosity metric.

[SummarizationVerbosityInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationVerbosityInstance)

Spec for summarization verbosity instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SummarizationVerbosityResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationVerbosityResult)

Spec for summarization verbosity result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SummarizationVerbositySpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationVerbositySpec)

Spec for summarization verbosity score metric.

[SupervisedHyperParameters](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SupervisedHyperParameters)

Hyperparameters for SFT.

[SupervisedTuningDataStats](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SupervisedTuningDataStats)

Tuning data statistics for Supervised Tuning.

[SupervisedTuningDatasetDistribution](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SupervisedTuningDatasetDistribution)

Dataset distribution for Supervised Tuning.

[SupervisedTuningSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SupervisedTuningSpec)

Tuning Spec for Supervised Tuning for first party models.

[SyncFeatureViewRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SyncFeatureViewRequest)

Request message for FeatureOnlineStoreAdminService.SyncFeatureView.

[SyncFeatureViewResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SyncFeatureViewResponse)

Response message for FeatureOnlineStoreAdminService.SyncFeatureView.

[TFRecordDestination](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TFRecordDestination)

The storage details for TFRecord output content.

[Tensor](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tensor)

A tensor value type.

[Tensorboard](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tensorboard)

Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects.

[TensorboardBlob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardBlob)

One blob (e.g, image, graph) viewable on a blob metric plot.

[TensorboardBlobSequence](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardBlobSequence)

One point viewable on a blob metric plot, but mostly just a wrapper
message to work around repeated fields can't be used directly within
`oneof`

fields.

[TensorboardExperiment](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardExperiment)

A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard.

[TensorboardRun](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardRun)

TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc

[TensorboardTensor](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardTensor)

One point viewable on a tensor metric plot.

[TensorboardTimeSeries](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardTimeSeries)

TensorboardTimeSeries maps to times series produced in training runs

[ThresholdConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ThresholdConfig)

The config for feature monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TimeSeriesData](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TimeSeriesData)

All the data stored in a TensorboardTimeSeries.

[TimeSeriesDataPoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TimeSeriesDataPoint)

A TensorboardTimeSeries data point.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TimestampSplit](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TimestampSplit)

Assigns input data to training, validation, and test sets based on a provided timestamps. The youngest data pieces are assigned to training set, next to validation set, and the oldest to the test set.

Supported only for tabular Datasets.

[TokensInfo](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TokensInfo)

Tokens info with a list of tokens and the corresponding list of token ids.

[Tool](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tool)

Tool details that the model may use to generate response.

A `Tool`

is a piece of code that enables the system to interact
with external systems to perform an action, or set of actions,
outside of knowledge and scope of the model. A Tool object should
contain exactly one type of Tool (e.g FunctionDeclaration, Retrieval
or GoogleSearchRetrieval).

[ToolCall](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCall)

Spec for tool call.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ToolCallValidInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidInput)

Input for tool call valid metric.

[ToolCallValidInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidInstance)

Spec for tool call valid instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ToolCallValidMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidMetricValue)

Tool call valid metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ToolCallValidResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidResults)

Results for tool call valid metric.

[ToolCallValidSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidSpec)

Spec for tool call valid metric.

[ToolConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolConfig)

Tool config. This config is shared for all tools provided in the request.

[ToolNameMatchInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchInput)

Input for tool name match metric.

[ToolNameMatchInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchInstance)

Spec for tool name match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ToolNameMatchMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchMetricValue)

Tool name match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ToolNameMatchResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchResults)

Results for tool name match metric.

[ToolNameMatchSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchSpec)

Spec for tool name match metric.

[ToolParameterKVMatchInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchInput)

Input for tool parameter key value match metric.

[ToolParameterKVMatchInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchInstance)

Spec for tool parameter key value match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ToolParameterKVMatchMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchMetricValue)

Tool parameter key value match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ToolParameterKVMatchResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchResults)

Results for tool parameter key value match metric.

[ToolParameterKVMatchSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchSpec)

Spec for tool parameter key value match metric.

[ToolParameterKeyMatchInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKeyMatchInput)

Input for tool parameter key match metric.

[ToolParameterKeyMatchInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKeyMatchInstance)

Spec for tool parameter key match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ToolParameterKeyMatchMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKeyMatchMetricValue)

Tool parameter key match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ToolParameterKeyMatchResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKeyMatchResults)

Results for tool parameter key match metric.

[ToolParameterKeyMatchSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKeyMatchSpec)

Spec for tool parameter key match metric.

[ToolUseExample](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolUseExample)

A single example of the tool usage.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrainingConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrainingConfig)

CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems.

[TrainingPipeline](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrainingPipeline)

The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model.

[Trajectory](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Trajectory)

Spec for trajectory.

[TrajectoryAnyOrderMatchInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchInput)

Instances and metric spec for TrajectoryAnyOrderMatch metric.

[TrajectoryAnyOrderMatchInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchInstance)

Spec for TrajectoryAnyOrderMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectoryAnyOrderMatchMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchMetricValue)

TrajectoryAnyOrderMatch metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectoryAnyOrderMatchResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchResults)

Results for TrajectoryAnyOrderMatch metric.

[TrajectoryAnyOrderMatchSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchSpec)

Spec for TrajectoryAnyOrderMatch metric - returns 1 if all tool calls in the reference trajectory appear in the predicted trajectory in any order, else 0.

[TrajectoryExactMatchInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchInput)

Instances and metric spec for TrajectoryExactMatch metric.

[TrajectoryExactMatchInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchInstance)

Spec for TrajectoryExactMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectoryExactMatchMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchMetricValue)

TrajectoryExactMatch metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectoryExactMatchResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchResults)

Results for TrajectoryExactMatch metric.

[TrajectoryExactMatchSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchSpec)

Spec for TrajectoryExactMatch metric - returns 1 if tool calls in the reference trajectory exactly match the predicted trajectory, else 0.

[TrajectoryInOrderMatchInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryInOrderMatchInput)

Instances and metric spec for TrajectoryInOrderMatch metric.

[TrajectoryInOrderMatchInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryInOrderMatchInstance)

Spec for TrajectoryInOrderMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectoryInOrderMatchMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryInOrderMatchMetricValue)

TrajectoryInOrderMatch metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectoryInOrderMatchResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryInOrderMatchResults)

Results for TrajectoryInOrderMatch metric.

[TrajectoryInOrderMatchSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryInOrderMatchSpec)

Spec for TrajectoryInOrderMatch metric - returns 1 if tool calls in the reference trajectory appear in the predicted trajectory in the same order, else 0.

[TrajectoryPrecisionInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryPrecisionInput)

Instances and metric spec for TrajectoryPrecision metric.

[TrajectoryPrecisionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryPrecisionInstance)

Spec for TrajectoryPrecision instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectoryPrecisionMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryPrecisionMetricValue)

TrajectoryPrecision metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectoryPrecisionResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryPrecisionResults)

Results for TrajectoryPrecision metric.

[TrajectoryPrecisionSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryPrecisionSpec)

Spec for TrajectoryPrecision metric - returns a float score based on average precision of individual tool calls.

[TrajectoryRecallInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryRecallInput)

Instances and metric spec for TrajectoryRecall metric.

[TrajectoryRecallInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryRecallInstance)

Spec for TrajectoryRecall instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectoryRecallMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryRecallMetricValue)

TrajectoryRecall metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectoryRecallResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryRecallResults)

Results for TrajectoryRecall metric.

[TrajectoryRecallSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryRecallSpec)

Spec for TrajectoryRecall metric - returns a float score based on average recall of individual tool calls.

[TrajectorySingleToolUseInput](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseInput)

Instances and metric spec for TrajectorySingleToolUse metric.

[TrajectorySingleToolUseInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseInstance)

Spec for TrajectorySingleToolUse instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectorySingleToolUseMetricValue](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseMetricValue)

TrajectorySingleToolUse metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrajectorySingleToolUseResults](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseResults)

Results for TrajectorySingleToolUse metric.

[TrajectorySingleToolUseSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseSpec)

Spec for TrajectorySingleToolUse metric - returns 1 if tool is present in the predicted trajectory, else 0.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[Trial](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Trial)

A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial.

[TrialContext](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrialContext)

[TunedModel](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TunedModel)

The Model Registry Model and Online Prediction Endpoint associated with this TuningJob.

[TunedModelCheckpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TunedModelCheckpoint)

TunedModelCheckpoint for the Tuned Model of a Tuning Job.

[TunedModelRef](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TunedModelRef)

TunedModel Reference for legacy model migration.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TuningDataStats](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TuningDataStats)

The tuning data statistic values for TuningJob.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TuningJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TuningJob)

Represents a TuningJob that runs with Google owned models.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[Type](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Type)

Type contains the list of OpenAPI data types as defined by
[https://swagger.io/docs/specification/data-models/data-types/](https://swagger.io/docs/specification/data-models/data-types/)

[UndeployIndexOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployIndexOperationMetadata)

Runtime operation information for IndexEndpointService.UndeployIndex.

[UndeployIndexRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployIndexRequest)

Request message for IndexEndpointService.UndeployIndex.

[UndeployIndexResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployIndexResponse)

Response message for IndexEndpointService.UndeployIndex.

[UndeployModelOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelOperationMetadata)

Runtime operation information for EndpointService.UndeployModel.

[UndeployModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelRequest)

Request message for EndpointService.UndeployModel.

[UndeployModelResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelResponse)

Response message for EndpointService.UndeployModel.

[UnmanagedContainerModel](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UnmanagedContainerModel)

Contains model information necessary to perform batch prediction without requiring a full model import.

[UpdateArtifactRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateArtifactRequest)

Request message for MetadataService.UpdateArtifact.

[UpdateCachedContentRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateCachedContentRequest)

Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated.

[UpdateContextRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateContextRequest)

Request message for MetadataService.UpdateContext.

[UpdateDatasetRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetRequest)

Request message for DatasetService.UpdateDataset.

[UpdateDatasetVersionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetVersionRequest)

Request message for DatasetService.UpdateDatasetVersion.

[UpdateDeploymentResourcePoolOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDeploymentResourcePoolOperationMetadata)

Runtime operation information for UpdateDeploymentResourcePool method.

[UpdateDeploymentResourcePoolRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDeploymentResourcePoolRequest)

Request message for UpdateDeploymentResourcePool method.

[UpdateEndpointLongRunningRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointLongRunningRequest)

Request message for EndpointService.UpdateEndpointLongRunning.

[UpdateEndpointOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointOperationMetadata)

Runtime operation information for EndpointService.UpdateEndpointLongRunning.

[UpdateEndpointRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointRequest)

Request message for EndpointService.UpdateEndpoint.

[UpdateEntityTypeRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEntityTypeRequest)

Request message for FeaturestoreService.UpdateEntityType.

[UpdateExampleStoreOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExampleStoreOperationMetadata)

Details of ExampleStoreService.UpdateExampleStore operation.

[UpdateExampleStoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExampleStoreRequest)

Request message for ExampleStoreService.UpdateExampleStore.

[UpdateExecutionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExecutionRequest)

Request message for MetadataService.UpdateExecution.

[UpdateExplanationDatasetOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetOperationMetadata)

Runtime operation information for ModelService.UpdateExplanationDataset.

[UpdateExplanationDatasetRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetRequest)

Request message for ModelService.UpdateExplanationDataset.

[UpdateExplanationDatasetResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetResponse)

Response message of ModelService.UpdateExplanationDataset operation.

[UpdateExtensionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExtensionRequest)

Request message for ExtensionRegistryService.UpdateExtension.

[UpdateFeatureGroupOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureGroupOperationMetadata)

Details of operations that perform update FeatureGroup.

[UpdateFeatureGroupRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureGroupRequest)

Request message for FeatureRegistryService.UpdateFeatureGroup.

[UpdateFeatureMonitorOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureMonitorOperationMetadata)

Details of operations that perform update FeatureMonitor.

[UpdateFeatureMonitorRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureMonitorRequest)

Request message for FeatureRegistryService.UpdateFeatureMonitor.

[UpdateFeatureOnlineStoreOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureOnlineStoreOperationMetadata)

Details of operations that perform update FeatureOnlineStore.

[UpdateFeatureOnlineStoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureOnlineStoreRequest)

Request message for FeatureOnlineStoreAdminService.UpdateFeatureOnlineStore.

[UpdateFeatureOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureOperationMetadata)

Details of operations that perform update Feature.

[UpdateFeatureRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureRequest)

Request message for FeaturestoreService.UpdateFeature. Request message for FeatureRegistryService.UpdateFeature.

[UpdateFeatureViewOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureViewOperationMetadata)

Details of operations that perform update FeatureView.

[UpdateFeatureViewRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureViewRequest)

Request message for FeatureOnlineStoreAdminService.UpdateFeatureView.

[UpdateFeaturestoreOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeaturestoreOperationMetadata)

Details of operations that perform update Featurestore.

[UpdateFeaturestoreRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeaturestoreRequest)

Request message for FeaturestoreService.UpdateFeaturestore.

[UpdateIndexEndpointRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexEndpointRequest)

Request message for IndexEndpointService.UpdateIndexEndpoint.

[UpdateIndexOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexOperationMetadata)

Runtime operation information for IndexService.UpdateIndex.

[UpdateIndexRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexRequest)

Request message for IndexService.UpdateIndex.

[UpdateMemoryOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateMemoryOperationMetadata)

Details of MemoryBankService.UpdateMemory operation.

[UpdateMemoryRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateMemoryRequest)

Request message for MemoryBankService.UpdateMemory.

[UpdateModelDeploymentMonitoringJobOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelDeploymentMonitoringJobOperationMetadata)

Runtime operation information for JobService.UpdateModelDeploymentMonitoringJob.

[UpdateModelDeploymentMonitoringJobRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelDeploymentMonitoringJobRequest)

Request message for JobService.UpdateModelDeploymentMonitoringJob.

[UpdateModelMonitorOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelMonitorOperationMetadata)

Runtime operation information for ModelMonitoringService.UpdateModelMonitor.

[UpdateModelMonitorRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelMonitorRequest)

Request message for ModelMonitoringService.UpdateModelMonitor.

[UpdateModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelRequest)

Request message for ModelService.UpdateModel.

[UpdateNotebookRuntimeTemplateRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateNotebookRuntimeTemplateRequest)

Request message for NotebookService.UpdateNotebookRuntimeTemplate.

[UpdatePersistentResourceOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdatePersistentResourceOperationMetadata)

Details of operations that perform update PersistentResource.

[UpdatePersistentResourceRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdatePersistentResourceRequest)

Request message for UpdatePersistentResource method.

[UpdateRagCorpusOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagCorpusOperationMetadata)

Runtime operation information for VertexRagDataService.UpdateRagCorpus.

[UpdateRagCorpusRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagCorpusRequest)

Request message for VertexRagDataService.UpdateRagCorpus.

[UpdateRagEngineConfigOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagEngineConfigOperationMetadata)

Runtime operation information for VertexRagDataService.UpdateRagEngineConfig.

[UpdateRagEngineConfigRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagEngineConfigRequest)

Request message for VertexRagDataService.UpdateRagEngineConfig.

[UpdateReasoningEngineOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateReasoningEngineOperationMetadata)

Details of ReasoningEngineService.UpdateReasoningEngine operation.

[UpdateReasoningEngineRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateReasoningEngineRequest)

Request message for ReasoningEngineService.UpdateReasoningEngine.

[UpdateScheduleRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateScheduleRequest)

Request message for ScheduleService.UpdateSchedule.

[UpdateSessionRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateSessionRequest)

Request message for SessionService.UpdateSession.

[UpdateSpecialistPoolOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateSpecialistPoolOperationMetadata)

Runtime operation metadata for SpecialistPoolService.UpdateSpecialistPool.

[UpdateSpecialistPoolRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateSpecialistPoolRequest)

Request message for SpecialistPoolService.UpdateSpecialistPool.

[UpdateTensorboardExperimentRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardExperimentRequest)

Request message for TensorboardService.UpdateTensorboardExperiment.

[UpdateTensorboardOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardOperationMetadata)

Details of operations that perform update Tensorboard.

[UpdateTensorboardRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardRequest)

Request message for TensorboardService.UpdateTensorboard.

[UpdateTensorboardRunRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardRunRequest)

Request message for TensorboardService.UpdateTensorboardRun.

[UpdateTensorboardTimeSeriesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardTimeSeriesRequest)

Request message for TensorboardService.UpdateTensorboardTimeSeries.

[UpgradeNotebookRuntimeOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeOperationMetadata)

Metadata information for NotebookService.UpgradeNotebookRuntime.

[UpgradeNotebookRuntimeRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeRequest)

Request message for NotebookService.UpgradeNotebookRuntime.

[UpgradeNotebookRuntimeResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeResponse)

Response message for NotebookService.UpgradeNotebookRuntime.

[UploadModelOperationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadModelOperationMetadata)

Details of ModelService.UploadModel operation.

[UploadModelRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadModelRequest)

Request message for ModelService.UploadModel.

[UploadModelResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadModelResponse)

Response message of ModelService.UploadModel operation.

[UploadRagFileConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadRagFileConfig)

Config for uploading RagFile.

[UploadRagFileRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadRagFileRequest)

Request message for VertexRagDataService.UploadRagFile.

[UploadRagFileResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadRagFileResponse)

Response message for VertexRagDataService.UploadRagFile.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[UpsertDatapointsRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertDatapointsRequest)

Request message for IndexService.UpsertDatapoints

[UpsertDatapointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertDatapointsResponse)

Response message for IndexService.UpsertDatapoints

[UpsertExamplesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertExamplesRequest)

Request message for ExampleStoreService.UpsertExamples.

[UpsertExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertExamplesResponse)

Response message for ExampleStoreService.UpsertExamples.

[UrlContext](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UrlContext)

Tool to support URL context.

[UrlContextMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UrlContextMetadata)

Metadata related to url context retrieval tool.

[UrlMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UrlMetadata)

Context of the a single url retrieval.

[UsageMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UsageMetadata)

Usage metadata about the content generation request and response. This message provides a detailed breakdown of token usage and other relevant metrics.

[UserActionReference](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UserActionReference)

References an API call. It contains more information about long running operation and Jobs that are triggered by the API call.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[Value](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Value)

Value is the value of the field.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[VeoHyperParameters](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VeoHyperParameters)

Hyperparameters for Veo.

[VeoTuningSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VeoTuningSpec)

Tuning Spec for Veo Model Tuning.

[VertexAISearch](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VertexAISearch)

Retrieve from Vertex AI Search datastore or engine for
grounding. datastore and engine are mutually exclusive. See
[https://cloud.google.com/products/agent-builder](https://cloud.google.com/products/agent-builder)

[VertexAiSearchConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VertexAiSearchConfig)

Config for the Vertex AI Search.

[VertexRagStore](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VertexRagStore)

Retrieve from Vertex RAG Store for grounding.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[VideoMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VideoMetadata)

Metadata describes the input video content.

[VoiceConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VoiceConfig)

Configuration for a voice.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[WorkerPoolSpec](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WorkerPoolSpec)

Represents the spec of a worker pool in a job.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[WriteFeatureValuesPayload](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteFeatureValuesPayload)

Contains Feature values to be written for a specific entity.

[WriteFeatureValuesRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteFeatureValuesRequest)

Request message for FeaturestoreOnlineServingService.WriteFeatureValues.

[WriteFeatureValuesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteFeatureValuesResponse)

Response message for FeaturestoreOnlineServingService.WriteFeatureValues.

[WriteTensorboardExperimentDataRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteTensorboardExperimentDataRequest)

Request message for TensorboardService.WriteTensorboardExperimentData.

[WriteTensorboardExperimentDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteTensorboardExperimentDataResponse)

Response message for TensorboardService.WriteTensorboardExperimentData.

[WriteTensorboardRunDataRequest](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteTensorboardRunDataRequest)

Request message for TensorboardService.WriteTensorboardRunData.

[WriteTensorboardRunDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteTensorboardRunDataResponse)

Response message for TensorboardService.WriteTensorboardRunData.

[XraiAttribution](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.XraiAttribution)

An explanation method that redistributes Integrated Gradients attributions to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details:

[https://arxiv.org/abs/1906.02825](https://arxiv.org/abs/1906.02825)

Supported only by image Models.