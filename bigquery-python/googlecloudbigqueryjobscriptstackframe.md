---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame
fetched_at: 2026-01-25T03:15:48.746453
---

# Class ScriptStackFrame (3.40.0)


      
      Save and categorize content based on your preferences.

`ScriptStackFrame(resource)`


Stack frame showing the line/column/procedure name where the current evaluation happened.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### end_column

int: One-based end column.

### end_line

int: One-based end line.

### procedure_id

Optional[str]: Name of the active procedure.

Omitted if in a top-level script.

### start_column

int: One-based start column.

### start_line

int: One-based start line.

### text

str: Text of the current statement/expression.