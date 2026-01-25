---
merged_at: 2026-01-25T15:38:56.562761
merged_files: 2
---

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
