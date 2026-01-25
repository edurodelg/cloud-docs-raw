---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions
fetched_at: 2026-01-25T03:14:00.128735
---

# Class ExternalCatalogDatasetOptions (3.40.0)


      
      Save and categorize content based on your preferences.

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