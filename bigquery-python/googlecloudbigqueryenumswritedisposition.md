---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.WriteDisposition
fetched_at: 2026-01-25T03:13:46.824663
---

# Class WriteDisposition (3.40.0)


      
      Save and categorize content based on your preferences.

`WriteDisposition()`


Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.