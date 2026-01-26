---
merged_at: 2026-01-26T21:00:49.245080
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine -->

# Package routine (3.40.0)

API documentation for `bigquery.routine`

package.

## Classes

[DeterminismLevel](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.DeterminismLevel)

Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)

[ExternalRuntimeOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions)

Options for the runtime of the external system.

[RemoteFunctionOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions)

Configuration options for controlling remote BigQuery functions.

[Routine](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine)

Resource representing a user-defined routine.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines)

[RoutineArgument](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument)

Input/output argument of a function or a stored procedure.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#argument](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#argument)

[RoutineReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference)

A pointer to a routine.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference)

[RoutineType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineType)

The fine-grained type of the routine.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinetype](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinetype)

.. versionadded:: 2.22.0

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem -->

# Class DatasetListItem (3.40.0)

`DatasetListItem(resource)`


A read-only dataset resource from a list operation.

For performance reasons, the BigQuery API only includes some of the dataset properties when listing datasets. Notably, xref_access_entries is missing.

For a full list of the properties that the BigQuery API returns, see the
```
REST documentation for datasets.list
<https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/list>
```

_.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, str]`
A dataset-like resource object from a dataset list response. A |

## Properties

### dataset_id

str: Dataset ID.

### friendly_name

Union[str, None]: Title of the dataset as set by the user
(defaults to :data:`None`

).

### full_dataset_id

Union[str, None]: ID for the dataset resource (:data:`None`

until
set from the server)

In the format `project_id:dataset_id`

.

### labels

Dict[str, str]: Labels for the dataset.

### project

str: Project bound to the dataset.

### reference

[google.cloud.bigquery.dataset.DatasetReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference): A reference to this
dataset.

## Methods

### model

`model(model_id)`


Constructs a ModelReference.

Parameter |
|
|---|---|
Name |
Description |
`model_id` |
`str`
the ID of the model. |

Returns |
|
|---|---|
Type |
Description |
|
A ModelReference for a model in this dataset. |

### routine

`routine(routine_id)`


Constructs a RoutineReference.

Parameter |
|
|---|---|
Name |
Description |
`routine_id` |
`str`
the ID of the routine. |

Returns |
|
|---|---|
Type |
Description |
|
A RoutineReference for a routine in this dataset. |

### table

`table(table_id: str) -> google.cloud.bigquery.table.TableReference`


Constructs a TableReference.

Parameter |
|
|---|---|
Name |
Description |
`table_id` |
`str`
The ID of the table. |

Returns |
|
|---|---|
Type |
Description |
|
A table reference for a table in this dataset. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.StreamingBuffer -->

# Class StreamingBuffer (3.40.0)

`StreamingBuffer(resource)`


Information about a table's streaming buffer.

See [https://cloud.google.com/bigquery/streaming-data-into-bigquery](https://cloud.google.com/bigquery/streaming-data-into-bigquery).

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
streaming buffer representation returned from the API |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.AutoRowIDs -->

# Class AutoRowIDs (3.40.0)

`AutoRowIDs(value)`


How to handle automatic insert IDs when inserting rows as a stream.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPriority -->

# Class QueryPriority (3.40.0)

`QueryPriority()`


Specifies a priority for the query. The default value is
`INTERACTIVE`

.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.AvroOptions -->

# Class AvroOptions (3.40.0)

`AvroOptions()`


Options if source format is set to AVRO.

## Properties

### use_avro_logical_types

[Optional] If sourceFormat is set to 'AVRO', indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER).

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, bool],
) -> google.cloud.bigquery.format_options.AvroOptions
```


Factory: construct an instance from a resource dict.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, bool]`
Definition of a |

Returns |
|
|---|---|
Type |
Description |
|
Configuration parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, bool]` |
A dictionary in the format used by the BigQuery API. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration -->

# Class BigLakeConfiguration (3.40.0)

```
BigLakeConfiguration(
connection_id: typing.Optional[str] = None,
storage_uri: typing.Optional[str] = None,
file_format: typing.Optional[str] = None,
table_format: typing.Optional[str] = None,
_properties: typing.Optional[dict] = None,
)
```


