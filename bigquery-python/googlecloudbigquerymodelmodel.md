---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.Model
fetched_at: 2026-01-25T02:09:56.638892
---

# Class Model (3.40.0)


      
      Save and categorize content based on your preferences.

```
Model(
model_ref: typing.Optional[
typing.Union[google.cloud.bigquery.model.ModelReference, str]
],
)
```


Model represents a machine learning model resource.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models](https://cloud.google.com/bigquery/docs/reference/rest/v2/models)

## Properties

### best_trial_id

The best trial_id across all training runs.

Read-only.### created

Datetime at which the model was created (:data:`None`

until set from the server).

Read-only.

### dataset_id

ID of dataset containing the model.

### description

Description of the model (defaults to :data:`None`

).

### encryption_configuration

Custom encryption configuration for the model.

Custom encryption configuration (e.g., Cloud KMS keys) or :data:`None`

if using default encryption.

See ```
protecting data with Cloud KMS keys
<
```

_
in the BigQuery documentation.[https://cloud.google.com/bigquery/docs/customer-managed-encryption>](https://cloud.google.com/bigquery/docs/customer-managed-encryption>);

### etag

ETag for the model resource (:data:`None`

until set from the server).

Read-only.

### expires

The datetime when this model expires.

If not present, the model will persist indefinitely. Expired models will be deleted and their storage reclaimed.

### feature_columns

Input feature columns that were used to train this model.

Read-only.

### friendly_name

Title of the table (defaults to :data:`None`

).

### label_columns

Label columns that were used to train this model.

The output of the model will have a `predicted_`

prefix to these columns.

Read-only.

### labels

Labels for the table.

This method always returns a dict. To change a model's labels, modify the dict,
then call `Client.update_model`

. To delete a label, set its value to
:data:`None`

before updating.

### location

The geographic location where the model resides.

This value is inherited from the dataset.

Read-only.

### model_id

The model ID.

### model_type

Type of the model resource.

Read-only.

### modified

Datetime at which the model was last modified (:data:`None`

until set from the server).

Read-only.

### path

URL path for the model's APIs.

### project

Project bound to the model.

### reference

A model reference pointing to this model.

Read-only.

### training_runs

Information for all training runs in increasing order of start time.

Dictionaries are in REST API format. See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#trainingrun](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#trainingrun)

Read-only.

### transform_columns

The input feature columns that were used to train this model. The output transform columns used to train this model.

See REST API:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn)

Read-only.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.model.Model
```


Factory: construct a model resource given its API representation

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this model.