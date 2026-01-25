---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/summary_property
fetched_at: 2026-01-25T02:04:46.070066
---

# Package Properties and Attributes (3.40.0)


      
      Save and categorize content based on your preferences.

Summary of entries of Properties and Attributes for bigquery.

### google.cloud.bigquery.client.Client.SCOPE

The scopes required for authenticating as a BigQuery consumer.

### google.cloud.bigquery.client.Client.default_job_creation_mode

Default job creation mode used for query execution.

See more: [google.cloud.bigquery.client.Client.default_job_creation_mode](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_default_job_creation_mode)

### google.cloud.bigquery.client.Client.default_load_job_config

Default `LoadJobConfig`

.

See more: [google.cloud.bigquery.client.Client.default_load_job_config](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_default_load_job_config)

### google.cloud.bigquery.client.Client.default_query_job_config

Default `QueryJobConfig`

or `None`

.

See more: [google.cloud.bigquery.client.Client.default_query_job_config](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_default_query_job_config)

### google.cloud.bigquery.client.Client.location

Default location for jobs / datasets / tables.

### google.cloud.bigquery.dataset.AccessEntry.condition

Optional[Condition]: The IAM condition associated with this entry.

See more: [google.cloud.bigquery.dataset.AccessEntry.condition](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry#google_cloud_bigquery_dataset_AccessEntry_condition)

### google.cloud.bigquery.dataset.AccessEntry.dataset

API resource representation of a dataset reference.

### google.cloud.bigquery.dataset.AccessEntry.dataset_target_types

Which resources that the dataset in this entry applies to.

See more: [google.cloud.bigquery.dataset.AccessEntry.dataset_target_types](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry#google_cloud_bigquery_dataset_AccessEntry_dataset_target_types)

### google.cloud.bigquery.dataset.AccessEntry.domain

A domain to grant access to.

### google.cloud.bigquery.dataset.AccessEntry.entity_id

The entity_id of the entry.

See more: [google.cloud.bigquery.dataset.AccessEntry.entity_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry#google_cloud_bigquery_dataset_AccessEntry_entity_id)

### google.cloud.bigquery.dataset.AccessEntry.entity_type

The entity_type of the entry.

See more: [google.cloud.bigquery.dataset.AccessEntry.entity_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry#google_cloud_bigquery_dataset_AccessEntry_entity_type)

### google.cloud.bigquery.dataset.AccessEntry.group_by_email

An email address of a Google Group to grant access to.

See more: [google.cloud.bigquery.dataset.AccessEntry.group_by_email](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry#google_cloud_bigquery_dataset_AccessEntry_group_by_email)

### google.cloud.bigquery.dataset.AccessEntry.role

The role of the entry.

### google.cloud.bigquery.dataset.AccessEntry.routine

API resource representation of a routine reference.

### google.cloud.bigquery.dataset.AccessEntry.special_group

A special group to grant access to.

See more: [google.cloud.bigquery.dataset.AccessEntry.special_group](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry#google_cloud_bigquery_dataset_AccessEntry_special_group)

### google.cloud.bigquery.dataset.AccessEntry.user_by_email

An email address of a user to grant access to.

See more: [google.cloud.bigquery.dataset.AccessEntry.user_by_email](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry#google_cloud_bigquery_dataset_AccessEntry_user_by_email)

### google.cloud.bigquery.dataset.AccessEntry.view

API resource representation of a view reference.

### google.cloud.bigquery.dataset.Condition.description

Optional[str]: The description for the condition.

See more: [google.cloud.bigquery.dataset.Condition.description](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Condition#google_cloud_bigquery_dataset_Condition_description)

### google.cloud.bigquery.dataset.Condition.expression

str: The expression string for the condition.

See more: [google.cloud.bigquery.dataset.Condition.expression](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Condition#google_cloud_bigquery_dataset_Condition_expression)

### google.cloud.bigquery.dataset.Condition.title

Optional[str]: The title for the condition.

### google.cloud.bigquery.dataset.Dataset.access_entries

List[[google.cloud.bigquery.dataset.AccessEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry)]: Dataset's access
entries.

See more: [google.cloud.bigquery.dataset.Dataset.access_entries](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_access_entries)

### google.cloud.bigquery.dataset.Dataset.created

Union[datetime.datetime, None]: Output only.

### google.cloud.bigquery.dataset.Dataset.dataset_id

str: Dataset ID.

### google.cloud.bigquery.dataset.Dataset.default_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for all tables in the dataset.

See more: [google.cloud.bigquery.dataset.Dataset.default_encryption_configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_default_encryption_configuration)

### google.cloud.bigquery.dataset.Dataset.default_partition_expiration_ms

Optional[int]: The default partition expiration for all partitioned tables in the dataset, in milliseconds.

See more: [google.cloud.bigquery.dataset.Dataset.default_partition_expiration_ms](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_default_partition_expiration_ms)

### google.cloud.bigquery.dataset.Dataset.default_rounding_mode

Union[str, None]: defaultRoundingMode of the dataset as set by the user
(defaults to :data:`None`

).

See more: [google.cloud.bigquery.dataset.Dataset.default_rounding_mode](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_default_rounding_mode)

### google.cloud.bigquery.dataset.Dataset.default_table_expiration_ms

Union[int, None]: Default expiration time for tables in the dataset
(defaults to :data:`None`

).

See more: [google.cloud.bigquery.dataset.Dataset.default_table_expiration_ms](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_default_table_expiration_ms)

### google.cloud.bigquery.dataset.Dataset.description

Optional[str]: Description of the dataset as set by the user
(defaults to :data:`None`

).

### google.cloud.bigquery.dataset.Dataset.etag

Union[str, None]: Output only.

### google.cloud.bigquery.dataset.Dataset.external_catalog_dataset_options

Options defining open source compatible datasets living in the BigQuery catalog.

See more: [google.cloud.bigquery.dataset.Dataset.external_catalog_dataset_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_external_catalog_dataset_options)

### google.cloud.bigquery.dataset.Dataset.friendly_name

Union[str, None]: Title of the dataset as set by the user
(defaults to :data:`None`

).

See more: [google.cloud.bigquery.dataset.Dataset.friendly_name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_friendly_name)

### google.cloud.bigquery.dataset.Dataset.full_dataset_id

Union[str, None]: Output only.

See more: [google.cloud.bigquery.dataset.Dataset.full_dataset_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_full_dataset_id)

### google.cloud.bigquery.dataset.Dataset.is_case_insensitive

Optional[bool]: True if the dataset and its table names are case-insensitive, otherwise False.

See more: [google.cloud.bigquery.dataset.Dataset.is_case_insensitive](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_is_case_insensitive)

### google.cloud.bigquery.dataset.Dataset.labels

Dict[str, str]: Labels for the dataset.

### google.cloud.bigquery.dataset.Dataset.location

Union[str, None]: Location in which the dataset is hosted as set by
the user (defaults to :data:`None`

).

### google.cloud.bigquery.dataset.Dataset.max_time_travel_hours

Optional[int]: Defines the time travel window in hours.

See more: [google.cloud.bigquery.dataset.Dataset.max_time_travel_hours](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_max_time_travel_hours)

### google.cloud.bigquery.dataset.Dataset.modified

Union[datetime.datetime, None]: Output only.

### google.cloud.bigquery.dataset.Dataset.path

str: URL path for the dataset based on project and dataset ID.

### google.cloud.bigquery.dataset.Dataset.project

str: Project ID of the project bound to the dataset.

### google.cloud.bigquery.dataset.Dataset.reference

[google.cloud.bigquery.dataset.DatasetReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference): A reference to this
dataset.

### google.cloud.bigquery.dataset.Dataset.resource_tags

Dict[str, str]: Resource tags of the dataset.

See more: [google.cloud.bigquery.dataset.Dataset.resource_tags](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_resource_tags)

### google.cloud.bigquery.dataset.Dataset.self_link

Union[str, None]: Output only.

### google.cloud.bigquery.dataset.Dataset.storage_billing_model

Union[str, None]: StorageBillingModel of the dataset as set by the user
(defaults to :data:`None`

).

See more: [google.cloud.bigquery.dataset.Dataset.storage_billing_model](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset#google_cloud_bigquery_dataset_Dataset_storage_billing_model)

### google.cloud.bigquery.dataset.DatasetListItem.dataset_id

str: Dataset ID.

See more: [google.cloud.bigquery.dataset.DatasetListItem.dataset_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem#google_cloud_bigquery_dataset_DatasetListItem_dataset_id)

### google.cloud.bigquery.dataset.DatasetListItem.friendly_name

Union[str, None]: Title of the dataset as set by the user
(defaults to :data:`None`

).

See more: [google.cloud.bigquery.dataset.DatasetListItem.friendly_name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem#google_cloud_bigquery_dataset_DatasetListItem_friendly_name)

### google.cloud.bigquery.dataset.DatasetListItem.full_dataset_id

Union[str, None]: ID for the dataset resource (:data:`None`

until
set from the server).

See more: [google.cloud.bigquery.dataset.DatasetListItem.full_dataset_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem#google_cloud_bigquery_dataset_DatasetListItem_full_dataset_id)

### google.cloud.bigquery.dataset.DatasetListItem.labels

Dict[str, str]: Labels for the dataset.

See more: [google.cloud.bigquery.dataset.DatasetListItem.labels](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem#google_cloud_bigquery_dataset_DatasetListItem_labels)

### google.cloud.bigquery.dataset.DatasetListItem.project

str: Project bound to the dataset.

See more: [google.cloud.bigquery.dataset.DatasetListItem.project](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem#google_cloud_bigquery_dataset_DatasetListItem_project)

### google.cloud.bigquery.dataset.DatasetListItem.reference

[google.cloud.bigquery.dataset.DatasetReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference): A reference to this
dataset.

See more: [google.cloud.bigquery.dataset.DatasetListItem.reference](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem#google_cloud_bigquery_dataset_DatasetListItem_reference)

### google.cloud.bigquery.dataset.DatasetReference.dataset_id

str: Dataset ID.

See more: [google.cloud.bigquery.dataset.DatasetReference.dataset_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference#google_cloud_bigquery_dataset_DatasetReference_dataset_id)

### google.cloud.bigquery.dataset.DatasetReference.path

str: URL path for the dataset based on project and dataset ID.

See more: [google.cloud.bigquery.dataset.DatasetReference.path](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference#google_cloud_bigquery_dataset_DatasetReference_path)

### google.cloud.bigquery.dataset.DatasetReference.project

str: Project ID of the dataset.

See more: [google.cloud.bigquery.dataset.DatasetReference.project](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference#google_cloud_bigquery_dataset_DatasetReference_project)

### google.cloud.bigquery.dbapi.Cursor.query_job

[google.cloud.bigquery.job](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job).query.QueryJob | None: The query job
created by the last `execute*()`

call, if a query job was created.

### google.cloud.bigquery.encryption_configuration.EncryptionConfiguration.kms_key_name

str: Resource ID of Cloud KMS key.

See more: [google.cloud.bigquery.encryption_configuration.EncryptionConfiguration.kms_key_name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration#google_cloud_bigquery_encryption_configuration_EncryptionConfiguration_kms_key_name)

### google.cloud.bigquery.enums.BigLakeFileFormat.FILE_FORMAT_UNSPECIFIED

The default unspecified value.

See more: [google.cloud.bigquery.enums.BigLakeFileFormat.FILE_FORMAT_UNSPECIFIED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeFileFormat#google_cloud_bigquery_enums_BigLakeFileFormat_FILE_FORMAT_UNSPECIFIED)

### google.cloud.bigquery.enums.BigLakeFileFormat.PARQUET

Apache Parquet format.

See more: [google.cloud.bigquery.enums.BigLakeFileFormat.PARQUET](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeFileFormat#google_cloud_bigquery_enums_BigLakeFileFormat_PARQUET)

### google.cloud.bigquery.enums.BigLakeTableFormat.ICEBERG

Apache Iceberg format.

See more: [google.cloud.bigquery.enums.BigLakeTableFormat.ICEBERG](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeTableFormat#google_cloud_bigquery_enums_BigLakeTableFormat_ICEBERG)

### google.cloud.bigquery.enums.BigLakeTableFormat.TABLE_FORMAT_UNSPECIFIED

The default unspecified value.

See more: [google.cloud.bigquery.enums.BigLakeTableFormat.TABLE_FORMAT_UNSPECIFIED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeTableFormat#google_cloud_bigquery_enums_BigLakeTableFormat_TABLE_FORMAT_UNSPECIFIED)

### google.cloud.bigquery.enums.Compression.DEFLATE

Specifies DEFLATE format.

### google.cloud.bigquery.enums.Compression.GZIP

Specifies GZIP format.

### google.cloud.bigquery.enums.Compression.NONE

Specifies no compression.

### google.cloud.bigquery.enums.Compression.SNAPPY

Specifies SNAPPY format.

### google.cloud.bigquery.enums.Compression.ZSTD

Specifies ZSTD format.

### google.cloud.bigquery.enums.CreateDisposition.CREATE_IF_NEEDED

If the table does not exist, BigQuery creates the table.

See more: [google.cloud.bigquery.enums.CreateDisposition.CREATE_IF_NEEDED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.CreateDisposition#google_cloud_bigquery_enums_CreateDisposition_CREATE_IF_NEEDED)

### google.cloud.bigquery.enums.CreateDisposition.CREATE_NEVER

The table must already exist.

See more: [google.cloud.bigquery.enums.CreateDisposition.CREATE_NEVER](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.CreateDisposition#google_cloud_bigquery_enums_CreateDisposition_CREATE_NEVER)

### google.cloud.bigquery.enums.DatasetView.ACL

View ACL information for the dataset, which defines dataset access for one or more entities.

### google.cloud.bigquery.enums.DatasetView.DATASET_VIEW_UNSPECIFIED

The default value.

See more: [google.cloud.bigquery.enums.DatasetView.DATASET_VIEW_UNSPECIFIED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DatasetView#google_cloud_bigquery_enums_DatasetView_DATASET_VIEW_UNSPECIFIED)

### google.cloud.bigquery.enums.DatasetView.FULL

View both dataset metadata and ACL information.

### google.cloud.bigquery.enums.DatasetView.METADATA

View metadata information for the dataset, such as friendlyName, description, labels, etc.

### google.cloud.bigquery.enums.DecimalTargetType.BIGNUMERIC

Decimal values could be converted to BIGNUMERIC type.

See more: [google.cloud.bigquery.enums.DecimalTargetType.BIGNUMERIC](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DecimalTargetType#google_cloud_bigquery_enums_DecimalTargetType_BIGNUMERIC)

### google.cloud.bigquery.enums.DecimalTargetType.NUMERIC

Decimal values could be converted to NUMERIC type.

See more: [google.cloud.bigquery.enums.DecimalTargetType.NUMERIC](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DecimalTargetType#google_cloud_bigquery_enums_DecimalTargetType_NUMERIC)

### google.cloud.bigquery.enums.DecimalTargetType.STRING

Decimal values could be converted to STRING type.

See more: [google.cloud.bigquery.enums.DecimalTargetType.STRING](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DecimalTargetType#google_cloud_bigquery_enums_DecimalTargetType_STRING)

### google.cloud.bigquery.enums.DefaultPandasDTypes.BOOL_DTYPE

Specifies default bool dtype.

See more: [google.cloud.bigquery.enums.DefaultPandasDTypes.BOOL_DTYPE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes#google_cloud_bigquery_enums_DefaultPandasDTypes_BOOL_DTYPE)

### google.cloud.bigquery.enums.DefaultPandasDTypes.DATE_DTYPE

Specifies default date dtype.

See more: [google.cloud.bigquery.enums.DefaultPandasDTypes.DATE_DTYPE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes#google_cloud_bigquery_enums_DefaultPandasDTypes_DATE_DTYPE)

### google.cloud.bigquery.enums.DefaultPandasDTypes.INT_DTYPE

Specifies default integer dtype.

See more: [google.cloud.bigquery.enums.DefaultPandasDTypes.INT_DTYPE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes#google_cloud_bigquery_enums_DefaultPandasDTypes_INT_DTYPE)

### google.cloud.bigquery.enums.DefaultPandasDTypes.RANGE_DATETIME_DTYPE

Specifies default range datetime dtype.

See more: [google.cloud.bigquery.enums.DefaultPandasDTypes.RANGE_DATETIME_DTYPE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes#google_cloud_bigquery_enums_DefaultPandasDTypes_RANGE_DATETIME_DTYPE)

### google.cloud.bigquery.enums.DefaultPandasDTypes.RANGE_DATE_DTYPE

Specifies default range date dtype.

See more: [google.cloud.bigquery.enums.DefaultPandasDTypes.RANGE_DATE_DTYPE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes#google_cloud_bigquery_enums_DefaultPandasDTypes_RANGE_DATE_DTYPE)

### google.cloud.bigquery.enums.DefaultPandasDTypes.RANGE_TIMESTAMP_DTYPE

Specifies default range timestamp dtype.

See more: [google.cloud.bigquery.enums.DefaultPandasDTypes.RANGE_TIMESTAMP_DTYPE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes#google_cloud_bigquery_enums_DefaultPandasDTypes_RANGE_TIMESTAMP_DTYPE)

### google.cloud.bigquery.enums.DefaultPandasDTypes.TIME_DTYPE

Specifies default time dtype.

See more: [google.cloud.bigquery.enums.DefaultPandasDTypes.TIME_DTYPE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes#google_cloud_bigquery_enums_DefaultPandasDTypes_TIME_DTYPE)

### google.cloud.bigquery.enums.DestinationFormat.AVRO

Specifies Avro format.

See more: [google.cloud.bigquery.enums.DestinationFormat.AVRO](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DestinationFormat#google_cloud_bigquery_enums_DestinationFormat_AVRO)

### google.cloud.bigquery.enums.DestinationFormat.CSV

Specifies CSV format.

### google.cloud.bigquery.enums.DestinationFormat.NEWLINE_DELIMITED_JSON

Specifies newline delimited JSON format.

See more: [google.cloud.bigquery.enums.DestinationFormat.NEWLINE_DELIMITED_JSON](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DestinationFormat#google_cloud_bigquery_enums_DestinationFormat_NEWLINE_DELIMITED_JSON)

### google.cloud.bigquery.enums.DestinationFormat.PARQUET

Specifies Parquet format.

See more: [google.cloud.bigquery.enums.DestinationFormat.PARQUET](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DestinationFormat#google_cloud_bigquery_enums_DestinationFormat_PARQUET)

### google.cloud.bigquery.enums.DeterminismLevel.DETERMINISM_LEVEL_UNSPECIFIED

The determinism of the UDF is unspecified.

See more: [google.cloud.bigquery.enums.DeterminismLevel.DETERMINISM_LEVEL_UNSPECIFIED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DeterminismLevel#google_cloud_bigquery_enums_DeterminismLevel_DETERMINISM_LEVEL_UNSPECIFIED)

### google.cloud.bigquery.enums.DeterminismLevel.DETERMINISTIC

The UDF is deterministic, meaning that 2 function calls with the same inputs always produce the same result, even across 2 query runs.

See more: [google.cloud.bigquery.enums.DeterminismLevel.DETERMINISTIC](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DeterminismLevel#google_cloud_bigquery_enums_DeterminismLevel_DETERMINISTIC)

### google.cloud.bigquery.enums.DeterminismLevel.NOT_DETERMINISTIC

The UDF is not deterministic.

See more: [google.cloud.bigquery.enums.DeterminismLevel.NOT_DETERMINISTIC](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DeterminismLevel#google_cloud_bigquery_enums_DeterminismLevel_NOT_DETERMINISTIC)

### google.cloud.bigquery.enums.Encoding.ISO_8859_1

Specifies ISO-8859-1 encoding.

### google.cloud.bigquery.enums.Encoding.UTF_8

Specifies UTF-8 encoding.

### google.cloud.bigquery.enums.JobCreationMode.JOB_CREATION_MODE_UNSPECIFIED

Job creation mode is unspecified.

See more: [google.cloud.bigquery.enums.JobCreationMode.JOB_CREATION_MODE_UNSPECIFIED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.JobCreationMode#google_cloud_bigquery_enums_JobCreationMode_JOB_CREATION_MODE_UNSPECIFIED)

### google.cloud.bigquery.enums.JobCreationMode.JOB_CREATION_OPTIONAL

Job creation is optional.

See more: [google.cloud.bigquery.enums.JobCreationMode.JOB_CREATION_OPTIONAL](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.JobCreationMode#google_cloud_bigquery_enums_JobCreationMode_JOB_CREATION_OPTIONAL)

### google.cloud.bigquery.enums.JobCreationMode.JOB_CREATION_REQUIRED

Job creation is always required.

See more: [google.cloud.bigquery.enums.JobCreationMode.JOB_CREATION_REQUIRED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.JobCreationMode#google_cloud_bigquery_enums_JobCreationMode_JOB_CREATION_REQUIRED)

### google.cloud.bigquery.enums.QueryApiMethod.INSERT

Submit a query job by using the ```
jobs.insert REST API method
<https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/insert>
```

_.

### google.cloud.bigquery.enums.QueryApiMethod.QUERY

Submit a query job by using the ```
jobs.query REST API method
<https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query>
```

_.

### google.cloud.bigquery.enums.QueryPriority.BATCH

Specifies batch priority.

### google.cloud.bigquery.enums.QueryPriority.INTERACTIVE

Specifies interactive priority.

See more: [google.cloud.bigquery.enums.QueryPriority.INTERACTIVE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.QueryPriority#google_cloud_bigquery_enums_QueryPriority_INTERACTIVE)

### google.cloud.bigquery.enums.SchemaUpdateOption.ALLOW_FIELD_ADDITION

Allow adding a nullable field to the schema.

See more: [google.cloud.bigquery.enums.SchemaUpdateOption.ALLOW_FIELD_ADDITION](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SchemaUpdateOption#google_cloud_bigquery_enums_SchemaUpdateOption_ALLOW_FIELD_ADDITION)

### google.cloud.bigquery.enums.SchemaUpdateOption.ALLOW_FIELD_RELAXATION

Allow relaxing a required field in the original schema to nullable.

See more: [google.cloud.bigquery.enums.SchemaUpdateOption.ALLOW_FIELD_RELAXATION](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SchemaUpdateOption#google_cloud_bigquery_enums_SchemaUpdateOption_ALLOW_FIELD_RELAXATION)

### google.cloud.bigquery.enums.SourceColumnMatch.NAME

Matches by name.

See more: [google.cloud.bigquery.enums.SourceColumnMatch.NAME](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch#google_cloud_bigquery_enums_SourceColumnMatch_NAME)

### google.cloud.bigquery.enums.SourceColumnMatch.POSITION

Matches by position.

See more: [google.cloud.bigquery.enums.SourceColumnMatch.POSITION](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch#google_cloud_bigquery_enums_SourceColumnMatch_POSITION)

### google.cloud.bigquery.enums.SourceColumnMatch.SOURCE_COLUMN_MATCH_UNSPECIFIED

Unspecified column name match option.

See more: [google.cloud.bigquery.enums.SourceColumnMatch.SOURCE_COLUMN_MATCH_UNSPECIFIED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch#google_cloud_bigquery_enums_SourceColumnMatch_SOURCE_COLUMN_MATCH_UNSPECIFIED)

### google.cloud.bigquery.enums.SourceFormat.AVRO

Specifies Avro format.

### google.cloud.bigquery.enums.SourceFormat.CSV

Specifies CSV format.

### google.cloud.bigquery.enums.SourceFormat.DATASTORE_BACKUP

Specifies datastore backup format.

See more: [google.cloud.bigquery.enums.SourceFormat.DATASTORE_BACKUP](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceFormat#google_cloud_bigquery_enums_SourceFormat_DATASTORE_BACKUP)

### google.cloud.bigquery.enums.SourceFormat.NEWLINE_DELIMITED_JSON

Specifies newline delimited JSON format.

See more: [google.cloud.bigquery.enums.SourceFormat.NEWLINE_DELIMITED_JSON](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceFormat#google_cloud_bigquery_enums_SourceFormat_NEWLINE_DELIMITED_JSON)

### google.cloud.bigquery.enums.SourceFormat.ORC

Specifies Orc format.

### google.cloud.bigquery.enums.SourceFormat.PARQUET

Specifies Parquet format.

### google.cloud.bigquery.enums.TimestampPrecision.MICROSECOND

Default, for TIMESTAMP type with microsecond precision.

See more: [google.cloud.bigquery.enums.TimestampPrecision.MICROSECOND](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.TimestampPrecision#google_cloud_bigquery_enums_TimestampPrecision_MICROSECOND)

### google.cloud.bigquery.enums.TimestampPrecision.PICOSECOND

For TIMESTAMP type with picosecond precision.

See more: [google.cloud.bigquery.enums.TimestampPrecision.PICOSECOND](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.TimestampPrecision#google_cloud_bigquery_enums_TimestampPrecision_PICOSECOND)

### google.cloud.bigquery.enums.UpdateMode.UPDATE_ACL

Includes ACL information for the dataset, which defines dataset access for one or more entities.

### google.cloud.bigquery.enums.UpdateMode.UPDATE_FULL

Includes both dataset metadata and ACL information.

See more: [google.cloud.bigquery.enums.UpdateMode.UPDATE_FULL](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.UpdateMode#google_cloud_bigquery_enums_UpdateMode_UPDATE_FULL)

### google.cloud.bigquery.enums.UpdateMode.UPDATE_METADATA

Includes metadata information for the dataset, such as friendlyName, description, labels, etc.

See more: [google.cloud.bigquery.enums.UpdateMode.UPDATE_METADATA](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.UpdateMode#google_cloud_bigquery_enums_UpdateMode_UPDATE_METADATA)

### google.cloud.bigquery.enums.UpdateMode.UPDATE_MODE_UNSPECIFIED

The default value.

See more: [google.cloud.bigquery.enums.UpdateMode.UPDATE_MODE_UNSPECIFIED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.UpdateMode#google_cloud_bigquery_enums_UpdateMode_UPDATE_MODE_UNSPECIFIED)

### google.cloud.bigquery.enums.WriteDisposition.WRITE_APPEND

If the table already exists, BigQuery appends the data to the table.

See more: [google.cloud.bigquery.enums.WriteDisposition.WRITE_APPEND](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.WriteDisposition#google_cloud_bigquery_enums_WriteDisposition_WRITE_APPEND)

### google.cloud.bigquery.enums.WriteDisposition.WRITE_EMPTY

If the table already exists and contains data, a 'duplicate' error is returned in the job result.

See more: [google.cloud.bigquery.enums.WriteDisposition.WRITE_EMPTY](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.WriteDisposition#google_cloud_bigquery_enums_WriteDisposition_WRITE_EMPTY)

### google.cloud.bigquery.enums.WriteDisposition.WRITE_TRUNCATE

If the table already exists, BigQuery overwrites the table data.

See more: [google.cloud.bigquery.enums.WriteDisposition.WRITE_TRUNCATE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.WriteDisposition#google_cloud_bigquery_enums_WriteDisposition_WRITE_TRUNCATE)

### google.cloud.bigquery.enums.WriteDisposition.WRITE_TRUNCATE_DATA

For existing tables, truncate data but preserve existing schema and constraints.

See more: [google.cloud.bigquery.enums.WriteDisposition.WRITE_TRUNCATE_DATA](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.WriteDisposition#google_cloud_bigquery_enums_WriteDisposition_WRITE_TRUNCATE_DATA)

### google.cloud.bigquery.external_config.BigtableColumn.encoding

str: The encoding of the values when the type is not `STRING`

.

See more: [google.cloud.bigquery.external_config.BigtableColumn.encoding](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn#google_cloud_bigquery_external_config_BigtableColumn_encoding)

### google.cloud.bigquery.external_config.BigtableColumn.field_name

str: An identifier to use if the qualifier is not a valid BigQuery field identifier.

See more: [google.cloud.bigquery.external_config.BigtableColumn.field_name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn#google_cloud_bigquery_external_config_BigtableColumn_field_name)

### google.cloud.bigquery.external_config.BigtableColumn.only_read_latest

bool: If this is set, only the latest version of value in this column are exposed.

See more: [google.cloud.bigquery.external_config.BigtableColumn.only_read_latest](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn#google_cloud_bigquery_external_config_BigtableColumn_only_read_latest)

### google.cloud.bigquery.external_config.BigtableColumn.qualifier_encoded

Union[str, bytes]: The qualifier encoded in binary.

See more: [google.cloud.bigquery.external_config.BigtableColumn.qualifier_encoded](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn#google_cloud_bigquery_external_config_BigtableColumn_qualifier_encoded)

### google.cloud.bigquery.external_config.BigtableColumn.qualifier_string

str: A valid UTF-8 string qualifier.

See more: [google.cloud.bigquery.external_config.BigtableColumn.qualifier_string](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn#google_cloud_bigquery_external_config_BigtableColumn_qualifier_string)

### google.cloud.bigquery.external_config.BigtableColumn.type_

str: The type to convert the value in cells of this column.

See more: [google.cloud.bigquery.external_config.BigtableColumn.type_](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn#google_cloud_bigquery_external_config_BigtableColumn_type_)

### google.cloud.bigquery.external_config.BigtableColumnFamily.columns

List[BigtableColumn]: Lists of columns that should be exposed as individual fields.

See more: [google.cloud.bigquery.external_config.BigtableColumnFamily.columns](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily#google_cloud_bigquery_external_config_BigtableColumnFamily_columns)

### google.cloud.bigquery.external_config.BigtableColumnFamily.encoding

str: The encoding of the values when the type is not `STRING`

.

See more: [google.cloud.bigquery.external_config.BigtableColumnFamily.encoding](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily#google_cloud_bigquery_external_config_BigtableColumnFamily_encoding)

### google.cloud.bigquery.external_config.BigtableColumnFamily.family_id

str: Identifier of the column family.

See more: [google.cloud.bigquery.external_config.BigtableColumnFamily.family_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily#google_cloud_bigquery_external_config_BigtableColumnFamily_family_id)

### google.cloud.bigquery.external_config.BigtableColumnFamily.only_read_latest

bool: If this is set only the latest version of value are exposed for all columns in this column family.

See more: [google.cloud.bigquery.external_config.BigtableColumnFamily.only_read_latest](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily#google_cloud_bigquery_external_config_BigtableColumnFamily_only_read_latest)

### google.cloud.bigquery.external_config.BigtableColumnFamily.type_

str: The type to convert the value in cells of this column family.

See more: [google.cloud.bigquery.external_config.BigtableColumnFamily.type_](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily#google_cloud_bigquery_external_config_BigtableColumnFamily_type_)

### google.cloud.bigquery.external_config.BigtableOptions.column_families

List[`.external_config.BigtableColumnFamily`

]: List of
column families to expose in the table schema along with their types.

See more: [google.cloud.bigquery.external_config.BigtableOptions.column_families](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableOptions#google_cloud_bigquery_external_config_BigtableOptions_column_families)

### google.cloud.bigquery.external_config.BigtableOptions.ignore_unspecified_column_families

bool: If :data:`True`

, ignore columns not specified in
`column_families`

list.

See more: [google.cloud.bigquery.external_config.BigtableOptions.ignore_unspecified_column_families](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableOptions#google_cloud_bigquery_external_config_BigtableOptions_ignore_unspecified_column_families)

### google.cloud.bigquery.external_config.BigtableOptions.read_rowkey_as_string

bool: If :data:`True`

, rowkey column families will be read and
converted to string.

See more: [google.cloud.bigquery.external_config.BigtableOptions.read_rowkey_as_string](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableOptions#google_cloud_bigquery_external_config_BigtableOptions_read_rowkey_as_string)

### google.cloud.bigquery.external_config.CSVOptions.allow_jagged_rows

bool: If :data:`True`

, BigQuery treats missing trailing columns as
null values.

See more: [google.cloud.bigquery.external_config.CSVOptions.allow_jagged_rows](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions#google_cloud_bigquery_external_config_CSVOptions_allow_jagged_rows)

### google.cloud.bigquery.external_config.CSVOptions.allow_quoted_newlines

bool: If :data:`True`

, quoted data sections that contain newline
characters in a CSV file are allowed.

See more: [google.cloud.bigquery.external_config.CSVOptions.allow_quoted_newlines](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions#google_cloud_bigquery_external_config_CSVOptions_allow_quoted_newlines)

### google.cloud.bigquery.external_config.CSVOptions.encoding

str: The character encoding of the data.

See more: [google.cloud.bigquery.external_config.CSVOptions.encoding](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions#google_cloud_bigquery_external_config_CSVOptions_encoding)

### google.cloud.bigquery.external_config.CSVOptions.field_delimiter

str: The separator for fields in a CSV file.

See more: [google.cloud.bigquery.external_config.CSVOptions.field_delimiter](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions#google_cloud_bigquery_external_config_CSVOptions_field_delimiter)

### google.cloud.bigquery.external_config.CSVOptions.null_markers

Optional[Iterable[str]]: A list of strings represented as SQL NULL values in a CSV file.

See more: [google.cloud.bigquery.external_config.CSVOptions.null_markers](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions#google_cloud_bigquery_external_config_CSVOptions_null_markers)

### google.cloud.bigquery.external_config.CSVOptions.preserve_ascii_control_characters

bool: Indicates if the embedded ASCII control characters (the first 32 characters in the ASCII-table, from '' to ' ') are preserved.

See more: [google.cloud.bigquery.external_config.CSVOptions.preserve_ascii_control_characters](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions#google_cloud_bigquery_external_config_CSVOptions_preserve_ascii_control_characters)

### google.cloud.bigquery.external_config.CSVOptions.quote_character

str: The value that is used to quote data sections in a CSV file.

See more: [google.cloud.bigquery.external_config.CSVOptions.quote_character](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions#google_cloud_bigquery_external_config_CSVOptions_quote_character)

### google.cloud.bigquery.external_config.CSVOptions.skip_leading_rows

int: The number of rows at the top of a CSV file.

See more: [google.cloud.bigquery.external_config.CSVOptions.skip_leading_rows](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions#google_cloud_bigquery_external_config_CSVOptions_skip_leading_rows)

### google.cloud.bigquery.external_config.CSVOptions.source_column_match

Optional[[google.cloud.bigquery.enums.SourceColumnMatch](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch)]: Controls the
strategy used to match loaded columns to the schema.

See more: [google.cloud.bigquery.external_config.CSVOptions.source_column_match](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions#google_cloud_bigquery_external_config_CSVOptions_source_column_match)

### google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions.default_storage_location_uri

Optional.

See more: [google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions.default_storage_location_uri](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions#google_cloud_bigquery_external_config_ExternalCatalogDatasetOptions_default_storage_location_uri)

### google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions.parameters

Optional.

See more: [google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions.parameters](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions#google_cloud_bigquery_external_config_ExternalCatalogDatasetOptions_parameters)

### google.cloud.bigquery.external_config.ExternalCatalogTableOptions.connection_id

Optional.

See more: [google.cloud.bigquery.external_config.ExternalCatalogTableOptions.connection_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogTableOptions#google_cloud_bigquery_external_config_ExternalCatalogTableOptions_connection_id)

### google.cloud.bigquery.external_config.ExternalCatalogTableOptions.parameters

Optional.

See more: [google.cloud.bigquery.external_config.ExternalCatalogTableOptions.parameters](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogTableOptions#google_cloud_bigquery_external_config_ExternalCatalogTableOptions_parameters)

### google.cloud.bigquery.external_config.ExternalCatalogTableOptions.storage_descriptor

Optional.

See more: [google.cloud.bigquery.external_config.ExternalCatalogTableOptions.storage_descriptor](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogTableOptions#google_cloud_bigquery_external_config_ExternalCatalogTableOptions_storage_descriptor)

### google.cloud.bigquery.external_config.ExternalConfig.autodetect

bool: If :data:`True`

, try to detect schema and format options
automatically.

See more: [google.cloud.bigquery.external_config.ExternalConfig.autodetect](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_autodetect)

### google.cloud.bigquery.external_config.ExternalConfig.avro_options

Additional properties to set if `sourceFormat`

is set to AVRO.

See more: [google.cloud.bigquery.external_config.ExternalConfig.avro_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_avro_options)

### google.cloud.bigquery.external_config.ExternalConfig.bigtable_options

Additional properties to set if `sourceFormat`

is set to BIGTABLE.

See more: [google.cloud.bigquery.external_config.ExternalConfig.bigtable_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_bigtable_options)

### google.cloud.bigquery.external_config.ExternalConfig.compression

str: The compression type of the data source.

See more: [google.cloud.bigquery.external_config.ExternalConfig.compression](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_compression)

### google.cloud.bigquery.external_config.ExternalConfig.connection_id

Optional[str]: ID of a BigQuery Connection API resource.

See more: [google.cloud.bigquery.external_config.ExternalConfig.connection_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_connection_id)

### google.cloud.bigquery.external_config.ExternalConfig.csv_options

Additional properties to set if `sourceFormat`

is set to CSV.

See more: [google.cloud.bigquery.external_config.ExternalConfig.csv_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_csv_options)

### google.cloud.bigquery.external_config.ExternalConfig.date_format

Optional[str]: Format used to parse DATE values.

See more: [google.cloud.bigquery.external_config.ExternalConfig.date_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_date_format)

### google.cloud.bigquery.external_config.ExternalConfig.datetime_format

Optional[str]: Format used to parse DATETIME values.

See more: [google.cloud.bigquery.external_config.ExternalConfig.datetime_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_datetime_format)

### google.cloud.bigquery.external_config.ExternalConfig.decimal_target_types

Possible SQL data types to which the source decimal values are converted.

See more: [google.cloud.bigquery.external_config.ExternalConfig.decimal_target_types](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_decimal_target_types)

### google.cloud.bigquery.external_config.ExternalConfig.google_sheets_options

Additional properties to set if `sourceFormat`

is set to
GOOGLE_SHEETS.

See more: [google.cloud.bigquery.external_config.ExternalConfig.google_sheets_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_google_sheets_options)

### google.cloud.bigquery.external_config.ExternalConfig.hive_partitioning

Optional[`.external_config.HivePartitioningOptions`

]: When set, it configures hive partitioning support.

See more: [google.cloud.bigquery.external_config.ExternalConfig.hive_partitioning](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_hive_partitioning)

### google.cloud.bigquery.external_config.ExternalConfig.ignore_unknown_values

bool: If :data:`True`

, extra values that are not represented in the
table schema are ignored.

See more: [google.cloud.bigquery.external_config.ExternalConfig.ignore_unknown_values](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_ignore_unknown_values)

### google.cloud.bigquery.external_config.ExternalConfig.max_bad_records

int: The maximum number of bad records that BigQuery can ignore when reading data.

See more: [google.cloud.bigquery.external_config.ExternalConfig.max_bad_records](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_max_bad_records)

### google.cloud.bigquery.external_config.ExternalConfig.options

Source-specific options.

See more: [google.cloud.bigquery.external_config.ExternalConfig.options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_options)

### google.cloud.bigquery.external_config.ExternalConfig.parquet_options

Additional properties to set if `sourceFormat`

is set to PARQUET.

See more: [google.cloud.bigquery.external_config.ExternalConfig.parquet_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_parquet_options)

### google.cloud.bigquery.external_config.ExternalConfig.reference_file_schema_uri

Optional[str]: When creating an external table, the user can provide a reference file with the table schema.

See more: [google.cloud.bigquery.external_config.ExternalConfig.reference_file_schema_uri](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_reference_file_schema_uri)

### google.cloud.bigquery.external_config.ExternalConfig.schema

List[[SchemaField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField)]: The schema
for the data.

See more: [google.cloud.bigquery.external_config.ExternalConfig.schema](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_schema)

### google.cloud.bigquery.external_config.ExternalConfig.source_format

`.external_config.ExternalSourceFormat`

:
Format of external source.

See more: [google.cloud.bigquery.external_config.ExternalConfig.source_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_source_format)

### google.cloud.bigquery.external_config.ExternalConfig.source_uris

List[str]: URIs that point to your data in Google Cloud.

See more: [google.cloud.bigquery.external_config.ExternalConfig.source_uris](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_source_uris)

### google.cloud.bigquery.external_config.ExternalConfig.time_format

Optional[str]: Format used to parse TIME values.

See more: [google.cloud.bigquery.external_config.ExternalConfig.time_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_time_format)

### google.cloud.bigquery.external_config.ExternalConfig.time_zone

Optional[str]: Time zone used when parsing timestamp values that do not have specific time zone information (e.g.

See more: [google.cloud.bigquery.external_config.ExternalConfig.time_zone](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_time_zone)

### google.cloud.bigquery.external_config.ExternalConfig.timestamp_format

Optional[str]: Format used to parse TIMESTAMP values.

See more: [google.cloud.bigquery.external_config.ExternalConfig.timestamp_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig#google_cloud_bigquery_external_config_ExternalConfig_timestamp_format)

### google.cloud.bigquery.external_config.ExternalSourceFormat.AVRO

Specifies Avro format.

See more: [google.cloud.bigquery.external_config.ExternalSourceFormat.AVRO](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat#google_cloud_bigquery_external_config_ExternalSourceFormat_AVRO)

### google.cloud.bigquery.external_config.ExternalSourceFormat.BIGTABLE

Specifies Bigtable format.

See more: [google.cloud.bigquery.external_config.ExternalSourceFormat.BIGTABLE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat#google_cloud_bigquery_external_config_ExternalSourceFormat_BIGTABLE)

### google.cloud.bigquery.external_config.ExternalSourceFormat.CSV

Specifies CSV format.

See more: [google.cloud.bigquery.external_config.ExternalSourceFormat.CSV](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat#google_cloud_bigquery_external_config_ExternalSourceFormat_CSV)

### google.cloud.bigquery.external_config.ExternalSourceFormat.DATASTORE_BACKUP

Specifies datastore backup format.

See more: [google.cloud.bigquery.external_config.ExternalSourceFormat.DATASTORE_BACKUP](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat#google_cloud_bigquery_external_config_ExternalSourceFormat_DATASTORE_BACKUP)

### google.cloud.bigquery.external_config.ExternalSourceFormat.GOOGLE_SHEETS

Specifies Google Sheets format.

See more: [google.cloud.bigquery.external_config.ExternalSourceFormat.GOOGLE_SHEETS](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat#google_cloud_bigquery_external_config_ExternalSourceFormat_GOOGLE_SHEETS)

### google.cloud.bigquery.external_config.ExternalSourceFormat.NEWLINE_DELIMITED_JSON

Specifies newline delimited JSON format.

See more: [google.cloud.bigquery.external_config.ExternalSourceFormat.NEWLINE_DELIMITED_JSON](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat#google_cloud_bigquery_external_config_ExternalSourceFormat_NEWLINE_DELIMITED_JSON)

### google.cloud.bigquery.external_config.ExternalSourceFormat.ORC

Specifies ORC format.

See more: [google.cloud.bigquery.external_config.ExternalSourceFormat.ORC](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat#google_cloud_bigquery_external_config_ExternalSourceFormat_ORC)

### google.cloud.bigquery.external_config.ExternalSourceFormat.PARQUET

Specifies Parquet format.

See more: [google.cloud.bigquery.external_config.ExternalSourceFormat.PARQUET](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat#google_cloud_bigquery_external_config_ExternalSourceFormat_PARQUET)

### google.cloud.bigquery.external_config.GoogleSheetsOptions.range

str: The range of a sheet that BigQuery will query from.

See more: [google.cloud.bigquery.external_config.GoogleSheetsOptions.range](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.GoogleSheetsOptions#google_cloud_bigquery_external_config_GoogleSheetsOptions_range)

### google.cloud.bigquery.external_config.GoogleSheetsOptions.skip_leading_rows

int: The number of rows at the top of a sheet that BigQuery will skip when reading the data.

See more: [google.cloud.bigquery.external_config.GoogleSheetsOptions.skip_leading_rows](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.GoogleSheetsOptions#google_cloud_bigquery_external_config_GoogleSheetsOptions_skip_leading_rows)

### google.cloud.bigquery.external_config.HivePartitioningOptions.mode

Optional[str]: When set, what mode of hive partitioning to use when reading data.

See more: [google.cloud.bigquery.external_config.HivePartitioningOptions.mode](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.HivePartitioningOptions#google_cloud_bigquery_external_config_HivePartitioningOptions_mode)

### google.cloud.bigquery.external_config.HivePartitioningOptions.require_partition_filter

Optional[bool]: If set to true, queries over the partitioned table require a partition filter that can be used for partition elimination to be specified.

See more: [google.cloud.bigquery.external_config.HivePartitioningOptions.require_partition_filter](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.HivePartitioningOptions#google_cloud_bigquery_external_config_HivePartitioningOptions_require_partition_filter)

### google.cloud.bigquery.external_config.HivePartitioningOptions.source_uri_prefix

Optional[str]: When hive partition detection is requested, a common prefix for all source URIs is required.

See more: [google.cloud.bigquery.external_config.HivePartitioningOptions.source_uri_prefix](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.HivePartitioningOptions#google_cloud_bigquery_external_config_HivePartitioningOptions_source_uri_prefix)

### google.cloud.bigquery.format_options.AvroOptions.use_avro_logical_types

[Optional] If sourceFormat is set to 'AVRO', indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER).

See more: [google.cloud.bigquery.format_options.AvroOptions.use_avro_logical_types](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.AvroOptions#google_cloud_bigquery_format_options_AvroOptions_use_avro_logical_types)

### google.cloud.bigquery.format_options.ParquetOptions.enable_list_inference

Indicates whether to use schema inference specifically for Parquet LIST logical type.

See more: [google.cloud.bigquery.format_options.ParquetOptions.enable_list_inference](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions#google_cloud_bigquery_format_options_ParquetOptions_enable_list_inference)

### google.cloud.bigquery.format_options.ParquetOptions.enum_as_string

Indicates whether to infer Parquet ENUM logical type as STRING instead of BYTES by default.

See more: [google.cloud.bigquery.format_options.ParquetOptions.enum_as_string](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions#google_cloud_bigquery_format_options_ParquetOptions_enum_as_string)

### google.cloud.bigquery.format_options.ParquetOptions.map_target_type

Indicates whether to simplify the representation of parquet maps to only show keys and values.

See more: [google.cloud.bigquery.format_options.ParquetOptions.map_target_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions#google_cloud_bigquery_format_options_ParquetOptions_map_target_type)

### google.cloud.bigquery.job.Compression.DEFLATE

Specifies DEFLATE format.

### google.cloud.bigquery.job.Compression.GZIP

Specifies GZIP format.

### google.cloud.bigquery.job.Compression.NONE

Specifies no compression.

### google.cloud.bigquery.job.Compression.SNAPPY

Specifies SNAPPY format.

### google.cloud.bigquery.job.Compression.ZSTD

Specifies ZSTD format.

### google.cloud.bigquery.job.CopyJob.configuration

The configuration for this copy job.

### google.cloud.bigquery.job.CopyJob.create_disposition

### google.cloud.bigquery.job.CopyJob.created

Datetime at which the job was created.

### google.cloud.bigquery.job.CopyJob.destination

[google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference): Table into which data
is to be loaded.

### google.cloud.bigquery.job.CopyJob.destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

See more: [google.cloud.bigquery.job.CopyJob.destination_encryption_configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_destination_encryption_configuration)

### google.cloud.bigquery.job.CopyJob.ended

Datetime at which the job finished.

See more: [google.cloud.bigquery.job.CopyJob.ended](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_ended)

### google.cloud.bigquery.job.CopyJob.error_result

Output only.

### google.cloud.bigquery.job.CopyJob.errors

Output only.

See more: [google.cloud.bigquery.job.CopyJob.errors](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_errors)

### google.cloud.bigquery.job.CopyJob.etag

ETag for the job resource.

See more: [google.cloud.bigquery.job.CopyJob.etag](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_etag)

### google.cloud.bigquery.job.CopyJob.job_id

str: ID of the job.

See more: [google.cloud.bigquery.job.CopyJob.job_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_job_id)

### google.cloud.bigquery.job.CopyJob.job_type

Type of job.

### google.cloud.bigquery.job.CopyJob.labels

Dict[str, str]: Labels for the job.

See more: [google.cloud.bigquery.job.CopyJob.labels](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_labels)

### google.cloud.bigquery.job.CopyJob.location

str: Location where the job runs.

### google.cloud.bigquery.job.CopyJob.num_child_jobs

The number of child jobs executed.

### google.cloud.bigquery.job.CopyJob.parent_job_id

Return the ID of the parent job.

### google.cloud.bigquery.job.CopyJob.path

URL path for the job's APIs.

See more: [google.cloud.bigquery.job.CopyJob.path](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_path)

### google.cloud.bigquery.job.CopyJob.project

Project bound to the job.

### google.cloud.bigquery.job.CopyJob.reservation_id

str: Name of the primary reservation assigned to this job.

### google.cloud.bigquery.job.CopyJob.reservation_usage

Job resource usage breakdown by reservation.

See more: [google.cloud.bigquery.job.CopyJob.reservation_usage](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_reservation_usage)

### google.cloud.bigquery.job.CopyJob.script_statistics

Statistics for a child job of a script.

See more: [google.cloud.bigquery.job.CopyJob.script_statistics](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_script_statistics)

### google.cloud.bigquery.job.CopyJob.self_link

URL for the job resource.

### google.cloud.bigquery.job.CopyJob.session_info

[Preview] Information of the session if this job is part of one.

### google.cloud.bigquery.job.CopyJob.sources

List[[google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference)]): Table(s) from
which data is to be loaded.

### google.cloud.bigquery.job.CopyJob.started

Datetime at which the job was started.

### google.cloud.bigquery.job.CopyJob.state

Output only.

See more: [google.cloud.bigquery.job.CopyJob.state](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_state)

### google.cloud.bigquery.job.CopyJob.transaction_info

Information of the multi-statement transaction if this job is part of one.

See more: [google.cloud.bigquery.job.CopyJob.transaction_info](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob#google_cloud_bigquery_job_CopyJob_transaction_info)

### google.cloud.bigquery.job.CopyJob.user_email

E-mail address of user who submitted the job.

### google.cloud.bigquery.job.CopyJob.write_disposition

### google.cloud.bigquery.job.CopyJobConfig.create_disposition

[google.cloud.bigquery.job.CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition): Specifies behavior
for creating tables.

See more: [google.cloud.bigquery.job.CopyJobConfig.create_disposition](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig#google_cloud_bigquery_job_CopyJobConfig_create_disposition)

### google.cloud.bigquery.job.CopyJobConfig.destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

See more: [google.cloud.bigquery.job.CopyJobConfig.destination_encryption_configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig#google_cloud_bigquery_job_CopyJobConfig_destination_encryption_configuration)

### google.cloud.bigquery.job.CopyJobConfig.destination_expiration_time

google.cloud.bigquery.job.DestinationExpirationTime: The time when the destination table expires.

See more: [google.cloud.bigquery.job.CopyJobConfig.destination_expiration_time](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig#google_cloud_bigquery_job_CopyJobConfig_destination_expiration_time)

### google.cloud.bigquery.job.CopyJobConfig.job_timeout_ms

Optional parameter.

See more: [google.cloud.bigquery.job.CopyJobConfig.job_timeout_ms](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig#google_cloud_bigquery_job_CopyJobConfig_job_timeout_ms)

### google.cloud.bigquery.job.CopyJobConfig.labels

Dict[str, str]: Labels for the job.

### google.cloud.bigquery.job.CopyJobConfig.max_slots

The maximum rate of slot consumption to allow for this job.

### google.cloud.bigquery.job.CopyJobConfig.operation_type

The operation to perform with this copy job.

See more: [google.cloud.bigquery.job.CopyJobConfig.operation_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig#google_cloud_bigquery_job_CopyJobConfig_operation_type)

### google.cloud.bigquery.job.CopyJobConfig.reservation

str: Optional.

See more: [google.cloud.bigquery.job.CopyJobConfig.reservation](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig#google_cloud_bigquery_job_CopyJobConfig_reservation)

### google.cloud.bigquery.job.CopyJobConfig.write_disposition

[google.cloud.bigquery.job.WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition): Action that occurs if
the destination table already exists.

See more: [google.cloud.bigquery.job.CopyJobConfig.write_disposition](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig#google_cloud_bigquery_job_CopyJobConfig_write_disposition)

### google.cloud.bigquery.job.CreateDisposition.CREATE_IF_NEEDED

If the table does not exist, BigQuery creates the table.

See more: [google.cloud.bigquery.job.CreateDisposition.CREATE_IF_NEEDED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition#google_cloud_bigquery_job_CreateDisposition_CREATE_IF_NEEDED)

### google.cloud.bigquery.job.CreateDisposition.CREATE_NEVER

The table must already exist.

See more: [google.cloud.bigquery.job.CreateDisposition.CREATE_NEVER](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition#google_cloud_bigquery_job_CreateDisposition_CREATE_NEVER)

### google.cloud.bigquery.job.DestinationFormat.AVRO

Specifies Avro format.

### google.cloud.bigquery.job.DestinationFormat.CSV

Specifies CSV format.

### google.cloud.bigquery.job.DestinationFormat.NEWLINE_DELIMITED_JSON

Specifies newline delimited JSON format.

See more: [google.cloud.bigquery.job.DestinationFormat.NEWLINE_DELIMITED_JSON](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DestinationFormat#google_cloud_bigquery_job_DestinationFormat_NEWLINE_DELIMITED_JSON)

### google.cloud.bigquery.job.DestinationFormat.PARQUET

Specifies Parquet format.

See more: [google.cloud.bigquery.job.DestinationFormat.PARQUET](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DestinationFormat#google_cloud_bigquery_job_DestinationFormat_PARQUET)

### google.cloud.bigquery.job.DmlStats.deleted_row_count

Number of deleted rows.

See more: [google.cloud.bigquery.job.DmlStats.deleted_row_count](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats#google_cloud_bigquery_job_DmlStats_deleted_row_count)

### google.cloud.bigquery.job.DmlStats.inserted_row_count

Number of inserted rows.

See more: [google.cloud.bigquery.job.DmlStats.inserted_row_count](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats#google_cloud_bigquery_job_DmlStats_inserted_row_count)

### google.cloud.bigquery.job.DmlStats.updated_row_count

Number of updated rows.

See more: [google.cloud.bigquery.job.DmlStats.updated_row_count](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats#google_cloud_bigquery_job_DmlStats_updated_row_count)

### google.cloud.bigquery.job.Encoding.ISO_8859_1

Specifies ISO-8859-1 encoding.

### google.cloud.bigquery.job.Encoding.UTF_8

Specifies UTF-8 encoding.

See more: [google.cloud.bigquery.job.Encoding.UTF_8](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Encoding#google_cloud_bigquery_job_Encoding_UTF_8)

### google.cloud.bigquery.job.ExtractJob.compression

See
[compression](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig).

### google.cloud.bigquery.job.ExtractJob.configuration

The configuration for this extract job.

See more: [google.cloud.bigquery.job.ExtractJob.configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_configuration)

### google.cloud.bigquery.job.ExtractJob.created

Datetime at which the job was created.

### google.cloud.bigquery.job.ExtractJob.destination_format

### google.cloud.bigquery.job.ExtractJob.destination_uri_file_counts

Return file counts from job statistics, if present.

See more: [google.cloud.bigquery.job.ExtractJob.destination_uri_file_counts](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_destination_uri_file_counts)

### google.cloud.bigquery.job.ExtractJob.destination_uris

List[str]: URIs describing where the extracted data will be
written in Cloud Storage, using the format
`gs://<bucket_name>/<object_name_or_glob>`

.

See more: [google.cloud.bigquery.job.ExtractJob.destination_uris](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_destination_uris)

### google.cloud.bigquery.job.ExtractJob.ended

Datetime at which the job finished.

### google.cloud.bigquery.job.ExtractJob.error_result

Output only.

### google.cloud.bigquery.job.ExtractJob.errors

Output only.

### google.cloud.bigquery.job.ExtractJob.etag

ETag for the job resource.

### google.cloud.bigquery.job.ExtractJob.field_delimiter

### google.cloud.bigquery.job.ExtractJob.job_id

str: ID of the job.

### google.cloud.bigquery.job.ExtractJob.job_type

Type of job.

### google.cloud.bigquery.job.ExtractJob.labels

Dict[str, str]: Labels for the job.

### google.cloud.bigquery.job.ExtractJob.location

str: Location where the job runs.

### google.cloud.bigquery.job.ExtractJob.num_child_jobs

The number of child jobs executed.

See more: [google.cloud.bigquery.job.ExtractJob.num_child_jobs](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_num_child_jobs)

### google.cloud.bigquery.job.ExtractJob.parent_job_id

Return the ID of the parent job.

See more: [google.cloud.bigquery.job.ExtractJob.parent_job_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_parent_job_id)

### google.cloud.bigquery.job.ExtractJob.path

URL path for the job's APIs.

### google.cloud.bigquery.job.ExtractJob.print_header

See
[print_header](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig).

### google.cloud.bigquery.job.ExtractJob.project

Project bound to the job.

### google.cloud.bigquery.job.ExtractJob.reservation_id

str: Name of the primary reservation assigned to this job.

See more: [google.cloud.bigquery.job.ExtractJob.reservation_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_reservation_id)

### google.cloud.bigquery.job.ExtractJob.reservation_usage

Job resource usage breakdown by reservation.

See more: [google.cloud.bigquery.job.ExtractJob.reservation_usage](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_reservation_usage)

### google.cloud.bigquery.job.ExtractJob.script_statistics

Statistics for a child job of a script.

See more: [google.cloud.bigquery.job.ExtractJob.script_statistics](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_script_statistics)

### google.cloud.bigquery.job.ExtractJob.self_link

URL for the job resource.

### google.cloud.bigquery.job.ExtractJob.session_info

[Preview] Information of the session if this job is part of one.

### google.cloud.bigquery.job.ExtractJob.source

Union[ [google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference), [google.cloud.bigquery.model.ModelReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference) ]: Table or Model from which data is to be loaded or extracted.

### google.cloud.bigquery.job.ExtractJob.started

Datetime at which the job was started.

### google.cloud.bigquery.job.ExtractJob.state

Output only.

### google.cloud.bigquery.job.ExtractJob.transaction_info

Information of the multi-statement transaction if this job is part of one.

See more: [google.cloud.bigquery.job.ExtractJob.transaction_info](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob#google_cloud_bigquery_job_ExtractJob_transaction_info)

### google.cloud.bigquery.job.ExtractJob.user_email

E-mail address of user who submitted the job.

### google.cloud.bigquery.job.ExtractJobConfig.compression

[google.cloud.bigquery.job.Compression](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Compression): Compression type to use for
exported files.

See more: [google.cloud.bigquery.job.ExtractJobConfig.compression](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig#google_cloud_bigquery_job_ExtractJobConfig_compression)

### google.cloud.bigquery.job.ExtractJobConfig.destination_format

[google.cloud.bigquery.job.DestinationFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DestinationFormat): Exported file format.

See more: [google.cloud.bigquery.job.ExtractJobConfig.destination_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig#google_cloud_bigquery_job_ExtractJobConfig_destination_format)

### google.cloud.bigquery.job.ExtractJobConfig.field_delimiter

str: Delimiter to use between fields in the exported data.

See more: [google.cloud.bigquery.job.ExtractJobConfig.field_delimiter](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig#google_cloud_bigquery_job_ExtractJobConfig_field_delimiter)

### google.cloud.bigquery.job.ExtractJobConfig.job_timeout_ms

Optional parameter.

See more: [google.cloud.bigquery.job.ExtractJobConfig.job_timeout_ms](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig#google_cloud_bigquery_job_ExtractJobConfig_job_timeout_ms)

### google.cloud.bigquery.job.ExtractJobConfig.labels

Dict[str, str]: Labels for the job.

### google.cloud.bigquery.job.ExtractJobConfig.max_slots

The maximum rate of slot consumption to allow for this job.

See more: [google.cloud.bigquery.job.ExtractJobConfig.max_slots](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig#google_cloud_bigquery_job_ExtractJobConfig_max_slots)

### google.cloud.bigquery.job.ExtractJobConfig.print_header

bool: Print a header row in the exported data.

See more: [google.cloud.bigquery.job.ExtractJobConfig.print_header](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig#google_cloud_bigquery_job_ExtractJobConfig_print_header)

### google.cloud.bigquery.job.ExtractJobConfig.reservation

str: Optional.

See more: [google.cloud.bigquery.job.ExtractJobConfig.reservation](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig#google_cloud_bigquery_job_ExtractJobConfig_reservation)

### google.cloud.bigquery.job.ExtractJobConfig.use_avro_logical_types

bool: For loads of Avro data, governs whether Avro logical types are converted to their corresponding BigQuery types (e.g.

See more: [google.cloud.bigquery.job.ExtractJobConfig.use_avro_logical_types](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig#google_cloud_bigquery_job_ExtractJobConfig_use_avro_logical_types)

### google.cloud.bigquery.job.IncrementalResultStats.disabled_reason

Optional[string]: Reason why incremental results were not written by the query.

See more: [google.cloud.bigquery.job.IncrementalResultStats.disabled_reason](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.IncrementalResultStats#google_cloud_bigquery_job_IncrementalResultStats_disabled_reason)

### google.cloud.bigquery.job.IncrementalResultStats.result_set_last_modify_time

Optional[datetime]: The time at which the result table's contents were modified.

See more: [google.cloud.bigquery.job.IncrementalResultStats.result_set_last_modify_time](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.IncrementalResultStats#google_cloud_bigquery_job_IncrementalResultStats_result_set_last_modify_time)

### google.cloud.bigquery.job.IncrementalResultStats.result_set_last_replace_time

Optional[datetime]: The time at which the result table's contents were completely replaced.

See more: [google.cloud.bigquery.job.IncrementalResultStats.result_set_last_replace_time](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.IncrementalResultStats#google_cloud_bigquery_job_IncrementalResultStats_result_set_last_replace_time)

### google.cloud.bigquery.job.LoadJob.allow_jagged_rows

### google.cloud.bigquery.job.LoadJob.allow_quoted_newlines

### google.cloud.bigquery.job.LoadJob.autodetect

See
[autodetect](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.clustering_fields

### google.cloud.bigquery.job.LoadJob.configuration

The configuration for this load job.

### google.cloud.bigquery.job.LoadJob.connection_properties

### google.cloud.bigquery.job.LoadJob.create_disposition

### google.cloud.bigquery.job.LoadJob.create_session

See
[create_session](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.created

Datetime at which the job was created.

### google.cloud.bigquery.job.LoadJob.date_format

See
[date_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.datetime_format

See
[datetime_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.destination

[google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference): table where loaded rows are written.

### google.cloud.bigquery.job.LoadJob.destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

See more: [google.cloud.bigquery.job.LoadJob.destination_encryption_configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_destination_encryption_configuration)

### google.cloud.bigquery.job.LoadJob.destination_table_description

Optional[str] name given to destination table.

See more: [google.cloud.bigquery.job.LoadJob.destination_table_description](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_destination_table_description)

### google.cloud.bigquery.job.LoadJob.destination_table_friendly_name

Optional[str] name given to destination table.

See more: [google.cloud.bigquery.job.LoadJob.destination_table_friendly_name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_destination_table_friendly_name)

### google.cloud.bigquery.job.LoadJob.encoding

See
[encoding](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.ended

Datetime at which the job finished.

See more: [google.cloud.bigquery.job.LoadJob.ended](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_ended)

### google.cloud.bigquery.job.LoadJob.error_result

Output only.

### google.cloud.bigquery.job.LoadJob.errors

Output only.

See more: [google.cloud.bigquery.job.LoadJob.errors](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_errors)

### google.cloud.bigquery.job.LoadJob.etag

ETag for the job resource.

See more: [google.cloud.bigquery.job.LoadJob.etag](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_etag)

### google.cloud.bigquery.job.LoadJob.field_delimiter

See
[field_delimiter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.ignore_unknown_values

### google.cloud.bigquery.job.LoadJob.input_file_bytes

Count of bytes loaded from source files.

See more: [google.cloud.bigquery.job.LoadJob.input_file_bytes](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_input_file_bytes)

### google.cloud.bigquery.job.LoadJob.input_files

Count of source files.

### google.cloud.bigquery.job.LoadJob.job_id

str: ID of the job.

See more: [google.cloud.bigquery.job.LoadJob.job_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_job_id)

### google.cloud.bigquery.job.LoadJob.job_type

Type of job.

### google.cloud.bigquery.job.LoadJob.labels

Dict[str, str]: Labels for the job.

See more: [google.cloud.bigquery.job.LoadJob.labels](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_labels)

### google.cloud.bigquery.job.LoadJob.location

str: Location where the job runs.

### google.cloud.bigquery.job.LoadJob.max_bad_records

See
[max_bad_records](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.null_marker

See
[null_marker](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.null_markers

See
[null_markers](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.num_child_jobs

The number of child jobs executed.

### google.cloud.bigquery.job.LoadJob.output_bytes

Count of bytes saved to destination table.

### google.cloud.bigquery.job.LoadJob.output_rows

Count of rows saved to destination table.

### google.cloud.bigquery.job.LoadJob.parent_job_id

Return the ID of the parent job.

### google.cloud.bigquery.job.LoadJob.path

URL path for the job's APIs.

See more: [google.cloud.bigquery.job.LoadJob.path](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_path)

### google.cloud.bigquery.job.LoadJob.project

Project bound to the job.

### google.cloud.bigquery.job.LoadJob.quote_character

See
[quote_character](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.range_partitioning

### google.cloud.bigquery.job.LoadJob.reference_file_schema_uri

See:
attr:`<xref uid="google.cloud.bigquery.job.LoadJobConfig.reference_file_schema_uri">google.cloud.bigquery.job.LoadJobConfig.reference_file_schema_uri</xref>`

.

See more: [google.cloud.bigquery.job.LoadJob.reference_file_schema_uri](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_reference_file_schema_uri)

### google.cloud.bigquery.job.LoadJob.reservation_id

str: Name of the primary reservation assigned to this job.

### google.cloud.bigquery.job.LoadJob.reservation_usage

Job resource usage breakdown by reservation.

See more: [google.cloud.bigquery.job.LoadJob.reservation_usage](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_reservation_usage)

### google.cloud.bigquery.job.LoadJob.schema

See
[schema](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

See more: [google.cloud.bigquery.job.LoadJob.schema](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_schema)

### google.cloud.bigquery.job.LoadJob.schema_update_options

### google.cloud.bigquery.job.LoadJob.script_statistics

Statistics for a child job of a script.

See more: [google.cloud.bigquery.job.LoadJob.script_statistics](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_script_statistics)

### google.cloud.bigquery.job.LoadJob.self_link

URL for the job resource.

### google.cloud.bigquery.job.LoadJob.session_info

[Preview] Information of the session if this job is part of one.

### google.cloud.bigquery.job.LoadJob.skip_leading_rows

### google.cloud.bigquery.job.LoadJob.source_column_match

### google.cloud.bigquery.job.LoadJob.source_format

See
[source_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.source_uris

Optional[Sequence[str]]: URIs of data files to be loaded.

### google.cloud.bigquery.job.LoadJob.started

Datetime at which the job was started.

### google.cloud.bigquery.job.LoadJob.state

Output only.

See more: [google.cloud.bigquery.job.LoadJob.state](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_state)

### google.cloud.bigquery.job.LoadJob.time_format

See
[time_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.time_partitioning

### google.cloud.bigquery.job.LoadJob.time_zone

See
[time_zone](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### google.cloud.bigquery.job.LoadJob.timestamp_format

### google.cloud.bigquery.job.LoadJob.transaction_info

Information of the multi-statement transaction if this job is part of one.

See more: [google.cloud.bigquery.job.LoadJob.transaction_info](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob#google_cloud_bigquery_job_LoadJob_transaction_info)

### google.cloud.bigquery.job.LoadJob.use_avro_logical_types

### google.cloud.bigquery.job.LoadJob.user_email

E-mail address of user who submitted the job.

### google.cloud.bigquery.job.LoadJob.write_disposition

### google.cloud.bigquery.job.LoadJobConfig.allow_jagged_rows

Optional[bool]: Allow missing trailing optional columns (CSV only).

See more: [google.cloud.bigquery.job.LoadJobConfig.allow_jagged_rows](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_allow_jagged_rows)

### google.cloud.bigquery.job.LoadJobConfig.allow_quoted_newlines

Optional[bool]: Allow quoted data containing newline characters (CSV only).

See more: [google.cloud.bigquery.job.LoadJobConfig.allow_quoted_newlines](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_allow_quoted_newlines)

### google.cloud.bigquery.job.LoadJobConfig.autodetect

Optional[bool]: Automatically infer the schema from a sample of the data.

See more: [google.cloud.bigquery.job.LoadJobConfig.autodetect](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_autodetect)

### google.cloud.bigquery.job.LoadJobConfig.clustering_fields

Optional[List[str]]: Fields defining clustering for the table.

See more: [google.cloud.bigquery.job.LoadJobConfig.clustering_fields](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_clustering_fields)

### google.cloud.bigquery.job.LoadJobConfig.column_name_character_map

Optional[google.cloud.bigquery.job.ColumnNameCharacterMap]: Character map supported for column names in CSV/Parquet loads.

See more: [google.cloud.bigquery.job.LoadJobConfig.column_name_character_map](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_column_name_character_map)

### google.cloud.bigquery.job.LoadJobConfig.connection_properties

Connection properties.

See more: [google.cloud.bigquery.job.LoadJobConfig.connection_properties](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_connection_properties)

### google.cloud.bigquery.job.LoadJobConfig.create_disposition

Optional[[google.cloud.bigquery.job.CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition)]: Specifies behavior
for creating tables.

See more: [google.cloud.bigquery.job.LoadJobConfig.create_disposition](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_create_disposition)

### google.cloud.bigquery.job.LoadJobConfig.create_session

[Preview] If :data:`True`

, creates a new session, where
[session_info](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob) will contain a
random server generated session id.

See more: [google.cloud.bigquery.job.LoadJobConfig.create_session](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_create_session)

### google.cloud.bigquery.job.LoadJobConfig.date_format

Optional[str]: Date format used for parsing DATE values.

See more: [google.cloud.bigquery.job.LoadJobConfig.date_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_date_format)

### google.cloud.bigquery.job.LoadJobConfig.datetime_format

Optional[str]: Date format used for parsing DATETIME values.

See more: [google.cloud.bigquery.job.LoadJobConfig.datetime_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_datetime_format)

### google.cloud.bigquery.job.LoadJobConfig.decimal_target_types

Possible SQL data types to which the source decimal values are converted.

See more: [google.cloud.bigquery.job.LoadJobConfig.decimal_target_types](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_decimal_target_types)

### google.cloud.bigquery.job.LoadJobConfig.destination_encryption_configuration

Optional[[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration)]: Custom
encryption configuration for the destination table.

See more: [google.cloud.bigquery.job.LoadJobConfig.destination_encryption_configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_destination_encryption_configuration)

### google.cloud.bigquery.job.LoadJobConfig.destination_table_description

Optional[str]: Description of the destination table.

See more: [google.cloud.bigquery.job.LoadJobConfig.destination_table_description](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_destination_table_description)

### google.cloud.bigquery.job.LoadJobConfig.destination_table_friendly_name

Optional[str]: Name given to destination table.

See more: [google.cloud.bigquery.job.LoadJobConfig.destination_table_friendly_name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_destination_table_friendly_name)

### google.cloud.bigquery.job.LoadJobConfig.encoding

Optional[[google.cloud.bigquery.job.Encoding](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Encoding)]: The character encoding of the
data.

### google.cloud.bigquery.job.LoadJobConfig.field_delimiter

Optional[str]: The separator for fields in a CSV file.

See more: [google.cloud.bigquery.job.LoadJobConfig.field_delimiter](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_field_delimiter)

### google.cloud.bigquery.job.LoadJobConfig.hive_partitioning

Optional[`.external_config.HivePartitioningOptions`

]: [Beta] When set, it configures hive partitioning support.

See more: [google.cloud.bigquery.job.LoadJobConfig.hive_partitioning](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_hive_partitioning)

### google.cloud.bigquery.job.LoadJobConfig.ignore_unknown_values

Optional[bool]: Ignore extra values not represented in the table schema.

See more: [google.cloud.bigquery.job.LoadJobConfig.ignore_unknown_values](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_ignore_unknown_values)

### google.cloud.bigquery.job.LoadJobConfig.job_timeout_ms

Optional parameter.

See more: [google.cloud.bigquery.job.LoadJobConfig.job_timeout_ms](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_job_timeout_ms)

### google.cloud.bigquery.job.LoadJobConfig.json_extension

Optional[str]: The extension to use for writing JSON data to BigQuery.

See more: [google.cloud.bigquery.job.LoadJobConfig.json_extension](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_json_extension)

### google.cloud.bigquery.job.LoadJobConfig.labels

Dict[str, str]: Labels for the job.

### google.cloud.bigquery.job.LoadJobConfig.max_bad_records

Optional[int]: Number of invalid rows to ignore.

See more: [google.cloud.bigquery.job.LoadJobConfig.max_bad_records](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_max_bad_records)

### google.cloud.bigquery.job.LoadJobConfig.max_slots

The maximum rate of slot consumption to allow for this job.

### google.cloud.bigquery.job.LoadJobConfig.null_marker

Optional[str]: Represents a null value (CSV only).

See more: [google.cloud.bigquery.job.LoadJobConfig.null_marker](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_null_marker)

### google.cloud.bigquery.job.LoadJobConfig.null_markers

Optional[List[str]]: A list of strings represented as SQL NULL values in a CSV file.

See more: [google.cloud.bigquery.job.LoadJobConfig.null_markers](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_null_markers)

### google.cloud.bigquery.job.LoadJobConfig.parquet_options

Optional[[google.cloud.bigquery.format_options.ParquetOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions)]: Additional
properties to set if `sourceFormat`

is set to PARQUET.

See more: [google.cloud.bigquery.job.LoadJobConfig.parquet_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_parquet_options)

### google.cloud.bigquery.job.LoadJobConfig.preserve_ascii_control_characters

Optional[bool]: Preserves the embedded ASCII control characters when sourceFormat is set to CSV.

See more: [google.cloud.bigquery.job.LoadJobConfig.preserve_ascii_control_characters](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_preserve_ascii_control_characters)

### google.cloud.bigquery.job.LoadJobConfig.projection_fields

Optional[List[str]]: If
[source_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) is set to
"DATASTORE_BACKUP", indicates which entity properties to load into
BigQuery from a Cloud Datastore backup.

See more: [google.cloud.bigquery.job.LoadJobConfig.projection_fields](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_projection_fields)

### google.cloud.bigquery.job.LoadJobConfig.quote_character

Optional[str]: Character used to quote data sections (CSV only).

See more: [google.cloud.bigquery.job.LoadJobConfig.quote_character](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_quote_character)

### google.cloud.bigquery.job.LoadJobConfig.range_partitioning

Optional[[google.cloud.bigquery.table.RangePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning)]:
Configures range-based partitioning for destination table.

See more: [google.cloud.bigquery.job.LoadJobConfig.range_partitioning](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_range_partitioning)

### google.cloud.bigquery.job.LoadJobConfig.reference_file_schema_uri

Optional[str]: When creating an external table, the user can provide a reference file with the table schema.

See more: [google.cloud.bigquery.job.LoadJobConfig.reference_file_schema_uri](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_reference_file_schema_uri)

### google.cloud.bigquery.job.LoadJobConfig.reservation

str: Optional.

See more: [google.cloud.bigquery.job.LoadJobConfig.reservation](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_reservation)

### google.cloud.bigquery.job.LoadJobConfig.schema

Optional[Sequence[Union[ [SchemaField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField), Mapping[str, Any] ]]]: Schema of the destination table.

### google.cloud.bigquery.job.LoadJobConfig.schema_update_options

Optional[List[[google.cloud.bigquery.job.SchemaUpdateOption](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SchemaUpdateOption)]]: Specifies
updates to the destination table schema to allow as a side effect of
the load job.

See more: [google.cloud.bigquery.job.LoadJobConfig.schema_update_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_schema_update_options)

### google.cloud.bigquery.job.LoadJobConfig.skip_leading_rows

Optional[int]: Number of rows to skip when reading data (CSV only).

See more: [google.cloud.bigquery.job.LoadJobConfig.skip_leading_rows](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_skip_leading_rows)

### google.cloud.bigquery.job.LoadJobConfig.source_column_match

Optional[[google.cloud.bigquery.enums.SourceColumnMatch](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch)]: Controls the
strategy used to match loaded columns to the schema.

See more: [google.cloud.bigquery.job.LoadJobConfig.source_column_match](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_source_column_match)

### google.cloud.bigquery.job.LoadJobConfig.source_format

Optional[[google.cloud.bigquery.job.SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat)]: File format of the data.

See more: [google.cloud.bigquery.job.LoadJobConfig.source_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_source_format)

### google.cloud.bigquery.job.LoadJobConfig.time_format

Optional[str]: Date format used for parsing TIME values.

See more: [google.cloud.bigquery.job.LoadJobConfig.time_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_time_format)

### google.cloud.bigquery.job.LoadJobConfig.time_partitioning

Optional[[google.cloud.bigquery.table.TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning)]: Specifies time-based
partitioning for the destination table.

See more: [google.cloud.bigquery.job.LoadJobConfig.time_partitioning](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_time_partitioning)

### google.cloud.bigquery.job.LoadJobConfig.time_zone

Optional[str]: Default time zone that will apply when parsing timestamp values that have no specific time zone.

### google.cloud.bigquery.job.LoadJobConfig.timestamp_format

Optional[str]: Date format used for parsing TIMESTAMP values.

See more: [google.cloud.bigquery.job.LoadJobConfig.timestamp_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_timestamp_format)

### google.cloud.bigquery.job.LoadJobConfig.timestamp_target_precision

Optional[list[int]]: [Private Preview] Precisions (maximum number of total digits in base 10) for seconds of TIMESTAMP types that are allowed to the destination table for autodetection mode.

See more: [google.cloud.bigquery.job.LoadJobConfig.timestamp_target_precision](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_timestamp_target_precision)

### google.cloud.bigquery.job.LoadJobConfig.use_avro_logical_types

Optional[bool]: For loads of Avro data, governs whether Avro logical types are converted to their corresponding BigQuery types (e.g.

See more: [google.cloud.bigquery.job.LoadJobConfig.use_avro_logical_types](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_use_avro_logical_types)

### google.cloud.bigquery.job.LoadJobConfig.write_disposition

Optional[[google.cloud.bigquery.job.WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition)]: Action that occurs if
the destination table already exists.

See more: [google.cloud.bigquery.job.LoadJobConfig.write_disposition](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_write_disposition)

### google.cloud.bigquery.job.OperationType.CLONE

The source table type is TABLE and the destination table type is CLONE.

### google.cloud.bigquery.job.OperationType.COPY

The source and destination table have the same table type.

### google.cloud.bigquery.job.OperationType.OPERATION_TYPE_UNSPECIFIED

Unspecified operation type.

See more: [google.cloud.bigquery.job.OperationType.OPERATION_TYPE_UNSPECIFIED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.OperationType#google_cloud_bigquery_job_OperationType_OPERATION_TYPE_UNSPECIFIED)

### google.cloud.bigquery.job.OperationType.RESTORE

The source table type is SNAPSHOT and the destination table type is TABLE.

### google.cloud.bigquery.job.OperationType.SNAPSHOT

The source table type is TABLE and the destination table type is SNAPSHOT.

### google.cloud.bigquery.job.QueryJob.allow_large_results

### google.cloud.bigquery.job.QueryJob.billing_tier

Return billing tier from job statistics, if present.

### google.cloud.bigquery.job.QueryJob.cache_hit

Return whether or not query results were served from cache.

### google.cloud.bigquery.job.QueryJob.clustering_fields

### google.cloud.bigquery.job.QueryJob.configuration

The configuration for this query job.

### google.cloud.bigquery.job.QueryJob.connection_properties

### google.cloud.bigquery.job.QueryJob.create_disposition

### google.cloud.bigquery.job.QueryJob.create_session

See
[create_session](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### google.cloud.bigquery.job.QueryJob.created

Datetime at which the job was created.

### google.cloud.bigquery.job.QueryJob.ddl_operation_performed

Optional[str]: Return the DDL operation performed.

See more: [google.cloud.bigquery.job.QueryJob.ddl_operation_performed](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_ddl_operation_performed)

### google.cloud.bigquery.job.QueryJob.ddl_target_routine

Optional[[google.cloud.bigquery.routine.RoutineReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference)]: Return the DDL target routine, present
for CREATE/DROP FUNCTION/PROCEDURE queries.

See more: [google.cloud.bigquery.job.QueryJob.ddl_target_routine](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_ddl_target_routine)

### google.cloud.bigquery.job.QueryJob.ddl_target_table

Optional[[google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference)]: Return the DDL target table, present
for CREATE/DROP TABLE/VIEW queries.

See more: [google.cloud.bigquery.job.QueryJob.ddl_target_table](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_ddl_target_table)

### google.cloud.bigquery.job.QueryJob.default_dataset

### google.cloud.bigquery.job.QueryJob.destination

See
[destination](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### google.cloud.bigquery.job.QueryJob.destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

See more: [google.cloud.bigquery.job.QueryJob.destination_encryption_configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_destination_encryption_configuration)

### google.cloud.bigquery.job.QueryJob.dry_run

See
[dry_run](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### google.cloud.bigquery.job.QueryJob.ended

Datetime at which the job finished.

See more: [google.cloud.bigquery.job.QueryJob.ended](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_ended)

### google.cloud.bigquery.job.QueryJob.error_result

Output only.

### google.cloud.bigquery.job.QueryJob.errors

Output only.

### google.cloud.bigquery.job.QueryJob.estimated_bytes_processed

Return the estimated number of bytes processed by the query.

See more: [google.cloud.bigquery.job.QueryJob.estimated_bytes_processed](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_estimated_bytes_processed)

### google.cloud.bigquery.job.QueryJob.etag

ETag for the job resource.

See more: [google.cloud.bigquery.job.QueryJob.etag](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_etag)

### google.cloud.bigquery.job.QueryJob.flatten_results

### google.cloud.bigquery.job.QueryJob.job_id

str: ID of the job.

### google.cloud.bigquery.job.QueryJob.job_type

Type of job.

### google.cloud.bigquery.job.QueryJob.labels

Dict[str, str]: Labels for the job.

### google.cloud.bigquery.job.QueryJob.location

str: Location where the job runs.

### google.cloud.bigquery.job.QueryJob.maximum_billing_tier

### google.cloud.bigquery.job.QueryJob.maximum_bytes_billed

### google.cloud.bigquery.job.QueryJob.num_child_jobs

The number of child jobs executed.

### google.cloud.bigquery.job.QueryJob.num_dml_affected_rows

Return the number of DML rows affected by the job.

See more: [google.cloud.bigquery.job.QueryJob.num_dml_affected_rows](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_num_dml_affected_rows)

### google.cloud.bigquery.job.QueryJob.parent_job_id

Return the ID of the parent job.

### google.cloud.bigquery.job.QueryJob.path

URL path for the job's APIs.

See more: [google.cloud.bigquery.job.QueryJob.path](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_path)

### google.cloud.bigquery.job.QueryJob.priority

See
[priority](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### google.cloud.bigquery.job.QueryJob.project

Project bound to the job.

### google.cloud.bigquery.job.QueryJob.query

str: The query text used in this query job.

See more: [google.cloud.bigquery.job.QueryJob.query](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_query)

### google.cloud.bigquery.job.QueryJob.query_id

[Preview] ID of a completed query.

### google.cloud.bigquery.job.QueryJob.query_parameters

### google.cloud.bigquery.job.QueryJob.query_plan

Return query plan from job statistics, if present.

### google.cloud.bigquery.job.QueryJob.range_partitioning

### google.cloud.bigquery.job.QueryJob.referenced_tables

Return referenced tables from job statistics, if present.

See more: [google.cloud.bigquery.job.QueryJob.referenced_tables](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_referenced_tables)

### google.cloud.bigquery.job.QueryJob.reservation_id

str: Name of the primary reservation assigned to this job.

### google.cloud.bigquery.job.QueryJob.reservation_usage

Job resource usage breakdown by reservation.

See more: [google.cloud.bigquery.job.QueryJob.reservation_usage](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_reservation_usage)

### google.cloud.bigquery.job.QueryJob.schema

The schema of the results.

### google.cloud.bigquery.job.QueryJob.schema_update_options

### google.cloud.bigquery.job.QueryJob.script_statistics

Statistics for a child job of a script.

See more: [google.cloud.bigquery.job.QueryJob.script_statistics](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_script_statistics)

### google.cloud.bigquery.job.QueryJob.search_stats

Returns a SearchStats object.

### google.cloud.bigquery.job.QueryJob.self_link

URL for the job resource.

### google.cloud.bigquery.job.QueryJob.session_info

[Preview] Information of the session if this job is part of one.

### google.cloud.bigquery.job.QueryJob.slot_millis

Union[int, None]: Slot-milliseconds used by this query job.

### google.cloud.bigquery.job.QueryJob.started

Datetime at which the job was started.

### google.cloud.bigquery.job.QueryJob.state

Output only.

See more: [google.cloud.bigquery.job.QueryJob.state](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_state)

### google.cloud.bigquery.job.QueryJob.statement_type

Return statement type from job statistics, if present.

### google.cloud.bigquery.job.QueryJob.table_definitions

### google.cloud.bigquery.job.QueryJob.time_partitioning

### google.cloud.bigquery.job.QueryJob.timeline

List(TimelineEntry): Return the query execution timeline from job statistics.

### google.cloud.bigquery.job.QueryJob.total_bytes_billed

Return total bytes billed from job statistics, if present.

See more: [google.cloud.bigquery.job.QueryJob.total_bytes_billed](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_total_bytes_billed)

### google.cloud.bigquery.job.QueryJob.total_bytes_processed

Return total bytes processed from job statistics, if present.

See more: [google.cloud.bigquery.job.QueryJob.total_bytes_processed](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_total_bytes_processed)

### google.cloud.bigquery.job.QueryJob.transaction_info

Information of the multi-statement transaction if this job is part of one.

See more: [google.cloud.bigquery.job.QueryJob.transaction_info](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_transaction_info)

### google.cloud.bigquery.job.QueryJob.udf_resources

See
[udf_resources](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### google.cloud.bigquery.job.QueryJob.undeclared_query_parameters

Return undeclared query parameters from job statistics, if present.

See more: [google.cloud.bigquery.job.QueryJob.undeclared_query_parameters](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_undeclared_query_parameters)

### google.cloud.bigquery.job.QueryJob.use_legacy_sql

See
[use_legacy_sql](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### google.cloud.bigquery.job.QueryJob.use_query_cache

### google.cloud.bigquery.job.QueryJob.user_email

E-mail address of user who submitted the job.

### google.cloud.bigquery.job.QueryJob.write_disposition

### google.cloud.bigquery.job.QueryJobConfig.allow_large_results

bool: Allow large query results tables (legacy SQL, only).

See more: [google.cloud.bigquery.job.QueryJobConfig.allow_large_results](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_allow_large_results)

### google.cloud.bigquery.job.QueryJobConfig.clustering_fields

Optional[List[str]]: Fields defining clustering for the table.

See more: [google.cloud.bigquery.job.QueryJobConfig.clustering_fields](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_clustering_fields)

### google.cloud.bigquery.job.QueryJobConfig.connection_properties

Connection properties.

See more: [google.cloud.bigquery.job.QueryJobConfig.connection_properties](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_connection_properties)

### google.cloud.bigquery.job.QueryJobConfig.create_disposition

[google.cloud.bigquery.job.CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition): Specifies behavior
for creating tables.

See more: [google.cloud.bigquery.job.QueryJobConfig.create_disposition](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_create_disposition)

### google.cloud.bigquery.job.QueryJobConfig.create_session

[Preview] If :data:`True`

, creates a new session, where
[session_info](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob) will contain a
random server generated session id.

See more: [google.cloud.bigquery.job.QueryJobConfig.create_session](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_create_session)

### google.cloud.bigquery.job.QueryJobConfig.default_dataset

[google.cloud.bigquery.dataset.DatasetReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference): the default dataset
to use for unqualified table names in the query or :data:`None`

if not
set.

See more: [google.cloud.bigquery.job.QueryJobConfig.default_dataset](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_default_dataset)

### google.cloud.bigquery.job.QueryJobConfig.destination

[google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference): table where results are
written or :data:`None`

if not set.

See more: [google.cloud.bigquery.job.QueryJobConfig.destination](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_destination)

### google.cloud.bigquery.job.QueryJobConfig.destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

See more: [google.cloud.bigquery.job.QueryJobConfig.destination_encryption_configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_destination_encryption_configuration)

### google.cloud.bigquery.job.QueryJobConfig.dry_run

bool: :data:`True`

if this query should be a dry run to estimate
costs.

### google.cloud.bigquery.job.QueryJobConfig.flatten_results

bool: Flatten nested/repeated fields in results.

See more: [google.cloud.bigquery.job.QueryJobConfig.flatten_results](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_flatten_results)

### google.cloud.bigquery.job.QueryJobConfig.job_timeout_ms

Optional parameter.

See more: [google.cloud.bigquery.job.QueryJobConfig.job_timeout_ms](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_job_timeout_ms)

### google.cloud.bigquery.job.QueryJobConfig.labels

Dict[str, str]: Labels for the job.

### google.cloud.bigquery.job.QueryJobConfig.max_slots

The maximum rate of slot consumption to allow for this job.

See more: [google.cloud.bigquery.job.QueryJobConfig.max_slots](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_max_slots)

### google.cloud.bigquery.job.QueryJobConfig.maximum_billing_tier

int: Deprecated.

See more: [google.cloud.bigquery.job.QueryJobConfig.maximum_billing_tier](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_maximum_billing_tier)

### google.cloud.bigquery.job.QueryJobConfig.maximum_bytes_billed

int: Maximum bytes to be billed for this job or :data:`None`

if not set.

See more: [google.cloud.bigquery.job.QueryJobConfig.maximum_bytes_billed](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_maximum_bytes_billed)

### google.cloud.bigquery.job.QueryJobConfig.priority

[google.cloud.bigquery.job.QueryPriority](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPriority): Priority of the query.

### google.cloud.bigquery.job.QueryJobConfig.query_parameters

List[Union[[google.cloud.bigquery.query.ArrayQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter), [google.cloud.bigquery.query.ScalarQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameter), [google.cloud.bigquery.query.StructQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter)]]: list of parameters
for parameterized query (empty by default).

See more: [google.cloud.bigquery.job.QueryJobConfig.query_parameters](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_query_parameters)

### google.cloud.bigquery.job.QueryJobConfig.range_partitioning

Optional[[google.cloud.bigquery.table.RangePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning)]:
Configures range-based partitioning for destination table.

See more: [google.cloud.bigquery.job.QueryJobConfig.range_partitioning](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_range_partitioning)

### google.cloud.bigquery.job.QueryJobConfig.reservation

str: Optional.

See more: [google.cloud.bigquery.job.QueryJobConfig.reservation](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_reservation)

### google.cloud.bigquery.job.QueryJobConfig.schema_update_options

List[[google.cloud.bigquery.job.SchemaUpdateOption](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SchemaUpdateOption)]: Specifies
updates to the destination table schema to allow as a side effect of
the query job.

See more: [google.cloud.bigquery.job.QueryJobConfig.schema_update_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_schema_update_options)

### google.cloud.bigquery.job.QueryJobConfig.script_options

Options controlling the execution of scripts.

See more: [google.cloud.bigquery.job.QueryJobConfig.script_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_script_options)

### google.cloud.bigquery.job.QueryJobConfig.table_definitions

Dict[str, [google.cloud.bigquery.external_config.ExternalConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig)]:
Definitions for external tables or :data:`None`

if not set.

See more: [google.cloud.bigquery.job.QueryJobConfig.table_definitions](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_table_definitions)

### google.cloud.bigquery.job.QueryJobConfig.time_partitioning

Optional[[google.cloud.bigquery.table.TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning)]: Specifies
time-based partitioning for the destination table.

See more: [google.cloud.bigquery.job.QueryJobConfig.time_partitioning](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_time_partitioning)

### google.cloud.bigquery.job.QueryJobConfig.udf_resources

List[[google.cloud.bigquery.query.UDFResource](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.UDFResource)]: user
defined function resources (empty by default).

See more: [google.cloud.bigquery.job.QueryJobConfig.udf_resources](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_udf_resources)

### google.cloud.bigquery.job.QueryJobConfig.use_legacy_sql

bool: Use legacy SQL syntax.

See more: [google.cloud.bigquery.job.QueryJobConfig.use_legacy_sql](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_use_legacy_sql)

### google.cloud.bigquery.job.QueryJobConfig.use_query_cache

bool: Look for the query result in the cache.

See more: [google.cloud.bigquery.job.QueryJobConfig.use_query_cache](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_use_query_cache)

### google.cloud.bigquery.job.QueryJobConfig.write_disposition

[google.cloud.bigquery.job.WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition): Action that occurs if
the destination table already exists.

See more: [google.cloud.bigquery.job.QueryJobConfig.write_disposition](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_write_disposition)

### google.cloud.bigquery.job.QueryJobConfig.write_incremental_results

This is only supported for a SELECT query using a temporary table.

See more: [google.cloud.bigquery.job.QueryJobConfig.write_incremental_results](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig#google_cloud_bigquery_job_QueryJobConfig_write_incremental_results)

### google.cloud.bigquery.job.QueryPlanEntry.completed_parallel_inputs

Optional[int]: Number of parallel input segments completed.

See more: [google.cloud.bigquery.job.QueryPlanEntry.completed_parallel_inputs](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_completed_parallel_inputs)

### google.cloud.bigquery.job.QueryPlanEntry.compute_ms_avg

Optional[int]: Milliseconds the average worker spent on CPU-bound processing.

See more: [google.cloud.bigquery.job.QueryPlanEntry.compute_ms_avg](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_compute_ms_avg)

### google.cloud.bigquery.job.QueryPlanEntry.compute_ms_max

Optional[int]: Milliseconds the slowest worker spent on CPU-bound processing.

See more: [google.cloud.bigquery.job.QueryPlanEntry.compute_ms_max](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_compute_ms_max)

### google.cloud.bigquery.job.QueryPlanEntry.compute_ratio_avg

Optional[float]: Ratio of time the average worker spent on CPU-bound processing, relative to the longest time spent by any worker in any stage of the overall plan.

See more: [google.cloud.bigquery.job.QueryPlanEntry.compute_ratio_avg](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_compute_ratio_avg)

### google.cloud.bigquery.job.QueryPlanEntry.compute_ratio_max

Optional[float]: Ratio of time the slowest worker spent on CPU-bound processing, relative to the longest time spent by any worker in any stage of the overall plan.

See more: [google.cloud.bigquery.job.QueryPlanEntry.compute_ratio_max](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_compute_ratio_max)

### google.cloud.bigquery.job.QueryPlanEntry.end

Optional[Datetime]: Datetime when the stage ended.

### google.cloud.bigquery.job.QueryPlanEntry.entry_id

Optional[str]: Unique ID for the stage within the plan.

### google.cloud.bigquery.job.QueryPlanEntry.input_stages

List(int): Entry IDs for stages that were inputs for this stage.

See more: [google.cloud.bigquery.job.QueryPlanEntry.input_stages](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_input_stages)

### google.cloud.bigquery.job.QueryPlanEntry.name

Optional[str]: Human-readable name of the stage.

### google.cloud.bigquery.job.QueryPlanEntry.parallel_inputs

Optional[int]: Number of parallel input segments within the stage.

See more: [google.cloud.bigquery.job.QueryPlanEntry.parallel_inputs](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_parallel_inputs)

### google.cloud.bigquery.job.QueryPlanEntry.read_ms_avg

Optional[int]: Milliseconds the average worker spent reading input.

See more: [google.cloud.bigquery.job.QueryPlanEntry.read_ms_avg](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_read_ms_avg)

### google.cloud.bigquery.job.QueryPlanEntry.read_ms_max

Optional[int]: Milliseconds the slowest worker spent reading input.

See more: [google.cloud.bigquery.job.QueryPlanEntry.read_ms_max](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_read_ms_max)

### google.cloud.bigquery.job.QueryPlanEntry.read_ratio_avg

Optional[float]: Ratio of time the average worker spent reading input, relative to the longest time spent by any worker in any stage of the overall plan.

See more: [google.cloud.bigquery.job.QueryPlanEntry.read_ratio_avg](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_read_ratio_avg)

### google.cloud.bigquery.job.QueryPlanEntry.read_ratio_max

Optional[float]: Ratio of time the slowest worker spent reading to be scheduled, relative to the longest time spent by any worker in any stage of the overall plan.

See more: [google.cloud.bigquery.job.QueryPlanEntry.read_ratio_max](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_read_ratio_max)

### google.cloud.bigquery.job.QueryPlanEntry.records_read

Optional[int]: Number of records read by this stage.

See more: [google.cloud.bigquery.job.QueryPlanEntry.records_read](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_records_read)

### google.cloud.bigquery.job.QueryPlanEntry.records_written

Optional[int]: Number of records written by this stage.

See more: [google.cloud.bigquery.job.QueryPlanEntry.records_written](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_records_written)

### google.cloud.bigquery.job.QueryPlanEntry.shuffle_output_bytes

Optional[int]: Number of bytes written by this stage to intermediate shuffle.

See more: [google.cloud.bigquery.job.QueryPlanEntry.shuffle_output_bytes](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_shuffle_output_bytes)

### google.cloud.bigquery.job.QueryPlanEntry.shuffle_output_bytes_spilled

Optional[int]: Number of bytes written by this stage to intermediate shuffle and spilled to disk.

See more: [google.cloud.bigquery.job.QueryPlanEntry.shuffle_output_bytes_spilled](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_shuffle_output_bytes_spilled)

### google.cloud.bigquery.job.QueryPlanEntry.slot_ms

Optional[int]: Slot-milliseconds used by the stage.

### google.cloud.bigquery.job.QueryPlanEntry.start

Optional[Datetime]: Datetime when the stage started.

### google.cloud.bigquery.job.QueryPlanEntry.status

Optional[str]: status of this stage.

### google.cloud.bigquery.job.QueryPlanEntry.steps

List(QueryPlanEntryStep): List of step operations performed by each worker in the stage.

### google.cloud.bigquery.job.QueryPlanEntry.wait_ms_avg

Optional[int]: Milliseconds the average worker spent waiting to be scheduled.

See more: [google.cloud.bigquery.job.QueryPlanEntry.wait_ms_avg](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_wait_ms_avg)

### google.cloud.bigquery.job.QueryPlanEntry.wait_ms_max

Optional[int]: Milliseconds the slowest worker spent waiting to be scheduled.

See more: [google.cloud.bigquery.job.QueryPlanEntry.wait_ms_max](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_wait_ms_max)

### google.cloud.bigquery.job.QueryPlanEntry.wait_ratio_avg

Optional[float]: Ratio of time the average worker spent waiting to be scheduled, relative to the longest time spent by any worker in any stage of the overall plan.

See more: [google.cloud.bigquery.job.QueryPlanEntry.wait_ratio_avg](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_wait_ratio_avg)

### google.cloud.bigquery.job.QueryPlanEntry.wait_ratio_max

Optional[float]: Ratio of time the slowest worker spent waiting to be scheduled, relative to the longest time spent by any worker in any stage of the overall plan.

See more: [google.cloud.bigquery.job.QueryPlanEntry.wait_ratio_max](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_wait_ratio_max)

### google.cloud.bigquery.job.QueryPlanEntry.write_ms_avg

Optional[int]: Milliseconds the average worker spent writing output data.

See more: [google.cloud.bigquery.job.QueryPlanEntry.write_ms_avg](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_write_ms_avg)

### google.cloud.bigquery.job.QueryPlanEntry.write_ms_max

Optional[int]: Milliseconds the slowest worker spent writing output data.

See more: [google.cloud.bigquery.job.QueryPlanEntry.write_ms_max](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_write_ms_max)

### google.cloud.bigquery.job.QueryPlanEntry.write_ratio_avg

Optional[float]: Ratio of time the average worker spent writing output data, relative to the longest time spent by any worker in any stage of the overall plan.

See more: [google.cloud.bigquery.job.QueryPlanEntry.write_ratio_avg](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_write_ratio_avg)

### google.cloud.bigquery.job.QueryPlanEntry.write_ratio_max

Optional[float]: Ratio of time the slowest worker spent writing output data, relative to the longest time spent by any worker in any stage of the overall plan.

See more: [google.cloud.bigquery.job.QueryPlanEntry.write_ratio_max](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry#google_cloud_bigquery_job_QueryPlanEntry_write_ratio_max)

### google.cloud.bigquery.job.QueryPriority.BATCH

Specifies batch priority.

### google.cloud.bigquery.job.QueryPriority.INTERACTIVE

Specifies interactive priority.

See more: [google.cloud.bigquery.job.QueryPriority.INTERACTIVE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPriority#google_cloud_bigquery_job_QueryPriority_INTERACTIVE)

### google.cloud.bigquery.job.ReservationUsage.name

Reservation name or "unreserved" for on-demand resources usage.

### google.cloud.bigquery.job.ReservationUsage.slot_ms

Total slot milliseconds used by the reservation for a particular job.

See more: [google.cloud.bigquery.job.ReservationUsage.slot_ms](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ReservationUsage#google_cloud_bigquery_job_ReservationUsage_slot_ms)

### google.cloud.bigquery.job.SchemaUpdateOption.ALLOW_FIELD_ADDITION

Allow adding a nullable field to the schema.

See more: [google.cloud.bigquery.job.SchemaUpdateOption.ALLOW_FIELD_ADDITION](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SchemaUpdateOption#google_cloud_bigquery_job_SchemaUpdateOption_ALLOW_FIELD_ADDITION)

### google.cloud.bigquery.job.SchemaUpdateOption.ALLOW_FIELD_RELAXATION

Allow relaxing a required field in the original schema to nullable.

See more: [google.cloud.bigquery.job.SchemaUpdateOption.ALLOW_FIELD_RELAXATION](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SchemaUpdateOption#google_cloud_bigquery_job_SchemaUpdateOption_ALLOW_FIELD_RELAXATION)

### google.cloud.bigquery.job.ScriptOptions.key_result_statement

Determines which statement in the script represents the "key result".

See more: [google.cloud.bigquery.job.ScriptOptions.key_result_statement](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptOptions#google_cloud_bigquery_job_ScriptOptions_key_result_statement)

### google.cloud.bigquery.job.ScriptOptions.statement_byte_budget

Limit on the number of bytes billed per statement.

See more: [google.cloud.bigquery.job.ScriptOptions.statement_byte_budget](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptOptions#google_cloud_bigquery_job_ScriptOptions_statement_byte_budget)

### google.cloud.bigquery.job.ScriptOptions.statement_timeout_ms

Timeout period for each statement in a script.

See more: [google.cloud.bigquery.job.ScriptOptions.statement_timeout_ms](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptOptions#google_cloud_bigquery_job_ScriptOptions_statement_timeout_ms)

### google.cloud.bigquery.job.ScriptStackFrame.end_column

int: One-based end column.

See more: [google.cloud.bigquery.job.ScriptStackFrame.end_column](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame#google_cloud_bigquery_job_ScriptStackFrame_end_column)

### google.cloud.bigquery.job.ScriptStackFrame.end_line

int: One-based end line.

See more: [google.cloud.bigquery.job.ScriptStackFrame.end_line](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame#google_cloud_bigquery_job_ScriptStackFrame_end_line)

### google.cloud.bigquery.job.ScriptStackFrame.procedure_id

Optional[str]: Name of the active procedure.

See more: [google.cloud.bigquery.job.ScriptStackFrame.procedure_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame#google_cloud_bigquery_job_ScriptStackFrame_procedure_id)

### google.cloud.bigquery.job.ScriptStackFrame.start_column

int: One-based start column.

See more: [google.cloud.bigquery.job.ScriptStackFrame.start_column](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame#google_cloud_bigquery_job_ScriptStackFrame_start_column)

### google.cloud.bigquery.job.ScriptStackFrame.start_line

int: One-based start line.

See more: [google.cloud.bigquery.job.ScriptStackFrame.start_line](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame#google_cloud_bigquery_job_ScriptStackFrame_start_line)

### google.cloud.bigquery.job.ScriptStackFrame.text

str: Text of the current statement/expression.

### google.cloud.bigquery.job.ScriptStatistics.evaluation_kind

str: Indicates the type of child job.

See more: [google.cloud.bigquery.job.ScriptStatistics.evaluation_kind](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStatistics#google_cloud_bigquery_job_ScriptStatistics_evaluation_kind)

### google.cloud.bigquery.job.ScriptStatistics.stack_frames

Stack trace where the current evaluation happened.

See more: [google.cloud.bigquery.job.ScriptStatistics.stack_frames](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStatistics#google_cloud_bigquery_job_ScriptStatistics_stack_frames)

### google.cloud.bigquery.job.SourceFormat.AVRO

Specifies Avro format.

### google.cloud.bigquery.job.SourceFormat.CSV

Specifies CSV format.

### google.cloud.bigquery.job.SourceFormat.DATASTORE_BACKUP

Specifies datastore backup format.

See more: [google.cloud.bigquery.job.SourceFormat.DATASTORE_BACKUP](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat#google_cloud_bigquery_job_SourceFormat_DATASTORE_BACKUP)

### google.cloud.bigquery.job.SourceFormat.NEWLINE_DELIMITED_JSON

Specifies newline delimited JSON format.

See more: [google.cloud.bigquery.job.SourceFormat.NEWLINE_DELIMITED_JSON](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat#google_cloud_bigquery_job_SourceFormat_NEWLINE_DELIMITED_JSON)

### google.cloud.bigquery.job.SourceFormat.ORC

Specifies Orc format.

### google.cloud.bigquery.job.SourceFormat.PARQUET

Specifies Parquet format.

### google.cloud.bigquery.job.TimelineEntry.active_units

Optional[int]: Current number of input units being processed by workers, reported as largest value since the last sample.

See more: [google.cloud.bigquery.job.TimelineEntry.active_units](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry#google_cloud_bigquery_job_TimelineEntry_active_units)

### google.cloud.bigquery.job.TimelineEntry.completed_units

Optional[int]: Current number of input units completed by this query.

See more: [google.cloud.bigquery.job.TimelineEntry.completed_units](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry#google_cloud_bigquery_job_TimelineEntry_completed_units)

### google.cloud.bigquery.job.TimelineEntry.elapsed_ms

Optional[int]: Milliseconds elapsed since start of query execution.

See more: [google.cloud.bigquery.job.TimelineEntry.elapsed_ms](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry#google_cloud_bigquery_job_TimelineEntry_elapsed_ms)

### google.cloud.bigquery.job.TimelineEntry.pending_units

Optional[int]: Current number of input units remaining for query stages active at this sample time.

See more: [google.cloud.bigquery.job.TimelineEntry.pending_units](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry#google_cloud_bigquery_job_TimelineEntry_pending_units)

### google.cloud.bigquery.job.TimelineEntry.slot_millis

Optional[int]: Cumulative slot-milliseconds consumed by this query.

See more: [google.cloud.bigquery.job.TimelineEntry.slot_millis](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry#google_cloud_bigquery_job_TimelineEntry_slot_millis)

### google.cloud.bigquery.job.TransactionInfo.transaction_id

Output only.

See more: [google.cloud.bigquery.job.TransactionInfo.transaction_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TransactionInfo#google_cloud_bigquery_job_TransactionInfo_transaction_id)

### google.cloud.bigquery.job.UnknownJob.configuration

Job-type specific configurtion.

See more: [google.cloud.bigquery.job.UnknownJob.configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob#google_cloud_bigquery_job_UnknownJob_configuration)

### google.cloud.bigquery.job.UnknownJob.created

Datetime at which the job was created.

### google.cloud.bigquery.job.UnknownJob.ended

Datetime at which the job finished.

### google.cloud.bigquery.job.UnknownJob.error_result

Output only.

### google.cloud.bigquery.job.UnknownJob.errors

Output only.

### google.cloud.bigquery.job.UnknownJob.etag

ETag for the job resource.

### google.cloud.bigquery.job.UnknownJob.job_id

str: ID of the job.

### google.cloud.bigquery.job.UnknownJob.job_type

Type of job.

### google.cloud.bigquery.job.UnknownJob.labels

Dict[str, str]: Labels for the job.

### google.cloud.bigquery.job.UnknownJob.location

str: Location where the job runs.

### google.cloud.bigquery.job.UnknownJob.num_child_jobs

The number of child jobs executed.

See more: [google.cloud.bigquery.job.UnknownJob.num_child_jobs](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob#google_cloud_bigquery_job_UnknownJob_num_child_jobs)

### google.cloud.bigquery.job.UnknownJob.parent_job_id

Return the ID of the parent job.

See more: [google.cloud.bigquery.job.UnknownJob.parent_job_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob#google_cloud_bigquery_job_UnknownJob_parent_job_id)

### google.cloud.bigquery.job.UnknownJob.path

URL path for the job's APIs.

### google.cloud.bigquery.job.UnknownJob.project

Project bound to the job.

### google.cloud.bigquery.job.UnknownJob.reservation_id

str: Name of the primary reservation assigned to this job.

See more: [google.cloud.bigquery.job.UnknownJob.reservation_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob#google_cloud_bigquery_job_UnknownJob_reservation_id)

### google.cloud.bigquery.job.UnknownJob.reservation_usage

Job resource usage breakdown by reservation.

See more: [google.cloud.bigquery.job.UnknownJob.reservation_usage](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob#google_cloud_bigquery_job_UnknownJob_reservation_usage)

### google.cloud.bigquery.job.UnknownJob.script_statistics

Statistics for a child job of a script.

See more: [google.cloud.bigquery.job.UnknownJob.script_statistics](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob#google_cloud_bigquery_job_UnknownJob_script_statistics)

### google.cloud.bigquery.job.UnknownJob.self_link

URL for the job resource.

### google.cloud.bigquery.job.UnknownJob.session_info

[Preview] Information of the session if this job is part of one.

### google.cloud.bigquery.job.UnknownJob.started

Datetime at which the job was started.

### google.cloud.bigquery.job.UnknownJob.state

Output only.

### google.cloud.bigquery.job.UnknownJob.transaction_info

Information of the multi-statement transaction if this job is part of one.

See more: [google.cloud.bigquery.job.UnknownJob.transaction_info](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob#google_cloud_bigquery_job_UnknownJob_transaction_info)

### google.cloud.bigquery.job.UnknownJob.user_email

E-mail address of user who submitted the job.

### google.cloud.bigquery.job.WriteDisposition.WRITE_APPEND

If the table already exists, BigQuery appends the data to the table.

See more: [google.cloud.bigquery.job.WriteDisposition.WRITE_APPEND](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition#google_cloud_bigquery_job_WriteDisposition_WRITE_APPEND)

### google.cloud.bigquery.job.WriteDisposition.WRITE_EMPTY

If the table already exists and contains data, a 'duplicate' error is returned in the job result.

See more: [google.cloud.bigquery.job.WriteDisposition.WRITE_EMPTY](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition#google_cloud_bigquery_job_WriteDisposition_WRITE_EMPTY)

### google.cloud.bigquery.job.WriteDisposition.WRITE_TRUNCATE

If the table already exists, BigQuery overwrites the table data.

See more: [google.cloud.bigquery.job.WriteDisposition.WRITE_TRUNCATE](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition#google_cloud_bigquery_job_WriteDisposition_WRITE_TRUNCATE)

### google.cloud.bigquery.job.WriteDisposition.WRITE_TRUNCATE_DATA

For existing tables, truncate data but preserve existing schema and constraints.

See more: [google.cloud.bigquery.job.WriteDisposition.WRITE_TRUNCATE_DATA](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition#google_cloud_bigquery_job_WriteDisposition_WRITE_TRUNCATE_DATA)

### google.cloud.bigquery.job.base.ReservationUsage.name

Reservation name or "unreserved" for on-demand resources usage.

See more: [google.cloud.bigquery.job.base.ReservationUsage.name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ReservationUsage#google_cloud_bigquery_job_base_ReservationUsage_name)

### google.cloud.bigquery.job.base.ReservationUsage.slot_ms

Total slot milliseconds used by the reservation for a particular job.

See more: [google.cloud.bigquery.job.base.ReservationUsage.slot_ms](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ReservationUsage#google_cloud_bigquery_job_base_ReservationUsage_slot_ms)

### google.cloud.bigquery.job.base.ScriptStackFrame.end_column

int: One-based end column.

See more: [google.cloud.bigquery.job.base.ScriptStackFrame.end_column](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame#google_cloud_bigquery_job_base_ScriptStackFrame_end_column)

### google.cloud.bigquery.job.base.ScriptStackFrame.end_line

int: One-based end line.

See more: [google.cloud.bigquery.job.base.ScriptStackFrame.end_line](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame#google_cloud_bigquery_job_base_ScriptStackFrame_end_line)

### google.cloud.bigquery.job.base.ScriptStackFrame.procedure_id

Optional[str]: Name of the active procedure.

See more: [google.cloud.bigquery.job.base.ScriptStackFrame.procedure_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame#google_cloud_bigquery_job_base_ScriptStackFrame_procedure_id)

### google.cloud.bigquery.job.base.ScriptStackFrame.start_column

int: One-based start column.

See more: [google.cloud.bigquery.job.base.ScriptStackFrame.start_column](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame#google_cloud_bigquery_job_base_ScriptStackFrame_start_column)

### google.cloud.bigquery.job.base.ScriptStackFrame.start_line

int: One-based start line.

See more: [google.cloud.bigquery.job.base.ScriptStackFrame.start_line](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame#google_cloud_bigquery_job_base_ScriptStackFrame_start_line)

### google.cloud.bigquery.job.base.ScriptStackFrame.text

str: Text of the current statement/expression.

See more: [google.cloud.bigquery.job.base.ScriptStackFrame.text](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame#google_cloud_bigquery_job_base_ScriptStackFrame_text)

### google.cloud.bigquery.job.base.ScriptStatistics.evaluation_kind

str: Indicates the type of child job.

See more: [google.cloud.bigquery.job.base.ScriptStatistics.evaluation_kind](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStatistics#google_cloud_bigquery_job_base_ScriptStatistics_evaluation_kind)

### google.cloud.bigquery.job.base.ScriptStatistics.stack_frames

Stack trace where the current evaluation happened.

See more: [google.cloud.bigquery.job.base.ScriptStatistics.stack_frames](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStatistics#google_cloud_bigquery_job_base_ScriptStatistics_stack_frames)

### google.cloud.bigquery.job.base.SessionInfo.session_id

The ID of the session.

See more: [google.cloud.bigquery.job.base.SessionInfo.session_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.SessionInfo#google_cloud_bigquery_job_base_SessionInfo_session_id)

### google.cloud.bigquery.job.base.TransactionInfo.transaction_id

Output only.

See more: [google.cloud.bigquery.job.base.TransactionInfo.transaction_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.TransactionInfo#google_cloud_bigquery_job_base_TransactionInfo_transaction_id)

### google.cloud.bigquery.model.Model.best_trial_id

The best trial_id across all training runs.

### google.cloud.bigquery.model.Model.created

Datetime at which the model was created (:data:`None`

until set from the server).

### google.cloud.bigquery.model.Model.dataset_id

ID of dataset containing the model.

### google.cloud.bigquery.model.Model.description

Description of the model (defaults to :data:`None`

).

### google.cloud.bigquery.model.Model.encryption_configuration

Custom encryption configuration for the model.

See more: [google.cloud.bigquery.model.Model.encryption_configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.Model#google_cloud_bigquery_model_Model_encryption_configuration)

### google.cloud.bigquery.model.Model.etag

ETag for the model resource (:data:`None`

until set from the server).

See more: [google.cloud.bigquery.model.Model.etag](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.Model#google_cloud_bigquery_model_Model_etag)

### google.cloud.bigquery.model.Model.expires

The datetime when this model expires.

### google.cloud.bigquery.model.Model.feature_columns

Input feature columns that were used to train this model.

### google.cloud.bigquery.model.Model.friendly_name

Title of the table (defaults to :data:`None`

).

### google.cloud.bigquery.model.Model.label_columns

Label columns that were used to train this model.

### google.cloud.bigquery.model.Model.labels

Labels for the table.

See more: [google.cloud.bigquery.model.Model.labels](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.Model#google_cloud_bigquery_model_Model_labels)

### google.cloud.bigquery.model.Model.location

The geographic location where the model resides.

### google.cloud.bigquery.model.Model.model_id

The model ID.

### google.cloud.bigquery.model.Model.model_type

Type of the model resource.

### google.cloud.bigquery.model.Model.modified

Datetime at which the model was last modified (:data:`None`

until set from the server).

### google.cloud.bigquery.model.Model.path

URL path for the model's APIs.

See more: [google.cloud.bigquery.model.Model.path](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.Model#google_cloud_bigquery_model_Model_path)

### google.cloud.bigquery.model.Model.project

Project bound to the model.

### google.cloud.bigquery.model.Model.reference

A model reference pointing to this model.

### google.cloud.bigquery.model.Model.training_runs

Information for all training runs in increasing order of start time.

### google.cloud.bigquery.model.Model.transform_columns

The input feature columns that were used to train this model.

See more: [google.cloud.bigquery.model.Model.transform_columns](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.Model#google_cloud_bigquery_model_Model_transform_columns)

### google.cloud.bigquery.model.ModelReference.dataset_id

str: ID of dataset containing the model.

See more: [google.cloud.bigquery.model.ModelReference.dataset_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference#google_cloud_bigquery_model_ModelReference_dataset_id)

### google.cloud.bigquery.model.ModelReference.model_id

str: The model ID.

See more: [google.cloud.bigquery.model.ModelReference.model_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference#google_cloud_bigquery_model_ModelReference_model_id)

### google.cloud.bigquery.model.ModelReference.path

URL path for the model's APIs.

### google.cloud.bigquery.model.ModelReference.project

str: Project bound to the model.

See more: [google.cloud.bigquery.model.ModelReference.project](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference#google_cloud_bigquery_model_ModelReference_project)

### google.cloud.bigquery.model.TransformColumn.name

Name of the column.

### google.cloud.bigquery.model.TransformColumn.transform_sql

The SQL expression used in the column transform.

See more: [google.cloud.bigquery.model.TransformColumn.transform_sql](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.TransformColumn#google_cloud_bigquery_model_TransformColumn_transform_sql)

### google.cloud.bigquery.model.TransformColumn.type_

Data type of the column after the transform.

### google.cloud.bigquery.query.ConnectionProperty.key

Name of the property.

See more: [google.cloud.bigquery.query.ConnectionProperty.key](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty#google_cloud_bigquery_query_ConnectionProperty_key)

### google.cloud.bigquery.query.ConnectionProperty.value

Value of the property.

See more: [google.cloud.bigquery.query.ConnectionProperty.value](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty#google_cloud_bigquery_query_ConnectionProperty_value)

### google.cloud.bigquery.routine.DeterminismLevel.DETERMINISM_LEVEL_UNSPECIFIED

The determinism of the UDF is unspecified.

See more: [google.cloud.bigquery.routine.DeterminismLevel.DETERMINISM_LEVEL_UNSPECIFIED](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.DeterminismLevel#google_cloud_bigquery_routine_DeterminismLevel_DETERMINISM_LEVEL_UNSPECIFIED)

### google.cloud.bigquery.routine.DeterminismLevel.DETERMINISTIC

The UDF is deterministic, meaning that 2 function calls with the same inputs always produce the same result, even across 2 query runs.

See more: [google.cloud.bigquery.routine.DeterminismLevel.DETERMINISTIC](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.DeterminismLevel#google_cloud_bigquery_routine_DeterminismLevel_DETERMINISTIC)

### google.cloud.bigquery.routine.DeterminismLevel.NOT_DETERMINISTIC

The UDF is not deterministic.

See more: [google.cloud.bigquery.routine.DeterminismLevel.NOT_DETERMINISTIC](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.DeterminismLevel#google_cloud_bigquery_routine_DeterminismLevel_NOT_DETERMINISTIC)

### google.cloud.bigquery.routine.ExternalRuntimeOptions.container_cpu

Optional.

See more: [google.cloud.bigquery.routine.ExternalRuntimeOptions.container_cpu](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions#google_cloud_bigquery_routine_ExternalRuntimeOptions_container_cpu)

### google.cloud.bigquery.routine.ExternalRuntimeOptions.container_memory

Optional.

See more: [google.cloud.bigquery.routine.ExternalRuntimeOptions.container_memory](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions#google_cloud_bigquery_routine_ExternalRuntimeOptions_container_memory)

### google.cloud.bigquery.routine.ExternalRuntimeOptions.max_batching_rows

Optional.

See more: [google.cloud.bigquery.routine.ExternalRuntimeOptions.max_batching_rows](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions#google_cloud_bigquery_routine_ExternalRuntimeOptions_max_batching_rows)

### google.cloud.bigquery.routine.ExternalRuntimeOptions.runtime_connection

Optional.

See more: [google.cloud.bigquery.routine.ExternalRuntimeOptions.runtime_connection](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions#google_cloud_bigquery_routine_ExternalRuntimeOptions_runtime_connection)

### google.cloud.bigquery.routine.ExternalRuntimeOptions.runtime_version

Optional.

See more: [google.cloud.bigquery.routine.ExternalRuntimeOptions.runtime_version](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions#google_cloud_bigquery_routine_ExternalRuntimeOptions_runtime_version)

### google.cloud.bigquery.routine.RemoteFunctionOptions.connection

string: Fully qualified name of the user-provided connection object which holds the authentication information to send requests to the remote service.

See more: [google.cloud.bigquery.routine.RemoteFunctionOptions.connection](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions#google_cloud_bigquery_routine_RemoteFunctionOptions_connection)

### google.cloud.bigquery.routine.RemoteFunctionOptions.endpoint

string: Endpoint of the user-provided remote service.

See more: [google.cloud.bigquery.routine.RemoteFunctionOptions.endpoint](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions#google_cloud_bigquery_routine_RemoteFunctionOptions_endpoint)

### google.cloud.bigquery.routine.RemoteFunctionOptions.max_batching_rows

int64: Max number of rows in each batch sent to the remote service.

See more: [google.cloud.bigquery.routine.RemoteFunctionOptions.max_batching_rows](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions#google_cloud_bigquery_routine_RemoteFunctionOptions_max_batching_rows)

### google.cloud.bigquery.routine.RemoteFunctionOptions.user_defined_context

Dict[str, str]: User-defined context as a set of key/value pairs, which will be sent as function invocation context together with batched arguments in the requests to the remote service.

See more: [google.cloud.bigquery.routine.RemoteFunctionOptions.user_defined_context](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions#google_cloud_bigquery_routine_RemoteFunctionOptions_user_defined_context)

### google.cloud.bigquery.routine.Routine.arguments

List[[google.cloud.bigquery.routine.RoutineArgument](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument)]: Input/output
argument of a function or a stored procedure.

### google.cloud.bigquery.routine.Routine.body

str: The body of the routine.

### google.cloud.bigquery.routine.Routine.created

Optional[datetime.datetime]: Datetime at which the routine was
created (:data:`None`

until set from the server).

### google.cloud.bigquery.routine.Routine.data_governance_type

Optional[str]: If set to `DATA_MASKING`

, the function is validated
and made available as a masking function.

See more: [google.cloud.bigquery.routine.Routine.data_governance_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine#google_cloud_bigquery_routine_Routine_data_governance_type)

### google.cloud.bigquery.routine.Routine.dataset_id

str: ID of dataset containing the routine.

### google.cloud.bigquery.routine.Routine.description

Optional[str]: Description of the routine (defaults to
:data:`None`

).

### google.cloud.bigquery.routine.Routine.determinism_level

Optional[str]: (experimental) The determinism level of the JavaScript UDF if defined.

See more: [google.cloud.bigquery.routine.Routine.determinism_level](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine#google_cloud_bigquery_routine_Routine_determinism_level)

### google.cloud.bigquery.routine.Routine.etag

str: ETag for the resource (:data:`None`

until set from the
server).

### google.cloud.bigquery.routine.Routine.external_runtime_options

Optional[[google.cloud.bigquery.routine.ExternalRuntimeOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions)]:
Configures the external runtime options for a routine.

See more: [google.cloud.bigquery.routine.Routine.external_runtime_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine#google_cloud_bigquery_routine_Routine_external_runtime_options)

### google.cloud.bigquery.routine.Routine.imported_libraries

List[str]: The path of the imported JavaScript libraries.

See more: [google.cloud.bigquery.routine.Routine.imported_libraries](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine#google_cloud_bigquery_routine_Routine_imported_libraries)

### google.cloud.bigquery.routine.Routine.language

Optional[str]: The language of the routine.

### google.cloud.bigquery.routine.Routine.modified

Optional[datetime.datetime]: Datetime at which the routine was
last modified (:data:`None`

until set from the server).

### google.cloud.bigquery.routine.Routine.path

str: URL path for the routine's APIs.

### google.cloud.bigquery.routine.Routine.project

str: ID of the project containing the routine.

### google.cloud.bigquery.routine.Routine.reference

[google.cloud.bigquery.routine.RoutineReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference): Reference
describing the ID of this routine.

### google.cloud.bigquery.routine.Routine.remote_function_options

Optional[[google.cloud.bigquery.routine.RemoteFunctionOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions)]:
Configures remote function options for a routine.

See more: [google.cloud.bigquery.routine.Routine.remote_function_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine#google_cloud_bigquery_routine_Routine_remote_function_options)

### google.cloud.bigquery.routine.Routine.return_table_type

The return type of a Table Valued Function (TVF) routine.

See more: [google.cloud.bigquery.routine.Routine.return_table_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine#google_cloud_bigquery_routine_Routine_return_table_type)

### google.cloud.bigquery.routine.Routine.return_type

google.cloud.bigquery.StandardSqlDataType: Return type of the routine.

### google.cloud.bigquery.routine.Routine.routine_id

str: The routine ID.

### google.cloud.bigquery.routine.Routine.type_

str: The fine-grained type of the routine.

### google.cloud.bigquery.routine.RoutineArgument.data_type

Optional[google.cloud.bigquery.StandardSqlDataType]: Type of a variable, e.g., a function argument.

See more: [google.cloud.bigquery.routine.RoutineArgument.data_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument#google_cloud_bigquery_routine_RoutineArgument_data_type)

### google.cloud.bigquery.routine.RoutineArgument.kind

Optional[str]: The kind of argument, for example `FIXED_TYPE`

or
`ANY_TYPE`

.

See more: [google.cloud.bigquery.routine.RoutineArgument.kind](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument#google_cloud_bigquery_routine_RoutineArgument_kind)

### google.cloud.bigquery.routine.RoutineArgument.mode

Optional[str]: The input/output mode of the argument.

See more: [google.cloud.bigquery.routine.RoutineArgument.mode](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument#google_cloud_bigquery_routine_RoutineArgument_mode)

### google.cloud.bigquery.routine.RoutineArgument.name

Optional[str]: Name of this argument.

See more: [google.cloud.bigquery.routine.RoutineArgument.name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument#google_cloud_bigquery_routine_RoutineArgument_name)

### google.cloud.bigquery.routine.RoutineReference.dataset_id

str: ID of dataset containing the routine.

See more: [google.cloud.bigquery.routine.RoutineReference.dataset_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference#google_cloud_bigquery_routine_RoutineReference_dataset_id)

### google.cloud.bigquery.routine.RoutineReference.path

str: URL path for the routine's APIs.

See more: [google.cloud.bigquery.routine.RoutineReference.path](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference#google_cloud_bigquery_routine_RoutineReference_path)

### google.cloud.bigquery.routine.RoutineReference.project

str: ID of the project containing the routine.

See more: [google.cloud.bigquery.routine.RoutineReference.project](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference#google_cloud_bigquery_routine_RoutineReference_project)

### google.cloud.bigquery.routine.RoutineReference.routine_id

str: The routine ID.

See more: [google.cloud.bigquery.routine.RoutineReference.routine_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference#google_cloud_bigquery_routine_RoutineReference_routine_id)

### google.cloud.bigquery.schema.ForeignTypeInfo.type_system

Required.

See more: [google.cloud.bigquery.schema.ForeignTypeInfo.type_system](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.ForeignTypeInfo#google_cloud_bigquery_schema_ForeignTypeInfo_type_system)

### google.cloud.bigquery.schema.PolicyTagList.names

Tuple[str]: Policy tags associated with this definition.

### google.cloud.bigquery.schema.SchemaField.default_value_expression

Optional[str] default value of a field, using an SQL expression.

See more: [google.cloud.bigquery.schema.SchemaField.default_value_expression](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_default_value_expression)

### google.cloud.bigquery.schema.SchemaField.description

Optional[str]: description for the field.

See more: [google.cloud.bigquery.schema.SchemaField.description](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_description)

### google.cloud.bigquery.schema.SchemaField.field_type

str: The type of the field.

See more: [google.cloud.bigquery.schema.SchemaField.field_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_field_type)

### google.cloud.bigquery.schema.SchemaField.fields

Optional[tuple]: Subfields contained in this field.

### google.cloud.bigquery.schema.SchemaField.foreign_type_definition

Definition of the foreign data type.

See more: [google.cloud.bigquery.schema.SchemaField.foreign_type_definition](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_foreign_type_definition)

### google.cloud.bigquery.schema.SchemaField.is_nullable

bool: whether 'mode' is 'nullable'.

See more: [google.cloud.bigquery.schema.SchemaField.is_nullable](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_is_nullable)

### google.cloud.bigquery.schema.SchemaField.max_length

Optional[int]: Maximum length for the STRING or BYTES field.

See more: [google.cloud.bigquery.schema.SchemaField.max_length](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_max_length)

### google.cloud.bigquery.schema.SchemaField.mode

Optional[str]: The mode of the field.

### google.cloud.bigquery.schema.SchemaField.name

str: The name of the field.

### google.cloud.bigquery.schema.SchemaField.policy_tags

Optional[[google.cloud.bigquery.schema.PolicyTagList](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.PolicyTagList)]: Policy tag list
definition for this field.

See more: [google.cloud.bigquery.schema.SchemaField.policy_tags](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_policy_tags)

### google.cloud.bigquery.schema.SchemaField.precision

Optional[int]: Precision (number of digits) for the NUMERIC field.

See more: [google.cloud.bigquery.schema.SchemaField.precision](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_precision)

### google.cloud.bigquery.schema.SchemaField.range_element_type

Optional[FieldElementType]: The subtype of the RANGE, if the type of this field is RANGE.

See more: [google.cloud.bigquery.schema.SchemaField.range_element_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_range_element_type)

### google.cloud.bigquery.schema.SchemaField.rounding_mode

Enum that specifies the rounding mode to be used when storing values of NUMERIC and BIGNUMERIC type.

See more: [google.cloud.bigquery.schema.SchemaField.rounding_mode](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_rounding_mode)

### google.cloud.bigquery.schema.SchemaField.scale

Optional[int]: Scale (digits after decimal) for the NUMERIC field.

### google.cloud.bigquery.schema.SchemaField.timestamp_precision

Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.

See more: [google.cloud.bigquery.schema.SchemaField.timestamp_precision](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField#google_cloud_bigquery_schema_SchemaField_timestamp_precision)

### google.cloud.bigquery.schema.SerDeInfo.name

Optional.

### google.cloud.bigquery.schema.SerDeInfo.parameters

Optional.

### google.cloud.bigquery.schema.SerDeInfo.serialization_library

Required.

See more: [google.cloud.bigquery.schema.SerDeInfo.serialization_library](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SerDeInfo#google_cloud_bigquery_schema_SerDeInfo_serialization_library)

### google.cloud.bigquery.schema.StorageDescriptor.input_format

Optional.

See more: [google.cloud.bigquery.schema.StorageDescriptor.input_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.StorageDescriptor#google_cloud_bigquery_schema_StorageDescriptor_input_format)

### google.cloud.bigquery.schema.StorageDescriptor.location_uri

Optional.

See more: [google.cloud.bigquery.schema.StorageDescriptor.location_uri](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.StorageDescriptor#google_cloud_bigquery_schema_StorageDescriptor_location_uri)

### google.cloud.bigquery.schema.StorageDescriptor.output_format

Optional.

See more: [google.cloud.bigquery.schema.StorageDescriptor.output_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.StorageDescriptor#google_cloud_bigquery_schema_StorageDescriptor_output_format)

### google.cloud.bigquery.schema.StorageDescriptor.serde_info

Optional.

See more: [google.cloud.bigquery.schema.StorageDescriptor.serde_info](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.StorageDescriptor#google_cloud_bigquery_schema_StorageDescriptor_serde_info)

### google.cloud.bigquery.standard_sql.StandardSqlDataType.array_element_type

The type of the array's elements, if type_kind is ARRAY.

See more: [google.cloud.bigquery.standard_sql.StandardSqlDataType.array_element_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType#google_cloud_bigquery_standard_sql_StandardSqlDataType_array_element_type)

### google.cloud.bigquery.standard_sql.StandardSqlDataType.range_element_type

The type of the range's elements, if type_kind = "RANGE".

See more: [google.cloud.bigquery.standard_sql.StandardSqlDataType.range_element_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType#google_cloud_bigquery_standard_sql_StandardSqlDataType_range_element_type)

### google.cloud.bigquery.standard_sql.StandardSqlDataType.struct_type

The fields of this struct, in order, if type_kind is STRUCT.

See more: [google.cloud.bigquery.standard_sql.StandardSqlDataType.struct_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType#google_cloud_bigquery_standard_sql_StandardSqlDataType_struct_type)

### google.cloud.bigquery.standard_sql.StandardSqlDataType.type_kind

The top level type of this field.

See more: [google.cloud.bigquery.standard_sql.StandardSqlDataType.type_kind](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType#google_cloud_bigquery_standard_sql_StandardSqlDataType_type_kind)

### google.cloud.bigquery.standard_sql.StandardSqlField.name

The name of this field.

See more: [google.cloud.bigquery.standard_sql.StandardSqlField.name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlField#google_cloud_bigquery_standard_sql_StandardSqlField_name)

### google.cloud.bigquery.standard_sql.StandardSqlField.type

The type of this parameter.

See more: [google.cloud.bigquery.standard_sql.StandardSqlField.type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlField#google_cloud_bigquery_standard_sql_StandardSqlField_type)

### google.cloud.bigquery.standard_sql.StandardSqlStructType.fields

The fields in this struct.

See more: [google.cloud.bigquery.standard_sql.StandardSqlStructType.fields](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlStructType#google_cloud_bigquery_standard_sql_StandardSqlStructType_fields)

### google.cloud.bigquery.standard_sql.StandardSqlTableType.columns

The columns in this table type.

See more: [google.cloud.bigquery.standard_sql.StandardSqlTableType.columns](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlTableType#google_cloud_bigquery_standard_sql_StandardSqlTableType_columns)

### google.cloud.bigquery.table.BigLakeConfiguration.connection_id

str: The connection specifying the credentials to be used to read and write to external storage, such as Cloud Storage.

See more: [google.cloud.bigquery.table.BigLakeConfiguration.connection_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration#google_cloud_bigquery_table_BigLakeConfiguration_connection_id)

### google.cloud.bigquery.table.BigLakeConfiguration.file_format

str: The file format the table data is stored in.

See more: [google.cloud.bigquery.table.BigLakeConfiguration.file_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration#google_cloud_bigquery_table_BigLakeConfiguration_file_format)

### google.cloud.bigquery.table.BigLakeConfiguration.storage_uri

str: The fully qualified location prefix of the external folder where table data is stored.

See more: [google.cloud.bigquery.table.BigLakeConfiguration.storage_uri](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration#google_cloud_bigquery_table_BigLakeConfiguration_storage_uri)

### google.cloud.bigquery.table.BigLakeConfiguration.table_format

str: The table format the metadata only snapshots are stored in.

See more: [google.cloud.bigquery.table.BigLakeConfiguration.table_format](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration#google_cloud_bigquery_table_BigLakeConfiguration_table_format)

### google.cloud.bigquery.table.PartitionRange.end

int: The end of range partitioning, exclusive.

### google.cloud.bigquery.table.PartitionRange.interval

int: The width of each interval.

See more: [google.cloud.bigquery.table.PartitionRange.interval](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PartitionRange#google_cloud_bigquery_table_PartitionRange_interval)

### google.cloud.bigquery.table.PartitionRange.start

int: The start of range partitioning, inclusive.

### google.cloud.bigquery.table.RangePartitioning.field

str: The table is partitioned by this field.

See more: [google.cloud.bigquery.table.RangePartitioning.field](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning#google_cloud_bigquery_table_RangePartitioning_field)

### google.cloud.bigquery.table.RangePartitioning.range_

[google.cloud.bigquery.table.PartitionRange](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PartitionRange): Defines the
ranges for range partitioning.

See more: [google.cloud.bigquery.table.RangePartitioning.range_](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning#google_cloud_bigquery_table_RangePartitioning_range_)

### google.cloud.bigquery.table.RowIterator.created

If representing query results, the creation time of the associated query.

### google.cloud.bigquery.table.RowIterator.ended

If representing query results, the end time of the associated query.

### google.cloud.bigquery.table.RowIterator.job_id

ID of the query job (if applicable).

### google.cloud.bigquery.table.RowIterator.location

Location where the query executed (if applicable).

### google.cloud.bigquery.table.RowIterator.num_dml_affected_rows

If this RowIterator is the result of a DML query, the number of rows that were affected.

See more: [google.cloud.bigquery.table.RowIterator.num_dml_affected_rows](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RowIterator#google_cloud_bigquery_table_RowIterator_num_dml_affected_rows)

### google.cloud.bigquery.table.RowIterator.project

GCP Project ID where these rows are read from.

### google.cloud.bigquery.table.RowIterator.query

The query text used.

### google.cloud.bigquery.table.RowIterator.query_id

[Preview] ID of a completed query.

### google.cloud.bigquery.table.RowIterator.schema

List[[google.cloud.bigquery.schema.SchemaField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField)]: The subset of
columns to be read from the table.

### google.cloud.bigquery.table.RowIterator.slot_millis

Number of slot ms the user is actually billed for.

See more: [google.cloud.bigquery.table.RowIterator.slot_millis](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RowIterator#google_cloud_bigquery_table_RowIterator_slot_millis)

### google.cloud.bigquery.table.RowIterator.started

If representing query results, the start time of the associated query.

### google.cloud.bigquery.table.RowIterator.total_bytes_processed

total bytes processed from job statistics, if present.

See more: [google.cloud.bigquery.table.RowIterator.total_bytes_processed](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RowIterator#google_cloud_bigquery_table_RowIterator_total_bytes_processed)

### google.cloud.bigquery.table.RowIterator.total_rows

int: The total number of rows in the table or query results.

See more: [google.cloud.bigquery.table.RowIterator.total_rows](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RowIterator#google_cloud_bigquery_table_RowIterator_total_rows)

### google.cloud.bigquery.table.Table.biglake_configuration

[google.cloud.bigquery.table.BigLakeConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration): Configuration
for managed tables for Apache Iceberg.

See more: [google.cloud.bigquery.table.Table.biglake_configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_biglake_configuration)

### google.cloud.bigquery.table.Table.clone_definition

Information about the clone.

See more: [google.cloud.bigquery.table.Table.clone_definition](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_clone_definition)

### google.cloud.bigquery.table.Table.clustering_fields

Union[List[str], None]: Fields defining clustering for the table.

See more: [google.cloud.bigquery.table.Table.clustering_fields](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_clustering_fields)

### google.cloud.bigquery.table.Table.created

Union[datetime.datetime, None]: Datetime at which the table was
created (:data:`None`

until set from the server).

### google.cloud.bigquery.table.Table.description

Union[str, None]: Description of the table (defaults to
:data:`None`

).

### google.cloud.bigquery.table.Table.encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the table.

See more: [google.cloud.bigquery.table.Table.encryption_configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_encryption_configuration)

### google.cloud.bigquery.table.Table.etag

Union[str, None]: ETag for the table resource (:data:`None`

until
set from the server).

See more: [google.cloud.bigquery.table.Table.etag](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_etag)

### google.cloud.bigquery.table.Table.expires

Union[datetime.datetime, None]: Datetime at which the table will be deleted.

### google.cloud.bigquery.table.Table.external_catalog_table_options

Options defining open source compatible datasets living in the BigQuery catalog.

See more: [google.cloud.bigquery.table.Table.external_catalog_table_options](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_external_catalog_table_options)

### google.cloud.bigquery.table.Table.external_data_configuration

Union[google.cloud.bigquery.ExternalConfig, None]: Configuration for
an external data source (defaults to :data:`None`

).

See more: [google.cloud.bigquery.table.Table.external_data_configuration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_external_data_configuration)

### google.cloud.bigquery.table.Table.foreign_type_info

Optional.

See more: [google.cloud.bigquery.table.Table.foreign_type_info](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_foreign_type_info)

### google.cloud.bigquery.table.Table.friendly_name

Union[str, None]: Title of the table (defaults to :data:`None`

).

### google.cloud.bigquery.table.Table.full_table_id

Union[str, None]: ID for the table (:data:`None`

until set from the
server).

### google.cloud.bigquery.table.Table.labels

Dict[str, str]: Labels for the table.

See more: [google.cloud.bigquery.table.Table.labels](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_labels)

### google.cloud.bigquery.table.Table.location

Union[str, None]: Location in which the table is hosted.

### google.cloud.bigquery.table.Table.max_staleness

Union[str, None]: The maximum staleness of data that could be returned when the table is queried.

### google.cloud.bigquery.table.Table.modified

Union[datetime.datetime, None]: Datetime at which the table was last
modified (:data:`None`

until set from the server).

### google.cloud.bigquery.table.Table.mview_allow_non_incremental_definition

Optional[bool]: This option declares the intention to construct a materialized view that isn't refreshed incrementally.

See more: [google.cloud.bigquery.table.Table.mview_allow_non_incremental_definition](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_mview_allow_non_incremental_definition)

### google.cloud.bigquery.table.Table.mview_enable_refresh

Optional[bool]: Enable automatic refresh of the materialized view when the base table is updated.

See more: [google.cloud.bigquery.table.Table.mview_enable_refresh](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_mview_enable_refresh)

### google.cloud.bigquery.table.Table.mview_last_refresh_time

Optional[datetime.datetime]: Datetime at which the materialized view was last
refreshed (:data:`None`

until set from the server).

See more: [google.cloud.bigquery.table.Table.mview_last_refresh_time](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_mview_last_refresh_time)

### google.cloud.bigquery.table.Table.mview_query

Optional[str]: SQL query defining the table as a materialized
view (defaults to :data:`None`

).

### google.cloud.bigquery.table.Table.mview_refresh_interval

Optional[datetime.timedelta]: The maximum frequency at which this materialized view will be refreshed.

See more: [google.cloud.bigquery.table.Table.mview_refresh_interval](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_mview_refresh_interval)

### google.cloud.bigquery.table.Table.num_bytes

Union[int, None]: The size of the table in bytes (:data:`None`

until
set from the server).

### google.cloud.bigquery.table.Table.num_rows

Union[int, None]: The number of rows in the table (:data:`None`

until set from the server).

### google.cloud.bigquery.table.Table.partition_expiration

Union[int, None]: Expiration time in milliseconds for a partition.

See more: [google.cloud.bigquery.table.Table.partition_expiration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_partition_expiration)

### google.cloud.bigquery.table.Table.partitioning_type

Union[str, None]: Time partitioning of the table if it is
partitioned (Defaults to :data:`None`

).

See more: [google.cloud.bigquery.table.Table.partitioning_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_partitioning_type)

### google.cloud.bigquery.table.Table.range_partitioning

Optional[[google.cloud.bigquery.table.RangePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning)]:
Configures range-based partitioning for a table.

See more: [google.cloud.bigquery.table.Table.range_partitioning](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_range_partitioning)

### google.cloud.bigquery.table.Table.reference

A xref_TableReference pointing to this table.

### google.cloud.bigquery.table.Table.require_partition_filter

bool: If set to true, queries over the partitioned table require a partition filter that can be used for partition elimination to be specified.

See more: [google.cloud.bigquery.table.Table.require_partition_filter](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_require_partition_filter)

### google.cloud.bigquery.table.Table.resource_tags

Dict[str, str]: Resource tags for the table.

### google.cloud.bigquery.table.Table.schema

Sequence[Union[ xref_SchemaField, Mapping[str, Any] ]]: Table's schema.

See more: [google.cloud.bigquery.table.Table.schema](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_schema)

### google.cloud.bigquery.table.Table.self_link

Union[str, None]: URL for the table resource (:data:`None`

until set
from the server).

### google.cloud.bigquery.table.Table.snapshot_definition

Information about the snapshot.

See more: [google.cloud.bigquery.table.Table.snapshot_definition](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_snapshot_definition)

### google.cloud.bigquery.table.Table.streaming_buffer

google.cloud.bigquery.StreamingBuffer: Information about a table's streaming buffer.

See more: [google.cloud.bigquery.table.Table.streaming_buffer](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_streaming_buffer)

### google.cloud.bigquery.table.Table.table_constraints

Tables Primary Key and Foreign Key information.

See more: [google.cloud.bigquery.table.Table.table_constraints](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_table_constraints)

### google.cloud.bigquery.table.Table.table_type

Union[str, None]: The type of the table (:data:`None`

until set from
the server).

### google.cloud.bigquery.table.Table.time_partitioning

Optional[[google.cloud.bigquery.table.TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning)]: Configures time-based
partitioning for a table.

See more: [google.cloud.bigquery.table.Table.time_partitioning](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_time_partitioning)

### google.cloud.bigquery.table.Table.view_query

Union[str, None]: SQL query defining the table as a view (defaults
to :data:`None`

).

### google.cloud.bigquery.table.Table.view_use_legacy_sql

bool: Specifies whether to execute the view with Legacy or Standard SQL.

See more: [google.cloud.bigquery.table.Table.view_use_legacy_sql](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table#google_cloud_bigquery_table_Table_view_use_legacy_sql)

### google.cloud.bigquery.table.TableListItem.clustering_fields

Union[List[str], None]: Fields defining clustering for the table.

See more: [google.cloud.bigquery.table.TableListItem.clustering_fields](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_clustering_fields)

### google.cloud.bigquery.table.TableListItem.created

Union[datetime.datetime, None]: Datetime at which the table was
created (:data:`None`

until set from the server).

### google.cloud.bigquery.table.TableListItem.expires

Union[datetime.datetime, None]: Datetime at which the table will be deleted.

### google.cloud.bigquery.table.TableListItem.friendly_name

Union[str, None]: Title of the table (defaults to :data:`None`

).

See more: [google.cloud.bigquery.table.TableListItem.friendly_name](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_friendly_name)

### google.cloud.bigquery.table.TableListItem.full_table_id

Union[str, None]: ID for the table (:data:`None`

until set from the
server).

See more: [google.cloud.bigquery.table.TableListItem.full_table_id](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_full_table_id)

### google.cloud.bigquery.table.TableListItem.labels

Dict[str, str]: Labels for the table.

### google.cloud.bigquery.table.TableListItem.partition_expiration

Union[int, None]: Expiration time in milliseconds for a partition.

See more: [google.cloud.bigquery.table.TableListItem.partition_expiration](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_partition_expiration)

### google.cloud.bigquery.table.TableListItem.partitioning_type

Union[str, None]: Time partitioning of the table if it is
partitioned (Defaults to :data:`None`

).

See more: [google.cloud.bigquery.table.TableListItem.partitioning_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_partitioning_type)

### google.cloud.bigquery.table.TableListItem.reference

A xref_TableReference pointing to this table.

See more: [google.cloud.bigquery.table.TableListItem.reference](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_reference)

### google.cloud.bigquery.table.TableListItem.table_type

Union[str, None]: The type of the table (:data:`None`

until set from
the server).

See more: [google.cloud.bigquery.table.TableListItem.table_type](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_table_type)

### google.cloud.bigquery.table.TableListItem.time_partitioning

[google.cloud.bigquery.table.TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning): Configures time-based
partitioning for a table.

See more: [google.cloud.bigquery.table.TableListItem.time_partitioning](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_time_partitioning)

### google.cloud.bigquery.table.TableListItem.view_use_legacy_sql

bool: Specifies whether to execute the view with Legacy or Standard SQL.

See more: [google.cloud.bigquery.table.TableListItem.view_use_legacy_sql](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem#google_cloud_bigquery_table_TableListItem_view_use_legacy_sql)

### google.cloud.bigquery.table.TimePartitioning.expiration_ms

int: Number of milliseconds to keep the storage for a partition.

See more: [google.cloud.bigquery.table.TimePartitioning.expiration_ms](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning#google_cloud_bigquery_table_TimePartitioning_expiration_ms)

### google.cloud.bigquery.table.TimePartitioning.field

str: Field in the table to use for partitioning.

See more: [google.cloud.bigquery.table.TimePartitioning.field](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning#google_cloud_bigquery_table_TimePartitioning_field)

### google.cloud.bigquery.table.TimePartitioning.require_partition_filter

bool: Specifies whether partition filters are required for queries.

See more: [google.cloud.bigquery.table.TimePartitioning.require_partition_filter](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning#google_cloud_bigquery_table_TimePartitioning_require_partition_filter)

### google.cloud.bigquery.table.TimePartitioning.type_

[google.cloud.bigquery.table.TimePartitioningType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType): The type of time
partitioning to use.

See more: [google.cloud.bigquery.table.TimePartitioning.type_](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning#google_cloud_bigquery_table_TimePartitioning_type_)

### google.cloud.bigquery.table.TimePartitioningType.DAY

Generates one partition per day.

See more: [google.cloud.bigquery.table.TimePartitioningType.DAY](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType#google_cloud_bigquery_table_TimePartitioningType_DAY)

### google.cloud.bigquery.table.TimePartitioningType.HOUR

Generates one partition per hour.

See more: [google.cloud.bigquery.table.TimePartitioningType.HOUR](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType#google_cloud_bigquery_table_TimePartitioningType_HOUR)

### google.cloud.bigquery.table.TimePartitioningType.MONTH

Generates one partition per month.

See more: [google.cloud.bigquery.table.TimePartitioningType.MONTH](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType#google_cloud_bigquery_table_TimePartitioningType_MONTH)

### google.cloud.bigquery.table.TimePartitioningType.YEAR

Generates one partition per year.

See more: [google.cloud.bigquery.table.TimePartitioningType.YEAR](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType#google_cloud_bigquery_table_TimePartitioningType_YEAR)