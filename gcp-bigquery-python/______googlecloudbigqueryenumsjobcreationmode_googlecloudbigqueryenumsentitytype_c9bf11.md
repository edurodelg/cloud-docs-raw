---
merged_at: 2026-02-04T00:41:39.712146
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.JobCreationMode -->

# Class JobCreationMode (3.40.0)

`JobCreationMode()`


Documented values for Job Creation Mode.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.EntityTypes -->

# Class EntityTypes (3.40.0)

`EntityTypes(value)`


Enum of allowed entity type names in AccessEntry

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.UDFResource -->

# Class UDFResource (3.40.0)

`UDFResource(udf_type, value)`


Describe a single user-defined function (UDF) resource.

## Parameters |
|
|---|---|
Name |
Description |
`udf_type` |
`str`
The type of the resource ('inlineCode' or 'resourceUri') |
`value` |
`str See: https://cloud.google.com/bigquery/user-defined-functions#api`
The inline code or resource URI. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.LossType -->

# Class LossType (3.40.0)

`LossType(value)`


Loss metric to evaluate model training performance.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.NotSupportedError -->

# Class NotSupportedError (3.40.0)

DB-API error for operations not supported by the database or API.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.GetModelRequest -->

# Class GetModelRequest (3.40.0)

`GetModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project ID of the requested model. |
`dataset_id` |
`str`
Required. Dataset ID of the requested model. |
`model_id` |
`str`
Required. Model ID of the requested model. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaOrder -->

# Class ArimaOrder (3.40.0)

`ArimaOrder(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima order, can be used for both non-seasonal and seasonal parts.

## Attributes |
|
|---|---|
Name |
Description |
`p` |
`int`
Order of the autoregressive part. |
`d` |
`int`
Order of the differencing part. |
`q` |
`int`
Order of the moving-average part. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes -->

# Class DefaultPandasDTypes (3.40.0)

`DefaultPandasDTypes(value)`


Default Pandas DataFrem DTypes to convert BigQuery data. These
Sentinel values are used instead of None to maintain backward compatibility,
and allow Pandas package is not available. For more information:
[https://stackoverflow.com/a/60605919/101923](https://stackoverflow.com/a/60605919/101923)

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty -->

# Class ConnectionProperty (3.40.0)

`ConnectionProperty(key: str = "", value: str = "")`


A connection-level property to customize query behavior.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty](https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty)

## Parameters |
|
|---|---|
Name |
Description |
`key` |
`str`
The key of the property to set, for example, |
`value` |
`str`
The value of the property to set. |

## Properties

### key

Name of the property.

For example:

`time_zone`

`session_id`


### value

Value of the property.

## Methods

### from_api_repr

`from_api_repr(resource) -> google.cloud.bigquery.query.ConnectionProperty`


Construct xref_ConnectionProperty from JSON resource.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct JSON API representation for the connection property.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry -->

# Class QueryPlanEntry (3.40.0)

`QueryPlanEntry()`


QueryPlanEntry represents a single stage of a query execution plan.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage)
for the underlying API representation within query statistics.

## Properties

### completed_parallel_inputs

Optional[int]: Number of parallel input segments completed.

### compute_ms_avg

Optional[int]: Milliseconds the average worker spent on CPU-bound processing.

### compute_ms_max

Optional[int]: Milliseconds the slowest worker spent on CPU-bound processing.

### compute_ratio_avg

Optional[float]: Ratio of time the average worker spent on CPU-bound processing, relative to the longest time spent by any worker in any stage of the overall plan.

### compute_ratio_max

Optional[float]: Ratio of time the slowest worker spent on CPU-bound processing, relative to the longest time spent by any worker in any stage of the overall plan.

### end

Optional[Datetime]: Datetime when the stage ended.

### entry_id

Optional[str]: Unique ID for the stage within the plan.

### input_stages

List(int): Entry IDs for stages that were inputs for this stage.

### name

Optional[str]: Human-readable name of the stage.

### parallel_inputs

Optional[int]: Number of parallel input segments within the stage.

### read_ms_avg

