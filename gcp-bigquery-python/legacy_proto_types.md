---
source_url: https://cloud.google.com/python/docs/reference/bigquery/latest/legacy_proto_types
fetched_at: 2026-02-01T08:00:08.878084
---

# Legacy proto-based Types for Google Cloud Bigquery v2 API

**WARNING**: These types are provided for backward compatibility only, and are not maintained
anymore. They might also differ from the types supported on the backend. It is
therefore strongly advised to migrate to the types found in [Types for Google Cloud Bigquery v2 API](/python/docs/reference/bigquery/latest/standard_sql).

Also see the [3.0.0 Migration Guide](https://docs.cloud.google.com/python/docs/reference/bigquery/UPGRADING.md) for more information.

*class* google.cloud.bigquery_v2.types.DeleteModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### project_id()

Required. Project ID of the model to delete.

**Type**

#### dataset_id()

Required. Dataset ID of the model to delete.

**Type**

#### model_id()

Required. Model ID of the model to delete.

**Type**

*class* google.cloud.bigquery_v2.types.EncryptionConfiguration(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### kms_key_name()

Optional. Describes the Cloud KMS encryption key that will be used to protect destination BigQuery table. The BigQuery Service Account associated with your project requires access to this encryption key.

*class* google.cloud.bigquery_v2.types.GetModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### project_id()

Required. Project ID of the requested model.

**Type**

#### dataset_id()

Required. Dataset ID of the requested model.

**Type**

#### model_id()

Required. Model ID of the requested model.

**Type**

*class* google.cloud.bigquery_v2.types.ListModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### project_id()

Required. Project ID of the models to list.

**Type**

#### dataset_id()

Required. Dataset ID of the models to list.

**Type**

#### max_results()

The maximum number of results to return in a single response page. Leverage the page tokens to iterate through the entire collection.

#### page_token()

Page token, returned by a previous call to request the next page of results

**Type**

*class* google.cloud.bigquery_v2.types.ListModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### models()

Models in the requested dataset. Only the following fields are populated: model_reference, model_type, creation_time, last_modified_time and labels.

**Type**Sequence[google.cloud.bigquery_v2.types.Model]


#### next_page_token()

A token to request the next page of results.

**Type**

*class* google.cloud.bigquery_v2.types.Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### etag()

Output only. A hash of this resource.

**Type**

#### model_reference()

Required. Unique identifier for this model.

**Type**google.cloud.bigquery_v2.types.ModelReference


#### creation_time()

Output only. The time when this model was created, in millisecs since the epoch.

**Type**

#### last_modified_time()

Output only. The time when this model was last modified, in millisecs since the epoch.

**Type**

#### description()

Optional. A user-friendly description of this model.

**Type**

#### friendly_name()

Optional. A descriptive name for this model.

**Type**

#### labels()

The labels associated with this model. You can use these to organize and group your models. Label keys and values can be no longer than 63 characters, can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter and each label in the list must have a different key.

#### expiration_time()

Optional. The time when this model expires, in milliseconds since the epoch. If not present, the model will persist indefinitely. Expired models will be deleted and their storage reclaimed. The defaultTableExpirationMs property of the encapsulating dataset can be used to set a default expirationTime on newly created models.

**Type**

#### location()

Output only. The geographic location where the model resides. This value is inherited from the dataset.

**Type**

#### encryption_configuration()

Custom encryption configuration (e.g., Cloud KMS keys). This shows the encryption configuration of the model data while stored in BigQuery storage. This field can be used with PatchModel to update encryption key for an already encrypted model.

**Type**google.cloud.bigquery_v2.types.EncryptionConfiguration


#### model_type()

Output only. Type of the model resource.

**Type**google.cloud.bigquery_v2.types.Model.ModelType


#### training_runs()

Output only. Information for all training runs in increasing order of start_time.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.TrainingRun]


#### feature_columns()

Output only. Input feature columns that were used to train this model.

**Type**Sequence[google.cloud.bigquery_v2.types.StandardSqlField]


#### label_columns()

Output only. Label columns that were used to train this model. The output of the model will have a predicted_ prefix to these columns.

**Type**Sequence[google.cloud.bigquery_v2.types.StandardSqlField]


#### best_trial_id()

The best trial_id across all training runs.

**Type**

*class* AggregateClassificationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Aggregate metrics for classification/classifier models. For multi-class models, the metrics are either macro-averaged or micro-averaged. When macro-averaged, the metrics are calculated for each label and then an unweighted average is taken of those values. When micro-averaged, the metric is calculated globally by counting the total number of correctly predicted rows.

#### precision()

Precision is the fraction of actual positive predictions that had positive actual labels. For multiclass this is a macro-averaged metric treating each class as a binary classifier.

#### recall()

Recall is the fraction of actual positive labels that were given a positive prediction. For multiclass this is a macro-averaged metric.

#### accuracy()

Accuracy is the fraction of predictions given the correct label. For multiclass this is a micro-averaged metric.

#### threshold()

Threshold at which the metrics are computed. For binary classification models this is the positive class threshold. For multi-class classfication models this is the confidence threshold.

#### f1_score()

The F1 score is an average of recall and precision. For multiclass this is a macro-averaged metric.

#### log_loss()

Logarithmic Loss. For multiclass this is a macro-averaged metric.

#### roc_auc()

Area Under a ROC Curve. For multiclass this is a macro-averaged metric.

*class* ArimaFittingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


ARIMA model fitting metrics.

#### log_likelihood()

Log-likelihood.

**Type**

#### aic()

AIC.

**Type**

#### variance()

Variance.

**Type**

*class* ArimaForecastingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Model evaluation metrics for ARIMA forecasting models.

#### non_seasonal_order()

Non-seasonal order.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.ArimaOrder]


