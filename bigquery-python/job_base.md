---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/job_base
fetched_at: 2026-01-25T03:11:31.224619
---

# Common Job Resource Classes

Base classes and helpers for job classes.

*class* google.cloud.bigquery.job.base.ReservationUsage(name, slot_ms)

Job resource usage for a reservation.

Create new instance of ReservationUsage(name, slot_ms)

#### name()

Reservation name or “unreserved” for on-demand resources usage.

#### slot_ms()

Total slot milliseconds used by the reservation for a particular job.

*class* google.cloud.bigquery.job.base.ScriptStackFrame(resource)

Stack frame showing the line/column/procedure name where the current evaluation happened.

**Parameters****resource**(*Map**[**str**, **Any**]*) – JSON representation of object.

*property* end_column()

One-based end column.

**Type**

*property* end_line()

One-based end line.

**Type**

*property* procedure_id()

Name of the active procedure.

Omitted if in a top-level script.

**Type**Optional[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

*property* start_column()

One-based start column.

**Type**

*property* start_line()

One-based start line.

**Type**

*property* text()

Text of the current statement/expression.

**Type**

*class* google.cloud.bigquery.job.base.ScriptStatistics(resource)

Statistics for a child job of a script.

**Parameters****resource**(*Map**[**str**, **Any**]*) – JSON representation of object.

*property* evaluation_kind(*: Optional[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

Indicates the type of child job.

Possible values include `STATEMENT`

and `EXPRESSION`

.

**Type**

*property* stack_frames(*: Sequence[google.cloud.bigquery.job.base.ScriptStackFrame* )

Stack trace where the current evaluation happened.

Shows line/column/procedure name of each frame on the stack at the point where the current evaluation happened.

The leaf frame is first, the primary script is last.

*class* google.cloud.bigquery.job.base.SessionInfo(resource)

[Preview] Information of the session if this job is part of one.

**Versionadded:** New in version 2.29.0.

**Parameters****resource**(*Map**[**str**, **Any**]*) – JSON representation of object.

*property* session_id(*: Optional[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

The ID of the session.

*class* google.cloud.bigquery.job.base.TransactionInfo(transaction_id: [str](https://docs.python.org/3/library/stdtypes.html#str))

[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

**Versionadded:** New in version 2.24.0.

Create new instance of TransactionInfo(transaction_id,)

#### transaction_id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

Output only. ID of the transaction.

*class* google.cloud.bigquery.job.base.UnknownJob(job_id, client)

A job whose type cannot be determined.

*classmethod* from_api_repr(resource: [dict](https://docs.python.org/3/library/stdtypes.html#dict), client)

Construct an UnknownJob from the JSON representation.

**Parameters****resource**(*Dict*) – JSON representation of a job.**client**() – Client connected to BigQuery API.*google.cloud.bigquery.client.Client*

**Returns**Job corresponding to the resource.

**Return type**UnknownJob