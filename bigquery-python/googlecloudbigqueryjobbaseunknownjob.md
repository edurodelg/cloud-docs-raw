---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.UnknownJob
fetched_at: 2026-01-25T03:14:36.099470
---

# Class UnknownJob (3.40.0)


      
      Save and categorize content based on your preferences.

`UnknownJob(job_id, client)`


A job whose type cannot be determined.

## Methods

### from_api_repr

`from_api_repr(resource: dict, client) -> google.cloud.bigquery.job.base.UnknownJob`


Construct an UnknownJob from the JSON representation.

Parameters |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON representation of a job. |
`client` |
Client connected to BigQuery API. |

Returns |
|
|---|---|
Type |
Description |
`UnknownJob` |
Job corresponding to the resource. |