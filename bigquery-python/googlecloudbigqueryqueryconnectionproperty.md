---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty
fetched_at: 2026-01-25T02:10:17.551422
---

# Class ConnectionProperty (3.40.0)


      
      Save and categorize content based on your preferences.

`ConnectionProperty(key: str = "", value: str = "")`


A connection-level property to customize query behavior.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty](https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty)

## Parameters |
|
|---|---|
Name |
Description |
`key` |
`str`
The key of the property to set, for example, |
`value` |
`str`
The value of the property to set. |

## Properties

### key

Name of the property.

For example:

`time_zone`

`session_id`


### value

Value of the property.

## Methods

### from_api_repr

`from_api_repr(resource) -> google.cloud.bigquery.query.ConnectionProperty`


Construct xref_ConnectionProperty from JSON resource.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct JSON API representation for the connection property.