Optional[int]: Milliseconds the average worker spent reading input.

### read_ms_max

Optional[int]: Milliseconds the slowest worker spent reading input.

### read_ratio_avg

Optional[float]: Ratio of time the average worker spent reading input, relative to the longest time spent by any worker in any stage of the overall plan.

### read_ratio_max

Optional[float]: Ratio of time the slowest worker spent reading to be scheduled, relative to the longest time spent by any worker in any stage of the overall plan.

### records_read

Optional[int]: Number of records read by this stage.

### records_written

Optional[int]: Number of records written by this stage.

### shuffle_output_bytes

Optional[int]: Number of bytes written by this stage to intermediate shuffle.

### shuffle_output_bytes_spilled

Optional[int]: Number of bytes written by this stage to intermediate shuffle and spilled to disk.

### slot_ms

Optional[int]: Slot-milliseconds used by the stage.

### start

Optional[Datetime]: Datetime when the stage started.

### status

Optional[str]: status of this stage.

### steps

List(QueryPlanEntryStep): List of step operations performed by each worker in the stage.

### wait_ms_avg

Optional[int]: Milliseconds the average worker spent waiting to be scheduled.

### wait_ms_max

Optional[int]: Milliseconds the slowest worker spent waiting to be scheduled.

### wait_ratio_avg

Optional[float]: Ratio of time the average worker spent waiting to be scheduled, relative to the longest time spent by any worker in any stage of the overall plan.

### wait_ratio_max

Optional[float]: Ratio of time the slowest worker spent waiting to be scheduled, relative to the longest time spent by any worker in any stage of the overall plan.

### write_ms_avg

Optional[int]: Milliseconds the average worker spent writing output data.

### write_ms_max

Optional[int]: Milliseconds the slowest worker spent writing output data.

### write_ratio_avg

Optional[float]: Ratio of time the average worker spent writing output data, relative to the longest time spent by any worker in any stage of the overall plan.

### write_ratio_max

Optional[float]: Ratio of time the slowest worker spent writing output data, relative to the longest time spent by any worker in any stage of the overall plan.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.query.QueryPlanEntry`


Factory: construct instance from the JSON repr.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job.QueryPlanEntry` |
Query plan entry parsed from `resource` . |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn -->

# Class BigtableColumn (3.40.0)

`BigtableColumn()`


Options for a Bigtable column.

## Properties

### encoding

str: The encoding of the values when the type is not `STRING`


See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.encoding](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.encoding)

### field_name

str: An identifier to use if the qualifier is not a valid BigQuery field identifier

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.field_name](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.field_name)

### only_read_latest

bool: If this is set, only the latest version of value in this column are exposed.

### qualifier_encoded

Union[str, bytes]: The qualifier encoded in binary.

The type is `str`

(Python 2.x) or `bytes`

(Python 3.x). The module
will handle base64 encoding for you.

### qualifier_string

str: A valid UTF-8 string qualifier

### type_

str: The type to convert the value in cells of this column.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.type](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.type)

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableColumn
```


Factory: construct a `.external_config.BigtableColumn`

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
`external_config.BigtableColumn` |
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.UpdateMode -->

# Class UpdateMode (3.40.0)

`UpdateMode(value)`


Specifies the kind of information to update in a dataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DatasetView -->

# Class DatasetView (3.40.0)

`DatasetView(value)`


DatasetView specifies which dataset information is returned.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.DeleteModelRequest -->

# Class DeleteModelRequest (3.40.0)

`DeleteModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project ID of the model to delete. |
`dataset_id` |
`str`
Required. Dataset ID of the model to delete. |
`model_id` |
`str`
Required. Model ID of the model to delete. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.FieldElementType -->

# Class FieldElementType (3.40.0)

`FieldElementType(element_type: str)`


Represents the type of a field element.

## Parameter |
|
|---|---|
Name |
Description |
`element_type` |
`str`
The type of a field element. |

## Methods

### from_api_repr

```
from_api_repr(
api_repr: typing.Optional[dict],
) -> typing.Optional[google.cloud.bigquery.schema.FieldElementType]
```


