---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptOptions
fetched_at: 2026-01-25T02:09:33.951313
---

# Class ScriptOptions (3.40.0)


      
      Save and categorize content based on your preferences.

```
ScriptOptions(
statement_timeout_ms: typing.Optional[int] = None,
statement_byte_budget: typing.Optional[int] = None,
key_result_statement: typing.Optional[
google.cloud.bigquery.enums.KeyResultStatementKind
] = None,
)
```


Options controlling the execution of scripts.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions)

## Properties

### key_result_statement

Determines which statement in the script represents the "key result".

This is used to populate the schema and query results of the script job.
Default is `KeyResultStatementKind.LAST`

.

### statement_byte_budget

Limit on the number of bytes billed per statement.

Exceeding this budget results in an error.

### statement_timeout_ms

Timeout period for each statement in a script.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.job.query.ScriptOptions
```


Factory: construct instance from the JSON repr.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.ScriptOptions` |
ScriptOptions sample parsed from `resource` . |

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation.