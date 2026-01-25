---
source_url: https://cloud.google.com/python/docs/reference/bigquery/latest/summary_method.html
fetched_at: 2026-01-25T15:38:43.573990
---

# Package Methods (3.40.0)

Summary of entries of Methods for bigquery.

### google.cloud.bigquery.dbapi.Binary

`Binary(data)`


Contruct a DB-API binary value.

See more: [google.cloud.bigquery.dbapi.Binary](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi#google_cloud_bigquery_dbapi_Binary)

### google.cloud.bigquery.dbapi.DateFromTicks

`DateFromTicks(timestamp, /)`


Create a date from a POSIX timestamp.

### google.cloud.bigquery.dbapi.TimeFromTicks

`TimeFromTicks(ticks, tz=None)`


Construct a DB-API time value from the given ticks value.

### google.cloud.bigquery.dbapi.TimestampFromTicks


timestamp[, tz] -> tz's local time from POSIX timestamp.

### google.cloud.bigquery.dbapi.connect

`connect(client=None, bqstorage_client=None, prefer_bqstorage_client=True)`


Construct a DB-API connection to Google BigQuery.

See more: [google.cloud.bigquery.dbapi.connect](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi#google_cloud_bigquery_dbapi_connect)

### google.cloud.bigquery.client.Client.cancel_job

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

### google.cloud.bigquery.client.Client.close

`close()`


Close the underlying transport objects, releasing system resources.

### google.cloud.bigquery.client.Client.copy_table

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

### google.cloud.bigquery.client.Client.create_dataset

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

See more: [google.cloud.bigquery.client.Client.create_dataset](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_create_dataset)

### google.cloud.bigquery.client.Client.create_job

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

### google.cloud.bigquery.client.Client.create_routine

```
create_routine(
routine: google.cloud.bigquery.routine.routine.Routine,
exists_ok: bool = False,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.routine.routine.Routine
```


[Beta] Create a routine via a POST request.

See more: [google.cloud.bigquery.client.Client.create_routine](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_create_routine)

### google.cloud.bigquery.client.Client.create_table

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


API call: create a table via a PUT request.

### google.cloud.bigquery.client.Client.dataset

```
dataset(
dataset_id: str, project: typing.Optional[str] = None
) -> google.cloud.bigquery.dataset.DatasetReference
```


Deprecated: Construct a reference to a dataset.

### google.cloud.bigquery.client.Client.delete_dataset

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

See more: [google.cloud.bigquery.client.Client.delete_dataset](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_delete_dataset)

### google.cloud.bigquery.client.Client.delete_job_metadata

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

See more: [google.cloud.bigquery.client.Client.delete_job_metadata](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_delete_job_metadata)

### google.cloud.bigquery.client.Client.delete_model

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


[Beta] Delete a model.

### google.cloud.bigquery.client.Client.delete_routine

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

See more: [google.cloud.bigquery.client.Client.delete_routine](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_delete_routine)

### google.cloud.bigquery.client.Client.delete_table

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


Delete a table.

### google.cloud.bigquery.client.Client.extract_table

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

### google.cloud.bigquery.client.Client.get_dataset

```
get_dataset(
dataset_ref: typing.Union[google.cloud.bigquery.dataset.DatasetReference, str],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
dataset_view: typing.Optional[google.cloud.bigquery.enums.DatasetView] = None,
) -> google.cloud.bigquery.dataset.Dataset
```


Fetch the dataset referenced by `dataset_ref`

.

### google.cloud.bigquery.client.Client.get_iam_policy

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

See more: [google.cloud.bigquery.client.Client.get_iam_policy](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_get_iam_policy)

### google.cloud.bigquery.client.Client.get_job

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

### google.cloud.bigquery.client.Client.get_model

```
get_model(
model_ref: typing.Union[google.cloud.bigquery.model.ModelReference, str],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.model.Model
```


[Beta] Fetch the model referenced by `model_ref`

.

### google.cloud.bigquery.client.Client.get_routine

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

### google.cloud.bigquery.client.Client.get_service_account_email

```
get_service_account_email(
project: typing.Optional[str] = None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> str
```


Get the email address of the project's BigQuery service account.

See more: [google.cloud.bigquery.client.Client.get_service_account_email](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_get_service_account_email)

### google.cloud.bigquery.client.Client.get_table

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

### google.cloud.bigquery.client.Client.insert_rows

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

### google.cloud.bigquery.client.Client.insert_rows_from_dataframe

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

See more: [google.cloud.bigquery.client.Client.insert_rows_from_dataframe](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_insert_rows_from_dataframe)

### google.cloud.bigquery.client.Client.insert_rows_json

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

See more: [google.cloud.bigquery.client.Client.insert_rows_json](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_insert_rows_json)

### google.cloud.bigquery.client.Client.job_from_resource

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

See more: [google.cloud.bigquery.client.Client.job_from_resource](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_job_from_resource)

### google.cloud.bigquery.client.Client.list_datasets

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

### google.cloud.bigquery.client.Client.list_jobs

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

### google.cloud.bigquery.client.Client.list_models

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

### google.cloud.bigquery.client.Client.list_partitions

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

See more: [google.cloud.bigquery.client.Client.list_partitions](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_list_partitions)

### google.cloud.bigquery.client.Client.list_projects

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

### google.cloud.bigquery.client.Client.list_routines

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

### google.cloud.bigquery.client.Client.list_rows

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

### google.cloud.bigquery.client.Client.list_tables

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

### google.cloud.bigquery.client.Client.load_table_from_dataframe

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

See more: [google.cloud.bigquery.client.Client.load_table_from_dataframe](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_load_table_from_dataframe)

### google.cloud.bigquery.client.Client.load_table_from_file

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

See more: [google.cloud.bigquery.client.Client.load_table_from_file](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_load_table_from_file)

### google.cloud.bigquery.client.Client.load_table_from_json

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

See more: [google.cloud.bigquery.client.Client.load_table_from_json](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_load_table_from_json)

### google.cloud.bigquery.client.Client.load_table_from_uri

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

See more: [google.cloud.bigquery.client.Client.load_table_from_uri](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_load_table_from_uri)

### google.cloud.bigquery.client.Client.query

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

### google.cloud.bigquery.client.Client.query_and_wait

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

See more: [google.cloud.bigquery.client.Client.query_and_wait](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_query_and_wait)

### google.cloud.bigquery.client.Client.schema_from_json

`schema_from_json(file_or_path: PathType) -> List[SchemaField]`


Takes a file object or file path that contains json that describes a table schema.

See more: [google.cloud.bigquery.client.Client.schema_from_json](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_schema_from_json)

### google.cloud.bigquery.client.Client.schema_to_json

`schema_to_json(schema_list: Sequence[SchemaField], destination: PathType)`


Takes a list of schema field objects.

See more: [google.cloud.bigquery.client.Client.schema_to_json](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_schema_to_json)

### google.cloud.bigquery.client.Client.set_iam_policy

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

See more: [google.cloud.bigquery.client.Client.set_iam_policy](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_set_iam_policy)

### google.cloud.bigquery.client.Client.update_dataset

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

See more: [google.cloud.bigquery.client.Client.update_dataset](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_update_dataset)

### google.cloud.bigquery.client.Client.update_model

```
update_model(
model: google.cloud.bigquery.model.Model,
fields: typing.Sequence[str],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.model.Model
```


[Beta] Change some fields of a model.

### google.cloud.bigquery.client.Client.update_routine

```
update_routine(
routine: google.cloud.bigquery.routine.routine.Routine,
fields: typing.Sequence[str],
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.routine.routine.Routine
```


[Beta] Change some fields of a routine.

See more: [google.cloud.bigquery.client.Client.update_routine](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_update_routine)

### google.cloud.bigquery.client.Client.update_table

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

### google.cloud.bigquery.client.Project.from_api_repr

`from_api_repr(resource)`


Factory: construct an instance from a resource dict.

See more: [google.cloud.bigquery.client.Project.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Project#google_cloud_bigquery_client_Project_from_api_repr)

### google.cloud.bigquery.dataset.AccessEntry.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.dataset.AccessEntry`


Factory: construct an access entry given its API representation .

See more: [google.cloud.bigquery.dataset.AccessEntry.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry#google_cloud_bigquery_dataset_AccessEntry_from_api_repr)

### google.cloud.bigquery.dataset.AccessEntry.to_api_repr

`to_api_repr()`


Construct the API resource representation of this access entry .

See more: [google.cloud.bigquery.dataset.AccessEntry.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry#google_cloud_bigquery_dataset_AccessEntry_to_api_repr)

### google.cloud.bigquery.dataset.Condition.__eq__

`__eq__(other: object) -> bool`


Check for equality based on expression, title, and description.

### google.cloud.bigquery.dataset.Condition.__hash__

`__hash__() -> int`


Generate a hash based on expression, title, and description.

### google.cloud.bigquery.dataset.Condition.__ne__

`__ne__(other: object) -> bool`


Check for inequality.

### google.cloud.bigquery.dataset.Condition.__repr__

`__repr__() -> str`


Return a string representation of the Condition object.

### google.cloud.bigquery.dataset.Condition.from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.dataset.Condition
```


Factory: construct a Condition instance given its API representation.

See more: [google.cloud.bigquery.dataset.Condition.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Condition#google_cloud_bigquery_dataset_Condition_from_api_repr)

### google.cloud.bigquery.dataset.Condition.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this Condition.

See more: [google.cloud.bigquery.dataset.Condition.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Condition#google_cloud_bigquery_dataset_Condition_to_api_repr)

### google.cloud.bigquery.dataset.Dataset.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.dataset.Dataset`


Factory: construct a dataset given its API representation .

See more: [google.cloud.bigquery.dataset.Dataset.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_from_api_repr)

### google.cloud.bigquery.dataset.Dataset.from_string

`from_string(full_dataset_id: str) -> google.cloud.bigquery.dataset.Dataset`


Construct a dataset from fully-qualified dataset ID.

### google.cloud.bigquery.dataset.Dataset.model

`model(model_id)`


Constructs a ModelReference.

### google.cloud.bigquery.dataset.Dataset.routine

`routine(routine_id)`


Constructs a RoutineReference.

### google.cloud.bigquery.dataset.Dataset.table

`table(table_id: str) -> google.cloud.bigquery.table.TableReference`


Constructs a TableReference.

### google.cloud.bigquery.dataset.Dataset.to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this dataset .

### google.cloud.bigquery.dataset.DatasetListItem.model

`model(model_id)`


Constructs a ModelReference.

See more: [google.cloud.bigquery.dataset.DatasetListItem.model](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem#google_cloud_bigquery_dataset_DatasetListItem_model)

### google.cloud.bigquery.dataset.DatasetListItem.routine

`routine(routine_id)`


Constructs a RoutineReference.

See more: [google.cloud.bigquery.dataset.DatasetListItem.routine](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem#google_cloud_bigquery_dataset_DatasetListItem_routine)

### google.cloud.bigquery.dataset.DatasetListItem.table

`table(table_id: str) -> google.cloud.bigquery.table.TableReference`


Constructs a TableReference.

See more: [google.cloud.bigquery.dataset.DatasetListItem.table](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem#google_cloud_bigquery_dataset_DatasetListItem_table)

### google.cloud.bigquery.dataset.DatasetReference.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.dataset.DatasetReference`


Factory: construct a dataset reference given its API representation .

See more: [google.cloud.bigquery.dataset.DatasetReference.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference#google_cloud_bigquery_dataset_DatasetReference_from_api_repr)

### google.cloud.bigquery.dataset.DatasetReference.from_string

```
from_string(
dataset_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.dataset.DatasetReference
```


Construct a dataset reference from dataset ID string.

See more: [google.cloud.bigquery.dataset.DatasetReference.from_string](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference#google_cloud_bigquery_dataset_DatasetReference_from_string)

### google.cloud.bigquery.dataset.DatasetReference.model

`model(model_id)`


Constructs a ModelReference.

See more: [google.cloud.bigquery.dataset.DatasetReference.model](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference#google_cloud_bigquery_dataset_DatasetReference_model)

### google.cloud.bigquery.dataset.DatasetReference.routine

`routine(routine_id)`


Constructs a RoutineReference.

See more: [google.cloud.bigquery.dataset.DatasetReference.routine](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference#google_cloud_bigquery_dataset_DatasetReference_routine)

### google.cloud.bigquery.dataset.DatasetReference.table

`table(table_id: str) -> google.cloud.bigquery.table.TableReference`


Constructs a TableReference.

See more: [google.cloud.bigquery.dataset.DatasetReference.table](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference#google_cloud_bigquery_dataset_DatasetReference_table)

### google.cloud.bigquery.dataset.DatasetReference.to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this dataset reference .

See more: [google.cloud.bigquery.dataset.DatasetReference.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference#google_cloud_bigquery_dataset_DatasetReference_to_api_repr)

### google.cloud.bigquery.dbapi.Connection.close

`close()`


Close the connection and any cursors created from it.

### google.cloud.bigquery.dbapi.Connection.commit

`commit()`


No-op, but for consistency raise an error if connection is closed.

### google.cloud.bigquery.dbapi.Connection.cursor

`cursor()`


Return a new cursor object.

### google.cloud.bigquery.dbapi.Cursor.close

`close()`


Mark the cursor as closed, preventing its further use.

See more: [google.cloud.bigquery.dbapi.Cursor.close](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Cursor#google_cloud_bigquery_dbapi_Cursor_close)

### google.cloud.bigquery.dbapi.Cursor.execute

`execute(operation, parameters=None, job_id=None, job_config=None)`


Prepare and execute a database operation.

### google.cloud.bigquery.dbapi.Cursor.executemany

`executemany(operation, seq_of_parameters)`


Prepare and execute a database operation multiple times.

### google.cloud.bigquery.dbapi.Cursor.fetchall

`fetchall()`


Fetch all remaining results from the last `execute*()`

call.

### google.cloud.bigquery.dbapi.Cursor.fetchmany

`fetchmany(size=None)`


Fetch multiple results from the last `execute*()`

call.

### google.cloud.bigquery.dbapi.Cursor.fetchone

`fetchone()`


Fetch a single row from the results of the last `execute*()`

call.

### google.cloud.bigquery.dbapi.Cursor.setinputsizes

`setinputsizes(sizes)`


No-op, but for consistency raise an error if cursor is closed.

### google.cloud.bigquery.dbapi.Cursor.setoutputsize

`setoutputsize(size, column=None)`


No-op, but for consistency raise an error if cursor is closed.

### google.cloud.bigquery.encryption_configuration.EncryptionConfiguration.from_api_repr

`from_api_repr(resource)`


Construct an encryption configuration from its API representation .

See more: [google.cloud.bigquery.encryption_configuration.EncryptionConfiguration.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration#google_cloud_bigquery_encryption_configuration_EncryptionConfiguration_from_api_repr)

### google.cloud.bigquery.encryption_configuration.EncryptionConfiguration.to_api_repr

`to_api_repr()`


Construct the API resource representation of this encryption configuration.

See more: [google.cloud.bigquery.encryption_configuration.EncryptionConfiguration.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration#google_cloud_bigquery_encryption_configuration_EncryptionConfiguration_to_api_repr)

### google.cloud.bigquery.external_config.BigtableColumn.from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableColumn
```


Factory: construct a `.external_config.BigtableColumn`

instance given its API representation.

See more: [google.cloud.bigquery.external_config.BigtableColumn.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn#google_cloud_bigquery_external_config_BigtableColumn_from_api_repr)

### google.cloud.bigquery.external_config.BigtableColumn.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.external_config.BigtableColumn.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn#google_cloud_bigquery_external_config_BigtableColumn_to_api_repr)

### google.cloud.bigquery.external_config.BigtableColumnFamily.from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableColumnFamily
```


Factory: construct a `.external_config.BigtableColumnFamily`

instance given its API representation.

See more: [google.cloud.bigquery.external_config.BigtableColumnFamily.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily#google_cloud_bigquery_external_config_BigtableColumnFamily_from_api_repr)

### google.cloud.bigquery.external_config.BigtableColumnFamily.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.external_config.BigtableColumnFamily.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily#google_cloud_bigquery_external_config_BigtableColumnFamily_to_api_repr)

### google.cloud.bigquery.external_config.BigtableOptions.from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableOptions
```


Factory: construct a `.external_config.BigtableOptions`

instance given its API representation.

See more: [google.cloud.bigquery.external_config.BigtableOptions.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableOptions#google_cloud_bigquery_external_config_BigtableOptions_from_api_repr)

### google.cloud.bigquery.external_config.BigtableOptions.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.external_config.BigtableOptions.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableOptions#google_cloud_bigquery_external_config_BigtableOptions_to_api_repr)

### google.cloud.bigquery.external_config.CSVOptions.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.external_config.CSVOptions`


Factory: construct a `.external_config.CSVOptions`

instance
given its API representation.

See more: [google.cloud.bigquery.external_config.CSVOptions.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions#google_cloud_bigquery_external_config_CSVOptions_from_api_repr)

### google.cloud.bigquery.external_config.CSVOptions.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.external_config.CSVOptions.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions#google_cloud_bigquery_external_config_CSVOptions_to_api_repr)

### google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions.from_api_repr

```
from_api_repr(
api_repr: dict,
) -> google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions
```


Factory: constructs an instance of the class (cls) given its API representation.

See more: [google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions#google_cloud_bigquery_external_config_ExternalCatalogDatasetOptions_from_api_repr)

### google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions#google_cloud_bigquery_external_config_ExternalCatalogDatasetOptions_to_api_repr)

### google.cloud.bigquery.external_config.ExternalCatalogTableOptions.from_api_repr

```
from_api_repr(
api_repr: dict,
) -> google.cloud.bigquery.external_config.ExternalCatalogTableOptions
```


Factory: constructs an instance of the class (cls) given its API representation.

See more: [google.cloud.bigquery.external_config.ExternalCatalogTableOptions.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogTableOptions#google_cloud_bigquery_external_config_ExternalCatalogTableOptions_from_api_repr)

### google.cloud.bigquery.external_config.ExternalCatalogTableOptions.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.external_config.ExternalCatalogTableOptions.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogTableOptions#google_cloud_bigquery_external_config_ExternalCatalogTableOptions_to_api_repr)

### google.cloud.bigquery.external_config.ExternalConfig.from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.ExternalConfig
```


Factory: construct an `.external_config.ExternalConfig`

instance given its API representation.

See more: [google.cloud.bigquery.external_config.ExternalConfig.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_from_api_repr)

### google.cloud.bigquery.external_config.ExternalConfig.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.external_config.ExternalConfig.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_to_api_repr)

### google.cloud.bigquery.external_config.GoogleSheetsOptions.from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.GoogleSheetsOptions
```


Factory: construct a `.external_config.GoogleSheetsOptions`

instance given its API representation.

See more: [google.cloud.bigquery.external_config.GoogleSheetsOptions.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.GoogleSheetsOptions#google_cloud_bigquery_external_config_GoogleSheetsOptions_from_api_repr)

### google.cloud.bigquery.external_config.GoogleSheetsOptions.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.external_config.GoogleSheetsOptions.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.GoogleSheetsOptions#google_cloud_bigquery_external_config_GoogleSheetsOptions_to_api_repr)

### google.cloud.bigquery.external_config.HivePartitioningOptions.from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.HivePartitioningOptions
```


Factory: construct a `.external_config.HivePartitioningOptions`

instance given its API representation.

See more: [google.cloud.bigquery.external_config.HivePartitioningOptions.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.HivePartitioningOptions#google_cloud_bigquery_external_config_HivePartitioningOptions_from_api_repr)

### google.cloud.bigquery.external_config.HivePartitioningOptions.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.external_config.HivePartitioningOptions.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.HivePartitioningOptions#google_cloud_bigquery_external_config_HivePartitioningOptions_to_api_repr)

### google.cloud.bigquery.format_options.AvroOptions.from_api_repr

```
from_api_repr(
resource: typing.Dict[str, bool],
) -> google.cloud.bigquery.format_options.AvroOptions
```


Factory: construct an instance from a resource dict.

See more: [google.cloud.bigquery.format_options.AvroOptions.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.AvroOptions#google_cloud_bigquery_format_options_AvroOptions_from_api_repr)

### google.cloud.bigquery.format_options.AvroOptions.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.format_options.AvroOptions.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.AvroOptions#google_cloud_bigquery_format_options_AvroOptions_to_api_repr)

### google.cloud.bigquery.format_options.ParquetOptions.from_api_repr

```
from_api_repr(
resource: typing.Dict[str, bool],
) -> google.cloud.bigquery.format_options.ParquetOptions
```


Factory: construct an instance from a resource dict.

See more: [google.cloud.bigquery.format_options.ParquetOptions.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions#google_cloud_bigquery_format_options_ParquetOptions_from_api_repr)

### google.cloud.bigquery.format_options.ParquetOptions.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.format_options.ParquetOptions.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions#google_cloud_bigquery_format_options_ParquetOptions_to_api_repr)

### google.cloud.bigquery.job.CopyJob.add_done_callback

`add_done_callback(fn)`


Add a callback to be executed when the operation is complete.

See more: [google.cloud.bigquery.job.CopyJob.add_done_callback](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_add_done_callback)

### google.cloud.bigquery.job.CopyJob.cancel

```
cancel(
client=None,
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: cancel job via a POST request.

See more: [google.cloud.bigquery.job.CopyJob.cancel](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_cancel)

### google.cloud.bigquery.job.CopyJob.cancelled

`cancelled()`


Check if the job has been cancelled.

### google.cloud.bigquery.job.CopyJob.done

```
done(
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
reload: bool = True,
) -> bool
```


Checks if the job is complete.

See more: [google.cloud.bigquery.job.CopyJob.done](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_done)

### google.cloud.bigquery.job.CopyJob.exception

`exception(timeout=object)`


Get the exception from the operation, blocking if necessary.

### google.cloud.bigquery.job.CopyJob.exists

```
exists(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: test for the existence of the job via a GET request.

See more: [google.cloud.bigquery.job.CopyJob.exists](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_exists)

### google.cloud.bigquery.job.CopyJob.from_api_repr

`from_api_repr(resource, client)`


Factory: construct a job given its API representation.

### google.cloud.bigquery.job.CopyJob.reload

```
reload(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
)
```


API call: refresh job properties via a GET request.

See more: [google.cloud.bigquery.job.CopyJob.reload](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_reload)

### google.cloud.bigquery.job.CopyJob.result

```
result(
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.job.base._AsyncJob
```


Start the job and wait for it to complete and get the result.

See more: [google.cloud.bigquery.job.CopyJob.result](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_result)

### google.cloud.bigquery.job.CopyJob.running

`running()`


True if the operation is currently running.

### google.cloud.bigquery.job.CopyJob.set_exception

`set_exception(exception)`


Set the Future's exception.

### google.cloud.bigquery.job.CopyJob.set_result

`set_result(result)`


Set the Future's result.

### google.cloud.bigquery.job.CopyJob.to_api_repr

`to_api_repr()`


Generate a resource for `_begin`

.

### google.cloud.bigquery.job.CopyJobConfig.__setattr__

`__setattr__(name, value)`


Override to be able to raise error if an unknown property is being set.

### google.cloud.bigquery.job.CopyJobConfig.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.base._JobConfig`


Factory: construct a job configuration given its API representation .

See more: [google.cloud.bigquery.job.CopyJobConfig.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig#google_cloud_bigquery_job_CopyJobConfig_from_api_repr)

### google.cloud.bigquery.job.CopyJobConfig.to_api_repr

`to_api_repr() -> dict`


Build an API representation of the job config.

See more: [google.cloud.bigquery.job.CopyJobConfig.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig#google_cloud_bigquery_job_CopyJobConfig_to_api_repr)

### google.cloud.bigquery.job.DmlStats

```
DmlStats(
inserted_row_count: int = 0, deleted_row_count: int = 0, updated_row_count: int = 0
)
```


Create new instance of DmlStats(inserted_row_count, deleted_row_count, updated_row_count).

See more: [google.cloud.bigquery.job.DmlStats](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats#google_cloud_bigquery_job_DmlStats_DmlStats)

### google.cloud.bigquery.job.DmlStats.count

`count(value, /)`


Return number of occurrences of value.

See more: [google.cloud.bigquery.job.DmlStats.count](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats#google_cloud_bigquery_job_DmlStats_count)

### google.cloud.bigquery.job.DmlStats.index

`index(value, start=0, stop=9223372036854775807, /)`


Return first index of value.

See more: [google.cloud.bigquery.job.DmlStats.index](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats#google_cloud_bigquery_job_DmlStats_index)

### google.cloud.bigquery.job.ExtractJob.add_done_callback

`add_done_callback(fn)`


Add a callback to be executed when the operation is complete.

See more: [google.cloud.bigquery.job.ExtractJob.add_done_callback](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_add_done_callback)

### google.cloud.bigquery.job.ExtractJob.cancel

```
cancel(
client=None,
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: cancel job via a POST request.

### google.cloud.bigquery.job.ExtractJob.cancelled

`cancelled()`


Check if the job has been cancelled.

### google.cloud.bigquery.job.ExtractJob.done

```
done(
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
reload: bool = True,
) -> bool
```


Checks if the job is complete.

### google.cloud.bigquery.job.ExtractJob.exception

`exception(timeout=object)`


Get the exception from the operation, blocking if necessary.

### google.cloud.bigquery.job.ExtractJob.exists

```
exists(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: test for the existence of the job via a GET request.

### google.cloud.bigquery.job.ExtractJob.from_api_repr

```
from_api_repr(
resource: dict, client
) -> google.cloud.bigquery.job.extract.ExtractJob
```


Factory: construct a job given its API representation.

See more: [google.cloud.bigquery.job.ExtractJob.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_from_api_repr)

### google.cloud.bigquery.job.ExtractJob.reload

```
reload(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
)
```


API call: refresh job properties via a GET request.

### google.cloud.bigquery.job.ExtractJob.result

```
result(
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.job.base._AsyncJob
```


Start the job and wait for it to complete and get the result.

### google.cloud.bigquery.job.ExtractJob.running

`running()`


True if the operation is currently running.

### google.cloud.bigquery.job.ExtractJob.set_exception

`set_exception(exception)`


Set the Future's exception.

See more: [google.cloud.bigquery.job.ExtractJob.set_exception](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_set_exception)

### google.cloud.bigquery.job.ExtractJob.set_result

`set_result(result)`


Set the Future's result.

### google.cloud.bigquery.job.ExtractJob.to_api_repr

`to_api_repr()`


Generate a resource for `_begin`

.

### google.cloud.bigquery.job.ExtractJobConfig.__setattr__

`__setattr__(name, value)`


Override to be able to raise error if an unknown property is being set.

See more: [google.cloud.bigquery.job.ExtractJobConfig. setattr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig#google_cloud_bigquery_job_ExtractJobConfig___setattr__)

### google.cloud.bigquery.job.ExtractJobConfig.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.base._JobConfig`


Factory: construct a job configuration given its API representation .

See more: [google.cloud.bigquery.job.ExtractJobConfig.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig#google_cloud_bigquery_job_ExtractJobConfig_from_api_repr)

### google.cloud.bigquery.job.ExtractJobConfig.to_api_repr

`to_api_repr() -> dict`


Build an API representation of the job config.

See more: [google.cloud.bigquery.job.ExtractJobConfig.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig#google_cloud_bigquery_job_ExtractJobConfig_to_api_repr)

### google.cloud.bigquery.job.IncrementalResultStats.from_api_repr

`from_api_repr(resource) -> google.cloud.bigquery.job.query.IncrementalResultStats`


Factory: construct instance from the JSON repr.

See more: [google.cloud.bigquery.job.IncrementalResultStats.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.IncrementalResultStats#google_cloud_bigquery_job_IncrementalResultStats_from_api_repr)

### google.cloud.bigquery.job.LoadJob.add_done_callback

`add_done_callback(fn)`


Add a callback to be executed when the operation is complete.

See more: [google.cloud.bigquery.job.LoadJob.add_done_callback](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_add_done_callback)

### google.cloud.bigquery.job.LoadJob.cancel

```
cancel(
client=None,
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: cancel job via a POST request.

See more: [google.cloud.bigquery.job.LoadJob.cancel](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_cancel)

### google.cloud.bigquery.job.LoadJob.cancelled

`cancelled()`


Check if the job has been cancelled.

### google.cloud.bigquery.job.LoadJob.done

```
done(
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
reload: bool = True,
) -> bool
```


Checks if the job is complete.

See more: [google.cloud.bigquery.job.LoadJob.done](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_done)

### google.cloud.bigquery.job.LoadJob.exception

`exception(timeout=object)`


Get the exception from the operation, blocking if necessary.

### google.cloud.bigquery.job.LoadJob.exists

```
exists(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: test for the existence of the job via a GET request.

See more: [google.cloud.bigquery.job.LoadJob.exists](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_exists)

### google.cloud.bigquery.job.LoadJob.from_api_repr

`from_api_repr(resource: dict, client) -> google.cloud.bigquery.job.load.LoadJob`


Factory: construct a job given its API representation.

### google.cloud.bigquery.job.LoadJob.reload

```
reload(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
)
```


API call: refresh job properties via a GET request.

See more: [google.cloud.bigquery.job.LoadJob.reload](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_reload)

### google.cloud.bigquery.job.LoadJob.result

```
result(
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.job.base._AsyncJob
```


Start the job and wait for it to complete and get the result.

See more: [google.cloud.bigquery.job.LoadJob.result](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_result)

### google.cloud.bigquery.job.LoadJob.running

`running()`


True if the operation is currently running.

### google.cloud.bigquery.job.LoadJob.set_exception

`set_exception(exception)`


Set the Future's exception.

### google.cloud.bigquery.job.LoadJob.set_result

`set_result(result)`


Set the Future's result.

### google.cloud.bigquery.job.LoadJob.to_api_repr

`to_api_repr()`


Generate a resource for `_begin`

.

### google.cloud.bigquery.job.LoadJobConfig.__setattr__

`__setattr__(name, value)`


Override to be able to raise error if an unknown property is being set.

### google.cloud.bigquery.job.LoadJobConfig.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.base._JobConfig`


Factory: construct a job configuration given its API representation .

See more: [google.cloud.bigquery.job.LoadJobConfig.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_from_api_repr)

### google.cloud.bigquery.job.LoadJobConfig.to_api_repr

`to_api_repr() -> dict`


Build an API representation of the job config.

See more: [google.cloud.bigquery.job.LoadJobConfig.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_to_api_repr)

### google.cloud.bigquery.job.QueryJob.add_done_callback

`add_done_callback(fn)`


Add a callback to be executed when the operation is complete.

See more: [google.cloud.bigquery.job.QueryJob.add_done_callback](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_add_done_callback)

### google.cloud.bigquery.job.QueryJob.cancel

```
cancel(
client=None,
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: cancel job via a POST request.

### google.cloud.bigquery.job.QueryJob.cancelled

`cancelled()`


Check if the job has been cancelled.

### google.cloud.bigquery.job.QueryJob.done

```
done(
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
reload: bool = True,
) -> bool
```


Checks if the job is complete.

See more: [google.cloud.bigquery.job.QueryJob.done](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_done)

### google.cloud.bigquery.job.QueryJob.exception

`exception(timeout=object)`


Get the exception from the operation, blocking if necessary.

### google.cloud.bigquery.job.QueryJob.exists

```
exists(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: test for the existence of the job via a GET request.

### google.cloud.bigquery.job.QueryJob.from_api_repr

`from_api_repr(resource: dict, client: Client) -> QueryJob`


Factory: construct a job given its API representation .

### google.cloud.bigquery.job.QueryJob.reload

```
reload(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
)
```


API call: refresh job properties via a GET request.

### google.cloud.bigquery.job.QueryJob.result

```
result(
page_size: typing.Optional[int] = None,
max_results: typing.Optional[int] = None,
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[typing.Union[float, object]] = object,
start_index: typing.Optional[int] = None,
job_retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
) -> typing.Union[RowIterator, google.cloud.bigquery.table._EmptyRowIterator]
```


Start the job and wait for it to complete and get the result.

### google.cloud.bigquery.job.QueryJob.running

`running()`


True if the operation is currently running.

### google.cloud.bigquery.job.QueryJob.set_exception

`set_exception(exception)`


Set the Future's exception.

### google.cloud.bigquery.job.QueryJob.set_result

`set_result(result)`


Set the Future's result.

### google.cloud.bigquery.job.QueryJob.to_api_repr

`to_api_repr()`


Generate a resource for `_begin`

.

### google.cloud.bigquery.job.QueryJob.to_arrow

```
to_arrow(
progress_bar_type: typing.Optional[str] = None,
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
create_bqstorage_client: bool = True,
max_results: typing.Optional[int] = None,
) -> pyarrow.Table
```


[Beta] Create a class:`pyarrow.Table`

by loading all pages of a
table or query.

### google.cloud.bigquery.job.QueryJob.to_dataframe

```
to_dataframe(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
progress_bar_type: typing.Optional[str] = None,
create_bqstorage_client: bool = True,
max_results: typing.Optional[int] = None,
geography_as_object: bool = False,
bool_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.BOOL_DTYPE,
int_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.INT_DTYPE,
float_dtype: typing.Optional[typing.Any] = None,
string_dtype: typing.Optional[typing.Any] = None,
date_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.DATE_DTYPE,
datetime_dtype: typing.Optional[typing.Any] = None,
time_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.TIME_DTYPE,
timestamp_dtype: typing.Optional[typing.Any] = None,
range_date_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_DATE_DTYPE,
range_datetime_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_DATETIME_DTYPE,
range_timestamp_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_TIMESTAMP_DTYPE,
) -> pandas.DataFrame
```


Return a pandas DataFrame from a QueryJob .

### google.cloud.bigquery.job.QueryJob.to_geodataframe

```
to_geodataframe(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
progress_bar_type: typing.Optional[str] = None,
create_bqstorage_client: bool = True,
max_results: typing.Optional[int] = None,
geography_column: typing.Optional[str] = None,
bool_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.BOOL_DTYPE,
int_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.INT_DTYPE,
float_dtype: typing.Optional[typing.Any] = None,
string_dtype: typing.Optional[typing.Any] = None,
) -> geopandas.GeoDataFrame
```


Return a GeoPandas GeoDataFrame from a QueryJob .

See more: [google.cloud.bigquery.job.QueryJob.to_geodataframe](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_to_geodataframe)

### google.cloud.bigquery.job.QueryJobConfig.__setattr__

`__setattr__(name, value)`


Override to be able to raise error if an unknown property is being set.

### google.cloud.bigquery.job.QueryJobConfig.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.base._JobConfig`


Factory: construct a job configuration given its API representation .

See more: [google.cloud.bigquery.job.QueryJobConfig.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_from_api_repr)

### google.cloud.bigquery.job.QueryJobConfig.to_api_repr

`to_api_repr() -> dict`


Build an API representation of the query job config.

See more: [google.cloud.bigquery.job.QueryJobConfig.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_to_api_repr)

### google.cloud.bigquery.job.QueryPlanEntry.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.query.QueryPlanEntry`


Factory: construct instance from the JSON repr.

See more: [google.cloud.bigquery.job.QueryPlanEntry.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_from_api_repr)

### google.cloud.bigquery.job.QueryPlanEntryStep.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.query.QueryPlanEntryStep`


Factory: construct instance from the JSON repr.

See more: [google.cloud.bigquery.job.QueryPlanEntryStep.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntryStep#google_cloud_bigquery_job_QueryPlanEntryStep_from_api_repr)

### google.cloud.bigquery.job.ReservationUsage

`ReservationUsage(name, slot_ms)`


Create new instance of ReservationUsage(name, slot_ms).

### google.cloud.bigquery.job.ReservationUsage.count

`count(value, /)`


Return number of occurrences of value.

### google.cloud.bigquery.job.ReservationUsage.index

`index(value, start=0, stop=9223372036854775807, /)`


Return first index of value.

### google.cloud.bigquery.job.ScriptOptions.from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.job.query.ScriptOptions
```


Factory: construct instance from the JSON repr.

See more: [google.cloud.bigquery.job.ScriptOptions.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptOptions#google_cloud_bigquery_job_ScriptOptions_from_api_repr)

### google.cloud.bigquery.job.ScriptOptions.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation.

See more: [google.cloud.bigquery.job.ScriptOptions.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptOptions#google_cloud_bigquery_job_ScriptOptions_to_api_repr)

### google.cloud.bigquery.job.TimelineEntry.from_api_repr

`from_api_repr(resource)`


Factory: construct instance from the JSON repr.

See more: [google.cloud.bigquery.job.TimelineEntry.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry#google_cloud_bigquery_job_TimelineEntry_from_api_repr)

### google.cloud.bigquery.job.TransactionInfo

`TransactionInfo(transaction_id: str)`


Create new instance of TransactionInfo(transaction_id,).

### google.cloud.bigquery.job.TransactionInfo.count

`count(value, /)`


Return number of occurrences of value.

### google.cloud.bigquery.job.TransactionInfo.index

`index(value, start=0, stop=9223372036854775807, /)`


Return first index of value.

### google.cloud.bigquery.job.UnknownJob.add_done_callback

`add_done_callback(fn)`


Add a callback to be executed when the operation is complete.

See more: [google.cloud.bigquery.job.UnknownJob.add_done_callback](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob#google_cloud_bigquery_job_UnknownJob_add_done_callback)

### google.cloud.bigquery.job.UnknownJob.cancel

```
cancel(
client=None,
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: cancel job via a POST request.

### google.cloud.bigquery.job.UnknownJob.cancelled

`cancelled()`


Check if the job has been cancelled.

### google.cloud.bigquery.job.UnknownJob.done

```
done(
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
reload: bool = True,
) -> bool
```


Checks if the job is complete.

### google.cloud.bigquery.job.UnknownJob.exception

`exception(timeout=object)`


Get the exception from the operation, blocking if necessary.

### google.cloud.bigquery.job.UnknownJob.exists

```
exists(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: test for the existence of the job via a GET request.

### google.cloud.bigquery.job.UnknownJob.from_api_repr

`from_api_repr(resource: dict, client) -> google.cloud.bigquery.job.base.UnknownJob`


Construct an UnknownJob from the JSON representation.

See more: [google.cloud.bigquery.job.UnknownJob.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob#google_cloud_bigquery_job_UnknownJob_from_api_repr)

### google.cloud.bigquery.job.UnknownJob.reload

```
reload(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
)
```


API call: refresh job properties via a GET request.

### google.cloud.bigquery.job.UnknownJob.result

```
result(
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.job.base._AsyncJob
```


Start the job and wait for it to complete and get the result.

### google.cloud.bigquery.job.UnknownJob.running

`running()`


True if the operation is currently running.

### google.cloud.bigquery.job.UnknownJob.set_exception

`set_exception(exception)`


Set the Future's exception.

See more: [google.cloud.bigquery.job.UnknownJob.set_exception](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob#google_cloud_bigquery_job_UnknownJob_set_exception)

### google.cloud.bigquery.job.UnknownJob.set_result

`set_result(result)`


Set the Future's result.

### google.cloud.bigquery.job.UnknownJob.to_api_repr

`to_api_repr()`


Generate a resource for the job.

### google.cloud.bigquery.job.base.ReservationUsage

`ReservationUsage(name, slot_ms)`


Create new instance of ReservationUsage(name, slot_ms).

### google.cloud.bigquery.job.base.TransactionInfo

`TransactionInfo(transaction_id: str)`


Create new instance of TransactionInfo(transaction_id,).

### google.cloud.bigquery.job.base.UnknownJob.from_api_repr

`from_api_repr(resource: dict, client) -> google.cloud.bigquery.job.base.UnknownJob`


Construct an UnknownJob from the JSON representation.

See more: [google.cloud.bigquery.job.base.UnknownJob.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.UnknownJob#google_cloud_bigquery_job_base_UnknownJob_from_api_repr)

### google.cloud.bigquery.model.Model.from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.model.Model
```


Factory: construct a model resource given its API representation .

### google.cloud.bigquery.model.Model.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this model.

### google.cloud.bigquery.model.ModelReference.from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.model.ModelReference
```


Factory: construct a model reference given its API representation.

See more: [google.cloud.bigquery.model.ModelReference.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference#google_cloud_bigquery_model_ModelReference_from_api_repr)

### google.cloud.bigquery.model.ModelReference.from_string

```
from_string(
model_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.model.ModelReference
```


Construct a model reference from model ID string.

See more: [google.cloud.bigquery.model.ModelReference.from_string](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference#google_cloud_bigquery_model_ModelReference_from_string)

### google.cloud.bigquery.model.ModelReference.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this model reference.

See more: [google.cloud.bigquery.model.ModelReference.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference#google_cloud_bigquery_model_ModelReference_to_api_repr)

### google.cloud.bigquery.model.TransformColumn.from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.model.TransformColumn
```


Constructs a transform column feature given its API representation .

See more: [google.cloud.bigquery.model.TransformColumn.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.TransformColumn#google_cloud_bigquery_model_TransformColumn_from_api_repr)

### google.cloud.bigquery.query.ArrayQueryParameter.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.ArrayQueryParameter`


Factory: construct parameter from JSON resource.

See more: [google.cloud.bigquery.query.ArrayQueryParameter.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter#google_cloud_bigquery_query_ArrayQueryParameter_from_api_repr)

### google.cloud.bigquery.query.ArrayQueryParameter.positional

```
positional(
array_type: str, values: list
) -> google.cloud.bigquery.query.ArrayQueryParameter
```


Factory for positional parameters.

See more: [google.cloud.bigquery.query.ArrayQueryParameter.positional](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter#google_cloud_bigquery_query_ArrayQueryParameter_positional)

### google.cloud.bigquery.query.ArrayQueryParameter.to_api_repr

`to_api_repr() -> dict`


Construct JSON API representation for the parameter.

See more: [google.cloud.bigquery.query.ArrayQueryParameter.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter#google_cloud_bigquery_query_ArrayQueryParameter_to_api_repr)

### google.cloud.bigquery.query.ArrayQueryParameterType.from_api_repr

`from_api_repr(resource)`


Factory: construct parameter type from JSON resource.

See more: [google.cloud.bigquery.query.ArrayQueryParameterType.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameterType#google_cloud_bigquery_query_ArrayQueryParameterType_from_api_repr)

### google.cloud.bigquery.query.ArrayQueryParameterType.to_api_repr

`to_api_repr()`


Construct JSON API representation for the parameter type.

See more: [google.cloud.bigquery.query.ArrayQueryParameterType.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameterType#google_cloud_bigquery_query_ArrayQueryParameterType_to_api_repr)

### google.cloud.bigquery.query.ConnectionProperty.from_api_repr

`from_api_repr(resource) -> google.cloud.bigquery.query.ConnectionProperty`


Construct xref_ConnectionProperty from JSON resource.

See more: [google.cloud.bigquery.query.ConnectionProperty.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty#google_cloud_bigquery_query_ConnectionProperty_from_api_repr)

### google.cloud.bigquery.query.ConnectionProperty.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct JSON API representation for the connection property.

See more: [google.cloud.bigquery.query.ConnectionProperty.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty#google_cloud_bigquery_query_ConnectionProperty_to_api_repr)

### google.cloud.bigquery.query.RangeQueryParameter.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.RangeQueryParameter`


Factory: construct parameter from JSON resource.

See more: [google.cloud.bigquery.query.RangeQueryParameter.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameter#google_cloud_bigquery_query_RangeQueryParameter_from_api_repr)

### google.cloud.bigquery.query.RangeQueryParameter.positional

```
positional(
range_element_type, start=None, end=None
) -> google.cloud.bigquery.query.RangeQueryParameter
```


Factory for positional parameters.

See more: [google.cloud.bigquery.query.RangeQueryParameter.positional](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameter#google_cloud_bigquery_query_RangeQueryParameter_positional)

### google.cloud.bigquery.query.RangeQueryParameter.to_api_repr

`to_api_repr() -> dict`


Construct JSON API representation for the parameter.

See more: [google.cloud.bigquery.query.RangeQueryParameter.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameter#google_cloud_bigquery_query_RangeQueryParameter_to_api_repr)

### google.cloud.bigquery.query.RangeQueryParameterType.from_api_repr

`from_api_repr(resource)`


Factory: construct parameter type from JSON resource.

See more: [google.cloud.bigquery.query.RangeQueryParameterType.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameterType#google_cloud_bigquery_query_RangeQueryParameterType_from_api_repr)

### google.cloud.bigquery.query.RangeQueryParameterType.to_api_repr

`to_api_repr()`


Construct JSON API representation for the parameter type.

See more: [google.cloud.bigquery.query.RangeQueryParameterType.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameterType#google_cloud_bigquery_query_RangeQueryParameterType_to_api_repr)

### google.cloud.bigquery.query.RangeQueryParameterType.with_name

`with_name(new_name: typing.Optional[str])`


Return a copy of the instance with `name`

set to `new_name`

.

See more: [google.cloud.bigquery.query.RangeQueryParameterType.with_name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameterType#google_cloud_bigquery_query_RangeQueryParameterType_with_name)

### google.cloud.bigquery.query.ScalarQueryParameter.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.ScalarQueryParameter`


Factory: construct parameter from JSON resource.

See more: [google.cloud.bigquery.query.ScalarQueryParameter.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameter#google_cloud_bigquery_query_ScalarQueryParameter_from_api_repr)

### google.cloud.bigquery.query.ScalarQueryParameter.positional

```
positional(
type_: typing.Union[str, google.cloud.bigquery.query.ScalarQueryParameterType],
value: typing.Optional[
typing.Union[
str, int, float, decimal.Decimal, bool, datetime.datetime, datetime.date
]
],
) -> google.cloud.bigquery.query.ScalarQueryParameter
```


Factory for positional paramater.

See more: [google.cloud.bigquery.query.ScalarQueryParameter.positional](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameter#google_cloud_bigquery_query_ScalarQueryParameter_positional)

### google.cloud.bigquery.query.ScalarQueryParameter.to_api_repr

`to_api_repr() -> dict`


Construct JSON API representation for the parameter.

See more: [google.cloud.bigquery.query.ScalarQueryParameter.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameter#google_cloud_bigquery_query_ScalarQueryParameter_to_api_repr)

### google.cloud.bigquery.query.ScalarQueryParameterType.from_api_repr

`from_api_repr(resource)`


Factory: construct parameter type from JSON resource.

See more: [google.cloud.bigquery.query.ScalarQueryParameterType.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameterType#google_cloud_bigquery_query_ScalarQueryParameterType_from_api_repr)

### google.cloud.bigquery.query.ScalarQueryParameterType.to_api_repr

`to_api_repr()`


Construct JSON API representation for the parameter type.

See more: [google.cloud.bigquery.query.ScalarQueryParameterType.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameterType#google_cloud_bigquery_query_ScalarQueryParameterType_to_api_repr)

### google.cloud.bigquery.query.ScalarQueryParameterType.with_name

`with_name(new_name: typing.Optional[str])`


Return a copy of the instance with `name`

set to `new_name`

.

See more: [google.cloud.bigquery.query.ScalarQueryParameterType.with_name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameterType#google_cloud_bigquery_query_ScalarQueryParameterType_with_name)

### google.cloud.bigquery.query.StructQueryParameter.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.StructQueryParameter`


Factory: construct parameter from JSON resource.

See more: [google.cloud.bigquery.query.StructQueryParameter.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter#google_cloud_bigquery_query_StructQueryParameter_from_api_repr)

### google.cloud.bigquery.query.StructQueryParameter.positional

`positional(*sub_params)`


Factory for positional parameters.

See more: [google.cloud.bigquery.query.StructQueryParameter.positional](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter#google_cloud_bigquery_query_StructQueryParameter_positional)

### google.cloud.bigquery.query.StructQueryParameter.to_api_repr

`to_api_repr() -> dict`


Construct JSON API representation for the parameter.

See more: [google.cloud.bigquery.query.StructQueryParameter.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter#google_cloud_bigquery_query_StructQueryParameter_to_api_repr)

### google.cloud.bigquery.query.StructQueryParameterType.from_api_repr

`from_api_repr(resource)`


Factory: construct parameter type from JSON resource.

See more: [google.cloud.bigquery.query.StructQueryParameterType.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameterType#google_cloud_bigquery_query_StructQueryParameterType_from_api_repr)

### google.cloud.bigquery.query.StructQueryParameterType.to_api_repr

`to_api_repr()`


Construct JSON API representation for the parameter type.

See more: [google.cloud.bigquery.query.StructQueryParameterType.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameterType#google_cloud_bigquery_query_StructQueryParameterType_to_api_repr)

### google.cloud.bigquery.routine.ExternalRuntimeOptions.from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.ExternalRuntimeOptions
```


Factory: construct external runtime options given its API representation.

See more: [google.cloud.bigquery.routine.ExternalRuntimeOptions.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions#google_cloud_bigquery_routine_ExternalRuntimeOptions_from_api_repr)

### google.cloud.bigquery.routine.ExternalRuntimeOptions.to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this ExternalRuntimeOptions.

See more: [google.cloud.bigquery.routine.ExternalRuntimeOptions.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions#google_cloud_bigquery_routine_ExternalRuntimeOptions_to_api_repr)

### google.cloud.bigquery.routine.RemoteFunctionOptions.from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RemoteFunctionOptions
```


Factory: construct remote function options given its API representation.

See more: [google.cloud.bigquery.routine.RemoteFunctionOptions.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions#google_cloud_bigquery_routine_RemoteFunctionOptions_from_api_repr)

### google.cloud.bigquery.routine.RemoteFunctionOptions.to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this RemoteFunctionOptions.

See more: [google.cloud.bigquery.routine.RemoteFunctionOptions.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions#google_cloud_bigquery_routine_RemoteFunctionOptions_to_api_repr)

### google.cloud.bigquery.routine.Routine.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.routine.routine.Routine`


Factory: construct a routine given its API representation.

See more: [google.cloud.bigquery.routine.Routine.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine#google_cloud_bigquery_routine_Routine_from_api_repr)

### google.cloud.bigquery.routine.Routine.to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine.

### google.cloud.bigquery.routine.RoutineArgument.from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RoutineArgument
```


Factory: construct a routine argument given its API representation.

See more: [google.cloud.bigquery.routine.RoutineArgument.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument#google_cloud_bigquery_routine_RoutineArgument_from_api_repr)

### google.cloud.bigquery.routine.RoutineArgument.to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine argument.

See more: [google.cloud.bigquery.routine.RoutineArgument.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument#google_cloud_bigquery_routine_RoutineArgument_to_api_repr)

### google.cloud.bigquery.routine.RoutineReference.__eq__

`__eq__(other)`


Two RoutineReferences are equal if they point to the same routine.

### google.cloud.bigquery.routine.RoutineReference.__str__

`__str__()`


String representation of the reference.

See more: [google.cloud.bigquery.routine.RoutineReference. str](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference#google_cloud_bigquery_routine_RoutineReference___str__)

### google.cloud.bigquery.routine.RoutineReference.from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RoutineReference
```


Factory: construct a routine reference given its API representation.

See more: [google.cloud.bigquery.routine.RoutineReference.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference#google_cloud_bigquery_routine_RoutineReference_from_api_repr)

### google.cloud.bigquery.routine.RoutineReference.from_string

```
from_string(
routine_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.routine.routine.RoutineReference
```


Factory: construct a routine reference from routine ID string.

See more: [google.cloud.bigquery.routine.RoutineReference.from_string](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference#google_cloud_bigquery_routine_RoutineReference_from_string)

### google.cloud.bigquery.routine.RoutineReference.to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine reference.

See more: [google.cloud.bigquery.routine.RoutineReference.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference#google_cloud_bigquery_routine_RoutineReference_to_api_repr)

### google.cloud.bigquery.schema.FieldElementType.from_api_repr

```
from_api_repr(
api_repr: typing.Optional[dict],
) -> typing.Optional[google.cloud.bigquery.schema.FieldElementType]
```


Factory: construct a FieldElementType given its API representation.

See more: [google.cloud.bigquery.schema.FieldElementType.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.FieldElementType#google_cloud_bigquery_schema_FieldElementType_from_api_repr)

### google.cloud.bigquery.schema.FieldElementType.to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this field element type.

See more: [google.cloud.bigquery.schema.FieldElementType.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.FieldElementType#google_cloud_bigquery_schema_FieldElementType_to_api_repr)

### google.cloud.bigquery.schema.ForeignTypeInfo.from_api_repr

```
from_api_repr(
api_repr: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.schema.ForeignTypeInfo
```


Factory: constructs an instance of the class (cls) given its API representation.

See more: [google.cloud.bigquery.schema.ForeignTypeInfo.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.ForeignTypeInfo#google_cloud_bigquery_schema_ForeignTypeInfo_from_api_repr)

### google.cloud.bigquery.schema.ForeignTypeInfo.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.schema.ForeignTypeInfo.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.ForeignTypeInfo#google_cloud_bigquery_schema_ForeignTypeInfo_to_api_repr)

### google.cloud.bigquery.schema.PolicyTagList.from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.schema.PolicyTagList`


Return a `PolicyTagList`

object deserialized from a dict.

See more: [google.cloud.bigquery.schema.PolicyTagList.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.PolicyTagList#google_cloud_bigquery_schema_PolicyTagList_from_api_repr)

### google.cloud.bigquery.schema.PolicyTagList.to_api_repr

`to_api_repr() -> dict`


Return a dictionary representing this object.

See more: [google.cloud.bigquery.schema.PolicyTagList.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.PolicyTagList#google_cloud_bigquery_schema_PolicyTagList_to_api_repr)

### google.cloud.bigquery.schema.SchemaField.from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.schema.SchemaField`


Return a `SchemaField`

object deserialized from a dictionary.

See more: [google.cloud.bigquery.schema.SchemaField.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_from_api_repr)

### google.cloud.bigquery.schema.SchemaField.to_api_repr

`to_api_repr() -> dict`


Return a dictionary representing this schema field.

See more: [google.cloud.bigquery.schema.SchemaField.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_to_api_repr)

### google.cloud.bigquery.schema.SchemaField.to_standard_sql

`to_standard_sql() -> google.cloud.bigquery.standard_sql.StandardSqlField`


Return the field as the standard SQL field representation object.

See more: [google.cloud.bigquery.schema.SchemaField.to_standard_sql](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_to_standard_sql)

### google.cloud.bigquery.schema.SerDeInfo.from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.schema.SerDeInfo`


Factory: constructs an instance of the class (cls) given its API representation.

See more: [google.cloud.bigquery.schema.SerDeInfo.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SerDeInfo#google_cloud_bigquery_schema_SerDeInfo_from_api_repr)

### google.cloud.bigquery.schema.SerDeInfo.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.schema.SerDeInfo.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SerDeInfo#google_cloud_bigquery_schema_SerDeInfo_to_api_repr)

### google.cloud.bigquery.schema.StorageDescriptor.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.schema.StorageDescriptor`


Factory: constructs an instance of the class (cls) given its API representation.

See more: [google.cloud.bigquery.schema.StorageDescriptor.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.StorageDescriptor#google_cloud_bigquery_schema_StorageDescriptor_from_api_repr)

### google.cloud.bigquery.schema.StorageDescriptor.to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

See more: [google.cloud.bigquery.schema.StorageDescriptor.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.StorageDescriptor#google_cloud_bigquery_schema_StorageDescriptor_to_api_repr)

### google.cloud.bigquery.standard_sql.StandardSqlDataType.from_api_repr

`from_api_repr(resource: typing.Dict[str, typing.Any])`


Construct an SQL data type instance given its API representation.

See more: [google.cloud.bigquery.standard_sql.StandardSqlDataType.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType#google_cloud_bigquery_standard_sql_StandardSqlDataType_from_api_repr)

### google.cloud.bigquery.standard_sql.StandardSqlDataType.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL data type.

See more: [google.cloud.bigquery.standard_sql.StandardSqlDataType.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType#google_cloud_bigquery_standard_sql_StandardSqlDataType_to_api_repr)

### google.cloud.bigquery.standard_sql.StandardSqlField.from_api_repr

`from_api_repr(resource: typing.Dict[str, typing.Any])`


Construct an SQL field instance given its API representation.

See more: [google.cloud.bigquery.standard_sql.StandardSqlField.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlField#google_cloud_bigquery_standard_sql_StandardSqlField_from_api_repr)

### google.cloud.bigquery.standard_sql.StandardSqlField.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL field.

See more: [google.cloud.bigquery.standard_sql.StandardSqlField.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlField#google_cloud_bigquery_standard_sql_StandardSqlField_to_api_repr)

### google.cloud.bigquery.standard_sql.StandardSqlStructType.from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.standard_sql.StandardSqlStructType
```


Construct an SQL struct type instance given its API representation.

See more: [google.cloud.bigquery.standard_sql.StandardSqlStructType.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlStructType#google_cloud_bigquery_standard_sql_StandardSqlStructType_from_api_repr)

### google.cloud.bigquery.standard_sql.StandardSqlStructType.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL struct type.

See more: [google.cloud.bigquery.standard_sql.StandardSqlStructType.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlStructType#google_cloud_bigquery_standard_sql_StandardSqlStructType_to_api_repr)

### google.cloud.bigquery.standard_sql.StandardSqlTableType.from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.standard_sql.StandardSqlTableType
```


Construct an SQL table type instance given its API representation.

See more: [google.cloud.bigquery.standard_sql.StandardSqlTableType.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlTableType#google_cloud_bigquery_standard_sql_StandardSqlTableType_from_api_repr)

### google.cloud.bigquery.standard_sql.StandardSqlTableType.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL table type.

See more: [google.cloud.bigquery.standard_sql.StandardSqlTableType.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlTableType#google_cloud_bigquery_standard_sql_StandardSqlTableType_to_api_repr)

### google.cloud.bigquery.table.BigLakeConfiguration.from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.table.BigLakeConfiguration
```


Factory: construct a BigLakeConfiguration given its API representation.

See more: [google.cloud.bigquery.table.BigLakeConfiguration.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration#google_cloud_bigquery_table_BigLakeConfiguration_from_api_repr)

### google.cloud.bigquery.table.BigLakeConfiguration.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this BigLakeConfiguration.

See more: [google.cloud.bigquery.table.BigLakeConfiguration.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration#google_cloud_bigquery_table_BigLakeConfiguration_to_api_repr)

### google.cloud.bigquery.table.ForeignKey.from_api_repr

```
from_api_repr(
api_repr: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.table.ForeignKey
```


Create an instance from API representation.

See more: [google.cloud.bigquery.table.ForeignKey.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ForeignKey#google_cloud_bigquery_table_ForeignKey_from_api_repr)

### google.cloud.bigquery.table.ForeignKey.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Return a dictionary representing this object.

See more: [google.cloud.bigquery.table.ForeignKey.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ForeignKey#google_cloud_bigquery_table_ForeignKey_to_api_repr)

### google.cloud.bigquery.table.Row.get

`get(key: str, default: typing.Optional[typing.Any] = None) -> typing.Any`


Return a value for key, with a default value if it does not exist.

See more: [google.cloud.bigquery.table.Row.get](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Row#google_cloud_bigquery_table_Row_get)

### google.cloud.bigquery.table.Row.items

`items() -> typing.Iterable[typing.Tuple[str, typing.Any]]`


Return items as `(key, value)`

pairs.

See more: [google.cloud.bigquery.table.Row.items](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Row#google_cloud_bigquery_table_Row_items)

### google.cloud.bigquery.table.Row.keys

`keys() -> typing.Iterable[str]`


Return the keys for using a row as a dict.

See more: [google.cloud.bigquery.table.Row.keys](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Row#google_cloud_bigquery_table_Row_keys)

### google.cloud.bigquery.table.Row.values

`values()`


Return the values included in this row.

See more: [google.cloud.bigquery.table.Row.values](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Row#google_cloud_bigquery_table_Row_values)

### google.cloud.bigquery.table.RowIterator.to_arrow

```
to_arrow(
progress_bar_type: typing.Optional[str] = None,
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
create_bqstorage_client: bool = True,
) -> pyarrow.Table
```


[Beta] Create a class:`pyarrow.Table`

by loading all pages of a
table or query.

### google.cloud.bigquery.table.RowIterator.to_arrow_iterable

```
to_arrow_iterable(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
max_queue_size: int = object,
max_stream_count: typing.Optional[int] = None,
) -> typing.Iterator[pyarrow.RecordBatch]
```


[Beta] Create an iterable of class:`pyarrow.RecordBatch`

, to process the table as a stream.

See more: [google.cloud.bigquery.table.RowIterator.to_arrow_iterable](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RowIterator#google_cloud_bigquery_table_RowIterator_to_arrow_iterable)

### google.cloud.bigquery.table.RowIterator.to_dataframe

```
to_dataframe(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
progress_bar_type: typing.Optional[str] = None,
create_bqstorage_client: bool = True,
geography_as_object: bool = False,
bool_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.BOOL_DTYPE,
int_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.INT_DTYPE,
float_dtype: typing.Optional[typing.Any] = None,
string_dtype: typing.Optional[typing.Any] = None,
date_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.DATE_DTYPE,
datetime_dtype: typing.Optional[typing.Any] = None,
time_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.TIME_DTYPE,
timestamp_dtype: typing.Optional[typing.Any] = None,
range_date_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_DATE_DTYPE,
range_datetime_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_DATETIME_DTYPE,
range_timestamp_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_TIMESTAMP_DTYPE,
) -> pandas.DataFrame
```


Create a pandas DataFrame by loading all pages of a query.

See more: [google.cloud.bigquery.table.RowIterator.to_dataframe](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RowIterator#google_cloud_bigquery_table_RowIterator_to_dataframe)

### google.cloud.bigquery.table.RowIterator.to_dataframe_iterable

```
to_dataframe_iterable(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
max_queue_size: int = object,
max_stream_count: typing.Optional[int] = None,
) -> pandas.DataFrame
```


Create an iterable of pandas DataFrames, to process the table as a stream.

See more: [google.cloud.bigquery.table.RowIterator.to_dataframe_iterable](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RowIterator#google_cloud_bigquery_table_RowIterator_to_dataframe_iterable)

### google.cloud.bigquery.table.RowIterator.to_geodataframe

```
to_geodataframe(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
progress_bar_type: typing.Optional[str] = None,
create_bqstorage_client: bool = True,
geography_column: typing.Optional[str] = None,
bool_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.BOOL_DTYPE,
int_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.INT_DTYPE,
float_dtype: typing.Optional[typing.Any] = None,
string_dtype: typing.Optional[typing.Any] = None,
) -> geopandas.GeoDataFrame
```


Create a GeoPandas GeoDataFrame by loading all pages of a query.

See more: [google.cloud.bigquery.table.RowIterator.to_geodataframe](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RowIterator#google_cloud_bigquery_table_RowIterator_to_geodataframe)

### google.cloud.bigquery.table.Table.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.table.Table`


Factory: construct a table given its API representation .

### google.cloud.bigquery.table.Table.from_string

`from_string(full_table_id: str) -> google.cloud.bigquery.table.Table`


Construct a table from fully-qualified table ID.

### google.cloud.bigquery.table.Table.to_api_repr

`to_api_repr() -> dict`


Constructs the API resource of this table .

### google.cloud.bigquery.table.Table.to_bqstorage

`to_bqstorage() -> str`


Construct a BigQuery Storage API representation of this table.

### google.cloud.bigquery.table.TableConstraints.from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.table.TableConstraints
```


Create an instance from API representation.

See more: [google.cloud.bigquery.table.TableConstraints.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableConstraints#google_cloud_bigquery_table_TableConstraints_from_api_repr)

### google.cloud.bigquery.table.TableConstraints.to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Return a dictionary representing this object.

See more: [google.cloud.bigquery.table.TableConstraints.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableConstraints#google_cloud_bigquery_table_TableConstraints_to_api_repr)

### google.cloud.bigquery.table.TableListItem.from_string

`from_string(full_table_id: str) -> google.cloud.bigquery.table.TableListItem`


Construct a table from fully-qualified table ID.

See more: [google.cloud.bigquery.table.TableListItem.from_string](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_from_string)

### google.cloud.bigquery.table.TableListItem.to_api_repr

`to_api_repr() -> dict`


Constructs the API resource of this table .

See more: [google.cloud.bigquery.table.TableListItem.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_to_api_repr)

### google.cloud.bigquery.table.TableListItem.to_bqstorage

`to_bqstorage() -> str`


Construct a BigQuery Storage API representation of this table.

See more: [google.cloud.bigquery.table.TableListItem.to_bqstorage](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_to_bqstorage)

### google.cloud.bigquery.table.TableReference.from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.table.TableReference`


Factory: construct a table reference given its API representation .

See more: [google.cloud.bigquery.table.TableReference.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference#google_cloud_bigquery_table_TableReference_from_api_repr)

### google.cloud.bigquery.table.TableReference.from_string

```
from_string(
table_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.table.TableReference
```


Construct a table reference from table ID string.

See more: [google.cloud.bigquery.table.TableReference.from_string](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference#google_cloud_bigquery_table_TableReference_from_string)

### google.cloud.bigquery.table.TableReference.to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this table reference.

See more: [google.cloud.bigquery.table.TableReference.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference#google_cloud_bigquery_table_TableReference_to_api_repr)

### google.cloud.bigquery.table.TableReference.to_bqstorage

`to_bqstorage() -> str`


Construct a BigQuery Storage API representation of this table.

See more: [google.cloud.bigquery.table.TableReference.to_bqstorage](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference#google_cloud_bigquery_table_TableReference_to_bqstorage)

### google.cloud.bigquery.table.TimePartitioning.from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.table.TimePartitioning`


Return a `TimePartitioning`

object deserialized from a dict.

See more: [google.cloud.bigquery.table.TimePartitioning.from_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning#google_cloud_bigquery_table_TimePartitioning_from_api_repr)

### google.cloud.bigquery.table.TimePartitioning.to_api_repr

`to_api_repr() -> dict`


Return a dictionary representing this object.

See more: [google.cloud.bigquery.table.TimePartitioning.to_api_repr](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning#google_cloud_bigquery_table_TimePartitioning_to_api_repr)