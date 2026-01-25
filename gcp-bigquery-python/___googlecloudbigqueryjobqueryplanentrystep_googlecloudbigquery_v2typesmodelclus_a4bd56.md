---
merged_at: 2026-01-25T15:38:56.561783
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryjobqueryplanentrystep_googlecloudbigquery_v2typesmodelclust_37fd33.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryjobqueryplanentrystep_googlecloudbigquery_v2typesmodelcluste_e262d6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobqueryplanentrystep.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntryStep -->

# Class QueryPlanEntryStep (3.40.0)

`QueryPlanEntryStep(kind, substeps)`


Map a single step in a query plan entry.

## Parameters |
|
|---|---|
Name |
Description |
`kind` |
`str`
step type. |
`substeps` |
`List`
names of substeps. |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.query.QueryPlanEntryStep`


Factory: construct instance from the JSON repr.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON representation of the entry. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job.QueryPlanEntryStep` |
New instance built from the resource. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelclusteringmetrics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics -->

# Class ClusteringMetrics (3.40.0)

`ClusteringMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for clustering models.

## Attributes |
|
|---|---|
Name |
Description |
`davies_bouldin_index` |
`google.protobuf.wrappers_pb2.DoubleValue`
Davies-Bouldin index. |
`mean_squared_distance` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean of squared distances between each sample to its cluster centroid. |
`clusters` |
`Sequence[`
Information for all clusters. |

## Classes

### Cluster

`Cluster(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message containing the information about one cluster.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumsroundingmode_googlecloudbigqueryjobtransactioninfo.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsroundingmode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.RoundingMode -->

# Class RoundingMode (3.40.0)

`RoundingMode(value)`


Rounding mode options that can be used when storing NUMERIC or BIGNUMERIC values.

ROUNDING_MODE_UNSPECIFIED: will default to using ROUND_HALF_AWAY_FROM_ZERO.

ROUND_HALF_AWAY_FROM_ZERO: rounds half values away from zero when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0

- 1.1, 1.2, 1.3, 1.4 => 1
- 1.5, 1.6, 1.7, 1.8, 1.9 => 2

ROUND_HALF_EVEN: rounds half values to the nearest even value when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0

- 1.1, 1.2, 1.3, 1.4 => 1
- 1.5 => 2
- 1.6, 1.7, 1.8, 1.9 => 2
- 2.5 => 2


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobtransactioninfo.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TransactionInfo -->

# Class TransactionInfo (3.40.0)

`TransactionInfo(transaction_id: str)`


[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

.. versionadded:: 2.24.0

## Methods

### TransactionInfo

`TransactionInfo(transaction_id: str)`


Create new instance of TransactionInfo(transaction_id,)

### count

`count(value, /)`


Return number of occurrences of value.

### index

`index(value, start=0, stop=9223372036854775807, /)`


Return first index of value.

Raises ValueError if the value is not present.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerydatasetcondition_googlecloudbigquery_v2typesmodelaggregatecl_a983bb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydatasetcondition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Condition -->

# Class Condition (3.40.0)

```
Condition(
expression: str,
title: typing.Optional[str] = None,
description: typing.Optional[str] = None,
)
```


Represents a textual expression in the Common Expression Language (CEL) syntax.

Typically used for filtering or policy rules, such as in IAM Conditions or BigQuery row/column access policies.

See:
[https://cloud.google.com/iam/docs/reference/rest/Shared.Types/Expr](https://cloud.google.com/iam/docs/reference/rest/Shared.Types/Expr)
[https://github.com/google/cel-spec](https://github.com/google/cel-spec)

## Parameters |
|
|---|---|
Name |
Description |
`expression` |
`str`
The condition expression string using CEL syntax. This is required. Example: |
`title` |
`Optional[str]`
An optional title for the condition, providing a short summary. Example: |
`description` |
`Optional[str]`
An optional description of the condition, providing a detailed explanation. Example: |

## Properties

### description

Optional[str]: The description for the condition.

### expression

str: The expression string for the condition.

### title

Optional[str]: The title for the condition.

## Methods

### __eq__

`__eq__(other: object) -> bool`


Check for equality based on expression, title, and description.

### __hash__

`__hash__() -> int`


Generate a hash based on expression, title, and description.

### __ne__

`__ne__(other: object) -> bool`


Check for inequality.

### __repr__

`__repr__() -> str`


Return a string representation of the Condition object.

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.dataset.Condition
```


Factory: construct a Condition instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this Condition.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelaggregateclassificationmetrics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.AggregateClassificationMetrics -->

# Class AggregateClassificationMetrics (3.40.0)

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
