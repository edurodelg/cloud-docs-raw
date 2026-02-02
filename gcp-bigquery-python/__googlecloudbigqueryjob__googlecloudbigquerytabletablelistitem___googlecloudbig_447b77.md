---
merged_at: 2026-02-02T16:19:10.362312
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job -->

# Package job (3.40.0)

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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem -->

# Class TableListItem (3.40.0)

`TableListItem(resource)`


A read-only table resource from a list operation.

For performance reasons, the BigQuery API only includes some of the table properties when listing tables. Notably, xref_schema and xref_num_rows are missing.

For a full list of the properties that the BigQuery API returns, see the
```
REST documentation for tables.list
<https://cloud.google.com/bigquery/docs/reference/rest/v2/tables/list>
```

_.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
A table-like resource object from a table list response. A |

## Properties

### clustering_fields

Union[List[str], None]: Fields defining clustering for the table

(Defaults to :data:`None`

).

Clustering fields are immutable after table creation.

### created

Union[datetime.datetime, None]: Datetime at which the table was
created (:data:`None`

until set from the server).

### expires

Union[datetime.datetime, None]: Datetime at which the table will be deleted.

### friendly_name

Union[str, None]: Title of the table (defaults to :data:`None`

).

### full_table_id

Union[str, None]: ID for the table (:data:`None`

until set from the
server).

In the format `project_id:dataset_id.table_id`

.

### labels

Dict[str, str]: Labels for the table.

This method always returns a dict. To change a table's labels,
modify the dict, then call `Client.update_table`

. To delete a
label, set its value to :data:`None`

before updating.

### partition_expiration

Union[int, None]: Expiration time in milliseconds for a partition.

If this property is set and `type_`

is not set, `type_`

will default to `TimePartitioningType.DAY`

.

### partitioning_type

Union[str, None]: Time partitioning of the table if it is
partitioned (Defaults to :data:`None`

).

### reference

A xref_TableReference pointing to this table.

Returns |
|
|---|---|
Type |
Description |
|
pointer to this table. |

### table_type

Union[str, None]: The type of the table (:data:`None`

until set from
the server).

Possible values are `'TABLE'`

, `'VIEW'`

, or `'EXTERNAL'`

.

### time_partitioning

[google.cloud.bigquery.table.TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning): Configures time-based
partitioning for a table.

### view_use_legacy_sql

bool: Specifies whether to execute the view with Legacy or Standard SQL.

This boolean specifies whether to execute the view with Legacy SQL
(:data:`True`

) or Standard SQL (:data:`False`

). The client side default is
:data:`False`

. The server-side default is :data:`True`

. If this table is
not a view, :data:`None`

is returned.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
For invalid value types. |

## Methods

### from_string

`from_string(full_table_id: str) -> google.cloud.bigquery.table.TableListItem`


Construct a table from fully-qualified table ID.

Parameter |
|
|---|---|
Name |
Description |
`full_table_id` |
`str`
A fully-qualified table ID in standard SQL format. Must included a project ID, dataset ID, and table ID, each separated by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `full_table_id` is not a fully-qualified table ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`Table .. rubric:: Examples >>> Table.from_string('my-project.mydataset.mytable') Table(TableRef...(D...('my-project', 'mydataset'), 'mytable'))` |
Table parsed from `full_table_id` . |

### to_api_repr

`to_api_repr() -> dict`


Constructs the API resource of this table

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Table represented as an API resource |

### to_bqstorage

`to_bqstorage() -> str`


Construct a BigQuery Storage API representation of this table.

Returns |
|
|---|---|
Type |
Description |
`str` |
A reference to this table in the BigQuery Storage API. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning -->

# Class RangePartitioning (3.40.0)

`RangePartitioning(range_=None, field=None, _properties=None)`


Range-based partitioning configuration for a table.

## Parameters |
|
|---|---|
Name |
Description |
`range_` |
`Optional[`
Sets the range_ property. |
`field` |
`Optional[str]`
Sets the |
`_properties` |
`Optional[dict]`
Private. Used to construct object from API resource. |

## Properties

### field

str: The table is partitioned by this field.

The field must be a top-level `NULLABLE`

/ `REQUIRED`

field. The
only supported type is `INTEGER`

/ `INT64`

.

### range_

[google.cloud.bigquery.table.PartitionRange](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PartitionRange): Defines the
ranges for range partitioning.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not a `PartitionRange` . |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult -->

# Class ArimaResult (3.40.0)

`ArimaResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


(Auto-)arima fitting result. Wrap everything in ArimaResult for easier refactoring if we want to use model-specific iteration results.

## Attributes |
|
|---|---|
Name |
Description |
`arima_model_info` |
`Sequence[`
This message is repeated because there are multiple arima models fitted in auto-arima. For non-auto-arima model, its size is one. |
`seasonal_periods` |
`Sequence[`
Seasonal periods. Repeated because multiple periods are supported for one time series. |

## Classes

### ArimaCoefficients

`ArimaCoefficients(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima coefficients.

### ArimaModelInfo

`ArimaModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima model information.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions -->

# Class RemoteFunctionOptions (3.40.0)

```
RemoteFunctionOptions(
endpoint=None,
connection=None,
max_batching_rows=None,
user_defined_context=None,
_properties=None,
)
```


Configuration options for controlling remote BigQuery functions.

## Properties

### connection

string: Fully qualified name of the user-provided connection object which holds the authentication information to send requests to the remote service.

Format is "projects/{projectId}/locations/{locationId}/connections/{connectionId}"

### endpoint

string: Endpoint of the user-provided remote service

Example: "[https://us-east1-my_gcf_project.cloudfunctions.net/remote_add](https://us-east1-my_gcf_project.cloudfunctions.net/remote_add)"

### max_batching_rows

int64: Max number of rows in each batch sent to the remote service.

If absent or if 0, BigQuery dynamically decides the number of rows in a batch.

### user_defined_context

Dict[str, str]: User-defined context as a set of key/value pairs, which will be sent as function invocation context together with batched arguments in the requests to the remote service. The total number of bytes of keys and values must be less than 8KB.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RemoteFunctionOptions
```


Factory: construct remote function options given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Resource, as returned from the API. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.RemoteFunctionOptions` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this RemoteFunctionOptions.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Remote function options represented as an API resource. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/query -->

# Query Resource Classes

BigQuery query processing.

*class* google.cloud.bigquery.query.ArrayQueryParameter(name, array_type, values)

Named / positional query parameters for array values.

**Parameters****name**(*Optional**[**str**]*) – Parameter name, used via`@foo`

syntax. If None, the parameter can only be addressed via position (`?`

).**array_type**(*Union**[**str**, **ScalarQueryParameterType**, **StructQueryParameterType**]*) – The type of array elements. If given as a string, it must be one of ‘STRING’, ‘INT64’, ‘FLOAT64’, ‘NUMERIC’, ‘BIGNUMERIC’, ‘BOOL’, ‘TIMESTAMP’, ‘DATE’, or ‘STRUCT’/’RECORD’. If the type is`'STRUCT'`

/`'RECORD'`

and`values`

is empty, the exact item type cannot be deduced, thus a`StructQueryParameterType`

instance needs to be passed in.**values**(*List**[**appropriate type**]*) – The parameter array values.


*classmethod* from_api_repr(resource: [dict](https://docs.python.org/3/library/stdtypes.html#dict))

Factory: construct parameter from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.ArrayQueryParameter


*classmethod* positional(array_type: [str](https://docs.python.org/3/library/stdtypes.html#str), values: [list](https://docs.python.org/3/library/stdtypes.html#list))

Factory for positional parameters.

**Parameters****array_type**(*Union**[**str**, **ScalarQueryParameterType**, **StructQueryParameterType**]*) – The type of array elements. If given as a string, it must be one of ‘STRING’, ‘INT64’, ‘FLOAT64’, ‘NUMERIC’, ‘BIGNUMERIC’, ‘BOOL’, ‘TIMESTAMP’, ‘DATE’, or ‘STRUCT’/’RECORD’. If the type is`'STRUCT'`

/`'RECORD'`

and`values`

is empty, the exact item type cannot be deduced, thus a`StructQueryParameterType`

instance needs to be passed in.**values**(*List**[**appropriate type**]*) – The parameter array values.

**Returns**Instance without name

**Return type**google.cloud.bigquery.query.ArrayQueryParameter


#### to_api_repr()

Construct JSON API representation for the parameter.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.ArrayQueryParameterType(array_type, *, name=None, description=None)

Type representation for array query parameters.

**Parameters****array_type**(*Union**[**ScalarQueryParameterType**, **StructQueryParameterType**]*) – The type of array elements.**name**(*Optional**[**str**]*) – The name of the query parameter. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.**description**(*Optional**[**str**]*) – The query parameter description. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.


*classmethod* from_api_repr(resource)

Factory: construct parameter type from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.ArrayQueryParameterType


#### to_api_repr()

Construct JSON API representation for the parameter type.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.ConnectionProperty(key: [str](https://docs.python.org/3/library/stdtypes.html#str) = '', value: [str](https://docs.python.org/3/library/stdtypes.html#str) = '')

A connection-level property to customize query behavior.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty](https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty)

**Parameters****key**– The key of the property to set, for example,`'time_zone'`

or`'session_id'`

.**value**– The value of the property to set.


*classmethod* from_api_repr(resource)

Construct `ConnectionProperty`

from JSON resource.

**Parameters****resource**– JSON representation.**Returns**A connection property.


*property* key(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

Name of the property.

For example:

`time_zone`

`session_id`


#### to_api_repr()

Construct JSON API representation for the connection property.

**Returns**JSON mapping


*property* value(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

Value of the property.

*class* google.cloud.bigquery.query.RangeQueryParameter(range_element_type, start=None, end=None, name=None)

Named / positional query parameters for range values.

**Parameters****range_element_type**(*Union**[**str**, **RangeQueryParameterType**]*) – The type of range elements. It must be one of ‘TIMESTAMP’, ‘DATE’, or ‘DATETIME’.**start**(*Optional**[**Union**[**ScalarQueryParameter**, *[*str*](*][https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str))**]*) – The start of the range value. Must be the same type as range_element_type. If not provided, it’s interpreted as UNBOUNDED.**end**(*Optional**[**Union**[**ScalarQueryParameter**, *[*str*](*][https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str))**]*) – The end of the range value. Must be the same type as range_element_type. If not provided, it’s interpreted as UNBOUNDED.**name**(*Optional**[**str**]*) – Parameter name, used via`@foo`

syntax. If None, the parameter can only be addressed via position (`?`

).


*classmethod* from_api_repr(resource: [dict](https://docs.python.org/3/library/stdtypes.html#dict))

Factory: construct parameter from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.RangeQueryParameter


*classmethod* positional(range_element_type, start=None, end=None)

Factory for positional parameters.

**Parameters****range_element_type**(*Union**[**str**, **RangeQueryParameterType**]*) – The type of range elements. It must be one of ‘TIMESTAMP’, ‘DATE’, or ‘DATETIME’.**start**(*Optional**[**Union**[**ScalarQueryParameter**, *[*str*](*][https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str))**]*) – The start of the range value. Must be the same type as range_element_type. If not provided, it’s interpreted as UNBOUNDED.**end**(*Optional**[**Union**[**ScalarQueryParameter**, *[*str*](*][https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str))**]*) – The end of the range value. Must be the same type as range_element_type. If not provided, it’s interpreted as UNBOUNDED.

**Returns**Instance without name.

**Return type**google.cloud.bigquery.query.RangeQueryParameter


#### to_api_repr()

Construct JSON API representation for the parameter.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.RangeQueryParameterType(type_, *, name=None, description=None)

Type representation for range query parameters.

**Parameters****type**(*Union**[**ScalarQueryParameterType**, *[*str*](*]*) – Type of range element, must be one of ‘TIMESTAMP’, ‘DATETIME’, or ‘DATE’.[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str))**name**(*Optional**[**str**]*) – The name of the query parameter. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.**description**(*Optional**[**str**]*) – The query parameter description. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.


*classmethod* from_api_repr(resource)

Factory: construct parameter type from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.RangeQueryParameterType


#### to_api_repr()

Construct JSON API representation for the parameter type.

**Returns**JSON mapping

**Return type**Dict


#### with_name(new_name: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[str](https://docs.python.org/3/library/stdtypes.html#str)])

Return a copy of the instance with `name`

set to `new_name`

.

**Parameters****name**(*Union**[**str**, **None**]*) – The new name of the range query parameter type. If`None`

, the existing name is cleared.**Returns**A new instance with updated name.

**Return type**google.cloud.bigquery.query.RangeQueryParameterType


*class* google.cloud.bigquery.query.ScalarQueryParameter(name: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[str](https://docs.python.org/3/library/stdtypes.html#str)], type_: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[Union](https://docs.python.org/3/library/typing.html#typing.Union)[[str](https://docs.python.org/3/library/stdtypes.html#str), google.cloud.bigquery.query.ScalarQueryParameterType]], value: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[Union](https://docs.python.org/3/library/typing.html#typing.Union)[[str](https://docs.python.org/3/library/stdtypes.html#str), [int](https://docs.python.org/3/library/functions.html#int), [float](https://docs.python.org/3/library/functions.html#float), [decimal.Decimal](https://docs.python.org/3/library/decimal.html#decimal.Decimal), [bool](https://docs.python.org/3/library/functions.html#bool), [datetime.datetime](https://docs.python.org/3/library/datetime.html#datetime.datetime), [datetime.date](https://docs.python.org/3/library/datetime.html#datetime.date)]])

Named / positional query parameters for scalar values.

**Parameters****name**– Parameter name, used via`@foo`

syntax. If None, the parameter can only be addressed via position (`?`

).**type**– Name of parameter type. Seeand`google.cloud.bigquery.enums.SqlTypeNames`

`google.cloud.bigquery.query.SqlParameterScalarTypes`

for supported types.**value**– The scalar parameter value.


*classmethod* from_api_repr(resource: [dict](https://docs.python.org/3/library/stdtypes.html#dict))

Factory: construct parameter from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.ScalarQueryParameter


*classmethod* positional(type_: [Union](https://docs.python.org/3/library/typing.html#typing.Union)[[str](https://docs.python.org/3/library/stdtypes.html#str), google.cloud.bigquery.query.ScalarQueryParameterType], value: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[Union](https://docs.python.org/3/library/typing.html#typing.Union)[[str](https://docs.python.org/3/library/stdtypes.html#str), [int](https://docs.python.org/3/library/functions.html#int), [float](https://docs.python.org/3/library/functions.html#float), [decimal.Decimal](https://docs.python.org/3/library/decimal.html#decimal.Decimal), [bool](https://docs.python.org/3/library/functions.html#bool), [datetime.datetime](https://docs.python.org/3/library/datetime.html#datetime.datetime), [datetime.date](https://docs.python.org/3/library/datetime.html#datetime.date)]])

Factory for positional paramater.

**Parameters****type**– Name of parameter type. One of ‘STRING’, ‘INT64’, ‘FLOAT64’, ‘NUMERIC’, ‘BIGNUMERIC’, ‘BOOL’, ‘TIMESTAMP’, ‘DATETIME’, or ‘DATE’.**value**– The scalar parameter value.

**Returns**Instance without name

**Return type**google.cloud.bigquery.query.ScalarQueryParameter


#### to_api_repr()

Construct JSON API representation for the parameter.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.ScalarQueryParameterType(type_, *, name=None, description=None)

Type representation for scalar query parameters.

**Parameters****type**() – One of ‘STRING’, ‘INT64’, ‘FLOAT64’, ‘NUMERIC’, ‘BOOL’, ‘TIMESTAMP’, ‘DATETIME’, or ‘DATE’.*str***name**(*Optional**[**str**]*) – The name of the query parameter. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.**description**(*Optional**[**str**]*) – The query parameter description. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.


*classmethod* from_api_repr(resource)

Factory: construct parameter type from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.ScalarQueryParameterType


#### to_api_repr()

Construct JSON API representation for the parameter type.

**Returns**JSON mapping

**Return type**Dict


#### with_name(new_name: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[str](https://docs.python.org/3/library/stdtypes.html#str)])

Return a copy of the instance with `name`

set to `new_name`

.

**Parameters****name**(*Union**[**str**, **None**]*) – The new name of the query parameter type. If`None`

, the existing name is cleared.**Returns**A new instance with updated name.

**Return type**google.cloud.bigquery.query.ScalarQueryParameterType


*class* google.cloud.bigquery.query.SqlParameterScalarTypes()

Supported scalar SQL query parameter types as type objects.

*class* google.cloud.bigquery.query.StructQueryParameter(name, *sub_params)

Name / positional query parameters for struct values.

**Parameters****name**(*Optional**[**str**]*) – Parameter name, used via`@foo`

syntax. If None, the parameter can only be addressed via position (`?`

).**(****Union****[****Tuple****[**(*sub_params*) – google.cloud.bigquery.query.ScalarQueryParameter, google.cloud.bigquery.query.ArrayQueryParameter, google.cloud.bigquery.query.StructQueryParameter**]****]****)**– The sub-parameters for the struct


*classmethod* from_api_repr(resource: [dict](https://docs.python.org/3/library/stdtypes.html#dict))

Factory: construct parameter from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.StructQueryParameter


*classmethod* positional(*sub_params)

Factory for positional parameters.

**Parameters****(****Union****[****Tuple****[**(*sub_params*) – google.cloud.bigquery.query.ScalarQueryParameter, google.cloud.bigquery.query.ArrayQueryParameter, google.cloud.bigquery.query.StructQueryParameter**]****]****)**– The sub-parameters for the struct

**Returns**Instance without name

**Return type**google.cloud.bigquery.query.StructQueryParameter


#### to_api_repr()

Construct JSON API representation for the parameter.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.StructQueryParameterType(*fields, name=None, description=None)

Type representation for struct query parameters.

**Parameters****fields**(*Iterable**[**Union**[ **ArrayQueryParameterType**, **ScalarQueryParameterType**, **StructQueryParameterType** ]**]*) – An non-empty iterable describing the struct’s field types.**name**(*Optional**[**str**]*) – The name of the query parameter. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.**description**(*Optional**[**str**]*) – The query parameter description. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.


*classmethod* from_api_repr(resource)

Factory: construct parameter type from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.StructQueryParameterType


#### to_api_repr()

Construct JSON API representation for the parameter type.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.UDFResource(udf_type, value)

Describe a single user-defined function (UDF) resource.

**Parameters**

See:
[https://cloud.google.com/bigquery/user-defined-functions#api](https://cloud.google.com/bigquery/user-defined-functions#api)
