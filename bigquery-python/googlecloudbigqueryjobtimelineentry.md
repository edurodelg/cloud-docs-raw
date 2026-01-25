---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry
fetched_at: 2026-01-25T03:15:56.767647
---

# Class TimelineEntry (3.40.0)


      
      Save and categorize content based on your preferences.

`TimelineEntry()`


TimelineEntry represents progress of a query job at a particular point in time.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#querytimelinesample](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#querytimelinesample)
for the underlying API representation within query statistics.

## Properties

### active_units

Optional[int]: Current number of input units being processed by workers, reported as largest value since the last sample.

### completed_units

Optional[int]: Current number of input units completed by this query.

### elapsed_ms

Optional[int]: Milliseconds elapsed since start of query execution.

### pending_units

Optional[int]: Current number of input units remaining for query stages active at this sample time.

### slot_millis

Optional[int]: Cumulative slot-milliseconds consumed by this query.

## Methods

### from_api_repr

`from_api_repr(resource)`


Factory: construct instance from the JSON repr.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.TimelineEntry` |
Timeline sample parsed from `resource` . |