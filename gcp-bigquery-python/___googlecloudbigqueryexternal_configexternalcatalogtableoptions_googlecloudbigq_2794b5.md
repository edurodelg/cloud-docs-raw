---
merged_at: 2026-01-26T21:00:49.251522
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning -->

# Class TimePartitioning (3.40.0)

```
TimePartitioning(
type_=None, field=None, expiration_ms=None, require_partition_filter=None
)
```


Configures time-based partitioning for a table.

## Parameters |
|
|---|---|
Name |
Description |
`type_` |
`Optional[`
Specifies the type of time partitioning to perform. Defaults to |
`field` |
`Optional[str]`
If set, the table is partitioned by this field. If not set, the table is partitioned by pseudo column |
`expiration_ms` |
`Optional[int]`
Number of milliseconds for which to keep the storage for a partition. |
`require_partition_filter` |
`Optional[bool]`
DEPRECATED: Use |

## Properties

### expiration_ms

int: Number of milliseconds to keep the storage for a partition.

### field

str: Field in the table to use for partitioning

### require_partition_filter

bool: Specifies whether partition filters are required for queries

DEPRECATED: Use
[require_partition_filter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table),
instead.

### type_

[google.cloud.bigquery.table.TimePartitioningType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType): The type of time
partitioning to use.

## Methods

### from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.table.TimePartitioning`


Return a `TimePartitioning`

object deserialized from a dict.

This method creates a new `TimePartitioning`

instance that points to
the `api_repr`

parameter as its internal properties dict. This means
that when a `TimePartitioning`

instance is stored as a property of
another object, any changes made at the higher level will also appear
here::

```
>>> time_partitioning = TimePartitioning()
>>> table.time_partitioning = time_partitioning
>>> table.time_partitioning.field = 'timecolumn'
>>> time_partitioning.field
'timecolumn'
```


Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Mapping[str, str]`
The serialized representation of the TimePartitioning, such as what is output by |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.table.TimePartitioning` |
The `TimePartitioning` object. |

### to_api_repr

`to_api_repr() -> dict`


Return a dictionary representing this object.

This method returns the properties dict of the `TimePartitioning`

instance rather than making a copy. This means that when a
`TimePartitioning`

instance is stored as a property of another
object, any changes made at the higher level will also appear here.

Returns |
|
|---|---|
Type |
Description |
`dict` |
A dictionary representing the TimePartitioning object in serialized form. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaCoefficients -->

# Class ArimaCoefficients (3.40.0)

`ArimaCoefficients(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima coefficients.

## Attributes |
|
|---|---|
Name |
Description |
`auto_regressive_coefficients` |
`Sequence[float]`
Auto-regressive coefficients, an array of double. |
`moving_average_coefficients` |
`Sequence[float]`
Moving-average coefficients, an array of double. |
`intercept_coefficient` |
`float`
Intercept coefficient, just a double not an array. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.TrainingOptions.LabelClassWeightsEntry -->

# Class LabelClassWeightsEntry (3.40.0)

`LabelClassWeightsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Connection -->

# Class Connection (3.40.0)

`Connection(client=None, bqstorage_client=None, prefer_bqstorage_client=True)`


DB-API Connection to Google BigQuery.

## Parameters |
|
|---|---|
Name |
Description |
`client` |
`Optional[google.cloud.bigquery.Client]`
A REST API client used to connect to BigQuery. If not passed, a client is created using default options inferred from the environment. |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A client that uses the faster BigQuery Storage API to fetch rows from BigQuery. If not passed, it is created using the same credentials as |
`prefer_bqstorage_client` |
`Optional[bool]`
Prefer the BigQuery Storage client over the REST client. If Storage client isn't available, fall back to the REST client. Defaults to |

## Methods

### close

`close()`


Close the connection and any cursors created from it.

Any BigQuery clients explicitly passed to the constructor are *not*
closed, only those created by the connection instance itself.

### commit

`commit()`


No-op, but for consistency raise an error if connection is closed.

### cursor

`cursor()`


Return a new cursor object.