#### arima_fitting_metrics()

Arima model fitting metrics.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.ArimaFittingMetrics]


#### seasonal_periods()

Seasonal periods. Repeated because multiple periods are supported for one time series.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType]


#### has_drift()

Whether Arima model fitted with drift or not. It is always false when d is not 1.

**Type**Sequence[

[bool](https://docs.python.org/3/library/functions.html#bool)]

#### time_series_id()

Id to differentiate different time series for the large-scale case.

**Type**Sequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### arima_single_model_forecasting_metrics()

Repeated as there can be many metric sets (one for each model) in auto-arima and the large-scale case.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.ArimaForecastingMetrics.ArimaSingleModelForecastingMetrics]


*class* ArimaSingleModelForecastingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Model evaluation metrics for a single ARIMA forecasting model.

#### non_seasonal_order()

Non-seasonal order.

**Type**google.cloud.bigquery_v2.types.Model.ArimaOrder


#### arima_fitting_metrics()

Arima fitting metrics.

**Type**google.cloud.bigquery_v2.types.Model.ArimaFittingMetrics


#### has_drift()

Is arima model fitted with drift or not. It is always false when d is not 1.

**Type**

#### time_series_id()

The time_series_id value for this time series. It will be one of the unique values from the time_series_id_column specified during ARIMA model training. Only present when time_series_id_column training option was used.

**Type**

#### time_series_ids()

The tuple of time_series_ids identifying this time series. It will be one of the unique tuples of values present in the time_series_id_columns specified during ARIMA model training. Only present when time_series_id_columns training option was used and the order of values here are same as the order of time_series_id_columns.

**Type**Sequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### seasonal_periods()

Seasonal periods. Repeated because multiple periods are supported for one time series.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType]


#### has_holiday_effect()

If true, holiday_effect is a part of time series decomposition result.

#### has_spikes_and_dips()

If true, spikes_and_dips is a part of time series decomposition result.

#### has_step_changes()

If true, step_changes is a part of time series decomposition result.

*class* ArimaOrder(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Arima order, can be used for both non-seasonal and seasonal parts.

#### p()

Order of the autoregressive part.

**Type**

#### d()

Order of the differencing part.

**Type**

#### q()

Order of the moving-average part.

**Type**

*class* BinaryClassificationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Evaluation metrics for binary classification/classifier models.

#### aggregate_classification_metrics()

Aggregate classification metrics.

**Type**google.cloud.bigquery_v2.types.Model.AggregateClassificationMetrics


#### binary_confusion_matrix_list()

Binary confusion matrix at multiple thresholds.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.BinaryClassificationMetrics.BinaryConfusionMatrix]


#### positive_label()

Label representing the positive class.

**Type**

#### negative_label()

Label representing the negative class.

**Type**

*class* BinaryConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Confusion matrix for binary classification models.

