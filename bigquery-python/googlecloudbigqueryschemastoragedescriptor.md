---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.StorageDescriptor
fetched_at: 2026-01-25T03:17:32.134508
---

# Class StorageDescriptor (3.40.0)


      
      Save and categorize content based on your preferences.

```
StorageDescriptor(
input_format: typing.Optional[str] = None,
location_uri: typing.Optional[str] = None,
output_format: typing.Optional[str] = None,
serde_info: typing.Optional[
typing.Union[google.cloud.bigquery.schema.SerDeInfo, dict]
] = None,
)
```


Contains information about how a table's data is stored and accessed by open source query engines.

## Parameters |
|
|---|---|
Name |
Description |
`input_format` |
`Optional[str]`
Specifies the fully qualified class name of the InputFormat (e.g. "org.apache.hadoop.hive.ql.io.orc.OrcInputFormat"). The maximum length is 128 characters. |
`location_uri` |
`Optional[str]`
The physical location of the table (e.g. 'gs://spark-dataproc-data/pangea-data/case_sensitive/' or 'gs://spark-dataproc-data/pangea-data/'). The maximum length is 2056 bytes. |
`output_format` |
`Optional[str]`
Specifies the fully qualified class name of the OutputFormat (e.g. "org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat"). The maximum length is 128 characters. |
`serde_info` |
`Union[SerDeInfo, dict, None]`
Serializer and deserializer information. |

## Properties

### input_format

Optional. Specifies the fully qualified class name of the InputFormat (e.g. "org.apache.hadoop.hive.ql.io.orc.OrcInputFormat"). The maximum length is 128 characters.

### location_uri

Optional. The physical location of the table (e.g. 'gs://spark- dataproc-data/pangea-data/case_sensitive/' or 'gs://spark-dataproc- data/pangea-data/'). The maximum length is 2056 bytes.

### output_format

Optional. Specifies the fully qualified class name of the OutputFormat (e.g. "org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat"). The maximum length is 128 characters.

### serde_info

Optional. Serializer and deserializer information.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.schema.StorageDescriptor`


Factory: constructs an instance of the class (cls) given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
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