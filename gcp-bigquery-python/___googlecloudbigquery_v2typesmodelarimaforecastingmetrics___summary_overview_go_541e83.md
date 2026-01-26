---
merged_at: 2026-01-26T23:27:21.522166
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaForecastingMetrics -->

# Class ArimaForecastingMetrics (3.40.0)

`ArimaForecastingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model evaluation metrics for ARIMA forecasting models.

## Attributes |
|
|---|---|
Name |
Description |
`non_seasonal_order` |
`Sequence[`
Non-seasonal order. |
`arima_fitting_metrics` |
`Sequence[`
Arima model fitting metrics. |
`seasonal_periods` |
`Sequence[`
Seasonal periods. Repeated because multiple periods are supported for one time series. |
`has_drift` |
`Sequence[bool]`
Whether Arima model fitted with drift or not. It is always false when d is not 1. |
`time_series_id` |
`Sequence[str]`
Id to differentiate different time series for the large-scale case. |
`arima_single_model_forecasting_metrics` |
`Sequence[`
Repeated as there can be many metric sets (one for each model) in auto-arima and the large-scale case. |

## Classes

### ArimaSingleModelForecastingMetrics

```
ArimaSingleModelForecastingMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Model evaluation metrics for a single ARIMA forecasting model.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/summary_overview -->

# Google Cloud BigQuery API

Overview of the APIs available for Google Cloud BigQuery API.

## All entries

Classes, methods and properties & attributes for Google Cloud BigQuery API.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.StandardSqlTypeNames -->

# Class StandardSqlTypeNames (3.40.0)

`StandardSqlTypeNames(value)`


Enum of allowed SQL type names in schema.SchemaField.

Datatype used in GoogleSQL.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration -->

# Module encryption_configuration (3.40.0)

Define class for the custom encryption configuration.

## Classes

[EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration)

`EncryptionConfiguration(kms_key_name=None)`


Custom encryption configuration (e.g., Cloud KMS keys).

Parameter |
|
|---|---|
Name |
Description |
`kms_key_name` |
`str`
resource ID of Cloud KMS key used for encryption |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry -->

# Class AccessEntry (3.40.0)

```
AccessEntry(
role: typing.Optional[str] = None,
entity_type: typing.Optional[str] = None,
entity_id: typing.Optional[typing.Union[typing.Dict[str, typing.Any], str]] = None,
**kwargs
)
```


Represents grant of an access role to an entity.

An entry must have exactly one of the allowed
xref_EntityTypes. If anything but `view`

, `routine`

,
or `dataset`

are set, a `role`

is also required. `role`

is omitted for `view`

,
`routine`

, `dataset`

, because they are always read-only.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets).

## Parameters |
|
|---|---|
Name |
Description |
`role` |
`typing.Optional[str]`
Role granted to the entity. The following string values are supported: |
`entity_type` |
`typing.Optional[str]`
Type of entity being granted the role. See |
`entity_id` |
`typing.Union[typing.Dict[str, typing.Any], str, NoneType]`
If the |

## Properties

### condition

Optional[Condition]: The IAM condition associated with this entry.

### dataset

API resource representation of a dataset reference.

### dataset_target_types

Which resources that the dataset in this entry applies to.

### domain

A domain to grant access to.

### entity_id

The entity_id of the entry.

### entity_type

The entity_type of the entry.

### group_by_email

An email address of a Google Group to grant access to.

### role

The role of the entry.

### routine

API resource representation of a routine reference.

### special_group

A special group to grant access to.

### user_by_email

An email address of a user to grant access to.

### view

API resource representation of a view reference.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.dataset.AccessEntry`


Factory: construct an access entry given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Access entry resource representation returned from the API |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.dataset.AccessEntry` |
Access entry parsed from `resource` . |

### to_api_repr

`to_api_repr()`


Construct the API resource representation of this access entry

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Access entry represented as an API resource |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameterType -->

# Class StructQueryParameterType (3.40.0)

`StructQueryParameterType(*fields, name=None, description=None)`


Type representation for struct query parameters.

## Parameters |
|
|---|---|
Name |
Description |
`fields` |
`Iterable[Union[ ArrayQueryParameterType, ScalarQueryParameterType, StructQueryParameterType ]]`
An non-empty iterable describing the struct's field types. |
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
`google.cloud.bigquery.query.StructQueryParameterType` |
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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlField -->

# Class StandardSqlField (3.40.0)

`StandardSqlField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A field or a column.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Optional. The name of this field. Can be absent for struct fields. |
`type` |
Optional. The type of this parameter. Absent if not explicitly specified (e.g., CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this "type" field). |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.LabelsEntry -->

# Class LabelsEntry (3.40.0)

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry -->

# Class TimelineEntry (3.40.0)

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

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference -->

# Class ModelReference (3.40.0)

`ModelReference()`


ModelReferences are pointers to models.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference)

## Properties

### dataset_id

str: ID of dataset containing the model.

### model_id

str: The model ID.

### path

URL path for the model's APIs.

### project

str: Project bound to the model

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.model.ModelReference
```


Factory: construct a model reference given its API representation.

### from_string

```
from_string(
model_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.model.ModelReference
```


Construct a model reference from model ID string.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `model_id` is not a fully-qualified table ID in standard SQL format. |

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this model reference.
