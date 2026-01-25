---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SerDeInfo
fetched_at: 2026-01-25T03:17:30.108481
---

# Class SerDeInfo (3.40.0)


      
      Save and categorize content based on your preferences.

```
SerDeInfo(
serialization_library: str,
name: typing.Optional[str] = None,
parameters: typing.Optional[dict[str, str]] = None,
)
```


Serializer and deserializer information.

## Parameters |
|
|---|---|
Name |
Description |
`serialization_library` |
`str`
Required. Specifies a fully-qualified class name of the serialization library that is responsible for the translation of data between table representation and the underlying low-level input and output format structures. The maximum length is 256 characters. |
`name` |
`Optional[str]`
Name of the SerDe. The maximum length is 256 characters. |

## Properties

### name

Optional. Name of the SerDe. The maximum length is 256 characters.

### parameters

Optional. Key-value pairs that define the initialization parameters for the serialization library. Maximum size 10 Kib.

### serialization_library

Required. Specifies a fully-qualified class name of the serialization library that is responsible for the translation of data between table representation and the underlying low-level input and output format structures. The maximum length is 256 characters.

## Methods

### from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.schema.SerDeInfo`


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