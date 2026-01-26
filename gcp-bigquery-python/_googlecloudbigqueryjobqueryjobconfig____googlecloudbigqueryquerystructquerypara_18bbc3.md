---
merged_at: 2026-01-26T21:00:49.247106
merged_files: 2
---


---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig -->

# Class QueryJobConfig (3.40.0)

`QueryJobConfig(**kwargs)`


Configuration options for query jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

## Properties

### allow_large_results

bool: Allow large query results tables (legacy SQL, only)

### clustering_fields

Optional[List[str]]: Fields defining clustering for the table

(Defaults to :data:`None`

).

Clustering fields are immutable after table creation.

### connection_properties

Connection properties.

.. versionadded:: 2.29.0

### create_disposition

[google.cloud.bigquery.job.CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition): Specifies behavior
for creating tables.

### create_session

[Preview] If :data:`True`

, creates a new session, where
[session_info](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob) will contain a
random server generated session id.

If :data:`False`

, runs query with an existing `session_id`

passed in
[connection_properties](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig),
otherwise runs query in non-session mode.

.. versionadded:: 2.29.0

### default_dataset

[google.cloud.bigquery.dataset.DatasetReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference): the default dataset
to use for unqualified table names in the query or :data:`None`

if not
set.

The `default_dataset`

setter accepts:

- a
[Dataset](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset), or - a
[DatasetReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference), or - a
`str`

of the fully-qualified dataset ID in standard SQL format. The value must included a project ID and dataset ID separated by`.`

. For example:`your-project.your_dataset`

.

### destination

[google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference): table where results are
written or :data:`None`

if not set.

The `destination`

setter accepts:

- a
[Table](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table), or - a
[TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference), or - a
`str`

of the fully-qualified table ID in standard SQL format. The value must included a project ID, dataset ID, and table ID, each separated by`.`

. For example:`your-project.your_dataset.your_table`

.

### destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

Custom encryption configuration (e.g., Cloud KMS keys) or :data:`None`

if using default encryption.

### dry_run

bool: :data:`True`

if this query should be a dry run to estimate
costs.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfiguration.FIELDS.dry_run](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfiguration.FIELDS.dry_run)

### flatten_results

bool: Flatten nested/repeated fields in results. (Legacy SQL only)

### job_timeout_ms

Optional parameter. Job timeout in milliseconds. If this time limit is exceeded, BigQuery might attempt to stop the job.
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfiguration.FIELDS.job_timeout_ms](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfiguration.FIELDS.job_timeout_ms)
e.g.

```
job_config = bigquery.QueryJobConfig( job_timeout_ms = 5000 )
or
job_config.job_timeout_ms = 5000
```


Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `value` type is invalid. |

### labels

Dict[str, str]: Labels for the job.

This method always returns a dict. Once a job has been created on the server, its labels cannot be modified anymore.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `value` type is invalid. |

### max_slots

The maximum rate of slot consumption to allow for this job.

If set, the number of slots used to execute the job will be throttled to try and keep its slot consumption below the requested rate. This feature is not generally available.

### maximum_billing_tier

int: Deprecated. Changes the billing tier to allow high-compute queries.

### maximum_bytes_billed

int: Maximum bytes to be billed for this job or :data:`None`

if not set.

### priority

[google.cloud.bigquery.job.QueryPriority](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPriority): Priority of the query.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationQuery.FIELDS.priority](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationQuery.FIELDS.priority)

### query_parameters

List[Union[[google.cloud.bigquery.query.ArrayQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter), [google.cloud.bigquery.query.ScalarQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameter), [google.cloud.bigquery.query.StructQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter)]]: list of parameters
for parameterized query (empty by default)

### range_partitioning

Optional[[google.cloud.bigquery.table.RangePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning)]:
Configures range-based partitioning for destination table.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### reservation

str: Optional. The reservation that job would use.

User can specify a reservation to execute the job. If reservation is not set, reservation is determined based on the rules defined by the reservation assignments. The expected format is projects/{project}/locations/{location}/reservations/{reservation}.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `value` type is not None or of string type. |

### schema_update_options

List[[google.cloud.bigquery.job.SchemaUpdateOption](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SchemaUpdateOption)]: Specifies
updates to the destination table schema to allow as a side effect of
the query job.

### script_options

Options controlling the execution of scripts.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#scriptoptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#scriptoptions)

### table_definitions

Dict[str, [google.cloud.bigquery.external_config.ExternalConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig)]:
Definitions for external tables or :data:`None`

if not set.

### time_partitioning

Optional[[google.cloud.bigquery.table.TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning)]: Specifies
time-based partitioning for the destination table.

Only specify at most one of xref_time_partitioning or xref_range_partitioning.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### udf_resources

List[[google.cloud.bigquery.query.UDFResource](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.UDFResource)]: user
defined function resources (empty by default)

### use_legacy_sql

bool: Use legacy SQL syntax.

### use_query_cache

bool: Look for the query result in the cache.

### write_disposition

[google.cloud.bigquery.job.WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition): Action that occurs if
the destination table already exists.

### write_incremental_results

This is only supported for a SELECT query using a temporary table.

If set, the query is allowed to write results incrementally to the temporary result table. This may incur a performance penalty. This option cannot be used with Legacy SQL.

