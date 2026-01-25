---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base
fetched_at: 2026-01-25T02:08:16.353175
---

# Module base (3.40.0)


      
      Save and categorize content based on your preferences.

Base classes and helpers for job classes.

## Classes

[ReservationUsage](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ReservationUsage)

`ReservationUsage(name, slot_ms)`


Job resource usage for a reservation.

[ScriptStackFrame](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame)

`ScriptStackFrame(resource)`


Stack frame showing the line/column/procedure name where the current evaluation happened.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

[ScriptStatistics](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStatistics)

`ScriptStatistics(resource)`


Statistics for a child job of a script.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

[SessionInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.SessionInfo)

`SessionInfo(resource)`


[Preview] Information of the session if this job is part of one.

.. versionadded:: 2.29.0

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

[TransactionInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.TransactionInfo)

`TransactionInfo(transaction_id: str)`


[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

.. versionadded:: 2.24.0

[UnknownJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.UnknownJob)

`UnknownJob(job_id, client)`


A job whose type cannot be determined.