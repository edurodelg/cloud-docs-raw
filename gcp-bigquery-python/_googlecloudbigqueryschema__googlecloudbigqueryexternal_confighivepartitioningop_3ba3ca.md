---
merged_at: 2026-01-25T15:38:56.562277
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryschema.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema -->

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


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryexternal_confighivepartitioningoptions_googlecloudbigqueryro_7d3500.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_confighivepartitioningoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.HivePartitioningOptions -->

# Class HivePartitioningOptions (3.40.0)

`HivePartitioningOptions()`


Options that configure hive partitioning.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions)

## Properties

### mode

Optional[str]: When set, what mode of hive partitioning to use when reading data.

Two modes are supported: "AUTO" and "STRINGS".

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode)

### require_partition_filter

Optional[bool]: If set to true, queries over the partitioned table require a partition filter that can be used for partition elimination to be specified.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode)

### source_uri_prefix

Optional[str]: When hive partition detection is requested, a common prefix for all source URIs is required.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.HivePartitioningOptions
```


Factory: construct a `.external_config.HivePartitioningOptions`

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
`HivePartitioningOptions` |
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

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryroutineremotefunctionoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions -->

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
