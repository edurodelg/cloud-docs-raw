---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job
fetched_at: 2026-01-25T02:08:13.919493
---

# Package job (3.40.0)


      
      Save and categorize content based on your preferences.

API documentation for `bigquery.job`

package.

## Classes

[Compression](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Compression)

The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.

[CopyJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob)

Asynchronous job: copy data into a table from other tables.

[CopyJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig)

Configuration options for copy jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

[CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition)

Specifies whether the job is allowed to create new tables. The default
value is `CREATE_IF_NEEDED`

.

Creation, truncation and append actions occur as one atomic update upon job completion.

[DestinationFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DestinationFormat)

The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.

[DmlStats](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats)

Detailed statistics for DML statements.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats](https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats)

[Encoding](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Encoding)

The character encoding of the data. The default is `UTF_8`

.

BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.

[ExtractJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob)

Asynchronous job: extract data from a table into Cloud Storage.

[ExtractJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig)

Configuration options for extract jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

[IncrementalResultStats](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.IncrementalResultStats)

IncrementalResultStats provides information about incremental query execution.

[LoadJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob)

Asynchronous job for loading data into a table.

Can load from Google Cloud Storage URIs or from a file.

[LoadJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig)

Configuration options for load jobs.

Set properties on the constructed configuration by using the property name
as the name of a keyword argument. Values which are unset or :data:`None`

use the BigQuery REST API default values. See the ```
BigQuery REST API
reference documentation
<https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad>
```

_
for a list of default values.

Required options differ based on the
[source_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) value.
For example, the BigQuery API's default value for
[source_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) is `"CSV"`

.
When loading a CSV file, either
[schema](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) must be set or
[autodetect](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) must be set to
:data:`True`

.

[OperationType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.OperationType)

Different operation types supported in table copy job.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#operationtype](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#operationtype)

[QueryJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob)

Asynchronous job: query tables.

[QueryJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig)

Configuration options for query jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

[QueryPlanEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry)

QueryPlanEntry represents a single stage of a query execution plan.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage)
for the underlying API representation within query statistics.

[QueryPlanEntryStep](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntryStep)

Map a single step in a query plan entry.

[QueryPriority](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPriority)

Specifies a priority for the query. The default value is
`INTERACTIVE`

.

[ReservationUsage](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ReservationUsage)

Job resource usage for a reservation.

[SchemaUpdateOption](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SchemaUpdateOption)

Specifies an update to the destination table schema as a side effect of a load job.

[ScriptOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptOptions)

Options controlling the execution of scripts.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions)

[ScriptStackFrame](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame)

Stack frame showing the line/column/procedure name where the current evaluation happened.

[ScriptStatistics](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStatistics)

Statistics for a child job of a script.

[SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat)

The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)).

[TimelineEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry)

TimelineEntry represents progress of a query job at a particular point in time.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#querytimelinesample](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#querytimelinesample)
for the underlying API representation within query statistics.

[TransactionInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TransactionInfo)

[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

.. versionadded:: 2.24.0

[UnknownJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob)

A job whose type cannot be determined.

[WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition)

Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.