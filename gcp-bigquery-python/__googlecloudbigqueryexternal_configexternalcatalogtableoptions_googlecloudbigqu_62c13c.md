---
merged_at: 2026-01-26T23:27:21.521737
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogTableOptions -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.StorageDescriptor -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine -->

# Class Routine (3.40.0)

`Routine(routine_ref, **kwargs)`


Resource representing a user-defined routine.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines)

## Parameters |
|
|---|---|
Name |
Description |
`routine_ref` |
`Union[str, `
A pointer to a routine. If |
|
`Dict`
Initial property values. |

## Properties

### arguments

List[[google.cloud.bigquery.routine.RoutineArgument](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument)]: Input/output
argument of a function or a stored procedure.

In-place modification is not supported. To set, replace the entire
property value with the modified list of
[RoutineArgument](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument) objects.

### body

str: The body of the routine.

### created

Optional[datetime.datetime]: Datetime at which the routine was
created (:data:`None`

until set from the server).

Read-only.

### data_governance_type

Optional[str]: If set to `DATA_MASKING`

, the function is validated
and made available as a masking function.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not :data:`string` or :data:`None` . |

### dataset_id

str: ID of dataset containing the routine.

### description

Optional[str]: Description of the routine (defaults to
:data:`None`

).

### determinism_level

Optional[str]: (experimental) The determinism level of the JavaScript UDF if defined.

### etag

str: ETag for the resource (:data:`None`

until set from the
server).

Read-only.

### external_runtime_options

Optional[[google.cloud.bigquery.routine.ExternalRuntimeOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions)]:
Configures the external runtime options for a routine.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### imported_libraries

List[str]: The path of the imported JavaScript libraries.

The [language](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine) must
equal `JAVACRIPT`

.

Examples:
Set the `imported_libraries`

to a list of Google Cloud Storage
URIs.

```
.. code-block:: python
routine = bigquery.Routine("proj.dataset.routine_id")
routine.imported_libraries = [
"gs://cloud-samples-data/bigquery/udfs/max-value.js",
]
```


### language

Optional[str]: The language of the routine.

Defaults to `SQL`

.

### modified

Optional[datetime.datetime]: Datetime at which the routine was
last modified (:data:`None`

until set from the server).

Read-only.

### path

str: URL path for the routine's APIs.

### project

str: ID of the project containing the routine.

### reference

[google.cloud.bigquery.routine.RoutineReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference): Reference
describing the ID of this routine.

### remote_function_options

Optional[[google.cloud.bigquery.routine.RemoteFunctionOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions)]:
Configures remote function options for a routine.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### return_table_type

The return type of a Table Valued Function (TVF) routine.

.. versionadded:: 2.22.0

### return_type

google.cloud.bigquery.StandardSqlDataType: Return type of the routine.

If absent, the return type is inferred from
[body](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine) at query time in
each query that references this routine. If present, then the
evaluated result will be cast to the specified returned type at query
time.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Routine.FIELDS.return_type](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Routine.FIELDS.return_type)

### routine_id

str: The routine ID.

### type_

str: The fine-grained type of the routine.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#RoutineType](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#RoutineType)

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.routine.routine.Routine`


Factory: construct a routine given its API representation.

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
`google.cloud.bigquery.routine.Routine` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Routine represented as an API resource. |
