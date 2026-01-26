---
merged_at: 2026-01-26T21:00:49.243036
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/reference -->

# Python Client for Google BigQuery

Querying massive datasets can be time consuming and expensive without the
right hardware and infrastructure. Google [BigQuery](https://cloud.google.com/bigquery/what-is-bigquery) solves this problem by
enabling super-fast, SQL queries against append-mostly tables, using the
processing power of Google’s infrastructure.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Supported Python Versions

Python >= 3.9

#### Unsupported Python Versions

Python == 2.7, Python == 3.5, Python == 3.6, Python == 3.7, and Python == 3.8.

The last version of this library compatible with Python 2.7 and 3.5 is google-cloud-bigquery==1.28.0.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-bigquery
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-bigquery
```


## Example Usage

### Perform a query

`from google.cloud import `[bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest)
client = [bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest).[Client](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)()
# Perform a query.
QUERY = (
'SELECT name FROM `bigquery-public-data.usa_names.usa_1910_2013` '
'WHERE state = "TX" '
'LIMIT 100')
query_job = client.[query](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)(QUERY) # API request
rows = [query_job](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Cursor.html#google_cloud_bigquery_dbapi_Cursor_query_job).result() # Waits for query to finish
for row in rows:
print(row.name)


## Instrumenting With OpenTelemetry

This application uses [OpenTelemetry](https://opentelemetry.io) to output tracing data from
API calls to BigQuery. To enable OpenTelemetry tracing in
the BigQuery client the following PyPI packages need to be installed:

```
pip install google-cloud-bigquery[opentelemetry] opentelemetry-exporter-gcp-trace
```


After installation, OpenTelemetry can be used in the BigQuery client and in BigQuery jobs. First, however, an exporter must be specified for where the trace data will be outputted to. An example of this can be found here:

```
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.exporter.cloud_trace import CloudTraceSpanExporter
tracer_provider = TracerProvider()
tracer_provider = BatchSpanProcessor(CloudTraceSpanExporter())
trace.set_tracer_provider(TracerProvider())
```


In this example all tracing data will be published to the Google
[Cloud Trace](https://cloud.google.com/trace) console. For more information on OpenTelemetry, please consult the [OpenTelemetry documentation](https://opentelemetry-python.readthedocs.io).

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions -->

# Class CSVOptions (3.40.0)

`CSVOptions()`


Options that describe how to treat CSV files as BigQuery tables.

## Properties

### allow_jagged_rows

bool: If :data:`True`

, BigQuery treats missing trailing columns as
null values. Defaults to :data:`False`

.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.allow_jagged_rows](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.allow_jagged_rows)

### allow_quoted_newlines

bool: If :data:`True`

, quoted data sections that contain newline
characters in a CSV file are allowed. Defaults to :data:`False`

.

### encoding

str: The character encoding of the data.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.encoding](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.encoding)

### field_delimiter

str: The separator for fields in a CSV file. Defaults to comma (',').

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.field_delimiter](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.field_delimiter)

### null_markers

Optional[Iterable[str]]: A list of strings represented as SQL NULL values in a CSV file.

See[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.null_markers](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.null_markers)

### preserve_ascii_control_characters

bool: Indicates if the embedded ASCII control characters (the first 32 characters in the ASCII-table, from '' to ' ') are preserved.

### quote_character

str: The value that is used to quote data sections in a CSV file.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.quote](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.quote)

### skip_leading_rows

int: The number of rows at the top of a CSV file.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.skip_leading_rows](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.skip_leading_rows)

### source_column_match

Optional[[google.cloud.bigquery.enums.SourceColumnMatch](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch)]: Controls the
strategy used to match loaded columns to the schema. If not set, a sensible
default is chosen based on how the schema is provided. If autodetect is
used, then columns are matched by name. Otherwise, columns are matched by
position. This is done to keep the behavior backward-compatible.

Acceptable values are:

```
SOURCE_COLUMN_MATCH_UNSPECIFIED: Unspecified column name match option.
POSITION: matches by position. This assumes that the columns are ordered
the same way as the schema.
NAME: matches by name. This reads the header row as column names and
reorders columns to match the field names in the schema.
```


## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.external_config.CSVOptions`


Factory: construct a `.external_config.CSVOptions`

instance
given its API representation.

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
`CSVOptions` |
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.TransformColumn -->

# Class TransformColumn (3.40.0)

`TransformColumn(resource: typing.Dict[str, typing.Any])`


TransformColumn represents a transform column feature.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn)