Factory: construct a FieldElementType given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Dict[str, str]`
field element type as returned from |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.FieldElementType` |
Python object, as parsed from `api_repr` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this field element type.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, str]` |
Field element type represented as an API resource. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField -->

# Class SchemaField (3.40.0)

```
SchemaField(
name: str,
field_type: str,
mode: str = "NULLABLE",
default_value_expression: typing.Optional[str] = None,
description: typing.Union[
str, google.cloud.bigquery.schema._DefaultSentinel
] = _DefaultSentinel.DEFAULT_VALUE,
fields: typing.Iterable[google.cloud.bigquery.schema.SchemaField] = (),
policy_tags: typing.Union[
google.cloud.bigquery.schema.PolicyTagList,
None,
google.cloud.bigquery.schema._DefaultSentinel,
] = _DefaultSentinel.DEFAULT_VALUE,
precision: typing.Union[
int, google.cloud.bigquery.schema._DefaultSentinel
] = _DefaultSentinel.DEFAULT_VALUE,
scale: typing.Union[
int, google.cloud.bigquery.schema._DefaultSentinel
] = _DefaultSentinel.DEFAULT_VALUE,
max_length: typing.Union[
int, google.cloud.bigquery.schema._DefaultSentinel
] = _DefaultSentinel.DEFAULT_VALUE,
range_element_type: typing.Optional[
typing.Union[google.cloud.bigquery.schema.FieldElementType, str]
] = None,
rounding_mode: typing.Optional[
typing.Union[google.cloud.bigquery.enums.RoundingMode, str]
] = None,
foreign_type_definition: typing.Optional[str] = None,
timestamp_precision: typing.Optional[
google.cloud.bigquery.enums.TimestampPrecision
] = None,
)
```


Describe a single field within a table schema.

## Properties

### default_value_expression

Optional[str] default value of a field, using an SQL expression

### description

Optional[str]: description for the field.

### field_type

str: The type of the field.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#TableFieldSchema.FIELDS.type](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#TableFieldSchema.FIELDS.type)

### fields

Optional[tuple]: Subfields contained in this field.

Must be empty unset if `field_type`

is not 'RECORD'.

### foreign_type_definition

Definition of the foreign data type.

Only valid for top-level schema fields (not nested fields). If the type is FOREIGN, this field is required.

### is_nullable

bool: whether 'mode' is 'nullable'.

### max_length

Optional[int]: Maximum length for the STRING or BYTES field.

### mode

Optional[str]: The mode of the field.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#TableFieldSchema.FIELDS.mode](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#TableFieldSchema.FIELDS.mode)

### name

str: The name of the field.

### policy_tags

Optional[[google.cloud.bigquery.schema.PolicyTagList](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.PolicyTagList)]: Policy tag list
definition for this field.

### precision

Optional[int]: Precision (number of digits) for the NUMERIC field.

### range_element_type

Optional[FieldElementType]: The subtype of the RANGE, if the type of this field is RANGE.

Must be set when `type`

is `"RANGE"`

. Must be one of `"DATE"`

,
`"DATETIME"`

or `"TIMESTAMP"`

.

### rounding_mode

Enum that specifies the rounding mode to be used when storing values of NUMERIC and BIGNUMERIC type.

### scale

Optional[int]: Scale (digits after decimal) for the NUMERIC field.

### timestamp_precision

Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.

Returns |
|
|---|---|
Type |
Description |
`enums.TimestampPrecision` |
value of TimestampPrecision. |

## Methods

### from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.schema.SchemaField`


Return a `SchemaField`

object deserialized from a dictionary.

Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`dict`
The serialized representation of the SchemaField, such as what is output by |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.schema.SchemaField` |
The `SchemaField` object. |

### to_api_repr

`to_api_repr() -> dict`


Return a dictionary representing this schema field.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
A dictionary representing the SchemaField in a serialized form. |

### to_standard_sql

`to_standard_sql() -> google.cloud.bigquery.standard_sql.StandardSqlField`


Return the field as the standard SQL field representation object.
