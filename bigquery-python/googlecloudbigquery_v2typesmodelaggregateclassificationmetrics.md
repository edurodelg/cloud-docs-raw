---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.AggregateClassificationMetrics
fetched_at: 2026-01-25T02:12:27.282921
---

# Class AggregateClassificationMetrics (3.40.0)


      
      Save and categorize content based on your preferences.

```
AggregateClassificationMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Aggregate metrics for classification/classifier models. For multi-class models, the metrics are either macro-averaged or micro-averaged. When macro-averaged, the metrics are calculated for each label and then an unweighted average is taken of those values. When micro-averaged, the metric is calculated globally by counting the total number of correctly predicted rows.

## Attributes |
|
|---|---|
Name |
Description |
`precision` |
`google.protobuf.wrappers_pb2.DoubleValue`
Precision is the fraction of actual positive predictions that had positive actual labels. For multiclass this is a macro-averaged metric treating each class as a binary classifier. |
`recall` |
`google.protobuf.wrappers_pb2.DoubleValue`
Recall is the fraction of actual positive labels that were given a positive prediction. For multiclass this is a macro-averaged metric. |
`accuracy` |
`google.protobuf.wrappers_pb2.DoubleValue`
Accuracy is the fraction of predictions given the correct label. For multiclass this is a micro-averaged metric. |
`threshold` |
`google.protobuf.wrappers_pb2.DoubleValue`
Threshold at which the metrics are computed. For binary classification models this is the positive class threshold. For multi-class classfication models this is the confidence threshold. |
`f1_score` |
`google.protobuf.wrappers_pb2.DoubleValue`
The F1 score is an average of recall and precision. For multiclass this is a macro-averaged metric. |
`log_loss` |
`google.protobuf.wrappers_pb2.DoubleValue`
Logarithmic Loss. For multiclass this is a macro-averaged metric. |
`roc_auc` |
`google.protobuf.wrappers_pb2.DoubleValue`
Area Under a ROC Curve. For multiclass this is a macro-averaged metric. |