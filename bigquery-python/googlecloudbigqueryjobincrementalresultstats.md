---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.IncrementalResultStats
fetched_at: 2026-01-25T02:09:07.550770
---

# Class IncrementalResultStats (3.40.0)


      
      Save and categorize content based on your preferences.

`IncrementalResultStats()`


IncrementalResultStats provides information about incremental query execution.

## Properties

### disabled_reason

Optional[string]: Reason why incremental results were not written by the query.

### result_set_last_modify_time

Optional[datetime]: The time at which the result table's contents were modified. May be absent if no results have been written or the query has completed.

### result_set_last_replace_time

Optional[datetime]: The time at which the result table's contents were completely replaced. May be absent if no results have been written or the query has completed.

## Methods

### from_api_repr

`from_api_repr(resource) -> google.cloud.bigquery.job.query.IncrementalResultStats`


Factory: construct instance from the JSON repr.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job.IncrementalResultStats` |
stats parsed from `resource` . |