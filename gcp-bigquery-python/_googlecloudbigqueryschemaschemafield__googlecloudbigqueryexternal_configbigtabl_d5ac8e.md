---
merged_at: 2026-01-25T15:38:56.561279
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryschemaschemafield.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryexternal_configbigtablecolumnfamily_googlecloudbigqueryrouti_d909a4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_configbigtablecolumnfamily.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily -->

# Class BigtableColumnFamily (3.40.0)

`BigtableColumnFamily()`


Options for a Bigtable column family.

## Properties

### columns

List[BigtableColumn]: Lists of columns that should be exposed as individual fields.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.columns](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.columns)

### encoding

str: The encoding of the values when the type is not `STRING`


See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.encoding](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.encoding)

### family_id

str: Identifier of the column family.

### only_read_latest

bool: If this is set only the latest version of value are exposed for all columns in this column family.

### type_

str: The type to convert the value in cells of this column family.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.type](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.type)

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableColumnFamily
```


Factory: construct a `.external_config.BigtableColumnFamily`

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
`Dict[str, Any]` |
A dictionary in the format used by the BigQuery API. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryroutineroutineargument.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument -->

# Class RoutineArgument (3.40.0)

`RoutineArgument(**kwargs)`


Input/output argument of a function or a stored procedure.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#argument](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#argument)

## Parameter |
|
|---|---|
Name |
Description |
|
`Dict`
Initial property values. |

## Properties

### data_type

Optional[google.cloud.bigquery.StandardSqlDataType]: Type of a variable, e.g., a function argument.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.data_type](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.data_type)

### kind

Optional[str]: The kind of argument, for example `FIXED_TYPE`

or
`ANY_TYPE`

.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.argument_kind](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.argument_kind)

### mode

Optional[str]: The input/output mode of the argument.

### name

Optional[str]: Name of this argument.

Can be absent for function return argument.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RoutineArgument
```


Factory: construct a routine argument given its API representation.

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
`google.cloud.bigquery.routine.RoutineArgument` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine argument.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Routine argument represented as an API resource. |
