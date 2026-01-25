---
merged_at: 2026-01-25T15:38:56.565671
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2types___googlecloudbigquerytablecolumnreference_googleclo_62c800.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2types.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types -->

# Package types (3.40.0)

API documentation for `bigquery_v2.types`

package.

## Classes

[DeleteModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.DeleteModelRequest)

[EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.EncryptionConfiguration)

[GetModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.GetModelRequest)

[ListModelsRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsRequest)

[ListModelsResponse](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsResponse)

[Model](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model)

[ModelReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ModelReference)

Id path of a model.

[PatchModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.PatchModelRequest)

[StandardSqlDataType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType)

The type of a variable, e.g., a function argument. Examples: INT64: {type_kind="INT64"} ARRAY: {type_kind="ARRAY", array_element_type="STRING"} STRUCT<x STRING, y ARRAY>: {type_kind="STRUCT", struct_type={fields=[ {name="x", type={type_kind="STRING"}}, {name="y", type={type_kind="ARRAY", array_element_type="DATE"}} ]}}

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[StandardSqlField](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlField)

A field or a column.

[StandardSqlStructType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlStructType)

[StandardSqlTableType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlTableType)

A table type


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquerytablecolumnreference_googlecloudbigqueryjobcompression__goo_458031.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerytablecolumnreference_googlecloudbigqueryjobcompression.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytablecolumnreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ColumnReference -->

# Class ColumnReference (3.40.0)

`ColumnReference(referencing_column: str, referenced_column: str)`


The pair of the foreign key column and primary key column.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobcompression.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Compression -->

# Class Compression (3.40.0)

`Compression(value)`


The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryjobdestinationformat_googlecloudbigqueryenumscompression.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobdestinationformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DestinationFormat -->

# Class DestinationFormat (3.40.0)

`DestinationFormat()`


The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumscompression.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Compression -->

# Class Compression (3.40.0)

`Compression(value)`


The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquerytablerangepartitioning_googlecloudbigquery_v2typesmodeltrai_ecb4b6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerytablerangepartitioning_googlecloudbigquery_v2typesmodeltrain_a24f52.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytablerangepartitioning.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning -->

# Class RangePartitioning (3.40.0)

`RangePartitioning(range_=None, field=None, _properties=None)`


Range-based partitioning configuration for a table.

## Parameters |
|
|---|---|
Name |
Description |
`range_` |
`Optional[`
Sets the range_ property. |
`field` |
`Optional[str]`
Sets the |
`_properties` |
`Optional[dict]`
Private. Used to construct object from API resource. |

## Properties

### field

str: The table is partitioned by this field.

The field must be a top-level `NULLABLE`

/ `REQUIRED`

field. The
only supported type is `INTEGER`

/ `INT64`

.

### range_

[google.cloud.bigquery.table.PartitionRange](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PartitionRange): Defines the
ranges for range partitioning.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not a `PartitionRange` . |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeltrainingruniterationresultarimaresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult -->

# Class ArimaResult (3.40.0)

`ArimaResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


(Auto-)arima fitting result. Wrap everything in ArimaResult for easier refactoring if we want to use model-specific iteration results.

## Attributes |
|
|---|---|
Name |
Description |
`arima_model_info` |
`Sequence[`
This message is repeated because there are multiple arima models fitted in auto-arima. For non-auto-arima model, its size is one. |
`seasonal_periods` |
`Sequence[`
Seasonal periods. Repeated because multiple periods are supported for one time series. |

## Classes

### ArimaCoefficients

`ArimaCoefficients(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima coefficients.

### ArimaModelInfo

`ArimaModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima model information.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytabletablereference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference -->

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
