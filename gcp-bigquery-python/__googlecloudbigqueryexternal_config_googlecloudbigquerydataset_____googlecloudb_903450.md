---
merged_at: 2026-01-26T21:00:49.247589
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_config.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset -->

# Module dataset (3.40.0)

Define API Datasets.

## Classes

[AccessEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry)

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

Parameters |
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

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If a `view` , `routine` , or `dataset` has `role` set, or a non `view` , non `routine` , and non `dataset` **does not** have a `role` set. .. rubric:: Examples >>> entry = AccessEntry('OWNER', 'userByEmail', 'user@example.com') >>> view = { ... 'projectId': 'my-project', ... 'datasetId': 'my_dataset', ... 'tableId': 'my_table' ... } >>> entry = AccessEntry(None, 'view', view) |

[Condition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Condition)

```
Condition(
expression: str,
title: typing.Optional[str] = None,
description: typing.Optional[str] = None,
)
```


Represents a textual expression in the Common Expression Language (CEL) syntax.

Typically used for filtering or policy rules, such as in IAM Conditions or BigQuery row/column access policies.

See:
[https://cloud.google.com/iam/docs/reference/rest/Shared.Types/Expr](https://cloud.google.com/iam/docs/reference/rest/Shared.Types/Expr)
[https://github.com/google/cel-spec](https://github.com/google/cel-spec)

Parameters |
|
|---|---|
Name |
Description |
`expression` |
`str`
The condition expression string using CEL syntax. This is required. Example: |
`title` |
`Optional[str]`
An optional title for the condition, providing a short summary. Example: |
`description` |
`Optional[str]`
An optional description of the condition, providing a detailed explanation. Example: |

[Dataset](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset)

`Dataset(dataset_ref)`


Datasets are containers for tables.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#resource-dataset](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#resource-dataset)

Parameter |
|
|---|---|
Name |
Description |
`dataset_ref` |
`Union[`
A pointer to a dataset. If |

[DatasetListItem](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem)

`DatasetListItem(resource)`


A read-only dataset resource from a list operation.

For performance reasons, the BigQuery API only includes some of the dataset properties when listing datasets. Notably, xref_access_entries is missing.

For a full list of the properties that the BigQuery API returns, see the
```
REST documentation for datasets.list
<https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/list>
```

_.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, str]`
A dataset-like resource object from a dataset list response. A |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `datasetReference` or one of its required members is missing from `resource` . |

[DatasetReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference)

`DatasetReference(project: str, dataset_id: str)`


DatasetReferences are pointers to datasets.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference)

Parameters |
|
|---|---|
Name |
Description |
`project` |
`str`
The ID of the project |
`dataset_id` |
`str`
The ID of the dataset |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If either argument is not of type `str` . |

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigquerydbapiprogrammingerror_googlecloudbigquery_v2typesmodelmode_40f0d0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquerydbapiprogrammingerror_googlecloudbigquery_v2typesmodelmodel_4e610a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerydbapiprogrammingerror_googlecloudbigquery_v2typesmodelmodelt_e98b44.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapiprogrammingerror.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.ProgrammingError -->

# Class ProgrammingError (3.40.0)

DB-API exception raised for programming errors.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelmodeltype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ModelType -->

# Class ModelType (3.40.0)

`ModelType(value)`


Indicates the type of the Model.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerydbapiintegrityerror_googlecloudbigquerydbapiinternalerror.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapiintegrityerror.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.IntegrityError -->

# Class IntegrityError (3.40.0)

DB-API error when integrity of the database is affected.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapiinternalerror.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.InternalError -->

# Class InternalError (3.40.0)

DB-API error when the database encounters an internal error.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryenumsjobcreationmode_googlecloudbigqueryenumsentitytypes__g_db7559.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumsjobcreationmode_googlecloudbigqueryenumsentitytypes.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsjobcreationmode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.JobCreationMode -->

# Class JobCreationMode (3.40.0)

`JobCreationMode()`


Documented values for Job Creation Mode.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsentitytypes.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.EntityTypes -->

# Class EntityTypes (3.40.0)

`EntityTypes(value)`


Enum of allowed entity type names in AccessEntry


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumsupdatemode_googlecloudbigqueryenumsdatasetview.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsupdatemode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.UpdateMode -->

# Class UpdateMode (3.40.0)

`UpdateMode(value)`


Specifies the kind of information to update in a dataset.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsdatasetview.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DatasetView -->

# Class DatasetView (3.40.0)

`DatasetView(value)`


DatasetView specifies which dataset information is returned.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodelmulticlassclassificationmetricsconfusionmatrix_0e28c3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelmulticlassclassificationmetricsconfusionmatrix__fe3b20.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelmulticlassclassificationmetricsconfusionmatrix.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix -->

# Class ConfusionMatrix (3.40.0)

`ConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for multi-class classification models.

## Attributes |
|
|---|---|
Name |
Description |
`confidence_threshold` |
`google.protobuf.wrappers_pb2.DoubleValue`
Confidence threshold used when computing the entries of the confusion matrix. |
`rows` |
`Sequence[`
One row per actual label. |

## Classes

### Entry

`Entry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single entry in the confusion matrix.

### Row

`Row(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single row in the confusion matrix.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelglobalexplanation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.GlobalExplanation -->

# Class GlobalExplanation (3.40.0)

`GlobalExplanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Global explanations containing the top most important features after training.

## Attributes |
|
|---|---|
Name |
Description |
`explanations` |
`Sequence[`
A list of the top global explanations. Sorted by absolute value of attribution in descending order. |
`class_label` |
`str`
Class label for this set of global explanations. Will be empty/null for binary logistic and linear regression models. Sorted alphabetically in descending order. |

## Classes

### Explanation

`Explanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Explanation for a single feature.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_configbigtablecolumn.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn -->

# Class BigtableColumn (3.40.0)

`BigtableColumn()`


Options for a Bigtable column.

## Properties

### encoding

str: The encoding of the values when the type is not `STRING`


See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.encoding](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.encoding)

### field_name

str: An identifier to use if the qualifier is not a valid BigQuery field identifier

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.field_name](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.field_name)

### only_read_latest

bool: If this is set, only the latest version of value in this column are exposed.

### qualifier_encoded

Union[str, bytes]: The qualifier encoded in binary.

The type is `str`

(Python 2.x) or `bytes`

(Python 3.x). The module
will handle base64 encoding for you.

### qualifier_string

str: A valid UTF-8 string qualifier

### type_

str: The type to convert the value in cells of this column.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.type](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.type)

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableColumn
```


Factory: construct a `.external_config.BigtableColumn`

instance given its API representation.

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
`external_config.BigtableColumn` |
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
