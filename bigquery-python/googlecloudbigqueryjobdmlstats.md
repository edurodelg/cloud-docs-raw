---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats
fetched_at: 2026-01-25T02:08:57.997899
---

# Class DmlStats (3.40.0)


      
      Save and categorize content based on your preferences.

```
DmlStats(
inserted_row_count: int = 0, deleted_row_count: int = 0, updated_row_count: int = 0
)
```


Detailed statistics for DML statements.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats](https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats)

## Methods

### DmlStats

```
DmlStats(
inserted_row_count: int = 0, deleted_row_count: int = 0, updated_row_count: int = 0
)
```


Create new instance of DmlStats(inserted_row_count, deleted_row_count, updated_row_count)

### count

`count(value, /)`


Return number of occurrences of value.

### index

`index(value, start=0, stop=9223372036854775807, /)`


Return first index of value.

Raises ValueError if the value is not present.