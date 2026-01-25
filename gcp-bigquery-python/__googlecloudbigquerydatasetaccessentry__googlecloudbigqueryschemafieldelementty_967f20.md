---
merged_at: 2026-01-25T15:38:56.566629
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerydatasetaccessentry__googlecloudbigqueryschemafieldelementtyp_3e6980.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydatasetaccessentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry -->

# Class AccessEntry (3.40.0)

```
AccessEntry(
role: typing.Optional[str] = None,
entity_type: typing.Optional[str] = None,
entity_id: typing.Optional[typing.Union[typing.Dict[str, typing.Any], str]] = None,
**kwargs
)
```


Represents grant of an access role to an entity.

An entry must have exactly one of the allowed
xref_EntityTypes. If anything but `view`

, `routine`

,
or `dataset`

are set, a `role`

is also required. `role`

is omitted for `view`

,
`routine`

, `dataset`

, because they are always read-only.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets).

## Parameters |
|
|---|---|
Name |
Description |
`role` |
`typing.Optional[str]`
Role granted to the entity. The following string values are supported: |
`entity_type` |
`typing.Optional[str]`
Type of entity being granted the role. See |
`entity_id` |
`typing.Union[typing.Dict[str, typing.Any], str, NoneType]`
If the |

## Properties

### condition

Optional[Condition]: The IAM condition associated with this entry.

### dataset

API resource representation of a dataset reference.

### dataset_target_types

Which resources that the dataset in this entry applies to.

### domain

A domain to grant access to.

### entity_id

The entity_id of the entry.

### entity_type

The entity_type of the entry.

### group_by_email

An email address of a Google Group to grant access to.

### role

The role of the entry.

### routine

API resource representation of a routine reference.

### special_group

A special group to grant access to.

### user_by_email

An email address of a user to grant access to.

### view

API resource representation of a view reference.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.dataset.AccessEntry`


Factory: construct an access entry given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Access entry resource representation returned from the API |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.dataset.AccessEntry` |
Access entry parsed from `resource` . |

### to_api_repr

`to_api_repr()`


Construct the API resource representation of this access entry

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Access entry represented as an API resource |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryschemafieldelementtype__googlecloudbigquery_v2typesmodelkmea_dd73b2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryschemafieldelementtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.FieldElementType -->

# Class FieldElementType (3.40.0)

`FieldElementType(element_type: str)`


Represents the type of a field element.

## Parameter |
|
|---|---|
Name |
Description |
`element_type` |
`str`
The type of a field element. |

## Methods

### from_api_repr

```
from_api_repr(
api_repr: typing.Optional[dict],
) -> typing.Optional[google.cloud.bigquery.schema.FieldElementType]
```


Factory: construct a FieldElementType given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Dict[str, str]`
field element type as returned from |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.FieldElementType` |
Python object, as parsed from `api_repr` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this field element type.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, str]` |
Field element type represented as an API resource. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelkmeansenumskmeansinitializationmethod_googleclo_ecbbb9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelkmeansenumskmeansinitializationmethod.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.KmeansEnums.KmeansInitializationMethod -->

# Class KmeansInitializationMethod (3.40.0)

`KmeansInitializationMethod(value)`


Indicates the method used to initialize the centroids for KMeans clustering algorithm.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobencoding.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Encoding -->

# Class Encoding (3.40.0)

`Encoding()`


The character encoding of the data. The default is `UTF_8`

.

BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryformat_optionsavrooptions__googlecloudbigqueryenumsencoding_99dafe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryformat_optionsavrooptions__googlecloudbigqueryenumsencoding__aa097e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryformat_optionsavrooptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.AvroOptions -->

# Class AvroOptions (3.40.0)

`AvroOptions()`


Options if source format is set to AVRO.

## Properties

### use_avro_logical_types

[Optional] If sourceFormat is set to 'AVRO', indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER).

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, bool],
) -> google.cloud.bigquery.format_options.AvroOptions
```


Factory: construct an instance from a resource dict.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, bool]`
Definition of a |

Returns |
|
|---|---|
Type |
Description |
|
Configuration parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, bool]` |
A dictionary in the format used by the BigQuery API. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumsencoding_googlecloudbigqueryjobbasereservationusage.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsencoding.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Encoding -->

# Class Encoding (3.40.0)

`Encoding()`


The character encoding of the data. The default is `UTF_8`

.

BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobbasereservationusage.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ReservationUsage -->

# Class ReservationUsage (3.40.0)

`ReservationUsage(name, slot_ms)`


Job resource usage for a reservation.

## Methods

### ReservationUsage

`ReservationUsage(name, slot_ms)`


Create new instance of ReservationUsage(name, slot_ms)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryjobincrementalresultstats_googlecloudbigquerystandard_sqlsta_f0e3e4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobincrementalresultstats.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.IncrementalResultStats -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerystandard_sqlstandardsqlstructtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlStructType -->

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
