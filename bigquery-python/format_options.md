---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/format_options
fetched_at: 2026-01-25T02:05:00.734889
---

# BigQuery Format Options

*class* google.cloud.bigquery.format_options.AvroOptions()

Options if source format is set to AVRO.

*classmethod* from_api_repr(resource: [Dict](https://docs.python.org/3/library/typing.html#typing.Dict)[[str](https://docs.python.org/3/library/stdtypes.html#str), [bool](https://docs.python.org/3/library/functions.html#bool)])

Factory: construct an instance from a resource dict.

**Parameters****resource**(*Dict**[**str**, *[*bool*](*]*) – Definition of a[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool))`AvroOptions`

instance in the same representation as is returned from the API.**Returns**Configuration parsed from

`resource`

.**Return type**`AvroOptions`


#### to_api_repr()

Build an API representation of this object.

*property* use_avro_logical_types(*: Optional[*[bool](https://docs.python.org/3/library/functions.html#bool) )

[bool](https://docs.python.org/3/library/functions.html#bool)

[Optional] If sourceFormat is set to ‘AVRO’, indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER).

*class* google.cloud.bigquery.format_options.ParquetOptions()

Additional options if the PARQUET source format is used.

*property* enable_list_inference(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

Indicates whether to use schema inference specifically for Parquet LIST logical type.

*property* enum_as_string(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

Indicates whether to infer Parquet ENUM logical type as STRING instead of BYTES by default.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#ParquetOptions.FIELDS.enum_as_string](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#ParquetOptions.FIELDS.enum_as_string)

*classmethod* from_api_repr(resource: [Dict](https://docs.python.org/3/library/typing.html#typing.Dict)[[str](https://docs.python.org/3/library/stdtypes.html#str), [bool](https://docs.python.org/3/library/functions.html#bool)])

Factory: construct an instance from a resource dict.

**Parameters****resource**(*Dict**[**str**, *[*bool*](*]*) – Definition of a[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool))`ParquetOptions`

instance in the same representation as is returned from the API.**Returns**Configuration parsed from

`resource`

.**Return type**`ParquetOptions`


*property* map_target_type(*: Optional[Union[*[bool](https://docs.python.org/3/library/functions.html#bool), [str](https://docs.python.org/3/library/stdtypes.html#str)] )

[bool](https://docs.python.org/3/library/functions.html#bool),

[str](https://docs.python.org/3/library/stdtypes.html#str)]

Indicates whether to simplify the representation of parquet maps to only show keys and values.

#### to_api_repr()

Build an API representation of this object.