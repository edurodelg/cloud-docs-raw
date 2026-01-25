---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig
fetched_at: 2026-01-25T03:14:04.502317
---

# Class ExternalConfig (3.40.0)


      
      Save and categorize content based on your preferences.

`ExternalConfig(source_format)`


Description of an external data source.

## Parameter |
|
|---|---|
Name |
Description |
`source_format` |
`ExternalSourceFormat`
See |

## Properties

### autodetect

bool: If :data:`True`

, try to detect schema and format options
automatically.

### avro_options

Additional properties to set if `sourceFormat`

is set to AVRO.

### bigtable_options

Additional properties to set if `sourceFormat`

is set to BIGTABLE.

### compression

str: The compression type of the data source.

### connection_id

Optional[str]: ID of a BigQuery Connection API resource.

### csv_options

Additional properties to set if `sourceFormat`

is set to CSV.

### date_format

Optional[str]: Format used to parse DATE values. Supports C-style and SQL-style values.

### datetime_format

Optional[str]: Format used to parse DATETIME values. Supports C-style and SQL-style values.

### decimal_target_types

Possible SQL data types to which the source decimal values are converted.

.. versionadded:: 2.21.0

### google_sheets_options

Additional properties to set if `sourceFormat`

is set to
GOOGLE_SHEETS.

### hive_partitioning

Optional[`.external_config.HivePartitioningOptions`

]: When set, it configures hive partitioning support.

### ignore_unknown_values

bool: If :data:`True`

, extra values that are not represented in the
table schema are ignored. Defaults to :data:`False`

.

### max_bad_records

int: The maximum number of bad records that BigQuery can ignore when reading data.

### options

Source-specific options.

### parquet_options

Additional properties to set if `sourceFormat`

is set to PARQUET.

### reference_file_schema_uri

Optional[str]: When creating an external table, the user can provide a reference file with the table schema. This is enabled for the following formats:

AVRO, PARQUET, ORC

### schema

List[[SchemaField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField)]: The schema
for the data.

### source_format

`.external_config.ExternalSourceFormat`

:
Format of external source.

### source_uris

List[str]: URIs that point to your data in Google Cloud.

### time_format

Optional[str]: Format used to parse TIME values. Supports C-style and SQL-style values.

### time_zone

Optional[str]: Time zone used when parsing timestamp values that do not have specific time zone information (e.g. 2024-04-20 12:34:56). The expected format is an IANA timezone string (e.g. America/Los_Angeles).

### timestamp_format

Optional[str]: Format used to parse TIMESTAMP values. Supports C-style and SQL-style values.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.ExternalConfig
```


Factory: construct an `.external_config.ExternalConfig`

instance given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, Any]`
Definition of an |

Returns |
|
|---|---|
Type |
Description |
`ExternalConfig` |
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