#### positive_class_threshold()

Threshold value used when computing each of the following metric.

#### true_positives()

Number of true samples predicted as true.

#### false_positives()

Number of false samples predicted as true.

#### true_negatives()

Number of true samples predicted as false.

#### false_negatives()

Number of false samples predicted as false.

#### precision()

The fraction of actual positive predictions that had positive actual labels.

#### recall()

The fraction of actual positive labels that were given a positive prediction.

#### f1_score()

The equally weighted average of recall and precision.

#### accuracy()

The fraction of predictions given the correct label.

*class* ClusteringMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Evaluation metrics for clustering models.

#### davies_bouldin_index()

Davies-Bouldin index.

#### mean_squared_distance()

Mean of squared distances between each sample to its cluster centroid.

#### clusters()

Information for all clusters.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster]


*class* Cluster(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Message containing the information about one cluster.

#### centroid_id()

Centroid id.

**Type**

#### feature_values()

Values of highly variant features for this cluster.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue]


#### count()

Count of training data rows that were assigned to this cluster.

*class* FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Representative value of a single feature within the cluster.

This message has [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

#### feature_column()

The feature column name.

**Type**

#### numerical_value()

The numerical feature value. This is the centroid value for this feature.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `value`

.

#### categorical_value()

The categorical feature value.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `value`

.

**Type**google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue.CategoricalValue


*class* CategoricalValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Representative value of a categorical feature.

#### category_counts()

Counts of all categories for the categorical feature. If
there are more than ten categories, we return top ten (by
count) and return one more CategoryCount with category
“*OTHER*” and count as aggregate counts of remaining
categories.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue.CategoricalValue.CategoryCount]


*class* CategoryCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Represents the count of a single category within the cluster.

#### category()

The name of category.

**Type**

#### count()

The count of training samples matching the category within the cluster.

*class* DataFrequency(value)

Bases: `proto.enums.Enum`


Type of supported data frequency for time series forecasting models.

#### AUTO_FREQUENCY(* = * )

#### DAILY(* = * )

#### DATA_FREQUENCY_UNSPECIFIED(* = * )

#### HOURLY(* = * )

#### MONTHLY(* = * )

#### PER_MINUTE(* = * )

#### QUARTERLY(* = * )

#### WEEKLY(* = * )

#### YEARLY(* = * )

*class* DataSplitMethod(value)

Bases: `proto.enums.Enum`


Indicates the method to split input data into multiple tables.

#### AUTO_SPLIT(* = * )

#### CUSTOM(* = * )

#### DATA_SPLIT_METHOD_UNSPECIFIED(* = * )

#### NO_SPLIT(* = * )

#### RANDOM(* = * )

#### SEQUENTIAL(* = * )

*class* DataSplitResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Data split result. This contains references to the training and evaluation data tables that were used to train the model.

#### training_table()

Table reference of the training data after split.

**Type**google.cloud.bigquery_v2.types.TableReference


#### evaluation_table()

Table reference of the evaluation data after split.

**Type**google.cloud.bigquery_v2.types.TableReference


*class* DistanceType(value)

Bases: `proto.enums.Enum`


Distance metric used to compute the distance between two points.

#### COSINE(* = * )

#### DISTANCE_TYPE_UNSPECIFIED(* = * )

#### EUCLIDEAN(* = * )

*class* EvaluationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Evaluation metrics of a model. These are either computed on all training data or just the eval data based on whether eval data was used during training. These are not present for imported models.

This message has [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

#### regression_metrics()

Populated for regression models and explicit feedback type matrix factorization models.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `metrics`

.

**Type**google.cloud.bigquery_v2.types.Model.RegressionMetrics


#### binary_classification_metrics()

Populated for binary classification/classifier models.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `metrics`

.

**Type**google.cloud.bigquery_v2.types.Model.BinaryClassificationMetrics


#### multi_class_classification_metrics()

Populated for multi-class classification/classifier models.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `metrics`

.

**Type**google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics


#### clustering_metrics()

Populated for clustering models.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `metrics`

.

**Type**google.cloud.bigquery_v2.types.Model.ClusteringMetrics


#### ranking_metrics()

Populated for implicit feedback type matrix factorization models.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `metrics`

.

**Type**google.cloud.bigquery_v2.types.Model.RankingMetrics


#### arima_forecasting_metrics()

Populated for ARIMA models.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `metrics`

.

**Type**google.cloud.bigquery_v2.types.Model.ArimaForecastingMetrics


*class* FeedbackType(value)

Bases: `proto.enums.Enum`


Indicates the training algorithm to use for matrix factorization models.

#### EXPLICIT(* = * )

#### FEEDBACK_TYPE_UNSPECIFIED(* = * )

#### IMPLICIT(* = * )

*class* GlobalExplanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Global explanations containing the top most important features after training.

#### explanations()

A list of the top global explanations. Sorted by absolute value of attribution in descending order.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.GlobalExplanation.Explanation]