Returns |
|
|---|---|
Type |
Description |
|
A DB-API cursor that uses this connection. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ForeignKey -->

# Class ForeignKey (3.40.0)

```
ForeignKey(
name: str,
referenced_table: google.cloud.bigquery.table.TableReference,
column_references: typing.List[google.cloud.bigquery.table.ColumnReference],
)
```


Represents a foreign key constraint on a table's columns.

## Methods

### from_api_repr

```
from_api_repr(
api_repr: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.table.ForeignKey
```


Create an instance from API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Return a dictionary representing this object.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ClusterInfo -->

# Class ClusterInfo (3.40.0)

`ClusterInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single cluster for clustering model.

## Attributes |
|
|---|---|
Name |
Description |
`centroid_id` |
`int`
Centroid id. |
`cluster_radius` |
`google.protobuf.wrappers_pb2.DoubleValue`
Cluster radius, the average distance from centroid to each point assigned to the cluster. |
`cluster_size` |
`google.protobuf.wrappers_pb2.Int64Value`
Cluster size, the total number of points assigned to the cluster. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun -->

# Class TrainingRun (3.40.0)

`TrainingRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single training query run for the model.

## Attributes |
|
|---|---|
Name |
Description |
`training_options` |
Options that were used for this training run, includes user specified and default options that were used. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The start time of this training run. |
`results` |
`Sequence[`
Output of each iteration run, results.size() <= max_iterations.=""> |
`evaluation_metrics` |
The evaluation metrics over training/eval data that were computed at the end of training. |
`data_split_result` |
Data split result of the training run. Only set when the input data is actually split. |
`global_explanations` |
`Sequence[`
Global explanations for important features of the model. For multi-class models, there is one entry for each label class. For other models, there is only one entry in the list. |

## Classes

### IterationResult

`IterationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single iteration of the training run.

### TrainingOptions

`TrainingOptions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Options used in model training.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client -->

# Module client (3.40.0)

Client for interacting with the Google BigQuery API.

## Classes

[Client](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client)

```
Client(
project: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
_http: typing.Optional[requests.sessions.Session] = None,
location: typing.Optional[str] = None,
default_query_job_config: typing.Optional[
google.cloud.bigquery.job.query.QueryJobConfig
] = None,
default_load_job_config: typing.Optional[
google.cloud.bigquery.job.load.LoadJobConfig
] = None,
client_info: typing.Optional[google.api_core.client_info.ClientInfo] = None,
client_options: typing.Optional[
typing.Union[
google.api_core.client_options.ClientOptions, typing.Dict[str, typing.Any]
]
] = None,
default_job_creation_mode: typing.Optional[str] = None,
)
```


Client to bundle configuration needed for API requests.

Parameters |
|
|---|---|
Name |
Description |
`project` |
`Optional[str]`
Project ID for the project which the client acts on behalf of. Will be passed when creating a dataset / job. If not passed, falls back to the default inferred from the environment. |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The OAuth2 Credentials to use for this client. If not passed (and if no |
`_http` |
`Optional[requests.Session]`
HTTP object to make requests. Can be any object that defines |
`location` |
`Optional[str]`
Default location for jobs / datasets / tables. |
`default_query_job_config` |
`Optional[`
Default |
`default_load_job_config` |
`Optional[`
Default |
`client_info` |
`Optional[google.api_core.client_info.ClientInfo]`
The client info used to send a user-agent string along with API requests. If |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, Dict]]`
Client options used to set user options on the client. API Endpoint should be set through client_options. |
`default_job_creation_mode` |
`Optional[str]`
Sets the default job creation mode used by query methods such as query_and_wait(). For lightweight queries, JOB_CREATION_OPTIONAL is generally recommended. |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.DefaultCredentialsError` |
Raised if `credentials` is not specified and the library fails to acquire default credentials. |

[Project](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Project)

`Project(project_id, numeric_id, friendly_name)`


Wrapper for resource describing a BigQuery project.

Parameters |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Opaque ID of the project |
`numeric_id` |
`int`
Numeric ID of the project |
`friendly_name` |
`str`
Display name of the project |
