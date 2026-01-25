---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStatistics
fetched_at: 2026-01-25T02:08:28.152916
---

# Class ScriptStatistics (3.40.0)


      
      Save and categorize content based on your preferences.

`ScriptStatistics(resource)`


Statistics for a child job of a script.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### evaluation_kind

str: Indicates the type of child job.

Possible values include `STATEMENT`

and `EXPRESSION`

.

### stack_frames

Stack trace where the current evaluation happened.

Shows line/column/procedure name of each frame on the stack at the point where the current evaluation happened.

The leaf frame is first, the primary script is last.