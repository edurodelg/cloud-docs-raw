---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig
fetched_at: 2026-01-25T03:15:32.249365
---

# Class QueryJobConfig (3.40.0)


      
      Save and categorize content based on your preferences.

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