Configuration for managed tables for Apache Iceberg, formerly known as BigLake.

## Parameters |
|
|---|---|
Name |
Description |
`connection_id` |
`Optional[str]`
The connection specifying the credentials to be used to read and write to external storage, such as Cloud Storage. The connection_id can have the form |
`storage_uri` |
`Optional[str]`
The fully qualified location prefix of the external folder where table data is stored. The '*' wildcard character is not allowed. The URI should be in the format |
`file_format` |
`Optional[str]`
The file format the table data is stored in. See BigLakeFileFormat for available values. |
`table_format` |
`Optional[str]`
The table format the metadata only snapshots are stored in. See BigLakeTableFormat for available values. |
`_properties` |
`Optional[dict]`
Private. Used to construct object from API resource. |

## Properties

### connection_id

str: The connection specifying the credentials to be used to read and write to external storage, such as Cloud Storage.

### file_format

str: The file format the table data is stored in. See BigLakeFileFormat for available values.

### storage_uri

str: The fully qualified location prefix of the external folder where table data is stored.

### table_format

str: The table format the metadata only snapshots are stored in. See BigLakeTableFormat for available values.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.table.BigLakeConfiguration
```


Factory: construct a BigLakeConfiguration given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this BigLakeConfiguration.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema -->

# Module schema (3.40.0)

Schemas for BigQuery tables / queries.

## Classes

[FieldElementType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.FieldElementType)

`FieldElementType(element_type: str)`


Represents the type of a field element.

Parameter |
|
|---|---|
Name |
Description |
`element_type` |
`str`
The type of a field element. |

[ForeignTypeInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.ForeignTypeInfo)

`ForeignTypeInfo(type_system: typing.Optional[str] = None)`


Metadata about the foreign data type definition such as the system in which the type is defined.

Parameter |
|
|---|---|
Name |
Description |
`type_system` |
`str`
Required. Specifies the system which defines the foreign data type. TypeSystem enum currently includes: * "TYPE_SYSTEM_UNSPECIFIED" * "HIVE" |

[PolicyTagList](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.PolicyTagList)

`PolicyTagList(names: typing.Iterable[str] = ())`


Define Policy Tags for a column.

[SchemaField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField)

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

[SerDeInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SerDeInfo)

```
SerDeInfo(
serialization_library: str,
name: typing.Optional[str] = None,
parameters: typing.Optional[dict[str, str]] = None,
)
```


Serializer and deserializer information.

Parameters |
|
|---|---|
Name |
Description |
`serialization_library` |
`str`
Required. Specifies a fully-qualified class name of the serialization library that is responsible for the translation of data between table representation and the underlying low-level input and output format structures. The maximum length is 256 characters. |
`name` |
`Optional[str]`
Name of the SerDe. The maximum length is 256 characters. |

[StorageDescriptor](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.StorageDescriptor)

```
StorageDescriptor(
input_format: typing.Optional[str] = None,
location_uri: typing.Optional[str] = None,
output_format: typing.Optional[str] = None,
serde_info: typing.Optional[
typing.Union[google.cloud.bigquery.schema.SerDeInfo, dict]
] = None,
)
```


Contains information about how a table's data is stored and accessed by open source query engines.

Parameters |
|
|---|---|
Name |
Description |
`input_format` |
`Optional[str]`
Specifies the fully qualified class name of the InputFormat (e.g. "org.apache.hadoop.hive.ql.io.orc.OrcInputFormat"). The maximum length is 128 characters. |
`location_uri` |
`Optional[str]`
The physical location of the table (e.g. 'gs://spark-dataproc-data/pangea-data/case_sensitive/' or 'gs://spark-dataproc-data/pangea-data/'). The maximum length is 2056 bytes. |
`output_format` |
`Optional[str]`
Specifies the fully qualified class name of the OutputFormat (e.g. "org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat"). The maximum length is 128 characters. |
`serde_info` |
`Union[SerDeInfo, dict, None]`
Serializer and deserializer information. |
