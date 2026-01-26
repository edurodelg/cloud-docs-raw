---
merged_at: 2026-01-26T23:27:21.521315
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue.CategoricalValue.CategoryCount -->

# Class CategoryCount (3.40.0)

`CategoryCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the count of a single category within the cluster.

## Attributes |
|
|---|---|
Name |
Description |
`category` |
`str`
The name of category. |
`count` |
`google.protobuf.wrappers_pb2.Int64Value`
The count of training samples matching the category within the cluster. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.EncryptionConfiguration -->

# Class EncryptionConfiguration (3.40.0)

`EncryptionConfiguration(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attribute |
|
|---|---|
Name |
Description |
`kms_key_name` |
`google.protobuf.wrappers_pb2.StringValue`
Optional. Describes the Cloud KMS encryption key that will be used to protect destination BigQuery table. The BigQuery Service Account associated with your project requires access to this encryption key. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.ForeignTypeInfo -->

# Class ForeignTypeInfo (3.40.0)

`ForeignTypeInfo(type_system: typing.Optional[str] = None)`


Metadata about the foreign data type definition such as the system in which the type is defined.

## Parameter |
|
|---|---|
Name |
Description |
`type_system` |
`str`
Required. Specifies the system which defines the foreign data type. TypeSystem enum currently includes: * "TYPE_SYSTEM_UNSPECIFIED" * "HIVE" |

## Properties

### type_system

Required. Specifies the system which defines the foreign data type.

## Methods

### from_api_repr

```
from_api_repr(
api_repr: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.schema.ForeignTypeInfo
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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference -->

# Class TableReference (3.40.0)

`TableReference(dataset_ref: DatasetReference, table_id: str)`


TableReferences are pointers to tables.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#tablereference](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#tablereference)

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.table.TableReference`


Factory: construct a table reference given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Table reference representation returned from the API |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.table.TableReference` |
Table reference parsed from `resource` . |

### from_string

```
from_string(
table_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.table.TableReference
```


Construct a table reference from table ID string.

Parameters |
|
|---|---|
Name |
Description |
`table_id` |
`str`
A table ID in standard SQL format. If |
`default_project` |
`Optional[str]`
The project ID to use when |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `table_id` is not a fully-qualified table ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`TableReference .. rubric:: Examples >>> TableReference.from_string('my-project.mydataset.mytable') TableRef...(DatasetRef...('my-project', 'mydataset'), 'mytable')` |
Table reference parsed from `table_id` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this table reference.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Table reference represented as an API resource |

### to_bqstorage

`to_bqstorage() -> str`


Construct a BigQuery Storage API representation of this table.

Install the `google-cloud-bigquery-storage`

package to use this
feature.

If the `table_id`

contains a partition identifier (e.g.
`my_table$201812`

) or a snapshot identifier (e.g.
`mytable@1234567890`

), it is ignored. Use
xref_TableReadOptions
to filter rows by partition. Use
xref_TableModifiers
to select a specific snapshot to read from.

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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SchemaUpdateOption -->

# Class SchemaUpdateOption (3.40.0)

`SchemaUpdateOption()`


Specifies an update to the destination table schema as a side effect of a load job.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SchemaUpdateOption -->

# Class SchemaUpdateOption (3.40.0)

`SchemaUpdateOption()`


Specifies an update to the destination table schema as a side effect of a load job.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.TimestampPrecision -->

# Class TimestampPrecision (3.40.0)

`TimestampPrecision(value)`


Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.OperationalError -->

# Class OperationalError (3.40.0)

DB-API error related to the database operation.

These errors are not necessarily under the control of the programmer.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.TableReference -->

# Class TableReference (3.40.0)

`TableReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. The ID of the project containing this table. |
`dataset_id` |
`str`
Required. The ID of the dataset containing this table. |
`table_id` |
`str`
Required. The ID of the table. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (_). The maximum length is 1,024 characters. Certain operations allow suffixing of the table ID with a partition decorator, such as `sample_table$20190123` .
|
`project_id_alternative` |
`Sequence[str]`
The alternative field that will be used when ESF is not able to translate the received data to the project_id field. |
`dataset_id_alternative` |
`Sequence[str]`
The alternative field that will be used when ESF is not able to translate the received data to the project_id field. |
`table_id_alternative` |
`Sequence[str]`
The alternative field that will be used when ESF is not able to translate the received data to the project_id field. |