## Properties

### name

Name of the column.

### transform_sql

The SQL expression used in the column transform.

### type_

Data type of the column after the transform.

Returns |
|
|---|---|
Type |
Description |
`Optional[` |
Data type of the column. |

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.model.TransformColumn
```


Constructs a transform column feature given its API representation

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.DataError -->

# Class DataError (3.40.0)

DB-API error due to problems with the processed data.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.InterfaceError -->

# Class InterfaceError (3.40.0)

DB-API error related to the database interface.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.CloneDefinition -->

# Class CloneDefinition (3.40.0)

`CloneDefinition(resource: typing.Dict[str, typing.Any])`


Information about base table and clone time of the clone.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#clonedefinition](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#clonedefinition)

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions -->

# Class ExternalCatalogDatasetOptions (3.40.0)

```
ExternalCatalogDatasetOptions(
default_storage_location_uri: typing.Optional[str] = None,
parameters: typing.Optional[typing.Dict[str, typing.Any]] = None,
)
```


Options defining open source compatible datasets living in the BigQuery catalog. Contains metadata of open source database, schema or namespace represented by the current dataset.

## Parameters |
|
|---|---|
Name |
Description |
`default_storage_location_uri` |
`Optional[str]`
The storage location URI for all tables in the dataset. Equivalent to hive metastore's database locationUri. Maximum length of 1024 characters. (str) |
`parameters` |
`Optional[dict[str, Any]]`
A map of key value pairs defining the parameters and properties of the open source schema. Maximum size of 2Mib. |

## Properties

### default_storage_location_uri

Optional. The storage location URI for all tables in the dataset. Equivalent to hive metastore's database locationUri. Maximum length of 1024 characters.

### parameters

Optional. A map of key value pairs defining the parameters and properties of the open source schema. Maximum size of 2Mib.

## Methods

### from_api_repr

```
from_api_repr(
api_repr: dict,
) -> google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions
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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig -->

# Class CopyJobConfig (3.40.0)

`CopyJobConfig(**kwargs)`


Configuration options for copy jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

## Properties

### create_disposition

[google.cloud.bigquery.job.CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition): Specifies behavior
for creating tables.

### destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

Custom encryption configuration (e.g., Cloud KMS keys) or :data:`None`

if using default encryption.

### destination_expiration_time

google.cloud.bigquery.job.DestinationExpirationTime: The time when the destination table expires. Expired tables will be deleted and their storage reclaimed.

### job_timeout_ms

Optional parameter. Job timeout in milliseconds. If this time limit is exceeded, BigQuery might attempt to stop the job.
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfiguration.FIELDS.job_timeout_ms](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfiguration.FIELDS.job_timeout_ms)
e.g.

```
job_config = bigquery.QueryJobConfig( job_timeout_ms = 5000 )
or
job_config.job_timeout_ms = 5000
```


Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `value` type is invalid. |

### labels

Dict[str, str]: Labels for the job.

This method always returns a dict. Once a job has been created on the server, its labels cannot be modified anymore.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `value` type is invalid. |

### max_slots

The maximum rate of slot consumption to allow for this job.

If set, the number of slots used to execute the job will be throttled to try and keep its slot consumption below the requested rate. This feature is not generally available.

### operation_type

The operation to perform with this copy job.

### reservation

str: Optional. The reservation that job would use.

User can specify a reservation to execute the job. If reservation is not set, reservation is determined based on the rules defined by the reservation assignments. The expected format is projects/{project}/locations/{location}/reservations/{reservation}.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `value` type is not None or of string type. |

### write_disposition

[google.cloud.bigquery.job.WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition): Action that occurs if
the destination table already exists.

## Methods

### __setattr__

`__setattr__(name, value)`


Override to be able to raise error if an unknown property is being set

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.base._JobConfig`


Factory: construct a job configuration given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
A job configuration in the same representation as is returned from the API. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job._JobConfig` |
Configuration parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of the job config.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
A dictionary in the format used by the BigQuery API. |
