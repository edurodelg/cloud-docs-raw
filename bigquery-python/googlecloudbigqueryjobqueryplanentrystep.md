---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntryStep
fetched_at: 2026-01-25T02:09:25.087724
---

# Class QueryPlanEntryStep (3.40.0)


      
      Save and categorize content based on your preferences.

`QueryPlanEntryStep(kind, substeps)`


Map a single step in a query plan entry.

## Parameters |
|
|---|---|
Name |
Description |
`kind` |
`str`
step type. |
`substeps` |
`List`
names of substeps. |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.query.QueryPlanEntryStep`


Factory: construct instance from the JSON repr.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON representation of the entry. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job.QueryPlanEntryStep` |
New instance built from the resource. |