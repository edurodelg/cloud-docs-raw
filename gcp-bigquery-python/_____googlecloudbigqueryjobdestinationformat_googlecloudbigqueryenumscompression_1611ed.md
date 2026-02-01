---
merged_at: 2026-02-01T08:10:00.332851
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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DestinationFormat -->

# Class DestinationFormat (3.40.0)

`DestinationFormat()`


The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Compression -->

# Class Compression (3.40.0)

`Compression(value)`


The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DestinationFormat -->

# Class DestinationFormat (3.40.0)

`DestinationFormat()`


The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType -->

# Class SeasonalPeriodType (3.40.0)

`SeasonalPeriodType(value)`


API documentation for `bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType`

class.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult -->

# Class IterationResult (3.40.0)

`IterationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single iteration of the training run.

## Attributes |
|
|---|---|
Name |
Description |
`index` |
`google.protobuf.wrappers_pb2.Int32Value`
Index of the iteration, 0 based. |
`duration_ms` |
`google.protobuf.wrappers_pb2.Int64Value`
Time taken to run the iteration in milliseconds. |
`training_loss` |
`google.protobuf.wrappers_pb2.DoubleValue`
Loss computed on the training data at the end of iteration. |
`eval_loss` |
`google.protobuf.wrappers_pb2.DoubleValue`
Loss computed on the eval data at the end of iteration. |
`learn_rate` |
`float`
Learn rate used for this iteration. |
`cluster_infos` |
`Sequence[`
Information about top clusters for clustering models. |

## Classes

### ArimaResult

`ArimaResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


(Auto-)arima fitting result. Wrap everything in ArimaResult for easier refactoring if we want to use model-specific iteration results.

### ClusterInfo

`ClusterInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single cluster for clustering model.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.RankingMetrics -->

# Class RankingMetrics (3.40.0)

`RankingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics used by weighted-ALS models specified by feedback_type=implicit.

## Attributes |
|
|---|---|
Name |
Description |
`mean_average_precision` |
`google.protobuf.wrappers_pb2.DoubleValue`
Calculates a precision per user for all the items by ranking them and then averages all the precisions across all the users. |
`mean_squared_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Similar to the mean squared error computed in regression and explicit recommendation models except instead of computing the rating directly, the output from evaluate is computed against a preference which is 1 or 0 depending on if the rating exists or not. |
`normalized_discounted_cumulative_gain` |
`google.protobuf.wrappers_pb2.DoubleValue`
A metric to determine the goodness of a ranking calculated from the predicted confidence by comparing it to an ideal rank measured by the original ratings. |
`average_rank` |
`google.protobuf.wrappers_pb2.DoubleValue`
Determines the goodness of a ranking by computing the percentile rank from the predicted confidence and dividing it by the original rank. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableOptions -->

# Class BigtableOptions (3.40.0)

`BigtableOptions()`


Options that describe how to treat Bigtable tables as BigQuery tables.

## Properties

### column_families

List[`.external_config.BigtableColumnFamily`

]: List of
column families to expose in the table schema along with their types.

### ignore_unspecified_column_families

bool: If :data:`True`

, ignore columns not specified in
`column_families`

list. Defaults to :data:`False`

.

### read_rowkey_as_string

bool: If :data:`True`

, rowkey column families will be read and
converted to string. Defaults to :data:`False`

.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableOptions
```


Factory: construct a `.external_config.BigtableOptions`

instance given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, Any]`
Definition of a |

Returns |
|
|---|---|
Type |
Description |
`BigtableOptions` |
Configuration parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, Any]` |
A dictionary in the format used by the BigQuery API. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning -->

# Class TimePartitioning (3.40.0)

```
TimePartitioning(
type_=None, field=None, expiration_ms=None, require_partition_filter=None
)
```


Configures time-based partitioning for a table.

## Parameters |
|
|---|---|
Name |
Description |
`type_` |
`Optional[`
Specifies the type of time partitioning to perform. Defaults to |
`field` |
`Optional[str]`
If set, the table is partitioned by this field. If not set, the table is partitioned by pseudo column |
`expiration_ms` |
`Optional[int]`
Number of milliseconds for which to keep the storage for a partition. |
`require_partition_filter` |
`Optional[bool]`
DEPRECATED: Use |

## Properties

### expiration_ms

int: Number of milliseconds to keep the storage for a partition.

### field

str: Field in the table to use for partitioning

### require_partition_filter

bool: Specifies whether partition filters are required for queries

DEPRECATED: Use
[require_partition_filter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table),
instead.

### type_

[google.cloud.bigquery.table.TimePartitioningType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType): The type of time
partitioning to use.

## Methods

### from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.table.TimePartitioning`


Return a `TimePartitioning`

object deserialized from a dict.

This method creates a new `TimePartitioning`

instance that points to
the `api_repr`

parameter as its internal properties dict. This means
that when a `TimePartitioning`

instance is stored as a property of
another object, any changes made at the higher level will also appear
here::

```
>>> time_partitioning = TimePartitioning()
>>> table.time_partitioning = time_partitioning
>>> table.time_partitioning.field = 'timecolumn'
>>> time_partitioning.field
'timecolumn'
```


Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Mapping[str, str]`
The serialized representation of the TimePartitioning, such as what is output by |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.table.TimePartitioning` |
The `TimePartitioning` object. |

### to_api_repr

`to_api_repr() -> dict`


Return a dictionary representing this object.

This method returns the properties dict of the `TimePartitioning`

instance rather than making a copy. This means that when a
`TimePartitioning`

instance is stored as a property of another
object, any changes made at the higher level will also appear here.

Returns |
|
|---|---|
Type |
Description |
`dict` |
A dictionary representing the TimePartitioning object in serialized form. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaCoefficients -->

# Class ArimaCoefficients (3.40.0)

`ArimaCoefficients(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima coefficients.

## Attributes |
|
|---|---|
Name |
Description |
`auto_regressive_coefficients` |
`Sequence[float]`
Auto-regressive coefficients, an array of double. |
`moving_average_coefficients` |
`Sequence[float]`
Moving-average coefficients, an array of double. |
`intercept_coefficient` |
`float`
Intercept coefficient, just a double not an array. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.TrainingOptions.LabelClassWeightsEntry -->

# Class LabelClassWeightsEntry (3.40.0)

`LabelClassWeightsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Connection -->

# Class Connection (3.40.0)

`Connection(client=None, bqstorage_client=None, prefer_bqstorage_client=True)`


DB-API Connection to Google BigQuery.

## Parameters |
|
|---|---|
Name |
Description |
`client` |
`Optional[google.cloud.bigquery.Client]`
A REST API client used to connect to BigQuery. If not passed, a client is created using default options inferred from the environment. |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A client that uses the faster BigQuery Storage API to fetch rows from BigQuery. If not passed, it is created using the same credentials as |
`prefer_bqstorage_client` |
`Optional[bool]`
Prefer the BigQuery Storage client over the REST client. If Storage client isn't available, fall back to the REST client. Defaults to |

## Methods

### close

`close()`


Close the connection and any cursors created from it.

Any BigQuery clients explicitly passed to the constructor are *not*
closed, only those created by the connection instance itself.

### commit

`commit()`


No-op, but for consistency raise an error if connection is closed.

### cursor

`cursor()`


Return a new cursor object.

Returns |
|
|---|---|
Type |
Description |
|
A DB-API cursor that uses this connection. |
