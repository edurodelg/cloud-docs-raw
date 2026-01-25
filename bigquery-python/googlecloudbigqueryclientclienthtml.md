---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html
fetched_at: 2026-01-25T03:20:47.688755
---

# Class Client (3.40.0)


      
      Save and categorize content based on your preferences.

```
Client(
project: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
_http: typing.Optional[requests.sessions.Session] = None,
location: typing.Optional[str] = None,
default_query_job_config: typing.Optional[
google.cloud.bigquery.job.query.QueryJobConfig
] = None,
default_load_job_config: typing.Optional[
google.cloud.bigquery.job.load.LoadJobConfig
] = None,
client_info: typing.Optional[google.api_core.client_info.ClientInfo] = None,
client_options: typing.Optional[
typing.Union[
google.api_core.client_options.ClientOptions, typing.Dict[str, typing.Any]
]
] = None,
default_job_creation_mode: typing.Optional[str] = None,
)
```


Client to bundle configuration needed for API requests.

## Parameters |
|
|---|---|
Name |
Description |
`project` |
`Optional[str]`
Project ID for the project which the client acts on behalf of. Will be passed when creating a dataset / job. If not passed, falls back to the default inferred from the environment. |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The OAuth2 Credentials to use for this client. If not passed (and if no |
`_http` |
`Optional[requests.Session]`
HTTP object to make requests. Can be any object that defines |
`location` |
`Optional[str]`
Default location for jobs / datasets / tables. |
`default_query_job_config` |
`Optional[`
Default |
`default_load_job_config` |
`Optional[`
Default |
`client_info` |
`Optional[google.api_core.client_info.ClientInfo]`
The client info used to send a user-agent string along with API requests. If |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, Dict]]`
Client options used to set user options on the client. API Endpoint should be set through client_options. |
`default_job_creation_mode` |
`Optional[str]`
Sets the default job creation mode used by query methods such as query_and_wait(). For lightweight queries, JOB_CREATION_OPTIONAL is generally recommended. |

## Properties

### default_job_creation_mode

Default job creation mode used for query execution.

### default_load_job_config

Default `LoadJobConfig`

.
Will be merged into job configs passed into the `load_table_*`

methods.

### default_query_job_config

Default `QueryJobConfig`

or `None`

.

Will be merged into job configs passed into the `query`

or
`query_and_wait`

methods.

### location

Default location for jobs / datasets / tables.

## Methods

### cancel_job

```
cancel_job(
job_id: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> typing.Union[
google.cloud.bigquery.job.load.LoadJob,
google.cloud.bigquery.job.copy_.CopyJob,
google.cloud.bigquery.job.extract.ExtractJob,
google.cloud.bigquery.job.query.QueryJob,
]
```


Attempt to cancel a job from a job ID.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/cancel](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/cancel)

Parameters |
|
|---|---|
Name |
Description |
`job_id` |
`Union[ str, `
Job identifier. |
`project` |
`Optional[str]`
ID of the project which owns the job (defaults to the client's project). |
`location` |
`Optional[str]`
Location where the job was run. Ignored if |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
`Union[ ` |
Job instance, based on the resource returned by the API. |

### close

`close()`


Close the underlying transport objects, releasing system resources.

### copy_table

```
copy_table(
sources: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
typing.Sequence[
typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
]
],
],
destination: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
],
job_id: typing.Optional[str] = None,
job_id_prefix: typing.Optional[str] = None,
location: typing.Optional[str] = None,
project: typing.Optional[str] = None,
job_config: typing.Optional[google.cloud.bigquery.job.copy_.CopyJobConfig] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.job.copy_.CopyJob
```


Copy one or more tables to another table.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationtablecopy](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationtablecopy)

Parameters |
|
|---|---|
Name |
Description |
`sources` |
`Union[ `
Table or tables to be copied. |
`destination` |
`Union[ `
Table into which data is to be copied. |
`job_id` |
`Optional[str]`
The ID of the job. |
`job_id_prefix` |
`Optional[str]`
The user-provided prefix for a randomly generated job ID. This parameter will be ignored if a |
`location` |
`Optional[str]`
Location where to run the job. Must match the location of any source table as well as the destination table. |
`project` |
`Optional[str]`
Project ID of the project of where to run the job. Defaults to the client's project. |
`job_config` |
`Optional[`
Extra configuration options for the job. |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Exceptions |
|
|---|---|
Type |
Description |
`TypeError` |
If `job_config` is not an instance of
|

Returns |
|
|---|---|
Type |
Description |
|
A new copy job instance. |

### create_dataset

```
create_dataset(
dataset: typing.Union[
str,
google.cloud.bigquery.dataset.Dataset,
google.cloud.bigquery.dataset.DatasetReference,
google.cloud.bigquery.dataset.DatasetListItem,
],
exists_ok: bool = False,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.dataset.Dataset
```


API call: create the dataset via a POST request.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/insert](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/insert)

Example:

`from google.cloud import `[bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest)
client = [bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest).[Client](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)()
dataset = [bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest).[Dataset](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset.html)('my_project.my_dataset')
dataset = client.[create_dataset](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html#google_cloud_bigquery_client_Client_create_dataset)(dataset)


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`Union[ `
A |
`exists_ok` |
`Optional[bool]`
Defaults to |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Exceptions |
|
|---|---|
Type |
Description |
`google.cloud.exceptions.Conflict` |
If the dataset already exists. |

Returns |
|
|---|---|
Type |
Description |
|
A new `Dataset` returned from the API. |

### create_job

```
create_job(
job_config: dict,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> typing.Union[
google.cloud.bigquery.job.load.LoadJob,
google.cloud.bigquery.job.copy_.CopyJob,
google.cloud.bigquery.job.extract.ExtractJob,
google.cloud.bigquery.job.query.QueryJob,
]
```


Create a new job.

Parameters |
|
|---|---|
Name |
Description |
`job_config` |
`dict`
configuration job representation returned from the API. |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
`Union[ ` |
A new job instance. |

### create_routine

```
create_routine(
routine: google.cloud.bigquery.routine.routine.Routine,
exists_ok: bool = False,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.routine.routine.Routine
```


[Beta] Create a routine via a POST request.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines/insert](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines/insert)

Parameters |
|
|---|---|
Name |
Description |
`routine` |
A |
`exists_ok` |
`Optional[bool]`
Defaults to |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Exceptions |
|
|---|---|
Type |
Description |
`google.cloud.exceptions.Conflict` |
If the routine already exists. |

Returns |
|
|---|---|
Type |
Description |
|
A new `Routine` returned from the service. |

### create_table

```
create_table(
table: typing.Union[
str,
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
],
exists_ok: bool = False,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.table.Table
```


API call: create a table via a PUT request

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables/insert](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables/insert)

Parameters |
|
|---|---|
Name |
Description |
`table` |
`Union[ `
A |
`exists_ok` |
`Optional[bool]`
Defaults to |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Exceptions |
|
|---|---|
Type |
Description |
`google.cloud.exceptions.Conflict` |
If the table already exists. |

Returns |
|
|---|---|
Type |
Description |
|
A new `Table` returned from the service. |

### dataset

```
dataset(
dataset_id: str, project: typing.Optional[str] = None
) -> google.cloud.bigquery.dataset.DatasetReference
```


Deprecated: Construct a reference to a dataset.

As of`google-cloud-bigquery`

version 1.7.0, all client methods
that take a
xref_DatasetReference or
xref_TableReference also take a
string in standard SQL format, e.g. `project.dataset_id`

or
`project.dataset_id.table_id`

.
Parameters |
|
|---|---|
Name |
Description |
`dataset_id` |
`str`
ID of the dataset. |
`project` |
`Optional[str]`
Project ID for the dataset (defaults to the project of the client). |

Returns |
|
|---|---|
Type |
Description |
|
a new `DatasetReference` instance. |

### delete_dataset

```
delete_dataset(
dataset: typing.Union[
google.cloud.bigquery.dataset.Dataset,
google.cloud.bigquery.dataset.DatasetReference,
google.cloud.bigquery.dataset.DatasetListItem,
str,
],
delete_contents: bool = False,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
not_found_ok: bool = False,
) -> None
```


Delete a dataset.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/delete](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/delete)

Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`Union[ `
A reference to the dataset to delete. If a string is passed in, this method attempts to create a dataset reference from a string using |
`delete_contents` |
`Optional[bool]`
If True, delete all the tables in the dataset. If False and the dataset contains tables, the request will fail. Default is False. |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`not_found_ok` |
`Optional[bool]`
Defaults to |

### delete_job_metadata

```
delete_job_metadata(
job_id: typing.Union[
str,
google.cloud.bigquery.job.load.LoadJob,
google.cloud.bigquery.job.copy_.CopyJob,
google.cloud.bigquery.job.extract.ExtractJob,
google.cloud.bigquery.job.query.QueryJob,
],
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
not_found_ok: bool = False,
)
```


[Beta] Delete job metadata from job history.

Note: This does not stop a running job. Use xref_cancel_job instead.

Parameters |
|
|---|---|
Name |
Description |
`job_id` |
`Union[ str, LoadJob, CopyJob, ExtractJob, QueryJob ]`
Job or job identifier. |
`project` |
`Optional[str]`
ID of the project which owns the job (defaults to the client's project). |
`location` |
`Optional[str]`
Location where the job was run. Ignored if |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`not_found_ok` |
`Optional[bool]`
Defaults to |

### delete_model

```
delete_model(
model: typing.Union[
google.cloud.bigquery.model.Model,
google.cloud.bigquery.model.ModelReference,
str,
],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
not_found_ok: bool = False,
) -> None
```


[Beta] Delete a model

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models/delete](https://cloud.google.com/bigquery/docs/reference/rest/v2/models/delete)

Parameters |
|
|---|---|
Name |
Description |
`model` |
`Union[ `
A reference to the model to delete. If a string is passed in, this method attempts to create a model reference from a string using |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`not_found_ok` |
`Optional[bool]`
Defaults to |

### delete_routine

```
delete_routine(
routine: typing.Union[
google.cloud.bigquery.routine.routine.Routine,
google.cloud.bigquery.routine.routine.RoutineReference,
str,
],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
not_found_ok: bool = False,
) -> None
```


[Beta] Delete a routine.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines/delete](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines/delete)

Parameters |
|
|---|---|
Name |
Description |
`routine` |
`Union[ `
A reference to the routine to delete. If a string is passed in, this method attempts to create a routine reference from a string using |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`not_found_ok` |
`Optional[bool]`
Defaults to |

### delete_table

```
delete_table(
table: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
not_found_ok: bool = False,
) -> None
```


Delete a table

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables/delete](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables/delete)

Parameters |
|
|---|---|
Name |
Description |
`table` |
`Union[ `
A reference to the table to delete. If a string is passed in, this method attempts to create a table reference from a string using |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`not_found_ok` |
`Optional[bool]`
Defaults to |

### extract_table

```
extract_table(
source: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
google.cloud.bigquery.model.Model,
google.cloud.bigquery.model.ModelReference,
str,
],
destination_uris: typing.Union[str, typing.Sequence[str]],
job_id: typing.Optional[str] = None,
job_id_prefix: typing.Optional[str] = None,
location: typing.Optional[str] = None,
project: typing.Optional[str] = None,
job_config: typing.Optional[
google.cloud.bigquery.job.extract.ExtractJobConfig
] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
source_type: str = "Table",
) -> google.cloud.bigquery.job.extract.ExtractJob
```


Start a job to extract a table into Cloud Storage files.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationextract](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationextract)

Parameters |
|
|---|---|
Name |
Description |
`source` |
`Union[ `
Table or Model to be extracted. |
`destination_uris` |
`Union[str, Sequence[str]]`
URIs of Cloud Storage file(s) into which table data is to be extracted; in format |
`job_id` |
`Optional[str]`
The ID of the job. |
`job_id_prefix` |
`Optional[str]`
The user-provided prefix for a randomly generated job ID. This parameter will be ignored if a |
`location` |
`Optional[str]`
Location where to run the job. Must match the location of the source table. |
`project` |
`Optional[str]`
Project ID of the project of where to run the job. Defaults to the client's project. |
`job_config` |
`Optional[`
Extra configuration options for the job. |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`source_type` |
`Optional[str]`
Type of source to be extracted. |

Exceptions |
|
|---|---|
Type |
Description |
`TypeError` |
If `job_config` is not an instance of
|
`ValueError` |
If `source_type` is not among `Table` ,`Model` . |

Returns |
|
|---|---|
Type |
Description |
|
A new extract job instance. |

### get_dataset

```
get_dataset(
dataset_ref: typing.Union[google.cloud.bigquery.dataset.DatasetReference, str],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
dataset_view: typing.Optional[google.cloud.bigquery.enums.DatasetView] = None,
) -> google.cloud.bigquery.dataset.Dataset
```


Fetch the dataset referenced by `dataset_ref`


Parameters |
|
|---|---|
Name |
Description |
`dataset_ref` |
`Union[ `
A reference to the dataset to fetch from the BigQuery API. If a string is passed in, this method attempts to create a dataset reference from a string using |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`dataset_view` |
`Optional[`
Specifies the view that determines which dataset information is returned. By default, dataset metadata (e.g. friendlyName, description, labels, etc) and ACL information are returned. This argument can take on the following possible enum values. * |

Returns |
|
|---|---|
Type |
Description |
|
A `Dataset` instance. |

### get_iam_policy

```
get_iam_policy(
table: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
],
requested_policy_version: int = 1,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.api_core.iam.Policy
```


Return the access control policy for a table resource.

Parameters |
|
|---|---|
Name |
Description |
`table` |
`Union[ `
The table to get the access control policy for. If a string is passed in, this method attempts to create a table reference from a string using |
`requested_policy_version` |
`int`
Optional. The maximum policy version that will be used to format the policy. Only version |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.iam.Policy` |
The access control policy. |

### get_job

```
get_job(
job_id: typing.Union[
str,
google.cloud.bigquery.job.load.LoadJob,
google.cloud.bigquery.job.copy_.CopyJob,
google.cloud.bigquery.job.extract.ExtractJob,
google.cloud.bigquery.job.query.QueryJob,
],
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
) -> typing.Union[
google.cloud.bigquery.job.load.LoadJob,
google.cloud.bigquery.job.copy_.CopyJob,
google.cloud.bigquery.job.extract.ExtractJob,
google.cloud.bigquery.job.query.QueryJob,
google.cloud.bigquery.job.base.UnknownJob,
]
```


Fetch a job for the project associated with this client.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get)

Parameters |
|
|---|---|
Name |
Description |
`job_id` |
`Union[ str, job.LoadJob, job.CopyJob, job.ExtractJob, job.QueryJob ]`
Job identifier. |
`project` |
`Optional[str]`
ID of the project which owns the job (defaults to the client's project). |
`location` |
`Optional[str]`
Location where the job was run. Ignored if |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
`Union[job.LoadJob, job.CopyJob, job.ExtractJob, job.QueryJob, job.UnknownJob]` |
Job instance, based on the resource returned by the API. |

### get_model

```
get_model(
model_ref: typing.Union[google.cloud.bigquery.model.ModelReference, str],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.model.Model
```


[Beta] Fetch the model referenced by `model_ref`

.

Parameters |
|
|---|---|
Name |
Description |
`model_ref` |
`Union[ `
A reference to the model to fetch from the BigQuery API. If a string is passed in, this method attempts to create a model reference from a string using |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
|
A `Model` instance. |

### get_routine

```
get_routine(
routine_ref: typing.Union[
google.cloud.bigquery.routine.routine.Routine,
google.cloud.bigquery.routine.routine.RoutineReference,
str,
],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.routine.routine.Routine
```


[Beta] Get the routine referenced by `routine_ref`

.

Parameters |
|
|---|---|
Name |
Description |
`routine_ref` |
`Union[ `
A reference to the routine to fetch from the BigQuery API. If a string is passed in, this method attempts to create a reference from a string using |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the API call. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
|
A `Routine` instance. |

### get_service_account_email

```
get_service_account_email(
project: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> str
```


Get the email address of the project's BigQuery service account

Example:

`from google.cloud import `[bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest)
client = [bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest).[Client](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)()
client.[get_service_account_email](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html#google_cloud_bigquery_client_Client_get_service_account_email)()
# returns an email similar to: my_service_account@my-project.iam.gserviceaccount.com


Parameters |
|
|---|---|
Name |
Description |
`project` |
`Optional[str]`
Project ID to use for retreiving service account email. Defaults to the client's project. |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
`str` |
service account email address |

### get_table

```
get_table(
table: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.table.Table
```


Fetch the table referenced by `table`

.

Parameters |
|
|---|---|
Name |
Description |
`table` |
`Union[ `
A reference to the table to fetch from the BigQuery API. If a string is passed in, this method attempts to create a table reference from a string using |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
|
A `Table` instance. |

### insert_rows

```
insert_rows(
table: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
str,
],
rows: typing.Union[
typing.Iterable[typing.Tuple], typing.Iterable[typing.Mapping[str, typing.Any]]
],
selected_fields: typing.Optional[
typing.Sequence[google.cloud.bigquery.schema.SchemaField]
] = None,
**kwargs
) -> typing.Sequence[typing.Dict[str, typing.Any]]
```


Insert rows into a table via the streaming API.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tabledata/insertAll](https://cloud.google.com/bigquery/docs/reference/rest/v2/tabledata/insertAll)

BigQuery will reject insertAll payloads that exceed a defined limit (10MB). Additionally, if a payload vastly exceeds this limit, the request is rejected by the intermediate architecture, which returns a 413 (Payload Too Large) status code.

See
[https://cloud.google.com/bigquery/quotas#streaming_inserts](https://cloud.google.com/bigquery/quotas#streaming_inserts)

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keyword arguments to |
`table` |
`Union[ `
The destination table for the row data, or a reference to it. |
`rows` |
`Union[Sequence[Tuple], Sequence[Dict]]`
Row data to be inserted. If a list of tuples is given, each tuple should contain data for each schema field on the current table and in the same order as the schema fields. If a list of dictionaries is given, the keys must include all required fields in the schema. Keys which do not correspond to a field in the schema are ignored. |
`selected_fields` |
`Sequence[`
The fields to return. Required if |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
if table's schema is not set or `rows` is not a `Sequence` . |

Returns |
|
|---|---|
Type |
Description |
`Sequence[Mappings]` |
One mapping per row with insert errors: the "index" key identifies the row, and the "errors" key contains a list of the mappings describing one or more problems with the row. |

### insert_rows_from_dataframe

```
insert_rows_from_dataframe(
table: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
str,
],
dataframe,
selected_fields: typing.Optional[
typing.Sequence[google.cloud.bigquery.schema.SchemaField]
] = None,
chunk_size: int = 500,
**kwargs: typing.Dict
) -> typing.Sequence[typing.Sequence[dict]]
```


Insert rows into a table from a dataframe via the streaming API.

BigQuery will reject insertAll payloads that exceed a defined limit (10MB). Additionally, if a payload vastly exceeds this limit, the request is rejected by the intermediate architecture, which returns a 413 (Payload Too Large) status code.

See
[https://cloud.google.com/bigquery/quotas#streaming_inserts](https://cloud.google.com/bigquery/quotas#streaming_inserts)

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`Dict`
Keyword arguments to |
`table` |
`Union[ `
The destination table for the row data, or a reference to it. |
`dataframe` |
`pandas.DataFrame`
A |
`selected_fields` |
`Sequence[`
The fields to return. Required if |
`chunk_size` |
`int`
The number of rows to stream in a single chunk. Must be positive. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
if table's schema is not set |

Returns |
|
|---|---|
Type |
Description |
`Sequence[Sequence[Mappings]]` |
A list with insert errors for each insert chunk. Each element is a list containing one mapping per row with insert errors: the "index" key identifies the row, and the "errors" key contains a list of the mappings describing one or more problems with the row. |

### insert_rows_json

```
insert_rows_json(
table: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
],
json_rows: typing.Sequence[typing.Mapping[str, typing.Any]],
row_ids: typing.Optional[
typing.Union[
typing.Iterable[typing.Optional[str]],
google.cloud.bigquery.enums.AutoRowIDs,
]
] = AutoRowIDs.GENERATE_UUID,
skip_invalid_rows: typing.Optional[bool] = None,
ignore_unknown_values: typing.Optional[bool] = None,
template_suffix: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> typing.Sequence[dict]
```


Insert rows into a table without applying local type conversions.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tabledata/insertAll](https://cloud.google.com/bigquery/docs/reference/rest/v2/tabledata/insertAll)

BigQuery will reject insertAll payloads that exceed a defined limit (10MB). Additionally, if a payload vastly exceeds this limit, the request is rejected by the intermediate architecture, which returns a 413 (Payload Too Large) status code.

See
[https://cloud.google.com/bigquery/quotas#streaming_inserts](https://cloud.google.com/bigquery/quotas#streaming_inserts)

Parameters |
|
|---|---|
Name |
Description |
`table` |
`Union[ `
The destination table for the row data, or a reference to it. |
`json_rows` |
`Sequence[Dict]`
Row data to be inserted. Keys must match the table schema fields and values must be JSON-compatible representations. |
`row_ids` |
`Union[Iterable[str], AutoRowIDs, None]`
Unique IDs, one per row being inserted. An ID can also be |
`skip_invalid_rows` |
`Optional[bool]`
Insert all valid rows of a request, even if invalid rows exist. The default value is |
`ignore_unknown_values` |
`Optional[bool]`
Accept rows that contain values that do not match the schema. The unknown values are ignored. Default is |
`template_suffix` |
`Optional[str]`
Treat |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Exceptions |
|
|---|---|
Type |
Description |
`TypeError` |
if `json_rows` is not a `Sequence` . |

Returns |
|
|---|---|
Type |
Description |
`Sequence[Mappings]` |
One mapping per row with insert errors: the "index" key identifies the row, and the "errors" key contains a list of the mappings describing one or more problems with the row. |

### job_from_resource

```
job_from_resource(
resource: dict,
) -> typing.Union[
google.cloud.bigquery.job.copy_.CopyJob,
google.cloud.bigquery.job.extract.ExtractJob,
google.cloud.bigquery.job.load.LoadJob,
google.cloud.bigquery.job.query.QueryJob,
google.cloud.bigquery.job.base.UnknownJob,
]
```


Detect correct job type from resource and instantiate.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
one job resource from API response |

Returns |
|
|---|---|
Type |
Description |
`Union[job.CopyJob, job.ExtractJob, job.LoadJob, job.QueryJob, job.UnknownJob]` |
The job instance, constructed via the resource. |

### list_datasets

```
list_datasets(
project: typing.Optional[str] = None,
include_all: bool = False,
filter: typing.Optional[str] = None,
max_results: typing.Optional[int] = None,
page_token: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
page_size: typing.Optional[int] = None,
) -> google.api_core.page_iterator.Iterator
```


List datasets for the project associated with this client.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/list](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/list)

Parameters |
|
|---|---|
Name |
Description |
`project` |
`Optional[str]`
Project ID to use for retreiving datasets. Defaults to the client's project. |
`include_all` |
`Optional[bool]`
True if results include hidden datasets. Defaults to False. |
`filter` |
`Optional[str]`
An expression for filtering the results by label. For syntax, see |
`max_results` |
`Optional[int]`
Maximum number of datasets to return. |
`page_token` |
`Optional[str]`
Token representing a cursor into the datasets. If not passed, the API will return the first page of datasets. The token marks the beginning of the iterator to be returned and the value of the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`page_size` |
`Optional[int]`
Maximum number of datasets to return per page. |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.page_iterator.Iterator` |
Iterator of
|

### list_jobs

```
list_jobs(
project: typing.Optional[str] = None,
parent_job: typing.Optional[
typing.Union[google.cloud.bigquery.job.query.QueryJob, str]
] = None,
max_results: typing.Optional[int] = None,
page_token: typing.Optional[str] = None,
all_users: typing.Optional[bool] = None,
state_filter: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
min_creation_time: typing.Optional[datetime.datetime] = None,
max_creation_time: typing.Optional[datetime.datetime] = None,
page_size: typing.Optional[int] = None,
) -> google.api_core.page_iterator.Iterator
```


List jobs for the project associated with this client.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/list](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/list)

Parameters |
|
|---|---|
Name |
Description |
`project` |
`Optional[str]`
Project ID to use for retreiving datasets. Defaults to the client's project. |
`parent_job` |
`Optional[Union[ `
If set, retrieve only child jobs of the specified parent. |
`max_results` |
`Optional[int]`
Maximum number of jobs to return. |
`page_token` |
`Optional[str]`
Opaque marker for the next "page" of jobs. If not passed, the API will return the first page of jobs. The token marks the beginning of the iterator to be returned and the value of the |
`all_users` |
`Optional[bool]`
If true, include jobs owned by all users in the project. Defaults to :data: |
`state_filter` |
`Optional[str]`
If set, include only jobs matching the given state. One of: * |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`min_creation_time` |
`Optional[datetime.datetime]`
Min value for job creation time. If set, only jobs created after or at this timestamp are returned. If the datetime has no time zone assumes UTC time. |
`max_creation_time` |
`Optional[datetime.datetime]`
Max value for job creation time. If set, only jobs created before or at this timestamp are returned. If the datetime has no time zone assumes UTC time. |
`page_size` |
`Optional[int]`
Maximum number of jobs to return per page. |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.page_iterator.Iterator` |
Iterable of job instances. |

### list_models

```
list_models(
dataset: typing.Union[
google.cloud.bigquery.dataset.Dataset,
google.cloud.bigquery.dataset.DatasetReference,
google.cloud.bigquery.dataset.DatasetListItem,
str,
],
max_results: typing.Optional[int] = None,
page_token: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
page_size: typing.Optional[int] = None,
) -> google.api_core.page_iterator.Iterator
```


[Beta] List models in the dataset.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models/list](https://cloud.google.com/bigquery/docs/reference/rest/v2/models/list)

Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`Union[ `
A reference to the dataset whose models to list from the BigQuery API. If a string is passed in, this method attempts to create a dataset reference from a string using |
`max_results` |
`Optional[int]`
Maximum number of models to return. Defaults to a value set by the API. |
`page_token` |
`Optional[str]`
Token representing a cursor into the models. If not passed, the API will return the first page of models. The token marks the beginning of the iterator to be returned and the value of the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`page_size` |
`Optional[int] Returns: google.api_core.page_iterator.Iterator: Iterator of `
Maximum number of models to return per page. Defaults to a value set by the API. |

### list_partitions

```
list_partitions(
table: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> typing.Sequence[str]
```


List the partitions in a table.

Parameters |
|
|---|---|
Name |
Description |
`table` |
`Union[ `
The table or reference from which to get partition info |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
`List[str]` |
A list of the partition ids present in the partitioned table |

### list_projects

```
list_projects(
max_results: typing.Optional[int] = None,
page_token: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
page_size: typing.Optional[int] = None,
) -> google.api_core.page_iterator.Iterator
```


List projects for the project associated with this client.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/projects/list](https://cloud.google.com/bigquery/docs/reference/rest/v2/projects/list)

Parameters |
|
|---|---|
Name |
Description |
`max_results` |
`Optional[int]`
Maximum number of projects to return. Defaults to a value set by the API. |
`page_token` |
`Optional[str]`
Token representing a cursor into the projects. If not passed, the API will return the first page of projects. The token marks the beginning of the iterator to be returned and the value of the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`page_size` |
`Optional[int]`
Maximum number of projects to return in each page. Defaults to a value set by the API. |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.page_iterator.Iterator` |
Iterator of
|

### list_routines

```
list_routines(
dataset: typing.Union[
google.cloud.bigquery.dataset.Dataset,
google.cloud.bigquery.dataset.DatasetReference,
google.cloud.bigquery.dataset.DatasetListItem,
str,
],
max_results: typing.Optional[int] = None,
page_token: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
page_size: typing.Optional[int] = None,
) -> google.api_core.page_iterator.Iterator
```


[Beta] List routines in the dataset.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines/list](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines/list)

Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`Union[ `
A reference to the dataset whose routines to list from the BigQuery API. If a string is passed in, this method attempts to create a dataset reference from a string using |
`max_results` |
`Optional[int]`
Maximum number of routines to return. Defaults to a value set by the API. |
`page_token` |
`Optional[str]`
Token representing a cursor into the routines. If not passed, the API will return the first page of routines. The token marks the beginning of the iterator to be returned and the value of the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`page_size` |
`Optional[int] Returns: google.api_core.page_iterator.Iterator: Iterator of all `
Maximum number of routines to return per page. Defaults to a value set by the API. |

### list_rows

```
list_rows(
table: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableListItem,
google.cloud.bigquery.table.TableReference,
str,
],
selected_fields: typing.Optional[
typing.Sequence[google.cloud.bigquery.schema.SchemaField]
] = None,
max_results: typing.Optional[int] = None,
page_token: typing.Optional[str] = None,
start_index: typing.Optional[int] = None,
page_size: typing.Optional[int] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
*,
timestamp_precision: typing.Optional[
google.cloud.bigquery.enums.TimestampPrecision
] = None
) -> google.cloud.bigquery.table.RowIterator
```


List the rows of the table.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tabledata/list](https://cloud.google.com/bigquery/docs/reference/rest/v2/tabledata/list)

Parameters |
|
|---|---|
Name |
Description |
`table` |
`Union[ `
The table to list, or a reference to it. When the table object does not contain a schema and |
`selected_fields` |
`Sequence[`
The fields to return. If not supplied, data for all columns are downloaded. |
`max_results` |
`Optional[int]`
Maximum number of rows to return. |
`page_token` |
`Optional[str]`
Token representing a cursor into the table's rows. If not passed, the API will return the first page of the rows. The token marks the beginning of the iterator to be returned and the value of the |
`start_index` |
`Optional[int]`
The zero-based index of the starting row to read. |
`page_size` |
`Optional[int]`
The maximum number of rows in each page of results from this request. Non-positive values are ignored. Defaults to a sensible value set by the API. |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`timestamp_precision` |
`Optional[enums.TimestampPrecision]`
[Private Preview] If set to |

Returns |
|
|---|---|
Type |
Description |
|
Iterator of row data
`total_rows` attribute set, which counts the total number of rows **in the table** (this is distinct from the total number of rows in the current page: `iterator.page.num_items` ). |

### list_tables

```
list_tables(
dataset: typing.Union[
google.cloud.bigquery.dataset.Dataset,
google.cloud.bigquery.dataset.DatasetReference,
google.cloud.bigquery.dataset.DatasetListItem,
str,
],
max_results: typing.Optional[int] = None,
page_token: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
page_size: typing.Optional[int] = None,
) -> google.api_core.page_iterator.Iterator
```


List tables in the dataset.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables/list](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables/list)

Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`Union[ `
A reference to the dataset whose tables to list from the BigQuery API. If a string is passed in, this method attempts to create a dataset reference from a string using |
`max_results` |
`Optional[int]`
Maximum number of tables to return. Defaults to a value set by the API. |
`page_token` |
`Optional[str]`
Token representing a cursor into the tables. If not passed, the API will return the first page of tables. The token marks the beginning of the iterator to be returned and the value of the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`page_size` |
`Optional[int]`
Maximum number of tables to return per page. Defaults to a value set by the API. |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.page_iterator.Iterator` |
Iterator of
|

### load_table_from_dataframe

```
load_table_from_dataframe(
dataframe: pandas.DataFrame,
destination: Union[Table, TableReference, str],
num_retries: int = 6,
job_id: Optional[str] = None,
job_id_prefix: Optional[str] = None,
location: Optional[str] = None,
project: Optional[str] = None,
job_config: Optional[LoadJobConfig] = None,
parquet_compression: str = "snappy",
timeout: ResumableTimeoutType = None,
) -> job.LoadJob
```


Upload the contents of a table from a pandas DataFrame.

Similar to `load_table_from_uri`

, this method creates, starts and
returns a xref_LoadJob.

Parameters |
|
|---|---|
Name |
Description |
`dataframe` |
`pandas.Dataframe`
A |
`destination` |
`Union[ Table, TableReference, str ]`
The destination table to use for loading the data. If it is an existing table, the schema of the |
`num_retries` |
`Optional[int]`
Number of upload retries. Defaults to 6. |
`job_id` |
`Optional[str]`
Name of the job. |
`job_id_prefix` |
`Optional[str]`
The user-provided prefix for a randomly generated job ID. This parameter will be ignored if a |
`location` |
`Optional[str]`
Location where to run the job. Must match the location of the destination table. |
`project` |
`Optional[str]`
Project ID of the project of where to run the job. Defaults to the client's project. |
`job_config` |
`Optional[LoadJobConfig]`
Extra configuration options for the job. To override the default pandas data type conversions, supply a value for |
`parquet_compression` |
`Optional[str]`
[Beta] The compression method to use if intermittently serializing |
`timeout` |
`Optional[flaot]`
The number of seconds to wait for the underlying HTTP transport before using |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If a usable parquet engine cannot be found. This method requires `pyarrow` to be installed. |
`TypeError` |
If `job_config` is not an instance of
|

Returns |
|
|---|---|
Type |
Description |
|
A new load job. |

### load_table_from_file

```
load_table_from_file(
file_obj: typing.IO[bytes],
destination: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
],
rewind: bool = False,
size: typing.Optional[int] = None,
num_retries: int = 6,
job_id: typing.Optional[str] = None,
job_id_prefix: typing.Optional[str] = None,
location: typing.Optional[str] = None,
project: typing.Optional[str] = None,
job_config: typing.Optional[google.cloud.bigquery.job.load.LoadJobConfig] = None,
timeout: typing.Union[None, float, typing.Tuple[float, float]] = None,
) -> google.cloud.bigquery.job.load.LoadJob
```


Upload the contents of this table from a file-like object.

Similar to `load_table_from_uri`

, this method creates, starts and
returns a xref_LoadJob.

Parameters |
|
|---|---|
Name |
Description |
`file_obj` |
`IO[bytes]`
A file handle opened in binary mode for reading. |
`destination` |
`Union[Table, TableReference, TableListItem, str ]`
Table into which data is to be loaded. If a string is passed in, this method attempts to create a table reference from a string using |
`rewind` |
`Optional[bool]`
If True, seek to the beginning of the file handle before reading the file. Defaults to False. |
`size` |
`Optional[int]`
The number of bytes to read from the file handle. If size is |
`num_retries` |
`Optional[int]`
Number of upload retries. Defaults to 6. |
`job_id` |
`Optional[str]`
Name of the job. |
`job_id_prefix` |
`Optional[str]`
The user-provided prefix for a randomly generated job ID. This parameter will be ignored if a |
`location` |
`Optional[str]`
Location where to run the job. Must match the location of the destination table. |
`project` |
`Optional[str]`
Project ID of the project of where to run the job. Defaults to the client's project. |
`job_config` |
`Optional[LoadJobConfig]`
Extra configuration options for the job. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `size` is not passed in and can not be determined, or if the `file_obj` can be detected to be a file opened in text mode. |
`TypeError` |
If `job_config` is not an instance of
|

Returns |
|
|---|---|
Type |
Description |
|
A new load job. |

### load_table_from_json

```
load_table_from_json(
json_rows: typing.Iterable[typing.Dict[str, typing.Any]],
destination: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
],
num_retries: int = 6,
job_id: typing.Optional[str] = None,
job_id_prefix: typing.Optional[str] = None,
location: typing.Optional[str] = None,
project: typing.Optional[str] = None,
job_config: typing.Optional[google.cloud.bigquery.job.load.LoadJobConfig] = None,
timeout: typing.Union[None, float, typing.Tuple[float, float]] = None,
) -> google.cloud.bigquery.job.load.LoadJob
```


Upload the contents of a table from a JSON string or dict.

Parameters |
|
|---|---|
Name |
Description |
`json_rows` |
`Iterable[Dict[str, Any]]`
Row data to be inserted. Keys must match the table schema fields and values must be JSON-compatible representations. .. note:: If your data is already a newline-delimited JSON string, it is best to wrap it into a file-like object and pass it to |
`destination` |
`Union[ Table, TableReference, TableListItem, str ]`
Table into which data is to be loaded. If a string is passed in, this method attempts to create a table reference from a string using |
`num_retries` |
`Optional[int]`
Number of upload retries. Defaults to 6. |
`job_id` |
`Optional[str]`
Name of the job. |
`job_id_prefix` |
`Optional[str]`
The user-provided prefix for a randomly generated job ID. This parameter will be ignored if a |
`location` |
`Optional[str]`
Location where to run the job. Must match the location of the destination table. |
`project` |
`Optional[str]`
Project ID of the project of where to run the job. Defaults to the client's project. |
`job_config` |
`Optional[LoadJobConfig]`
Extra configuration options for the job. The |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Exceptions |
|
|---|---|
Type |
Description |
`TypeError` |
If `job_config` is not an instance of
|

Returns |
|
|---|---|
Type |
Description |
|
A new load job. |

### load_table_from_uri

```
load_table_from_uri(
source_uris: typing.Union[str, typing.Sequence[str]],
destination: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
],
job_id: typing.Optional[str] = None,
job_id_prefix: typing.Optional[str] = None,
location: typing.Optional[str] = None,
project: typing.Optional[str] = None,
job_config: typing.Optional[google.cloud.bigquery.job.load.LoadJobConfig] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.job.load.LoadJob
```


Starts a job for loading data into a table from Cloud Storage.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationload](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationload)

Parameters |
|
|---|---|
Name |
Description |
`source_uris` |
`Union[str, Sequence[str]]`
URIs of data files to be loaded; in format |
`destination` |
`Union[ `
Table into which data is to be loaded. If a string is passed in, this method attempts to create a table reference from a string using |
`job_id` |
`Optional[str]`
Name of the job. |
`job_id_prefix` |
`Optional[str]`
The user-provided prefix for a randomly generated job ID. This parameter will be ignored if a |
`location` |
`Optional[str]`
Location where to run the job. Must match the location of the destination table. |
`project` |
`Optional[str]`
Project ID of the project of where to run the job. Defaults to the client's project. |
`job_config` |
`Optional[`
Extra configuration options for the job. |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Exceptions |
|
|---|---|
Type |
Description |
`TypeError` |
If `job_config` is not an instance of
|

Returns |
|
|---|---|
Type |
Description |
|
A new load job. |

### query

```
query(
query: str,
job_config: typing.Optional[google.cloud.bigquery.job.query.QueryJobConfig] = None,
job_id: typing.Optional[str] = None,
job_id_prefix: typing.Optional[str] = None,
location: typing.Optional[str] = None,
project: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
job_retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
api_method: typing.Union[
str, google.cloud.bigquery.enums.QueryApiMethod
] = QueryApiMethod.INSERT,
*,
timestamp_precision: typing.Optional[
google.cloud.bigquery.enums.TimestampPrecision
] = None
) -> google.cloud.bigquery.job.query.QueryJob
```


Run a SQL query.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationquery](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfigurationquery)

Parameters |
|
|---|---|
Name |
Description |
`query` |
`str`
SQL query to be executed. Defaults to the standard SQL dialect. Use the |
`job_config` |
`Optional[`
Extra configuration options for the job. To override any options that were previously set in the |
`job_id` |
`Optional[str]`
ID to use for the query job. |
`job_id_prefix` |
`Optional[str]`
The prefix to use for a randomly generated job ID. This parameter will be ignored if a |
`location` |
`Optional[str]`
Location where to run the job. Must match the location of the table used in the query as well as the destination table. |
`project` |
`Optional[str]`
Project ID of the project of where to run the job. Defaults to the client's project. |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. This only applies to making RPC calls. It isn't used to retry failed jobs. This has a reasonable default that should only be overridden with care. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`job_retry` |
`Optional[google.api_core.retry.Retry]`
How to retry failed jobs. The default retries rate-limit-exceeded errors. Passing |
`api_method` |
`Union[str, enums.QueryApiMethod]`
Method with which to start the query job. By default, the jobs.insert API is used for starting a query. See |
`timestamp_precision` |
`Optional[enums.TimestampPrecision]`
[Private Preview] If set to |

Exceptions |
|
|---|---|
Type |
Description |
`TypeError` |
If `job_config` is not an instance of
`job_id` and non-`None` non-default `job_retry` are provided. |

Returns |
|
|---|---|
Type |
Description |
|
A new query job instance. |

### query_and_wait

```
query_and_wait(
query,
*,
job_config: typing.Optional[google.cloud.bigquery.job.query.QueryJobConfig] = None,
location: typing.Optional[str] = None,
project: typing.Optional[str] = None,
api_timeout: typing.Optional[float] = None,
wait_timeout: typing.Union[float, None, object] = object,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
job_retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
page_size: typing.Optional[int] = None,
max_results: typing.Optional[int] = None
) -> google.cloud.bigquery.table.RowIterator
```


Run the query, wait for it to finish, and return the results.

Parameters |
|
|---|---|
Name |
Description |
`query` |
`str`
SQL query to be executed. Defaults to the standard SQL dialect. Use the |
`job_config` |
`Optional[`
Extra configuration options for the job. To override any options that were previously set in the |
`location` |
`Optional[str]`
Location where to run the job. Must match the location of the table used in the query as well as the destination table. |
`project` |
`Optional[str]`
Project ID of the project of where to run the job. Defaults to the client's project. |
`api_timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`wait_timeout` |
`Optional[Union[float, object]]`
The number of seconds to wait for the query to finish. If the query doesn't finish before this timeout, the client attempts to cancel the query. If unset, the underlying REST API calls have timeouts, but we still wait indefinitely for the job to finish. |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. This only applies to making RPC calls. It isn't used to retry failed jobs. This has a reasonable default that should only be overridden with care. |
`job_retry` |
`Optional[google.api_core.retry.Retry]`
How to retry failed jobs. The default retries rate-limit-exceeded errors. Passing |
`page_size` |
`Optional[int]`
The maximum number of rows in each page of results from the initial jobs.query request. Non-positive values are ignored. |
`max_results` |
`Optional[int]`
The maximum total number of rows from this request. |

Exceptions |
|
|---|---|
Type |
Description |
`TypeError` |
If `job_config` is not an instance of
|

Returns |
|
|---|---|
Type |
Description |
|
Iterator of row data
`total_rows` attribute set, which counts the total number of rows **in the result set** (this is distinct from the total number of rows in the current page: `iterator.page.num_items` ). If the query is a special query that produces no results, e.g. a DDL query, an `_EmptyRowIterator` instance is returned. |

### schema_from_json

`schema_from_json(file_or_path: PathType) -> List[SchemaField]`


Takes a file object or file path that contains json that describes a table schema.

Returns |
|
|---|---|
Type |
Description |
`List[SchemaField]` |
List of
|

### schema_to_json

`schema_to_json(schema_list: Sequence[SchemaField], destination: PathType)`


Takes a list of schema field objects.

Serializes the list of schema field objects as json to a file.

Destination is a file path or a file object.

### set_iam_policy

```
set_iam_policy(
table: typing.Union[
google.cloud.bigquery.table.Table,
google.cloud.bigquery.table.TableReference,
google.cloud.bigquery.table.TableListItem,
str,
],
policy: google.api_core.iam.Policy,
updateMask: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
*,
fields: typing.Sequence[str] = ()
) -> google.api_core.iam.Policy
```


Return the access control policy for a table resource.

Parameters |
|
|---|---|
Name |
Description |
`table` |
`Union[ `
The table to get the access control policy for. If a string is passed in, this method attempts to create a table reference from a string using |
`policy` |
`google.api_core.iam.Policy`
The access control policy to set. |
`updateMask` |
`Optional[str]`
Mask as defined by |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`fields` |
`Sequence[str]`
Which properties to set on the policy. See: |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.iam.Policy` |
The updated access control policy. |

### update_dataset

```
update_dataset(
dataset: google.cloud.bigquery.dataset.Dataset,
fields: typing.Sequence[str],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
update_mode: typing.Optional[google.cloud.bigquery.enums.UpdateMode] = None,
) -> google.cloud.bigquery.dataset.Dataset
```


Change some fields of a dataset.

Use `fields`

to specify which fields to update. At least one field
must be provided. If a field is listed in `fields`

and is `None`

in
`dataset`

, it will be deleted.

For example, to update the default expiration times, specify
both properties in the `fields`

argument:

```
bigquery_client.update_dataset(
dataset,
[
"default_partition_expiration_ms",
"default_table_expiration_ms",
]
)
```


If `dataset.etag`

is not `None`

, the update will only
succeed if the dataset on the server has the same ETag. Thus
reading a dataset with `get_dataset`

, changing its fields,
and then passing it to `update_dataset`

will ensure that the changes
will only be saved if no modifications to the dataset occurred
since the read.

Parameters |
|
|---|---|
Name |
Description |
`dataset` |
The dataset to update. |
`fields` |
`Sequence[str]`
The properties of |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`update_mode` |
`Optional[`
Specifies the kind of information to update in a dataset. By default, dataset metadata (e.g. friendlyName, description, labels, etc) and ACL information are updated. This argument can take on the following possible enum values. * UPDATE_MODE_UNSPECIFIED: The default value. Behavior defaults to UPDATE_FULL. * |

Returns |
|
|---|---|
Type |
Description |
|
The modified `Dataset` instance. |

### update_model

```
update_model(
model: google.cloud.bigquery.model.Model,
fields: typing.Sequence[str],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.model.Model
```


[Beta] Change some fields of a model.

Use `fields`

to specify which fields to update. At least one field
must be provided. If a field is listed in `fields`

and is `None`

in `model`

, the field value will be deleted.

For example, to update the descriptive properties of the model,
specify them in the `fields`

argument:

```
bigquery_client.update_model(
model, ["description", "friendly_name"]
)
```


If `model.etag`

is not `None`

, the update will only succeed if
the model on the server has the same ETag. Thus reading a model with
`get_model`

, changing its fields, and then passing it to
`update_model`

will ensure that the changes will only be saved if
no modifications to the model occurred since the read.

Parameters |
|
|---|---|
Name |
Description |
`model` |
The model to update. |
`fields` |
`Sequence[str]`
The properties of |
`retry` |
`Optional[google.api_core.retry.Retry]`
A description of how to retry the API call. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
|
The model resource returned from the API call. |

### update_routine

```
update_routine(
routine: google.cloud.bigquery.routine.routine.Routine,
fields: typing.Sequence[str],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.routine.routine.Routine
```


[Beta] Change some fields of a routine.

Use `fields`

to specify which fields to update. At least one field
must be provided. If a field is listed in `fields`

and is `None`

in `routine`

, the field value will be deleted.

For example, to update the description property of the routine,
specify it in the `fields`

argument:

```
bigquery_client.update_routine(
routine, ["description"]
)
```


`None`

, the update will only succeed if the resource on the server
has the same ETag. Thus reading a routine with
xref_get_routine, changing
its fields, and then passing it to this method will ensure that the
changes will only be saved if no modifications to the resource
occurred since the read.
Parameters |
|
|---|---|
Name |
Description |
`routine` |
The routine to update. |
`fields` |
`Sequence[str]`
The fields of |
`retry` |
`Optional[google.api_core.retry.Retry]`
A description of how to retry the API call. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
|
The routine resource returned from the API call. |

### update_table

```
update_table(
table: google.cloud.bigquery.table.Table,
fields: typing.Sequence[str],
autodetect_schema: bool = False,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.table.Table
```


Change some fields of a table.

Use `fields`

to specify which fields to update. At least one field
must be provided. If a field is listed in `fields`

and is `None`

in `table`

, the field value will be deleted.

For example, to update the descriptive properties of the table,
specify them in the `fields`

argument:

```
bigquery_client.update_table(
table,
["description", "friendly_name"]
)
```


If `table.etag`

is not `None`

, the update will only succeed if
the table on the server has the same ETag. Thus reading a table with
`get_table`

, changing its fields, and then passing it to
`update_table`

will ensure that the changes will only be saved if
no modifications to the table occurred since the read.

Parameters |
|
|---|---|
Name |
Description |
`table` |
The table to update. |
`fields` |
`Sequence[str]`
The fields of |
`autodetect_schema` |
`bool`
Specifies if the schema of the table should be autodetected when updating the table from the underlying source. Only applicable for external tables. |
`retry` |
`Optional[google.api_core.retry.Retry]`
A description of how to retry the API call. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
|
The table resource returned from the API call. |