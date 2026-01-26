---
merged_at: 2026-01-26T21:00:49.246100
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameter -->

# Class RangeQueryParameter (3.40.0)

`RangeQueryParameter(range_element_type, start=None, end=None, name=None)`


Named / positional query parameters for range values.

## Parameters |
|
|---|---|
Name |
Description |
`range_element_type` |
`Union[str, RangeQueryParameterType]`
The type of range elements. It must be one of 'TIMESTAMP', 'DATE', or 'DATETIME'. |
`start` |
`Optional[Union[ScalarQueryParameter, str]]`
The start of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`end` |
`Optional[Union[ScalarQueryParameter, str]]`
The end of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`name` |
`Optional[str]`
Parameter name, used via |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.RangeQueryParameter`


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
`google.cloud.bigquery.query.RangeQueryParameter` |
Instance |

### positional

```
positional(
range_element_type, start=None, end=None
) -> google.cloud.bigquery.query.RangeQueryParameter
```


Factory for positional parameters.

Parameters |
|
|---|---|
Name |
Description |
`range_element_type` |
`Union[str, RangeQueryParameterType]`
The type of range elements. It must be one of |
`start` |
`Optional[Union[ScalarQueryParameter, str]]`
The start of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`end` |
`Optional[Union[ScalarQueryParameter, str]]`
The end of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.RangeQueryParameter` |
Instance without name. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference -->

# Class RoutineReference (3.40.0)

`RoutineReference()`


A pointer to a routine.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference)

## Properties

### dataset_id

str: ID of dataset containing the routine.

### path

str: URL path for the routine's APIs.

### project

str: ID of the project containing the routine.

### routine_id

str: The routine ID.

## Methods

### __eq__

`__eq__(other)`


Two RoutineReferences are equal if they point to the same routine.

### __str__

`__str__()`


String representation of the reference.

This is a fully-qualified ID, including the project ID and dataset ID.

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RoutineReference
```


Factory: construct a routine reference given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Routine reference representation returned from the API. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.RoutineReference` |
Routine reference parsed from `resource` . |

### from_string

```
from_string(
routine_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.routine.routine.RoutineReference
```


Factory: construct a routine reference from routine ID string.

Parameters |
|
|---|---|
Name |
Description |
`routine_id` |
`str`
A routine ID in standard SQL format. If |
`default_project` |
`Optional[str]`
The project ID to use when |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `routine_id` is not a fully-qualified routine ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.RoutineReference` |
Routine reference parsed from `routine_id` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine reference.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Routine reference represented as an API resource. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset -->

# Module dataset (3.40.0)

Define API Datasets.

## Classes

[AccessEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry)

```
AccessEntry(
role: typing.Optional[str] = None,
entity_type: typing.Optional[str] = None,
entity_id: typing.Optional[typing.Union[typing.Dict[str, typing.Any], str]] = None,
**kwargs
)
```


Represents grant of an access role to an entity.

An entry must have exactly one of the allowed
xref_EntityTypes. If anything but `view`

, `routine`

,
or `dataset`

are set, a `role`

is also required. `role`

is omitted for `view`

,
`routine`

, `dataset`

, because they are always read-only.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets).

Parameters |
|
|---|---|
Name |
Description |
`role` |
`typing.Optional[str]`
Role granted to the entity. The following string values are supported: |
`entity_type` |
`typing.Optional[str]`
Type of entity being granted the role. See |
`entity_id` |
`typing.Union[typing.Dict[str, typing.Any], str, NoneType]`
If the |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If a `view` , `routine` , or `dataset` has `role` set, or a non `view` , non `routine` , and non `dataset` **does not** have a `role` set. .. rubric:: Examples >>> entry = AccessEntry('OWNER', 'userByEmail', 'user@example.com') >>> view = { ... 'projectId': 'my-project', ... 'datasetId': 'my_dataset', ... 'tableId': 'my_table' ... } >>> entry = AccessEntry(None, 'view', view) |

[Condition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Condition)

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

Parameters |
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

[Dataset](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset)

`Dataset(dataset_ref)`


Datasets are containers for tables.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#resource-dataset](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#resource-dataset)

Parameter |
|
|---|---|
Name |
Description |
`dataset_ref` |
`Union[`
A pointer to a dataset. If |

[DatasetListItem](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem)

`DatasetListItem(resource)`


A read-only dataset resource from a list operation.

For performance reasons, the BigQuery API only includes some of the dataset properties when listing datasets. Notably, xref_access_entries is missing.

For a full list of the properties that the BigQuery API returns, see the
```
REST documentation for datasets.list
<https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/list>
```

_.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, str]`
A dataset-like resource object from a dataset list response. A |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `datasetReference` or one of its required members is missing from `resource` . |

[DatasetReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference)

`DatasetReference(project: str, dataset_id: str)`


DatasetReferences are pointers to datasets.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference)

Parameters |
|
|---|---|
Name |
Description |
`project` |
`str`
The ID of the project |
`dataset_id` |
`str`
The ID of the dataset |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If either argument is not of type `str` . |
