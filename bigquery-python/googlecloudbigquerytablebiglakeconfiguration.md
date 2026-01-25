---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration
fetched_at: 2026-01-25T03:17:48.395896
---

# Class BigLakeConfiguration (3.40.0)


      
      Save and categorize content based on your preferences.

```
BigLakeConfiguration(
connection_id: typing.Optional[str] = None,
storage_uri: typing.Optional[str] = None,
file_format: typing.Optional[str] = None,
table_format: typing.Optional[str] = None,
_properties: typing.Optional[dict] = None,
)
```


Configuration for managed tables for Apache Iceberg, formerly known as BigLake.

## Parameters |
|
|---|---|
Name |
Description |
`connection_id` |
`Optional[str]`
The connection specifying the credentials to be used to read and write to external storage, such as Cloud Storage. The connection_id can have the form |
`storage_uri` |
`Optional[str]`
The fully qualified location prefix of the external folder where table data is stored. The '*' wildcard character is not allowed. The URI should be in the format |
`file_format` |
`Optional[str]`
The file format the table data is stored in. See BigLakeFileFormat for available values. |
`table_format` |
`Optional[str]`
The table format the metadata only snapshots are stored in. See BigLakeTableFormat for available values. |
`_properties` |
`Optional[dict]`
Private. Used to construct object from API resource. |

## Properties

### connection_id

str: The connection specifying the credentials to be used to read and write to external storage, such as Cloud Storage.

### file_format

str: The file format the table data is stored in. See BigLakeFileFormat for available values.

### storage_uri

str: The fully qualified location prefix of the external folder where table data is stored.

### table_format

str: The table format the metadata only snapshots are stored in. See BigLakeTableFormat for available values.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.table.BigLakeConfiguration
```


Factory: construct a BigLakeConfiguration given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this BigLakeConfiguration.