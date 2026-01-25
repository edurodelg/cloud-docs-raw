---
merged_at: 2026-01-25T15:38:56.566159
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryexternal_configexternalcatalogtableoptions_googlecloudbigque_469504.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_configexternalcatalogtableoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogTableOptions -->

# Class ExternalCatalogTableOptions (3.40.0)

```
ExternalCatalogTableOptions(
connection_id: typing.Optional[str] = None,
parameters: typing.Optional[typing.Dict[str, typing.Any]] = None,
storage_descriptor: typing.Optional[
google.cloud.bigquery.schema.StorageDescriptor
] = None,
)
```


Metadata about open source compatible table. The fields contained in these options correspond to hive metastore's table level properties.

## Parameters |
|
|---|---|
Name |
Description |
`connection_id` |
`Optional[str]`
The connection specifying the credentials to be used to read external storage, such as Azure Blob, Cloud Storage, or S3. The connection is needed to read the open source table from BigQuery Engine. The connection_id can have the form |
`parameters` |
`Union[Dict[str, Any], None]`
A map of key value pairs defining the parameters and properties of the open source table. Corresponds with hive meta store table parameters. Maximum size of 4Mib. |
`storage_descriptor` |
`Optional[StorageDescriptor]`
A storage descriptor containing information about the physical storage of this table. |

## Properties

### connection_id

Optional. The connection specifying the credentials to be
used to read external storage, such as Azure Blob, Cloud Storage, or
S3. The connection is needed to read the open source table from
BigQuery Engine. The connection_id can have the form `..`

or
`projects//locations//connections/`

.

### parameters

Optional. A map of key value pairs defining the parameters and properties of the open source table. Corresponds with hive meta store table parameters. Maximum size of 4Mib.

### storage_descriptor

Optional. A storage descriptor containing information about the physical storage of this table.

## Methods

### from_api_repr

```
from_api_repr(
api_repr: dict,
) -> google.cloud.bigquery.external_config.ExternalCatalogTableOptions
```


Factory: constructs an instance of the class (cls) given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Dict[str, Any]`
API representation of the object to be instantiated. |

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

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryschemastoragedescriptor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.StorageDescriptor -->

# Class StorageDescriptor (3.40.0)

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

## Parameters |
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

## Properties

### input_format

Optional. Specifies the fully qualified class name of the InputFormat (e.g. "org.apache.hadoop.hive.ql.io.orc.OrcInputFormat"). The maximum length is 128 characters.

### location_uri

Optional. The physical location of the table (e.g. 'gs://spark- dataproc-data/pangea-data/case_sensitive/' or 'gs://spark-dataproc- data/pangea-data/'). The maximum length is 2056 bytes.

### output_format

Optional. Specifies the fully qualified class name of the OutputFormat (e.g. "org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat"). The maximum length is 128 characters.

### serde_info

Optional. Serializer and deserializer information.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.schema.StorageDescriptor`


Factory: constructs an instance of the class (cls) given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, Any]`
API representation of the object to be instantiated. |

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

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerystandard_sqlstandardsqldatatype___googlecloudbigqueryenumsde_fab6be.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerystandard_sqlstandardsqldatatype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType -->

# Class StandardSqlDataType (3.40.0)

```
StandardSqlDataType(
type_kind: typing.Optional[
google.cloud.bigquery.enums.StandardSqlTypeNames
] = StandardSqlTypeNames.TYPE_KIND_UNSPECIFIED,
array_element_type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlDataType
] = None,
struct_type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlStructType
] = None,
range_element_type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlDataType
] = None,
)
```


The type of a variable, e.g., a function argument.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType)

Examples:

```
INT64: {type_kind="INT64"}
ARRAY: {type_kind="ARRAY", array_element_type="STRING"}
STRUCT<x STRING, y ARRAY>: {
type_kind="STRUCT",
struct_type={
fields=[
{name="x", type={type_kind="STRING"}},
{
name="y",
type={type_kind="ARRAY", array_element_type="DATE"}
}
]
}
}
RANGE: {type_kind="RANGE", range_element_type="DATETIME"}
```


## Parameters |
|
|---|---|
Name |
Description |
`type_kind` |
`typing.Optional[`
The top level type of this field. Can be any standard SQL data type, e.g. INT64, DATE, ARRAY. |
`array_element_type` |
`typing.Optional[StandardSqlDataType]`
The type of the array's elements, if type_kind is ARRAY. |
`struct_type` |
`typing.Optional[StandardSqlStructType]`
The fields of this struct, in order, if type_kind is STRUCT. |
`range_element_type` |
`typing.Optional[StandardSqlDataType]`
The type of the range's elements, if type_kind is RANGE. |

## Properties

### array_element_type

The type of the array's elements, if type_kind is ARRAY.

### range_element_type

The type of the range's elements, if type_kind = "RANGE". Must be one of DATETIME, DATE, or TIMESTAMP.

### struct_type

The fields of this struct, in order, if type_kind is STRUCT.

### type_kind

The top level type of this field.

Can be any standard SQL data type, e.g. INT64, DATE, ARRAY.

## Methods

### from_api_repr

`from_api_repr(resource: typing.Dict[str, typing.Any])`


Construct an SQL data type instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL data type.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryenumsdestinationformat_googlecloudbigquery_v2typesmodelseas_4c63c0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumsdestinationformat_googlecloudbigquery_v2typesmodelseaso_d545d2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsdestinationformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DestinationFormat -->

# Class DestinationFormat (3.40.0)

`DestinationFormat()`


The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelseasonalperiodseasonalperiodtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType -->

# Class SeasonalPeriodType (3.40.0)

`SeasonalPeriodType(value)`


API documentation for `bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType`

class.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryqueryconnectionproperty.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty -->

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
