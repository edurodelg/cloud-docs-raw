---
merged_at: 2026-01-25T15:38:56.567558
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerytabletimepartitioning__googlecloudbigqueryencryption_configu_b0b7b2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytabletimepartitioning.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryencryption_configurationencryptionconfiguration_googlecloudb_dc6507.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryencryption_configurationencryptionconfiguration.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration -->

# Class EncryptionConfiguration (3.40.0)

`EncryptionConfiguration(kms_key_name=None)`


Custom encryption configuration (e.g., Cloud KMS keys).

## Parameter |
|
|---|---|
Name |
Description |
`kms_key_name` |
`str`
resource ID of Cloud KMS key used for encryption |

## Properties

### kms_key_name

str: Resource ID of Cloud KMS key

Resource ID of Cloud KMS key or :data:`None`

if using default
encryption.

## Methods

### from_api_repr

`from_api_repr(resource)`


Construct an encryption configuration from its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
An encryption configuration representation as returned from the API. |

Returns |
|
|---|---|
Type |
Description |
|
An encryption configuration parsed from `resource` . |

### to_api_repr

`to_api_repr()`


Construct the API resource representation of this encryption configuration.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Encryption configuration as represented as an API resource |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryschemaforeigntypeinfo.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.ForeignTypeInfo -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typestablereference_googlecloudbigquery_v2typesmodelarim_c17775.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typestablereference_googlecloudbigquery_v2typesmodelarima_397831.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typestablereference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.TableReference -->

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


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelarimaforecastingmetrics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaForecastingMetrics -->

# Class ArimaForecastingMetrics (3.40.0)

`ArimaForecastingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model evaluation metrics for ARIMA forecasting models.

## Attributes |
|
|---|---|
Name |
Description |
`non_seasonal_order` |
`Sequence[`
Non-seasonal order. |
`arima_fitting_metrics` |
`Sequence[`
Arima model fitting metrics. |
`seasonal_periods` |
`Sequence[`
Seasonal periods. Repeated because multiple periods are supported for one time series. |
`has_drift` |
`Sequence[bool]`
Whether Arima model fitted with drift or not. It is always false when d is not 1. |
`time_series_id` |
`Sequence[str]`
Id to differentiate different time series for the large-scale case. |
`arima_single_model_forecasting_metrics` |
`Sequence[`
Repeated as there can be many metric sets (one for each model) in auto-arima and the large-scale case. |

## Classes

### ArimaSingleModelForecastingMetrics

```
ArimaSingleModelForecastingMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Model evaluation metrics for a single ARIMA forecasting model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client -->

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
