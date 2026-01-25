---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema
fetched_at: 2026-01-25T02:11:00.411754
---

# Module schema (3.40.0)


      
      Save and categorize content based on your preferences.

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