This feature is not generally available.

## Methods

### __setattr__

`__setattr__(name, value)`


Override to be able to raise error if an unknown property is being set

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.base._JobConfig`


Factory: construct a job configuration given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
A job configuration in the same representation as is returned from the API. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job._JobConfig` |
Configuration parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of the query job config.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
A dictionary in the format used by the BigQuery API. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter -->

# Class StructQueryParameter (3.40.0)

`StructQueryParameter(name, *sub_params)`


Name / positional query parameters for struct values.

## Parameter |
|
|---|---|
Name |
Description |
`name` |
`Optional[str]`
Parameter name, used via |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.StructQueryParameter`


Factory: construct parameter from JSON resource.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON mapping of parameter |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.StructQueryParameter` |
Instance |

### positional

`positional(*sub_params)`


Factory for positional parameters.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.StructQueryParameter` |
Instance without name |

### to_api_repr

`to_api_repr() -> dict`


Construct JSON API representation for the parameter.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeFileFormat -->

# Class BigLakeFileFormat (3.40.0)

`BigLakeFileFormat()`


API documentation for `bigquery.enums.BigLakeFileFormat`

class.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.QueryApiMethod -->

# Class QueryApiMethod (3.40.0)

`QueryApiMethod(value)`


API method used to start the query. The default value is
`INSERT`

.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsResponse -->

# Class ListModelsResponse (3.40.0)

`ListModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`models` |
`Sequence[`
Models in the requested dataset. Only the following fields are populated: model_reference, model_type, creation_time, last_modified_time and labels. |
`next_page_token` |
`str`
A token to request the next page of results. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeTableFormat -->

# Class BigLakeTableFormat (3.40.0)

`BigLakeTableFormat()`


API documentation for `bigquery.enums.BigLakeTableFormat`

class.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DataFrequency -->

# Class DataFrequency (3.40.0)

`DataFrequency(value)`


Type of supported data frequency for time series forecasting models.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DataSplitMethod -->

# Class DataSplitMethod (3.40.0)

`DataSplitMethod(value)`


Indicates the method to split input data into multiple tables.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.FeedbackType -->

# Class FeedbackType (3.40.0)

`FeedbackType(value)`


Indicates the training algorithm to use for matrix factorization models.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.HolidayRegion -->

# Class HolidayRegion (3.40.0)

`HolidayRegion(value)`


Type of supported holiday regions for time series forecasting models.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.LearnRateStrategy -->

# Class LearnRateStrategy (3.40.0)

`LearnRateStrategy(value)`


Indicates the learning rate optimization strategy to use.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SqlTypeNames -->

# Class SqlTypeNames (3.40.0)

`SqlTypeNames(value)`


Enum of allowed SQL type names in schema.SchemaField.

Datatype used in Legacy SQL.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.SqlParameterScalarTypes -->

# Class SqlParameterScalarTypes (3.40.0)

`SqlParameterScalarTypes()`


Supported scalar SQL query parameter types as type objects.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types -->

# Package types (3.40.0)

API documentation for `bigquery_v2.types`

package.

## Classes

[DeleteModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.DeleteModelRequest)

[EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.EncryptionConfiguration)

[GetModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.GetModelRequest)

[ListModelsRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsRequest)

[ListModelsResponse](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsResponse)

[Model](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model)

[ModelReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ModelReference)

Id path of a model.

[PatchModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.PatchModelRequest)

[StandardSqlDataType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType)

The type of a variable, e.g., a function argument. Examples: INT64: {type_kind="INT64"} ARRAY: {type_kind="ARRAY", array_element_type="STRING"} STRUCT<x STRING, y ARRAY>: {type_kind="STRUCT", struct_type={fields=[ {name="x", type={type_kind="STRING"}}, {name="y", type={type_kind="ARRAY", array_element_type="DATE"}} ]}}

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[StandardSqlField](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlField)

A field or a column.

[StandardSqlStructType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlStructType)

[StandardSqlTableType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlTableType)

A table type

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Project -->

# Class Project (3.40.0)

`Project(project_id, numeric_id, friendly_name)`


Wrapper for resource describing a BigQuery project.

## Parameters |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Opaque ID of the project |
`numeric_id` |
`int`
Numeric ID of the project |
`friendly_name` |
`str`
Display name of the project |

## Methods

### from_api_repr

`from_api_repr(resource)`


Factory: construct an instance from a resource dict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DataSplitResult -->

# Class DataSplitResult (3.40.0)

`DataSplitResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data split result. This contains references to the training and evaluation data tables that were used to train the model.

## Attributes |
|
|---|---|
Name |
Description |
`training_table` |
Table reference of the training data after split. |
`evaluation_table` |
Table reference of the evaluation data after split. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster -->

# Class Cluster (3.40.0)

`Cluster(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message containing the information about one cluster.

## Attributes |
|
|---|---|
Name |
Description |
`centroid_id` |
`int`
Centroid id. |
`feature_values` |
`Sequence[`
Values of highly variant features for this cluster. |
`count` |
`google.protobuf.wrappers_pb2.Int64Value`
Count of training data rows that were assigned to this cluster. |

## Classes

### FeatureValue

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Representative value of a single feature within the cluster.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)
