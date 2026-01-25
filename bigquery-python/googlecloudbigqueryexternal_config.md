---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config
fetched_at: 2026-01-25T02:07:27.213839
---

# Module external_config (3.40.0)


      
      Save and categorize content based on your preferences.

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