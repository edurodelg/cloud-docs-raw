---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField
fetched_at: 2026-01-25T03:17:27.778888
---

# Class SchemaField (3.40.0)


      
      Save and categorize content based on your preferences.

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