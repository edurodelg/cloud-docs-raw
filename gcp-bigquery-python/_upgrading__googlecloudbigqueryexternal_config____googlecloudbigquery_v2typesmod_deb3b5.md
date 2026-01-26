---
merged_at: 2026-01-26T21:00:49.245567
merged_files: 2
---


---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/upgrading -->

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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config -->

# Module external_config (3.40.0)

Define classes that describe external data sources.

These are used for both Table.externalDataConfiguration and Job.configuration.query.tableDefinitions.

## Classes

[BigtableColumn](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn)

`BigtableColumn()`


Options for a Bigtable column.

[BigtableColumnFamily](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily)

`BigtableColumnFamily()`


Options for a Bigtable column family.

[BigtableOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableOptions)

`BigtableOptions()`


Options that describe how to treat Bigtable tables as BigQuery tables.

[CSVOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions)

`CSVOptions()`


Options that describe how to treat CSV files as BigQuery tables.

[ExternalCatalogDatasetOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions)

```
ExternalCatalogDatasetOptions(
default_storage_location_uri: typing.Optional[str] = None,
parameters: typing.Optional[typing.Dict[str, typing.Any]] = None,
)
```


Options defining open source compatible datasets living in the BigQuery catalog. Contains metadata of open source database, schema or namespace represented by the current dataset.

Parameters |
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

[ExternalCatalogTableOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogTableOptions)

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

Parameters |
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

[ExternalConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig)

`ExternalConfig(source_format)`


Description of an external data source.

Parameter |
|
|---|---|
Name |
Description |
`source_format` |
`ExternalSourceFormat`
See |

[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)

`ExternalSourceFormat()`


The format for external data files.

Note that the set of allowed values for external data sources is different
than the set used for loading data (see
[SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat)).

[GoogleSheetsOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.GoogleSheetsOptions)

`GoogleSheetsOptions()`


Options that describe how to treat Google Sheets as BigQuery tables.

[HivePartitioningOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.HivePartitioningOptions)

`HivePartitioningOptions()`


Options that configure hive partitioning.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.GlobalExplanation.Explanation -->

# Class Explanation (3.40.0)

`Explanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Explanation for a single feature.

## Attributes |
|
|---|---|
Name |
Description |
`feature_name` |
`str`
Full name of the feature. For non-numerical features, will be formatted like |
`attribution` |
`google.protobuf.wrappers_pb2.DoubleValue`
Attribution of feature. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType -->

# Class TimePartitioningType (3.40.0)

`TimePartitioningType()`


Specifies the type of time partitioning to perform.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.QueryPriority -->

# Class QueryPriority (3.40.0)

`QueryPriority()`


Specifies a priority for the query. The default value is
`INTERACTIVE`

.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.IncrementalResultStats -->

# Class IncrementalResultStats (3.40.0)

`IncrementalResultStats()`


IncrementalResultStats provides information about incremental query execution.

## Properties

### disabled_reason

Optional[string]: Reason why incremental results were not written by the query.

### result_set_last_modify_time

Optional[datetime]: The time at which the result table's contents were modified. May be absent if no results have been written or the query has completed.

### result_set_last_replace_time

Optional[datetime]: The time at which the result table's contents were completely replaced. May be absent if no results have been written or the query has completed.

## Methods

### from_api_repr

`from_api_repr(resource) -> google.cloud.bigquery.job.query.IncrementalResultStats`


Factory: construct instance from the JSON repr.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job.IncrementalResultStats` |
stats parsed from `resource` . |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlStructType -->

# Class StandardSqlStructType (3.40.0)

```
StandardSqlStructType(
fields: typing.Optional[
typing.Iterable[google.cloud.bigquery.standard_sql.StandardSqlField]
] = None,
)
```


Type of a struct field.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType#StandardSqlStructType](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType#StandardSqlStructType)

## Parameter |
|
|---|---|
Name |
Description |
`fields` |
`typing.Optional[typing.Iterable[`
The fields in this struct. |

## Properties

### fields

The fields in this struct.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.standard_sql.StandardSqlStructType
```


Construct an SQL struct type instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL struct type.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.KeyResultStatementKind -->

# Class KeyResultStatementKind (3.40.0)

`KeyResultStatementKind()`


Determines which statement in the script represents the "key result".

The "key result" is used to populate the schema and query results of the script job.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PrimaryKey -->

# Class PrimaryKey (3.40.0)

`PrimaryKey(columns: typing.List[str])`


Represents the primary key constraint on a table's columns.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DistanceType -->

# Class DistanceType (3.40.0)

`DistanceType(value)`


Distance metric used to compute the distance between two points.
