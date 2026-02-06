---
merged_at: 2026-02-06T17:08:52.145598
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types -->

# Package types (3.40.0)

API documentation for `bigquery_v2.types`

package.

## Classes

[DeleteModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.DeleteModelRequest)

[EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.EncryptionConfiguration)

[GetModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.GetModelRequest)

[ListModelsRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsRequest)

[ListModelsResponse](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsResponse)

[Model](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model)

[ModelReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ModelReference)

Id path of a model.

[PatchModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.PatchModelRequest)

[StandardSqlDataType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType)

The type of a variable, e.g., a function argument. Examples: INT64: {type_kind="INT64"} ARRAY: {type_kind="ARRAY", array_element_type="STRING"} STRUCT<x STRING, y ARRAY>: {type_kind="STRUCT", struct_type={fields=[ {name="x", type={type_kind="STRING"}}, {name="y", type={type_kind="ARRAY", array_element_type="DATE"}} ]}}

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[StandardSqlField](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlField)

A field or a column.

[StandardSqlStructType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlStructType)

[StandardSqlTableType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlTableType)

A table type

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Project -->

# Class Project (3.40.0)

`Project(project_id, numeric_id, friendly_name)`


Wrapper for resource describing a BigQuery project.

## Parameters |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Opaque ID of the project |
`numeric_id` |
`int`
Numeric ID of the project |
`friendly_name` |
`str`
Display name of the project |

## Methods

### from_api_repr

`from_api_repr(resource)`


Factory: construct an instance from a resource dict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DataSplitResult -->

# Class DataSplitResult (3.40.0)

`DataSplitResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data split result. This contains references to the training and evaluation data tables that were used to train the model.

## Attributes |
|
|---|---|
Name |
Description |
`training_table` |
Table reference of the training data after split. |
`evaluation_table` |
Table reference of the evaluation data after split. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster -->

# Class Cluster (3.40.0)

`Cluster(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message containing the information about one cluster.

## Attributes |
|
|---|---|
Name |
Description |
`centroid_id` |
`int`
Centroid id. |
`feature_values` |
`Sequence[`
Values of highly variant features for this cluster. |
`count` |
`google.protobuf.wrappers_pb2.Int64Value`
Count of training data rows that were assigned to this cluster. |

## Classes

### FeatureValue

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Representative value of a single feature within the cluster.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameterType -->

# Class ArrayQueryParameterType (3.40.0)

`ArrayQueryParameterType(array_type, *, name=None, description=None)`


Type representation for array query parameters.

## Parameters |
|
|---|---|
Name |
Description |
`array_type` |
`Union[ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

## Methods

### from_api_repr

`from_api_repr(resource)`


Factory: construct parameter type from JSON resource.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON mapping of parameter |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ArrayQueryParameterType` |
Instance |

### to_api_repr

`to_api_repr()`


Construct JSON API representation for the parameter type.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.OptimizationStrategy -->

# Class OptimizationStrategy (3.40.0)

`OptimizationStrategy(value)`


Indicates the optimization strategy used for training.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType.TypeKind -->

# Class TypeKind (3.40.0)

`TypeKind(value)`


API documentation for `bigquery_v2.types.StandardSqlDataType.TypeKind`

class.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.TransactionInfo -->

# Class TransactionInfo (3.40.0)

`TransactionInfo(transaction_id: str)`


[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

.. versionadded:: 2.24.0

## Methods

### TransactionInfo

`TransactionInfo(transaction_id: str)`


Create new instance of TransactionInfo(transaction_id,)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ReservationUsage -->

# Class ReservationUsage (3.40.0)

`ReservationUsage(name, slot_ms)`


Job resource usage for a reservation.

## Methods

### ReservationUsage

`ReservationUsage(name, slot_ms)`


Create new instance of ReservationUsage(name, slot_ms)

### count

`count(value, /)`


Return number of occurrences of value.

### index

`index(value, start=0, stop=9223372036854775807, /)`


Return first index of value.

Raises ValueError if the value is not present.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options -->

# Module format_options (3.40.0)

API documentation for `bigquery.format_options`

module.

## Classes

[AvroOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.AvroOptions)

`AvroOptions()`


Options if source format is set to AVRO.

[ParquetOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions)

`ParquetOptions()`


Additional options if the PARQUET source format is used.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration -->

# Class EncryptionConfiguration (3.40.0)

`EncryptionConfiguration(kms_key_name=None)`


Custom encryption configuration (e.g., Cloud KMS keys).

## Parameter |
|
|---|---|
Name |
Description |
`kms_key_name` |
`str`
resource ID of Cloud KMS key used for encryption |

## Properties

### kms_key_name

str: Resource ID of Cloud KMS key

Resource ID of Cloud KMS key or :data:`None`

if using default
encryption.

## Methods

### from_api_repr

`from_api_repr(resource)`


Construct an encryption configuration from its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
An encryption configuration representation as returned from the API. |

Returns |
|
|---|---|
Type |
Description |
|
An encryption configuration parsed from `resource` . |

### to_api_repr

`to_api_repr()`


Construct the API resource representation of this encryption configuration.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Encryption configuration as represented as an API resource |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset -->

# Class Dataset (3.40.0)

`Dataset(dataset_ref)`


Datasets are containers for tables.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#resource-dataset](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#resource-dataset)

## Parameter |
|
|---|---|
Name |
Description |
`dataset_ref` |
`Union[`
A pointer to a dataset. If |

## Properties

### access_entries

List[[google.cloud.bigquery.dataset.AccessEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry)]: Dataset's access
entries.

`role`

augments the entity type and must be present **unless** the
entity type is `view`

or `routine`

.

Exceptions |
|
|---|---|
Type |
Description |
`TypeError` |
If 'value' is not a sequence |
`ValueError` |
If any item in the sequence is not an
|

### created

Union[datetime.datetime, None]: Output only. Datetime at which the dataset was
created (:data:`None`

until set from the server).

### dataset_id

str: Dataset ID.

### default_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for all tables in the dataset.

Custom encryption configuration (e.g., Cloud KMS keys) or :data:`None`

if using default encryption.

See ```
protecting data with Cloud KMS keys
<
```

_
in the BigQuery documentation.[https://cloud.google.com/bigquery/docs/customer-managed-encryption>](https://cloud.google.com/bigquery/docs/customer-managed-encryption>);

### default_partition_expiration_ms

Optional[int]: The default partition expiration for all partitioned tables in the dataset, in milliseconds.

Once this property is set, all newly-created partitioned tables in
the dataset will have an `time_paritioning.expiration_ms`

property
set to this value, and changing the value will only affect new
tables, not existing ones. The storage in a partition will have an
expiration time of its partition time plus this value.

Setting this property overrides the use of
`default_table_expiration_ms`

for partitioned tables: only one of
`default_table_expiration_ms`

and
`default_partition_expiration_ms`

will be used for any new
partitioned table. If you provide an explicit
`time_partitioning.expiration_ms`

when creating or updating a
partitioned table, that value takes precedence over the default
partition expiration time indicated by this property.

### default_rounding_mode

Union[str, None]: defaultRoundingMode of the dataset as set by the user
(defaults to :data:`None`

).

Set the value to one of `'ROUND_HALF_AWAY_FROM_ZERO'`

, `'ROUND_HALF_EVEN'`

, or
`'ROUNDING_MODE_UNSPECIFIED'`

.

See ```
default rounding mode
<
```

[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#Dataset.FIELDS.default_rounding_mode>](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#Dataset.FIELDS.default_rounding_mode>);*
in REST API docs and updating the default rounding model
<*
guide.

[https://cloud.google.com/bigquery/docs/updating-datasets#update_rounding_mode>](https://cloud.google.com/bigquery/docs/updating-datasets#update_rounding_mode>);

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
for invalid value types. |

### default_table_expiration_ms

Union[int, None]: Default expiration time for tables in the dataset
(defaults to :data:`None`

).

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
For invalid value types. |

### description

Optional[str]: Description of the dataset as set by the user
(defaults to :data:`None`

).

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
for invalid value types. |

### etag

Union[str, None]: Output only. ETag for the dataset resource
(:data:`None`

until set from the server).

### external_catalog_dataset_options

Options defining open source compatible datasets living in the BigQuery catalog. Contains metadata of open source database, schema or namespace represented by the current dataset.

### friendly_name

Union[str, None]: Title of the dataset as set by the user
(defaults to :data:`None`

).

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
for invalid value types. |

### full_dataset_id

Union[str, None]: Output only. ID for the dataset resource
(:data:`None`

until set from the server).

In the format `project_id:dataset_id`

.

### is_case_insensitive

Optional[bool]: True if the dataset and its table names are case-insensitive, otherwise False. By default, this is False, which means the dataset and its table names are case-sensitive. This field does not affect routine references.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
for invalid value types. |

### labels

Dict[str, str]: Labels for the dataset.

This method always returns a dict. To change a dataset's labels,
modify the dict, then call
xref_update_dataset. To delete
a label, set its value to :data:`None`

before updating.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
for invalid value types. |

### location

Union[str, None]: Location in which the dataset is hosted as set by
the user (defaults to :data:`None`

).

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
for invalid value types. |

### max_time_travel_hours

Optional[int]: Defines the time travel window in hours. The value can be from 48 to 168 hours (2 to 7 days), and in multiple of 24 hours (48, 72, 96, 120, 144, 168). The default value is 168 hours if this is not set.

### modified

Union[datetime.datetime, None]: Output only. Datetime at which the dataset was
last modified (:data:`None`

until set from the server).

### path

str: URL path for the dataset based on project and dataset ID.

### project

str: Project ID of the project bound to the dataset.

### reference

[google.cloud.bigquery.dataset.DatasetReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference): A reference to this
dataset.

### resource_tags

Dict[str, str]: Resource tags of the dataset.

Optional. The tags attached to this dataset. Tag keys are globally unique. Tag key is expected to be in the namespaced format, for example "123456789012/environment" where 123456789012 is the ID of the parent organization or project resource for this tag key. Tag value is expected to be the short name, for example "Production".

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
for invalid value types. |

### self_link

Union[str, None]: Output only. URL for the dataset resource
(:data:`None`

until set from the server).

### storage_billing_model

Union[str, None]: StorageBillingModel of the dataset as set by the user
(defaults to :data:`None`

).

Set the value to one of `'LOGICAL'`

, `'PHYSICAL'`

, or
`'STORAGE_BILLING_MODEL_UNSPECIFIED'`

. This change takes 24 hours to
take effect and you must wait 14 days before you can change the storage
billing model again.

See ```
storage billing model
<
```

[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#Dataset.FIELDS.storage_billing_model>](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#Dataset.FIELDS.storage_billing_model>);*
in REST API docs and updating the storage billing model
<*
guide.

[https://cloud.google.com/bigquery/docs/updating-datasets#update_storage_billing_models>](https://cloud.google.com/bigquery/docs/updating-datasets#update_storage_billing_models>);

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
for invalid value types. |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.dataset.Dataset`


Factory: construct a dataset given its API representation

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.dataset.Dataset` |
Dataset parsed from `resource` . |

### from_string

`from_string(full_dataset_id: str) -> google.cloud.bigquery.dataset.Dataset`


Construct a dataset from fully-qualified dataset ID.

Parameter |
|
|---|---|
Name |
Description |
`full_dataset_id` |
`str`
A fully-qualified dataset ID in standard SQL format. Must include both the project ID and the dataset ID, separated by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `full_dataset_id` is not a fully-qualified dataset ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`Dataset .. rubric:: Examples >>> Dataset.from_string('my-project-id.some_dataset') Dataset(DatasetReference('my-project-id', 'some_dataset'))` |
Dataset parsed from `full_dataset_id` . |

### model

`model(model_id)`


Constructs a ModelReference.

Parameter |
|
|---|---|
Name |
Description |
`model_id` |
`str`
the ID of the model. |

Returns |
|
|---|---|
Type |
Description |
|
A ModelReference for a model in this dataset. |

### routine

`routine(routine_id)`


Constructs a RoutineReference.

Parameter |
|
|---|---|
Name |
Description |
`routine_id` |
`str`
the ID of the routine. |

Returns |
|
|---|---|
Type |
Description |
|
A RoutineReference for a routine in this dataset. |

### table

`table(table_id: str) -> google.cloud.bigquery.table.TableReference`


Constructs a TableReference.

Parameter |
|
|---|---|
Name |
Description |
`table_id` |
`str`
The ID of the table. |

Returns |
|
|---|---|
Type |
Description |
|
A table reference for a table in this dataset. |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this dataset

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
The dataset represented as an API resource |