#### class_label()

Class label for this set of global explanations. Will be empty/null for binary logistic and linear regression models. Sorted alphabetically in descending order.

**Type**

*class* Explanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Explanation for a single feature.

#### feature_name()

Full name of the feature. For non-numerical features, will be formatted like <column_name>.<encoded_feature_name>. Overall size of feature name will always be truncated to first 120 characters.

**Type**

#### attribution()

Attribution of feature.

*class* HolidayRegion(value)

Bases: `proto.enums.Enum`


Type of supported holiday regions for time series forecasting models.

#### AE(* = * )

#### AR(* = * )

#### AT(* = * )

#### AU(* = * )

#### BE(* = 1* )

#### BR(* = 1* )

#### CA(* = 1* )

#### CH(* = 1* )

#### CL(* = 1* )

#### CN(* = 1* )

#### CO(* = 1* )

#### CS(* = 1* )

#### CZ(* = 1* )

#### DE(* = 1* )

#### DK(* = 2* )

#### DZ(* = 2* )

#### EC(* = 2* )

#### EE(* = 2* )

#### EG(* = 2* )

#### EMEA(* = * )

#### ES(* = 2* )

#### FI(* = 2* )

#### FR(* = 2* )

#### GB(* = 2* )

#### GLOBAL(* = * )

#### GR(* = 2* )

#### HK(* = 3* )

#### HOLIDAY_REGION_UNSPECIFIED(* = * )

#### HU(* = 3* )

#### ID(* = 3* )

#### IE(* = 3* )

#### IL(* = 3* )

#### IN(* = 3* )

#### IR(* = 3* )

#### IT(* = 3* )

#### JAPAC(* = * )

#### JP(* = 3* )

#### KR(* = 3* )

#### LAC(* = * )

#### LV(* = 4* )

#### MA(* = 4* )

#### MX(* = 4* )

#### MY(* = 4* )

#### NA(* = * )

#### NG(* = 4* )

#### NL(* = 4* )

#### NO(* = 4* )

#### NZ(* = 4* )

#### PE(* = 4* )

#### PH(* = 4* )

#### PK(* = 5* )

#### PL(* = 5* )

#### PT(* = 5* )

#### RO(* = 5* )

#### RS(* = 5* )

#### RU(* = 5* )

#### SA(* = 5* )

#### SE(* = 5* )

#### SG(* = 5* )

#### SI(* = 5* )

#### SK(* = 6* )

#### TH(* = 6* )

#### TR(* = 6* )

#### TW(* = 6* )

#### UA(* = 6* )

#### US(* = 6* )

#### VE(* = 6* )

#### VN(* = 6* )

#### ZA(* = 6* )

*class* KmeansEnums(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


*class* KmeansInitializationMethod(value)

Bases: `proto.enums.Enum`


Indicates the method used to initialize the centroids for KMeans clustering algorithm.

#### CUSTOM(* = * )

#### KMEANS_INITIALIZATION_METHOD_UNSPECIFIED(* = * )

#### KMEANS_PLUS_PLUS(* = * )

#### RANDOM(* = * )

*class* LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


*class* LearnRateStrategy(value)

Bases: `proto.enums.Enum`


Indicates the learning rate optimization strategy to use.

#### CONSTANT(* = * )

#### LEARN_RATE_STRATEGY_UNSPECIFIED(* = * )

#### LINE_SEARCH(* = * )

*class* LossType(value)

Bases: `proto.enums.Enum`


Loss metric to evaluate model training performance.

#### LOSS_TYPE_UNSPECIFIED(* = * )

#### MEAN_LOG_LOSS(* = * )

#### MEAN_SQUARED_LOSS(* = * )

*class* ModelType(value)

Bases: `proto.enums.Enum`


Indicates the type of the Model.

#### ARIMA(* = 1* )

#### ARIMA_PLUS(* = 1* )

#### AUTOML_CLASSIFIER(* = 1* )

#### AUTOML_REGRESSOR(* = 1* )

#### BOOSTED_TREE_CLASSIFIER(* = 1* )

#### BOOSTED_TREE_REGRESSOR(* = * )

#### DNN_CLASSIFIER(* = * )

#### DNN_REGRESSOR(* = * )

#### KMEANS(* = * )

#### LINEAR_REGRESSION(* = * )

#### LOGISTIC_REGRESSION(* = * )

#### MATRIX_FACTORIZATION(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### TENSORFLOW(* = * )

*class* MultiClassClassificationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Evaluation metrics for multi-class classification/classifier models.

#### aggregate_classification_metrics()

Aggregate classification metrics.

**Type**google.cloud.bigquery_v2.types.Model.AggregateClassificationMetrics


#### confusion_matrix_list()

Confusion matrix at different thresholds.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix]


*class* ConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Confusion matrix for multi-class classification models.

#### confidence_threshold()

Confidence threshold used when computing the entries of the confusion matrix.

#### rows()

One row per actual label.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix.Row]


*class* Entry(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A single entry in the confusion matrix.

#### predicted_label()

The predicted label. For confidence_threshold > 0, we will also add an entry indicating the number of items under the confidence threshold.

**Type**

#### item_count()

Number of items being predicted as this label.

*class* Row(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A single row in the confusion matrix.

#### actual_label()

The original label of this row.

**Type**

#### entries()

Info describing predicted label distribution.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix.Entry]


*class* OptimizationStrategy(value)

Bases: `proto.enums.Enum`


Indicates the optimization strategy used for training.

#### BATCH_GRADIENT_DESCENT(* = * )

#### NORMAL_EQUATION(* = * )

#### OPTIMIZATION_STRATEGY_UNSPECIFIED(* = * )

*class* RankingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Evaluation metrics used by weighted-ALS models specified by feedback_type=implicit.

#### mean_average_precision()

Calculates a precision per user for all the items by ranking them and then averages all the precisions across all the users.

#### mean_squared_error()

Similar to the mean squared error computed in regression and explicit recommendation models except instead of computing the rating directly, the output from evaluate is computed against a preference which is 1 or 0 depending on if the rating exists or not.

#### normalized_discounted_cumulative_gain()

A metric to determine the goodness of a ranking calculated from the predicted confidence by comparing it to an ideal rank measured by the original ratings.

#### average_rank()

Determines the goodness of a ranking by computing the percentile rank from the predicted confidence and dividing it by the original rank.

*class* RegressionMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Evaluation metrics for regression and explicit feedback type matrix factorization models.

#### mean_absolute_error()

Mean absolute error.

#### mean_squared_error()

Mean squared error.

#### mean_squared_log_error()

Mean squared log error.

#### median_absolute_error()

Median absolute error.

#### r_squared()

R^2 score. This corresponds to r2_score in ML.EVALUATE.

*class* SeasonalPeriod(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


*class* SeasonalPeriodType(value)

Bases: `proto.enums.Enum`


#### DAILY(* = * )

#### MONTHLY(* = * )

#### NO_SEASONALITY(* = * )

#### QUARTERLY(* = * )

#### SEASONAL_PERIOD_TYPE_UNSPECIFIED(* = * )

#### WEEKLY(* = * )

#### YEARLY(* = * )

*class* TrainingRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Information about a single training query run for the model.

#### training_options()

Options that were used for this training run, includes user specified and default options that were used.

**Type**google.cloud.bigquery_v2.types.Model.TrainingRun.TrainingOptions


#### start_time()

The start time of this training run.

#### results()

Output of each iteration run, results.size() <= max_iterations.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult]


#### evaluation_metrics()

The evaluation metrics over training/eval data that were computed at the end of training.

**Type**google.cloud.bigquery_v2.types.Model.EvaluationMetrics


#### data_split_result()

Data split result of the training run. Only set when the input data is actually split.

**Type**google.cloud.bigquery_v2.types.Model.DataSplitResult


#### global_explanations()

Global explanations for important features of the model. For multi-class models, there is one entry for each label class. For other models, there is only one entry in the list.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.GlobalExplanation]


