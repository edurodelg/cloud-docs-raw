---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Condition
fetched_at: 2026-01-25T02:05:30.983905
---

# Class Condition (3.40.0)


      
      Save and categorize content based on your preferences.

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

## Parameters |
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

## Properties

### description

Optional[str]: The description for the condition.

### expression

str: The expression string for the condition.

### title

Optional[str]: The title for the condition.

## Methods

### __eq__

`__eq__(other: object) -> bool`


Check for equality based on expression, title, and description.

### __hash__

`__hash__() -> int`


Generate a hash based on expression, title, and description.

### __ne__

`__ne__(other: object) -> bool`


Check for inequality.

### __repr__

`__repr__() -> str`


Return a string representation of the Condition object.

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.dataset.Condition
```


Factory: construct a Condition instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this Condition.