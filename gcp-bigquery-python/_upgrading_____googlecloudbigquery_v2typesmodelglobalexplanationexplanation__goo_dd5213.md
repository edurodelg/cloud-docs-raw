---
merged_at: 2026-01-29T15:47:08.988623
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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameter -->

# Class RangeQueryParameter (3.40.0)

`RangeQueryParameter(range_element_type, start=None, end=None, name=None)`


Named / positional query parameters for range values.

## Parameters |
|
|---|---|
Name |
Description |
`range_element_type` |
`Union[str, RangeQueryParameterType]`
The type of range elements. It must be one of 'TIMESTAMP', 'DATE', or 'DATETIME'. |
`start` |
`Optional[Union[ScalarQueryParameter, str]]`
The start of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`end` |
`Optional[Union[ScalarQueryParameter, str]]`
The end of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`name` |
`Optional[str]`
Parameter name, used via |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.RangeQueryParameter`


Factory: construct parameter from JSON resource.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON mapping of parameter |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.RangeQueryParameter` |
Instance |

### positional

```
positional(
range_element_type, start=None, end=None
) -> google.cloud.bigquery.query.RangeQueryParameter
```


Factory for positional parameters.

Parameters |
|
|---|---|
Name |
Description |
`range_element_type` |
`Union[str, RangeQueryParameterType]`
The type of range elements. It must be one of |
`start` |
`Optional[Union[ScalarQueryParameter, str]]`
The start of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`end` |
`Optional[Union[ScalarQueryParameter, str]]`
The end of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.RangeQueryParameter` |
Instance without name. |

### to_api_repr

`to_api_repr() -> dict`


Construct JSON API representation for the parameter.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference -->

# Class RoutineReference (3.40.0)

`RoutineReference()`


A pointer to a routine.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference)

## Properties

### dataset_id

str: ID of dataset containing the routine.

### path

str: URL path for the routine's APIs.

### project

str: ID of the project containing the routine.

### routine_id

str: The routine ID.

## Methods

### __eq__

`__eq__(other)`


Two RoutineReferences are equal if they point to the same routine.

### __str__

`__str__()`


String representation of the reference.

This is a fully-qualified ID, including the project ID and dataset ID.

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RoutineReference
```


Factory: construct a routine reference given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Routine reference representation returned from the API. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.RoutineReference` |
Routine reference parsed from `resource` . |

### from_string

```
from_string(
routine_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.routine.routine.RoutineReference
```


Factory: construct a routine reference from routine ID string.

Parameters |
|
|---|---|
Name |
Description |
`routine_id` |
`str`
A routine ID in standard SQL format. If |
`default_project` |
`Optional[str]`
The project ID to use when |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `routine_id` is not a fully-qualified routine ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.RoutineReference` |
Routine reference parsed from `routine_id` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine reference.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Routine reference represented as an API resource. |