*class* IterationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Information about a single iteration of the training run.

#### index()

Index of the iteration, 0 based.

#### duration_ms()

Time taken to run the iteration in milliseconds.

#### training_loss()

Loss computed on the training data at the end of iteration.

#### eval_loss()

Loss computed on the eval data at the end of iteration.

#### learn_rate()

Learn rate used for this iteration.

**Type**

#### cluster_infos()

Information about top clusters for clustering models.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ClusterInfo]


#### arima_result()

**Type**google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult


*class* ArimaResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


(Auto-)arima fitting result. Wrap everything in ArimaResult for easier refactoring if we want to use model-specific iteration results.

#### arima_model_info()

This message is repeated because there are multiple arima models fitted in auto-arima. For non-auto-arima model, its size is one.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaModelInfo]


#### seasonal_periods()

Seasonal periods. Repeated because multiple periods are supported for one time series.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType]


*class* ArimaCoefficients(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Arima coefficients.

#### auto_regressive_coefficients()

Auto-regressive coefficients, an array of double.

**Type**Sequence[

[float](https://docs.python.org/3/library/functions.html#float)]

#### moving_average_coefficients()

Moving-average coefficients, an array of double.

**Type**Sequence[

[float](https://docs.python.org/3/library/functions.html#float)]

#### intercept_coefficient()

Intercept coefficient, just a double not an array.

**Type**

*class* ArimaModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Arima model information.

#### non_seasonal_order()

Non-seasonal order.

**Type**google.cloud.bigquery_v2.types.Model.ArimaOrder


#### arima_coefficients()

Arima coefficients.

**Type**google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaCoefficients


#### arima_fitting_metrics()

Arima fitting metrics.

**Type**google.cloud.bigquery_v2.types.Model.ArimaFittingMetrics


#### has_drift()

Whether Arima model fitted with drift or not. It is always false when d is not 1.

**Type**

#### time_series_id()

The time_series_id value for this time series. It will be one of the unique values from the time_series_id_column specified during ARIMA model training. Only present when time_series_id_column training option was used.

**Type**

#### time_series_ids()

The tuple of time_series_ids identifying this time series. It will be one of the unique tuples of values present in the time_series_id_columns specified during ARIMA model training. Only present when time_series_id_columns training option was used and the order of values here are same as the order of time_series_id_columns.

**Type**Sequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### seasonal_periods()

Seasonal periods. Repeated because multiple periods are supported for one time series.

**Type**Sequence[google.cloud.bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType]


#### has_holiday_effect()

If true, holiday_effect is a part of time series decomposition result.

#### has_spikes_and_dips()

If true, spikes_and_dips is a part of time series decomposition result.

#### has_step_changes()

If true, step_changes is a part of time series decomposition result.

*class* ClusterInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Information about a single cluster for clustering model.

#### centroid_id()

Centroid id.

**Type**

#### cluster_radius()

Cluster radius, the average distance from centroid to each point assigned to the cluster.

#### cluster_size()

Cluster size, the total number of points assigned to the cluster.

*class* TrainingOptions(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Options used in model training.

#### max_iterations()

The maximum number of iterations in training. Used only for iterative training algorithms.

**Type**

#### loss_type()

Type of loss function used during training run.

**Type**google.cloud.bigquery_v2.types.Model.LossType


#### learn_rate()

Learning rate in training. Used only for iterative training algorithms.

**Type**

#### l1_regularization()

L1 regularization coefficient.

#### l2_regularization()

L2 regularization coefficient.

#### min_relative_progress()

When early_stop is true, stops training when accuracy improvement is less than ‘min_relative_progress’. Used only for iterative training algorithms.

#### warm_start()

Whether to train a model from the last checkpoint.

#### early_stop()

Whether to stop early when the loss doesn’t improve significantly any more (compared to min_relative_progress). Used only for iterative training algorithms.

#### input_label_columns()

Name of input label columns in training data.

**Type**Sequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### data_split_method()

The data split type for training and evaluation, e.g. RANDOM.

**Type**google.cloud.bigquery_v2.types.Model.DataSplitMethod


#### data_split_eval_fraction()

The fraction of evaluation data over the whole input data. The rest of data will be used as training data. The format should be double. Accurate to two decimal places. Default value is 0.2.

**Type**

#### data_split_column()

The column to split data with. This column won’t be used as a feature.

When data_split_method is CUSTOM, the corresponding column should be boolean. The rows with true value tag are eval data, and the false are training data.

When data_split_method is SEQ, the first DATA_SPLIT_EVAL_FRACTION rows (from smallest to largest) in the corresponding column are used as training data, and the rest are eval data. It respects the order in Orderable data types:

[https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#data-type-properties](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#data-type-properties)

**Type**

#### learn_rate_strategy()

The strategy to determine learn rate for the current iteration.

**Type**google.cloud.bigquery_v2.types.Model.LearnRateStrategy


#### initial_learn_rate()

Specifies the initial learning rate for the line search learn rate strategy.

**Type**

#### label_class_weights()

Weights associated with each label class, for rebalancing the training data. Only applicable for classification models.

#### user_column()

User column specified for matrix factorization models.

**Type**

#### item_column()

Item column specified for matrix factorization models.

**Type**

#### distance_type()

Distance type for clustering models.

**Type**google.cloud.bigquery_v2.types.Model.DistanceType


#### num_clusters()

Number of clusters for clustering models.

**Type**

#### model_uri()

Google Cloud Storage URI from which the model was imported. Only applicable for imported models.

**Type**

#### optimization_strategy()

Optimization strategy for training linear regression models.

**Type**google.cloud.bigquery_v2.types.Model.OptimizationStrategy


#### hidden_units()

Hidden units for dnn models.

**Type**Sequence[

[int](https://docs.python.org/3/library/functions.html#int)]

#### batch_size()

Batch size for dnn models.

**Type**

#### dropout()

Dropout probability for dnn models.

#### max_tree_depth()

Maximum depth of a tree for boosted tree models.

**Type**

#### subsample()

Subsample fraction of the training data to grow tree to prevent overfitting for boosted tree models.

**Type**

#### min_split_loss()

Minimum split loss for boosted tree models.

#### num_factors()

Num factors specified for matrix factorization models.

**Type**

#### feedback_type()

Feedback type that specifies which algorithm to run for matrix factorization.

**Type**google.cloud.bigquery_v2.types.Model.FeedbackType


#### wals_alpha()

Hyperparameter for matrix factoration when implicit feedback type is specified.

#### kmeans_initialization_method()

The method used to initialize the centroids for kmeans algorithm.

**Type**google.cloud.bigquery_v2.types.Model.KmeansEnums.KmeansInitializationMethod


#### kmeans_initialization_column()

The column used to provide the initial centroids for kmeans algorithm when kmeans_initialization_method is CUSTOM.

**Type**

#### time_series_timestamp_column()

Column to be designated as time series timestamp for ARIMA model.

**Type**

#### time_series_data_column()

Column to be designated as time series data for ARIMA model.

**Type**

#### auto_arima()

Whether to enable auto ARIMA or not.

**Type**

#### non_seasonal_order()

A specification of the non-seasonal part of the ARIMA model: the three components (p, d, q) are the AR order, the degree of differencing, and the MA order.

**Type**google.cloud.bigquery_v2.types.Model.ArimaOrder


#### data_frequency()

The data frequency of a time series.

**Type**google.cloud.bigquery_v2.types.Model.DataFrequency


#### include_drift()

Include drift when fitting an ARIMA model.

**Type**

#### holiday_region()

The geographical region based on which the holidays are considered in time series modeling. If a valid value is specified, then holiday effects modeling is enabled.

**Type**google.cloud.bigquery_v2.types.Model.HolidayRegion


#### time_series_id_column()

The time series id column that was used during ARIMA model training.

**Type**

#### time_series_id_columns()

The time series id columns that were used during ARIMA model training.

**Type**Sequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### horizon()

The number of periods ahead that need to be forecasted.

**Type**

#### preserve_input_structs()

Whether to preserve the input structs in output feature names. Suppose there is a struct A with field b. When false (default), the output feature name is A_b. When true, the output feature name is A.b.

**Type**

#### auto_arima_max_order()

The max value of non-seasonal p and q.

**Type**

#### decompose_time_series()

If true, perform decompose time series and save the results.

#### clean_spikes_and_dips()

If true, clean spikes and dips in the input time series.

#### adjust_step_changes()

If true, detect step changes and make data adjustment in the input time series.

*class* LabelClassWeightsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


*class* google.cloud.bigquery_v2.types.ModelReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Id path of a model.

#### project_id()

Required. The ID of the project containing this model.

**Type**

#### dataset_id()

Required. The ID of the dataset containing this model.

**Type**

#### model_id()

Required. The ID of the model. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (_). The maximum length is 1,024 characters.

**Type**

*class* google.cloud.bigquery_v2.types.PatchModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### project_id()

Required. Project ID of the model to patch.

**Type**

#### dataset_id()

Required. Dataset ID of the model to patch.

**Type**

#### model_id()

Required. Model ID of the model to patch.

**Type**

#### model()

Required. Patched model. Follows RFC5789 patch semantics. Missing fields are not updated. To clear a field, explicitly set to default value.

**Type**google.cloud.bigquery_v2.types.Model


*class* google.cloud.bigquery_v2.types.StandardSqlDataType(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


The type of a variable, e.g., a function argument. Examples: INT64: {type_kind=”INT64”} ARRAY: {type_kind=”ARRAY”, array_element_type=”STRING”} STRUCT<x STRING, y ARRAY>: {type_kind=”STRUCT”, struct_type={fields=[ {name=”x”, type={type_kind=”STRING”}}, {name=”y”, type={type_kind=”ARRAY”, array_element_type=”DATE”}} ]}}

This message has [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

#### type_kind()

Required. The top level type of this field. Can be any standard SQL data type (e.g., “INT64”, “DATE”, “ARRAY”).

**Type**google.cloud.bigquery_v2.types.StandardSqlDataType.TypeKind


#### array_element_type()

The type of the array’s elements, if type_kind = “ARRAY”.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `sub_type`

.

**Type**google.cloud.bigquery_v2.types.StandardSqlDataType


#### struct_type()

The fields of this struct, in order, if type_kind = “STRUCT”.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `sub_type`

.

**Type**google.cloud.bigquery_v2.types.StandardSqlStructType


*class* TypeKind(value)

Bases: `proto.enums.Enum`


#### ARRAY(* = 1* )

#### BIGNUMERIC(* = 2* )

#### BOOL(* = * )

#### BYTES(* = * )

#### DATE(* = 1* )

#### DATETIME(* = 2* )

#### FLOAT64(* = * )

#### GEOGRAPHY(* = 2* )

#### INT64(* = * )

#### INTERVAL(* = 2* )

#### JSON(* = 2* )

#### NUMERIC(* = 2* )

#### STRING(* = * )

#### STRUCT(* = 1* )

#### TIME(* = 2* )

#### TIMESTAMP(* = 1* )

#### TYPE_KIND_UNSPECIFIED(* = * )

*class* google.cloud.bigquery_v2.types.StandardSqlField(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A field or a column.

#### name()

Optional. The name of this field. Can be absent for struct fields.

**Type**

#### type()

Optional. The type of this parameter. Absent if not explicitly specified (e.g., CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this “type” field).

**Type**google.cloud.bigquery_v2.types.StandardSqlDataType


*class* google.cloud.bigquery_v2.types.StandardSqlStructType(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### fields()

**Type**Sequence[google.cloud.bigquery_v2.types.StandardSqlField]


*class* google.cloud.bigquery_v2.types.StandardSqlTableType(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A table type

#### columns()

The columns in this table type

**Type**Sequence[google.cloud.bigquery_v2.types.StandardSqlField]


*class* google.cloud.bigquery_v2.types.TableReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### project_id()

Required. The ID of the project containing this table.

**Type**

#### dataset_id()

Required. The ID of the dataset containing this table.

**Type**

#### table_id()

Required. The ID of the table. The ID must contain only
letters (a-z, A-Z), numbers (0-9), or underscores (_). The
maximum length is 1,024 characters. Certain operations allow
suffixing of the table ID with a partition decorator, such
as `sample_table$20190123`

.

**Type**

#### project_id_alternative()

The alternative field that will be used when ESF is not able to translate the received data to the project_id field.

**Type**Sequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### dataset_id_alternative()

The alternative field that will be used when ESF is not able to translate the received data to the project_id field.

**Type**Sequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### table_id_alternative()

The alternative field that will be used when ESF is not able to translate the received data to the project_id field.

**Type**Sequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]