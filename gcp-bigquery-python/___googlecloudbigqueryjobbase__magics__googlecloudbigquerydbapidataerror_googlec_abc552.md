---
merged_at: 2026-01-25T15:38:56.574189
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryjobbase__magics__googlecloudbigquerydbapidataerror_googlecl_80ce4e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryjobbase__magics__googlecloudbigquerydbapidataerror_googleclo_b70d3d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobbase.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base -->

# Module base (3.40.0)

Base classes and helpers for job classes.

## Classes

[ReservationUsage](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ReservationUsage)

`ReservationUsage(name, slot_ms)`


Job resource usage for a reservation.

[ScriptStackFrame](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame)

`ScriptStackFrame(resource)`


Stack frame showing the line/column/procedure name where the current evaluation happened.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

[ScriptStatistics](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStatistics)

`ScriptStatistics(resource)`


Statistics for a child job of a script.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

[SessionInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.SessionInfo)

`SessionInfo(resource)`


[Preview] Information of the session if this job is part of one.

.. versionadded:: 2.29.0

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

[TransactionInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.TransactionInfo)

`TransactionInfo(transaction_id: str)`


[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

.. versionadded:: 2.24.0

[UnknownJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.UnknownJob)

`UnknownJob(job_id, client)`


A job whose type cannot be determined.


---

<!-- DOCUMENTO FUSIONADO: _magics__googlecloudbigquerydbapidataerror_googlecloudbigquerydbapiinterfaceerro_efe98f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: magics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/magics -->

# IPython Magics for BigQuery

To use these magics, you must first register them. Run the `%load_ext`

magic
in a Jupyter notebook cell.

```
%load_ext bigquery_magics
```


This makes the `%%bigquery`

magic available.

## Code Samples

Running a query:

```
%%bigquery
SELECT name, SUM(number) as count
FROM `bigquery-public-data.usa_names.usa_1910_current`
GROUP BY name
ORDER BY count DESC
LIMIT 3
```


Running a parameterized query:

```
%%bigquery --params {"corpus_name": "hamlet", "limit": 10}
SELECT word, SUM(word_count) as count
FROM `bigquery-public-data.samples.shakespeare`
WHERE corpus = @corpus_name
GROUP BY word
ORDER BY count DESC
LIMIT @limit
```


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerydbapidataerror_googlecloudbigquerydbapiinterfaceerror.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapidataerror.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.DataError -->

# Class DataError (3.40.0)

DB-API error due to problems with the processed data.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapiinterfaceerror.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.InterfaceError -->

# Class InterfaceError (3.40.0)

DB-API error related to the database interface.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryexternal_configexternalcatalogdatasetoptions___googlecloudbi_06f08d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_configexternalcatalogdatasetoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquerydbapierror_googlecloudbigquerydbapidatabaseerror_googleclou_e152a7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerydbapierror_googlecloudbigquerydbapidatabaseerror.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapierror.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Error -->

# Class Error (3.40.0)

Exception representing all non-warning DB-API errors.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapidatabaseerror.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.DatabaseError -->

# Class DatabaseError (3.40.0)

DB-API error related to the database.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobscriptstackframe.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame -->

# Class ScriptStackFrame (3.40.0)

`ScriptStackFrame(resource)`


Stack frame showing the line/column/procedure name where the current evaluation happened.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### end_column

int: One-based end column.

### end_line

int: One-based end line.

### procedure_id

Optional[str]: Name of the active procedure.

Omitted if in a top-level script.

### start_column

int: One-based start column.

### start_line

int: One-based start line.

### text

str: Text of the current statement/expression.


---

<!-- DOCUMENTO FUSIONADO: upgrading.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/upgrading -->

# 3.0.0 Migration Guide

## New Required Dependencies

Some of the previously optional dependencies are now *required* in `3.x`

versions of the
library, namely
[google-cloud-bigquery-storage](https://pypi.org/project/google-cloud-bigquery-storage/)
(minimum version `2.0.0`

) and [pyarrow](https://pypi.org/project/pyarrow/) (minimum
version `3.0.0`

).

The behavior of some of the package “extras” has thus also changed:

The

`pandas`

extra now requires the[db-types](https://pypi.org/project/db-dtypes/)package.The

`bqstorage`

extra has been preserved for comaptibility reasons, but it is now a no-op and should be omitted when installing the BigQuery client library.

**Before:**

```
$ pip install google-cloud-bigquery[bqstorage]
```


**After:**

```
$ pip install google-cloud-bigquery
```


- The
`bignumeric_type`

extra has been removed, as`BIGNUMERIC`

type is now automatically supported. That extra should thus not be used.

**Before:**

```
$ pip install google-cloud-bigquery[bignumeric_type]
```


**After:**

```
$ pip install google-cloud-bigquery
```


## Type Annotations

The library is now type-annotated and declares itself as such. If you use a static
type checker such as `mypy`

, you might start getting errors in places where
`google-cloud-bigquery`

package is used.

It is recommended to update your code and/or type annotations to fix these errors, but
if this is not feasible in the short term, you can temporarily ignore type annotations
in `google-cloud-bigquery`

, for example by using a special `# type: ignore`

comment:

`from google.cloud import `[bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest) # type: ignore


But again, this is only recommended as a possible short-term workaround if immediately fixing the type check errors in your project is not feasible.

## Re-organized Types

The auto-generated parts of the library has been removed, and proto-based types formerly
found in `google.cloud.bigquery_v2`

have been replaced by the new implementation (but
see the [section](#legacy-types) below).

For example, the standard SQL data types should new be imported from a new location:

**Before:**

```
from google.cloud.bigquery_v2 import StandardSqlDataType
from google.cloud.bigquery_v2.types import StandardSqlField
from google.cloud.bigquery_v2.types.standard_sql import StandardSqlStructType
```


**After:**

```
from google.cloud.bigquery import StandardSqlDataType
from google.cloud.bigquery.standard_sql import StandardSqlField
from google.cloud.bigquery.standard_sql import StandardSqlStructType
```


The `TypeKind`

enum defining all possible SQL types for schema fields has been renamed
and is not nested anymore under `StandardSqlDataType`

:

**Before:**

```
from google.cloud.bigquery_v2 import StandardSqlDataType
if field_type == StandardSqlDataType.
```[TypeKind](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType.TypeKind.html).[STRING](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DecimalTargetType.html#google_cloud_bigquery_enums_DecimalTargetType_STRING):
...


**After:**

```
from google.cloud.bigquery import
```[StandardSqlTypeNames](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.StandardSqlTypeNames.html)
if field_type == [StandardSqlTypeNames](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.StandardSqlTypeNames.html).[STRING](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DecimalTargetType.html#google_cloud_bigquery_enums_DecimalTargetType_STRING):
...


## Issuing queries with `Client.create_job`

preserves destination table

The `Client.create_job`

method no longer removes the destination table from a
query job’s configuration. Destination table for the query can thus be
explicitly defined by the user.

## Changes to data types when reading a pandas DataFrame

The default dtypes returned by the `to_dataframe`

method have changed.

Now, the BigQuery

`BOOLEAN`

data type maps to the pandas`boolean`

dtype. Previously, this mapped to the pandas`bool`

dtype when the column did not contain`NULL`

values and the pandas`object`

dtype when`NULL`

values are present.Now, the BigQuery

`INT64`

data type maps to the pandas`Int64`

dtype. Previously, this mapped to the pandas`int64`

dtype when the column did not contain`NULL`

values and the pandas`float64`

dtype when`NULL`

values are present.Now, the BigQuery

`DATE`

data type maps to the pandas`dbdate`

dtype, which is provided by the[db-dtypes](https://googleapis.dev/python/db-dtypes/latest/index.html)package. If any date value is outside of the range of[pandas.Timestamp.min](https://pandas.pydata.org/docs/reference/api/pandas.Timestamp.min.html)(1677-09-22) and[pandas.Timestamp.max](https://pandas.pydata.org/docs/reference/api/pandas.Timestamp.max.html)(2262-04-11), the data type maps to the pandas`object`

dtype. The`date_as_object`

parameter has been removed.Now, the BigQuery

`TIME`

data type maps to the pandas`dbtime`

dtype, which is provided by the[db-dtypes](https://googleapis.dev/python/db-dtypes/latest/index.html)package.

## Changes to data types loading a pandas DataFrame

In the absence of schema information, pandas columns with naive
`datetime64[ns]`

values, i.e. without timezone information, are recognized and
loaded using the `DATETIME`

type. On the other hand, for columns with
timezone-aware `datetime64[ns, UTC]`

values, the `TIMESTAMP`

type is continued
to be used.

## Changes to `Model`

, `Client.get_model`

, `Client.update_model`

, and `Client.list_models`


The types of several `Model`

properties have been changed.

`Model.feature_columns`

now returns a sequence of`google.cloud.bigquery.standard_sql.StandardSqlField`

.`Model.label_columns`

now returns a sequence of`google.cloud.bigquery.standard_sql.StandardSqlField`

.`Model.model_type`

now returns a string.`Model.training_runs`

now returns a sequence of dictionaries, as recieved from the[BigQuery REST API](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#Model.FIELDS.training_runs).

## Legacy Protocol Buffers Types

For compatibility reasons, the legacy proto-based types still exists as static code and can be imported:

```
from google.cloud.bigquery_v2 import Model # a sublcass of proto.Message
```


Mind, however, that importing them will issue a warning, because aside from
being importable, these types **are not maintained anymore**. They may differ
both from the types in `google.cloud.bigquery`

, and from the types supported on
the backend.

### Maintaining compatibility with `google-cloud-bigquery`

version 2.0

If you maintain a library or system that needs to support both
`google-cloud-bigquery`

version 2.x and 3.x, it is recommended that you detect
when version 2.x is in use and convert properties that use the legacy protocol
buffer types, such as `Model.training_runs`

, into the types used in 3.x.

Call the [ to_dict
method](https://proto-plus-python.readthedocs.io/en/latest/reference/message.html#proto.message.Message.to_dict)
on the protocol buffers objects to get a JSON-compatible dictionary.

```
from google.cloud.bigquery_v2 import Model
training_run: Model.
```[TrainingRun](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.html) = ...
training_run_dict = training_run.to_dict()


# 2.0.0 Migration Guide

The 2.0 release of the `google-cloud-bigquery`

client drops support for Python
versions below 3.6. The client surface itself has not changed, but the 1.x series
will not be receiving any more feature updates or bug fixes. You are thus
encouraged to upgrade to the 2.x series.

If you experience issues or have questions, please file an
[issue](https://github.com/googleapis/python-bigquery/issues).

## Supported Python Versions


WARNING: Breaking change

The 2.0.0 release requires Python 3.6+.

## Supported BigQuery Storage Clients

The 2.0.0 release requires BigQuery Storage `>= 2.0.0`

, which dropped support
for `v1beta1`

and `v1beta2`

versions of the BigQuery Storage API. If you want to
use a BigQuery Storage client, it must be the one supporting the `v1`

API version.

## Changed GAPIC Enums Path


WARNING: Breaking change

Generated GAPIC enum types have been moved under `types`

. Import paths need to be
adjusted.

**Before:**

```
from google.cloud.bigquery_v2.gapic import enums
distance_type = enums.Model.DistanceType.COSINE
```


**After:**

```
from google.cloud.bigquery_v2 import types
distance_type = types.Model.DistanceType.COSINE
```
