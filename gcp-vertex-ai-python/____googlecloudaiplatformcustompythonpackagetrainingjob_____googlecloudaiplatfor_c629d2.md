---
merged_at: 2026-01-28T15:11:44.732957
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob -->

# Class CustomPythonPackageTrainingJob (1.134.0)

```
CustomPythonPackageTrainingJob(
display_name: str,
python_package_gcs_uri: typing.Union[str, typing.List[str]],
python_module_name: str,
container_uri: str,
model_serving_container_image_uri: typing.Optional[str] = None,
model_serving_container_predict_route: typing.Optional[str] = None,
model_serving_container_health_route: typing.Optional[str] = None,
model_serving_container_command: typing.Optional[typing.Sequence[str]] = None,
model_serving_container_args: typing.Optional[typing.Sequence[str]] = None,
model_serving_container_environment_variables: typing.Optional[
typing.Dict[str, str]
] = None,
model_serving_container_ports: typing.Optional[typing.Sequence[int]] = None,
model_description: typing.Optional[str] = None,
model_instance_schema_uri: typing.Optional[str] = None,
model_parameters_schema_uri: typing.Optional[str] = None,
model_prediction_schema_uri: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
)
```


Class to launch a Custom Training Job in Vertex AI using a Python Package.

Use the `CustomPythonPackageTrainingJob`

class to use a Python package to
launch a custom training pipeline in Vertex AI. For an example of how to use
the `CustomPythonPackageTrainingJob`

class, see the tutorial in the [Custom
training using Python package, managed text dataset, and TensorFlow serving
container](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/sdk/SDK_Custom_Training_Python_Package_Managed_Text_Dataset_Tensorflow_Serving_Container.ipynb)
notebook.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Optional. The time when the training job entered the
`PIPELINE_STATE_SUCCEEDED`

, `PIPELINE_STATE_FAILED`

, or
`PIPELINE_STATE_CANCELLED`

state.

### error

Optional. Detailed error information for this training job resource.
Error information is created only when the state of the training job is
`PIPELINE_STATE_FAILED`

or `PIPELINE_STATE_CANCELLED`

.

### gca_resource

The underlying resource proto representation.

### has_failed

Returns `true`

if the training job failed, otherwise `false`

.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### network

The full name of the Google Compute Engine
[network](https://cloud.google.com/vpc/docs/vpc#networks) to which this
`CustomTrainingJob`

should be peered.

Specify the name of the network using the format
`projects/{project}/global/networks/{network}`

. Replace {project} with
the project number, such as `12345`

, and {network} with a network name.

Before specifying a network, private services access must be configured for the network. If private services access isn't configured, then the custom training job can't be peered with a network.

### resource_name

Full qualified resource name.

### start_time

Optional. The time when the training job first entered the
`PIPELINE_STATE_RUNNING`

state.

### state

Current training state.

### update_time

Time this resource was last updated.

### web_access_uris

Returns the URIs used to access the custom training job.

## Methods

### CustomPythonPackageTrainingJob

```
CustomPythonPackageTrainingJob(
display_name: str,
python_package_gcs_uri: typing.Union[str, typing.List[str]],
python_module_name: str,
container_uri: str,
model_serving_container_image_uri: typing.Optional[str] = None,
model_serving_container_predict_route: typing.Optional[str] = None,
model_serving_container_health_route: typing.Optional[str] = None,
model_serving_container_command: typing.Optional[typing.Sequence[str]] = None,
model_serving_container_args: typing.Optional[typing.Sequence[str]] = None,
model_serving_container_environment_variables: typing.Optional[
typing.Dict[str, str]
] = None,
model_serving_container_ports: typing.Optional[typing.Sequence[int]] = None,
model_description: typing.Optional[str] = None,
model_instance_schema_uri: typing.Optional[str] = None,
model_parameters_schema_uri: typing.Optional[str] = None,
model_prediction_schema_uri: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
)
```


Constructs a Custom Training Job from a Python Package.

A class to launch a custom training job in Vertex AI using a Python Package.

Use the `CustomPythonPackageTrainingJob`

class to use a Python package
to launch a custom training pipeline in Vertex AI. For an example of how
to use the `CustomPythonPackageTrainingJob`

class, see the tutorial in
the [Custom training using Python package, managed text dataset, and
TensorFlow serving
container](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/sdk/SDK_Custom_Training_Python_Package_Managed_Text_Dataset_Tensorflow_Serving_Container.ipynb)
notebook.

job = aiplatform.CustomPythonPackageTrainingJob( display_name='test-train', python_package_gcs_uri='gs://my-bucket/my-python-package.tar.gz', python_module_name='my-training-python-package.task', container_uri='gcr.io/cloud-aiplatform/training/tf-cpu.2-2:latest', model_serving_container_image_uri='gcr.io/my-trainer/serving:1', model_serving_container_predict_route='predict', model_serving_container_health_route='metadata, labels={'key': 'value'}, )

Usage with Dataset:

```
ds = aiplatform.TabularDataset(
'projects/my-project/locations/us-central1/datasets/12345'
)
job.run(
ds,
replica_count=1,
model_display_name='my-trained-model',
model_labels={'key': 'value'},
)
```


Usage without Dataset:

```
job.run(
replica_count=1,
model_display_name='my-trained-model',
model_labels={'key': 'value'},
)
```


To ensure your model gets saved in Vertex AI, write your saved model to os.environ["AIP_MODEL_DIR"] in your provided training script.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of this TrainingPipeline. |
`python_package_gcs_uri` |
`Union[str, List[str]]`
Required. GCS location of the training python package. Could be a string for single package or a list of string for multiple packages. |
`python_module_name` |
`str`
Required. The module name of the training python package. |
`container_uri` |
`str`
Required. Uri of the training container image in the GCR. |
`model_serving_container_image_uri` |
`str`
Optional. If the training produces a managed Vertex AI Model, the URI of the model serving container suitable for serving the model produced by the training script. |
`model_serving_container_predict_route` |
`str`
Optional. If the training produces a managed Vertex AI Model, an HTTP path to send prediction requests to the container, and which must be supported by it. If not specified a default HTTP path will be used by Vertex AI. |
`model_serving_container_health_route` |
`str`
Optional. If the training produces a managed Vertex AI Model, an HTTP path to send health check requests to the container, and which must be supported by it. If not specified a standard HTTP path will be used by AI Platform. |
`model_serving_container_command` |
`Sequence[str]`
Optional. The command with which the container is run. Not executed within a shell. The Docker image's ENTRYPOINT is used if this is not provided. Variable references $(VAR_NAME) are expanded using the container's environment. If a variable cannot be resolved, the reference in the input string will be unchanged. The $(VAR_NAME) syntax can be escaped with a double $$, ie: $$(VAR_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not. |
`model_serving_container_args` |
`Sequence[str]`
Optional. The arguments to the command. The Docker image's CMD is used if this is not provided. Variable references $(VAR_NAME) are expanded using the container's environment. If a variable cannot be resolved, the reference in the input string will be unchanged. The $(VAR_NAME) syntax can be escaped with a double $$, ie: $$(VAR_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not. |
`model_serving_container_environment_variables` |
`Dict[str, str]`
Optional. The environment variables that are to be present in the container. Should be a dictionary where keys are environment variable names and values are environment variable values for those names. |
`model_serving_container_ports` |
`Sequence[int]`
Optional. Declaration of ports that are exposed by the container. This field is primarily informational, it gives Vertex AI information about the network connections the container uses. Listing or not a port here has no impact on whether the port is actually exposed, any port listening on the default "0.0.0.0" address inside a container will be accessible from the network. |
`model_description` |
`str`
Optional. The description of the Model. |
`model_instance_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in |
`model_parameters_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via |
`model_prediction_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via |
`explanation_metadata` |
`explain.ExplanationMetadata`
Optional. Metadata describing the Model's input and output for explanation. |
`explanation_parameters` |
`explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. For more details, see |
`project` |
`str`
Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`staging_bucket` |
`str`
Optional. Bucket used to stage source and training artifacts. Overrides staging_bucket set in aiplatform.init. |

### cancel

`cancel() -> None`


Asynchronously attempts to cancel a training job.

The server makes a best effort to cancel the job, but the training job
can't always be cancelled. If the training job is canceled, its state
transitions to `CANCELLED`

and it's not deleted.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If this training job isn't running, then a runtime error is raised. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.training_jobs._TrainingJob
```


Gets a training job using the `resource_name`

that's passed in.

Parameters |
|
|---|---|
Name |
Description |
`resource_name` |
`str`
Required. A fully-qualified resource name or ID. |
`project` |
`str`
Optional. The name of the Google Cloud project to retrieve the training job from. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job is retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload this model. These credentials override the credentials set by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A `ValueError` is raised if the task definition of the retrieved training job doesn't match the custom training task definition. |

### get_model

`get_model(sync=True) -> google.cloud.aiplatform.models.Model`


Returns the Vertex AI model produced by this training job.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
If set to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
A runtime error is raised if the training job failed or if a model wasn't produced by the training job. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


Lists all instances of this training job resource.

The following shows an example of how to call `CustomTrainingJob.list`

:

```
aiplatform.CustomTrainingJob.list(
filter='display_name="experiment_a27"',
order_by='create_time desc'
)
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names, snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields used to sort the returned traing job resources. The defauilt sorting order is ascending. To sort by a field name in descending order, use |
`project` |
`str`
Optional. The name of the Google Cloud project to which to retrieve the list of training job resources. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job resources are retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to retrieve list. These credentials override the credentials set by |

Returns |
|
|---|---|
Type |
Description |
`List[VertexAiResourceNoun]` |
A list of training job resources. |

### run

```
run(
dataset: typing.Optional[
typing.Union[
google.cloud.aiplatform.datasets.image_dataset.ImageDataset,
google.cloud.aiplatform.datasets.tabular_dataset.TabularDataset,
google.cloud.aiplatform.datasets.text_dataset.TextDataset,
google.cloud.aiplatform.datasets.video_dataset.VideoDataset,
]
] = None,
annotation_schema_uri: typing.Optional[str] = None,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
base_output_dir: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
bigquery_destination: typing.Optional[str] = None,
args: typing.Optional[typing.List[typing.Union[str, float, int]]] = None,
environment_variables: typing.Optional[typing.Dict[str, str]] = None,
replica_count: int = 1,
machine_type: str = "n1-standard-4",
accelerator_type: str = "ACCELERATOR_TYPE_UNSPECIFIED",
accelerator_count: int = 0,
boot_disk_type: str = "pd-ssd",
boot_disk_size_gb: int = 100,
reduction_server_replica_count: int = 0,
reduction_server_machine_type: typing.Optional[str] = None,
reduction_server_container_uri: typing.Optional[str] = None,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
training_filter_split: typing.Optional[str] = None,
validation_filter_split: typing.Optional[str] = None,
test_filter_split: typing.Optional[str] = None,
predefined_split_column_name: typing.Optional[str] = None,
timestamp_split_column_name: typing.Optional[str] = None,
timeout: typing.Optional[int] = None,
restart_job_on_worker_restart: bool = False,
enable_web_access: bool = False,
enable_dashboard_access: bool = False,
tensorboard: typing.Optional[str] = None,
sync=True,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
persistent_resource_id: typing.Optional[str] = None,
tpu_topology: typing.Optional[str] = None,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
reservation_affinity_type: typing.Optional[
typing.Literal["NO_RESERVATION", "ANY_RESERVATION", "SPECIFIC_RESERVATION"]
] = None,
reservation_affinity_key: typing.Optional[str] = None,
reservation_affinity_values: typing.Optional[typing.List[str]] = None,
max_wait_duration: typing.Optional[int] = None,
psc_interface_config: typing.Optional[
google.cloud.aiplatform_v1.types.service_networking.PscInterfaceConfig
] = None,
) -> typing.Optional[google.cloud.aiplatform.models.Model]
```


Runs the custom training job.

Distributed Training Support: If replica count = 1 then one chief replica will be provisioned. If replica_count > 1 the remainder will be provisioned as a worker replica pool. ie: replica_count = 10 will result in 1 chief and 9 workers All replicas have same machine_type, accelerator_type, and accelerator_count

If training on a Vertex AI dataset, you can use one of the following split configurations:
Data fraction splits:
Any of `training_fraction_split`

, `validation_fraction_split`

and
`test_fraction_split`

may optionally be provided, they must sum to up to 1. If
the provided ones sum to less than 1, the remainder is assigned to sets as
decided by Vertex AI. If none of the fractions are set, by default roughly 80%
of data will be used for training, 10% for validation, and 10% for test.

```
Data filter splits:
Assigns input data to training, validation, and test sets
based on the given filters, data pieces not matched by any
filter are ignored. Currently only supported for Datasets
containing DataItems.
If any of the filters in this message are to match nothing, then
they can be set as '-' (the minus sign).
If using filter splits, all of `training_filter_split`, `validation_filter_split` and
`test_filter_split` must be provided.
Supported only for unstructured Datasets.
Predefined splits:
Assigns input data to training, validation, and test sets based on the value of a provided key.
If using predefined splits, `predefined_split_column_name` must be provided.
Supported only for tabular Datasets.
Timestamp splits:
Assigns input data to training, validation, and test sets
based on a provided timestamps. The youngest data pieces are
assigned to training set, next to validation set, and the oldest
to the test set.
Supported only for tabular Datasets.
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`Union[datasets.ImageDataset,datasets.TabularDataset,datasets.TextDataset,datasets.VideoDataset,]`
Vertex AI to fit this training against. Custom training script should retrieve datasets through passed in environment variables uris: os.environ["AIP_TRAINING_DATA_URI"] os.environ["AIP_VALIDATION_DATA_URI"] os.environ["AIP_TEST_DATA_URI"] Additionally the dataset format is passed in as: os.environ["AIP_DATA_FORMAT"] |
`annotation_schema_uri` |
`str`
Google Cloud Storage URI points to a YAML file describing annotation schema. The schema is defined as an OpenAPI 3.0.2 |
`model_display_name` |
`str`
If the script produces a managed Vertex AI Model. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
`model_labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`model_id` |
`str`
Optional. The ID to use for the Model produced by this job, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model. The new model uploaded by this job will be a version of |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of the model produced by this job without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the model version produced by this job will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`model_version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that the model version uploaded by this job can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`model_version_description` |
`str`
Optional. The description of the model version being uploaded by this job. |
`base_output_dir` |
`str`
GCS output directory of job. If not provided a timestamped directory in the staging directory will be used. Vertex AI sets the following environment variables when it runs your training code: - AIP_MODEL_DIR: a Cloud Storage URI of a directory intended for saving model artifacts, i.e. <base_output_dir>/model/ - AIP_CHECKPOINT_DIR: a Cloud Storage URI of a directory intended for saving checkpoints, i.e. <base_output_dir>/checkpoints/ - AIP_TENSORBOARD_LOG_DIR: a Cloud Storage URI of a directory intended for saving TensorBoard logs, i.e. <base_output_dir>/logs/ |
`service_account` |
`str`
Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. If not specified, uses the service account set in aiplatform.init. |
`network` |
`str`
The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. If left unspecified, the network set in aiplatform.init will be used. Otherwise, the job is not peered with any network. |
`bigquery_destination` |
`str`
Provide this field if |
`args` |
`List[Unions[str, int, float]]`
Command line arguments to be passed to the Python script. |
`environment_variables` |
`Dict[str, str]`
Environment variables to be passed to the container. Should be a dictionary where keys are environment variable names and values are environment variable values for those names. At most 10 environment variables can be specified. The Name of the environment variable must be unique. environment_variables = { 'MY_KEY': 'MY_VALUE' } |
`replica_count` |
`int`
The number of worker replicas. If replica count = 1 then one chief replica will be provisioned. If replica_count > 1 the remainder will be provisioned as a worker replica pool. |
`machine_type` |
`str`
The type of machine to use for training. |
`accelerator_type` |
`str`
Hardware accelerator type. One of ACCELERATOR_TYPE_UNSPECIFIED, NVIDIA_TESLA_K80, NVIDIA_TESLA_P100, NVIDIA_TESLA_V100, NVIDIA_TESLA_P4, NVIDIA_TESLA_T4 |
`accelerator_count` |
`int`
The number of accelerators to attach to a worker replica. |
`boot_disk_type` |
`str`
Type of the boot disk, default is |
`boot_disk_size_gb` |
`int`
Size in GB of the boot disk, default is 100GB. boot disk size must be within the range of [100, 64000]. |
`reduction_server_replica_count` |
`int`
The number of reduction server replicas, default is 0. |
`reduction_server_machine_type` |
`str`
Optional. The type of machine to use for reduction server. |
`reduction_server_container_uri` |
`str`
Optional. The Uri of the reduction server container image. See details: |
`training_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to train the Model. This is ignored if Dataset is not provided. |
`validation_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to validate the Model. This is ignored if Dataset is not provided. |
`test_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to evaluate the Model. This is ignored if Dataset is not provided. |
`training_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to train the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`validation_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to validate the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`test_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to test the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`predefined_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { |
`timestamp_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key values of the key (the values in the column) must be in RFC 3339 |
`timeout` |
`int`
The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
`enable_dashboard_access` |
`bool`
Whether you want Vertex AI to enable access to the customized dashboard to training containers. |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`disable_retries` |
`bool`
Indicates if the job should retry for internal errors after the job starts running. If True, overrides |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`tpu_topology` |
`str`
Optional. Specifies the tpu topology to be used for TPU training job. This field is required for TPU v5 versions. For details on the TPU topology, refer to |
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`reservation_affinity_type` |
`str`
Optional. The type of reservation affinity. One of: * "NO_RESERVATION" : No reservation is used. * "ANY_RESERVATION" : Any reservation that matches machine spec can be used. * "SPECIFIC_RESERVATION" : A specific reservation must be use used. See reservation_affinity_key and reservation_affinity_values for how to specify the reservation. |
`reservation_affinity_key` |
`str`
Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use |
`reservation_affinity_values` |
`List[str]`
Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation. Format: 'projects/{project_id_or_number}/zones/{zone}/reservations/{reservation_name}' |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 30 minutes. |
`psc_interface_config` |
`gca_service_networking.PscInterfaceConfig`
Optional. Configuration for Private Service Connect interface used for training. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource or None if training did not produce a Vertex AI Model. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until the resource has been created.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult.Frame -->

# Class Frame (1.134.0)

`Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.

## Attributes |
|
|---|---|
Name |
Description |
`time_offset` |
`google.protobuf.duration_pb2.Duration`
A time (frame) of a video in which the object has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. |
`x_min` |
`google.protobuf.wrappers_pb2.FloatValue`
The leftmost coordinate of the bounding box. |
`x_max` |
`google.protobuf.wrappers_pb2.FloatValue`
The rightmost coordinate of the bounding box. |
`y_min` |
`google.protobuf.wrappers_pb2.FloatValue`
The topmost coordinate of the bounding box. |
`y_max` |
`google.protobuf.wrappers_pb2.FloatValue`
The bottommost coordinate of the bounding box. |

## Methods

### Frame

`Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.

### Frame

`Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchMigrateResourcesRequest -->

# Class BatchMigrateResourcesRequest (1.134.0)

```
BatchMigrateResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MigrationService.BatchMigrateResources.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location of the migrated resource will live in. Format: `projects/{project}/locations/{location}`
|
`migrate_resource_requests` |
`MutableSequence[`
Required. The request messages specifying the resources to migrate. They must be in the same location as the destination. Up to 50 resources can be migrated in one batch. |

## Methods

### BatchMigrateResourcesRequest

```
BatchMigrateResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MigrationService.BatchMigrateResources.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ManualBatchTuningParameters -->

# Class ManualBatchTuningParameters (1.134.0)

`ManualBatchTuningParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Manual batch tuning parameters.

## Attribute |
|
|---|---|
Name |
Description |
`batch_size` |
`int`
Immutable. The number of the records (e.g. instances) of the operation given in each batch to a machine replica. Machine type, and size of a single record should be considered when setting this parameter, higher value speeds up the batch operation's execution, but too high value will result in a whole batch not fitting in a machine's memory, and the whole operation will fail. The default value is 64. |

## Methods

### ManualBatchTuningParameters

`ManualBatchTuningParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Manual batch tuning parameters.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse -->

# Class SearchMigratableResourcesResponse (1.134.0)

```
SearchMigratableResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MigrationService.SearchMigratableResources.

## Attributes |
|
|---|---|
Name |
Description |
`migratable_resources` |
`MutableSequence[`
All migratable resources that can be migrated to the location specified in the request. |
`next_page_token` |
`str`
The standard next-page token. The migratable_resources may not fill page_size in SearchMigratableResourcesRequest even when there are subsequent pages. |

## Methods

### SearchMigratableResourcesResponse

```
SearchMigratableResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MigrationService.SearchMigratableResources.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model.ExportFormat -->

# Class ExportFormat (1.134.0)

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Output only. The ID of the export format. The possible format IDs are: - `tflite` Used for Android mobile devices.
- `edgetpu-tflite` Used for `Edge
TPU |
`exportable_contents` |
`MutableSequence[`
Output only. The content of this Model that may be exported. |

## Classes

### ExportableContent

`ExportableContent(value)`


The Model content that can be exported.

## Methods

### ExportFormat

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest.SimpleRetrievalParams -->

# Class SimpleRetrievalParams (1.134.0)

`SimpleRetrievalParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for simple (non-similarity search) retrieval.

## Attributes |
|
|---|---|
Name |
Description |
`page_size` |
`int`
Optional. The maximum number of memories to return. The service may return fewer than this value. If unspecified, at most 3 memories will be returned. The maximum value is 100; values above 100 will be coerced to 100. |
`page_token` |
`str`
Optional. A page token, received from a previous `RetrieveMemories` call. Provide this to retrieve the
subsequent page.
|

## Methods

### SimpleRetrievalParams

`SimpleRetrievalParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for simple (non-similarity search) retrieval.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNotebookExecutionJobRequest -->

# Class CreateNotebookExecutionJobRequest (1.134.0)

```
CreateNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.CreateNotebookExecutionJob]

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the NotebookExecutionJob. Format: `projects/{project}/locations/{location}`
|
`notebook_execution_job` |
Required. The NotebookExecutionJob to create. |
`notebook_execution_job_id` |
`str`
Optional. User specified ID for the NotebookExecutionJob. |

## Methods

### CreateNotebookExecutionJobRequest

```
CreateNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.CreateNotebookExecutionJob]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectRawPredictRequest -->

# Class DirectRawPredictRequest (1.134.0)

`DirectRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.DirectRawPredict.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform predictions. Format: `/namespace.Service/Method/` Example:
`/tensorflow.serving.PredictionService/Predict`
|
`input` |
`bytes`
The prediction input. |

## Methods

### DirectRawPredictRequest

`DirectRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.DirectRawPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AcceptPublisherModelEulaRequest -->

# Class AcceptPublisherModelEulaRequest (1.134.0)

```
AcceptPublisherModelEulaRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelGardenService.AcceptPublisherModelEula.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The project requesting access for named model. The format is `projects/{project}` .
|
`publisher_model` |
`str`
Required. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisher_model}` , or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}`
|

## Methods

### AcceptPublisherModelEulaRequest

```
AcceptPublisherModelEulaRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelGardenService.AcceptPublisherModelEula.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs -->

# Class AutoMlImageObjectDetectionInputs (1.134.0)

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`budget_milli_node_hours` |
`int`
The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node_hour = actual_hour \*
number_of_nodes_involved. For modelType
`cloud` \ (default), the budget must be between 20,000 and
900,000 milli node hours, inclusive. The default value is
216,000 which represents one day in wall time, considering 9
nodes are used. For model types `mobile-tf-low-latency-1` ,
`mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` the
training budget must be between 1,000 and 100,000 milli node
hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.
|
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Object Detection might stop training before the entire training budget has been used. |

## Classes

### ModelType

`ModelType(value)`


## Methods

### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AggregationResult -->

# Class AggregationResult (1.134.0)

`AggregationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The aggregation result for a single metric.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`pointwise_metric_result` |
Result for pointwise metric. This field is a member of `oneof` _ `aggregation_result` .
|
`pairwise_metric_result` |
Result for pairwise metric. This field is a member of `oneof` _ `aggregation_result` .
|
`exact_match_metric_value` |
Results for exact match metric. This field is a member of `oneof` _ `aggregation_result` .
|
`bleu_metric_value` |
Results for bleu metric. This field is a member of `oneof` _ `aggregation_result` .
|
`rouge_metric_value` |
Results for rouge metric. This field is a member of `oneof` _ `aggregation_result` .
|
`aggregation_metric` |
Aggregation metric. |

## Methods

### AggregationResult

`AggregationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The aggregation result for a single metric.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseMetricInstance -->

# Class PairwiseMetricInstance (1.134.0)

`PairwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pairwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`json_instance` |
`str`
Instance specified as a json string. String key-value pairs are expected in the json_instance to render PairwiseMetricSpec.instance_prompt_template. This field is a member of `oneof` _ `instance` .
|
`content_map_instance` |
Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content. This field is a member of `oneof` _ `instance` .
|

## Methods

### PairwiseMetricInstance

`PairwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pairwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportEvaluatedAnnotationsRequest -->

# Class BatchImportEvaluatedAnnotationsRequest (1.134.0)

```
BatchImportEvaluatedAnnotationsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.BatchImportEvaluatedAnnotations

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the parent ModelEvaluationSlice resource. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}/slices/{slice}`
|
`evaluated_annotations` |
`MutableSequence[`
Required. Evaluated annotations resource to be imported. |

## Methods

### BatchImportEvaluatedAnnotationsRequest

```
BatchImportEvaluatedAnnotationsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.BatchImportEvaluatedAnnotations

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchDeletePipelineJobsRequest -->

# Class BatchDeletePipelineJobsRequest (1.134.0)

```
BatchDeletePipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchDeletePipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: `projects/{project}/locations/{location}`
|
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}`
|

## Methods

### BatchDeletePipelineJobsRequest

```
BatchDeletePipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchDeletePipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpecialistPool -->

# Class SpecialistPool (1.134.0)

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the SpecialistPool. |
`display_name` |
`str`
Required. The user-defined name of the SpecialistPool. The name can be up to 128 characters long and can consist of any UTF-8 characters. This field should be unique on project-level. |
`specialist_managers_count` |
`int`
Output only. The number of managers in this SpecialistPool. |
`specialist_manager_emails` |
`MutableSequence[str]`
The email addresses of the managers in the SpecialistPool. |
`pending_data_labeling_jobs` |
`MutableSequence[str]`
Output only. The resource name of the pending data labeling jobs. |
`specialist_worker_emails` |
`MutableSequence[str]`
The email addresses of workers in the SpecialistPool. |

## Methods

### SpecialistPool

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesRequest -->

# Class BatchMigrateResourcesRequest (1.134.0)

```
BatchMigrateResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MigrationService.BatchMigrateResources.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location of the migrated resource will live in. Format: `projects/{project}/locations/{location}`
|
`migrate_resource_requests` |
`MutableSequence[`
Required. The request messages specifying the resources to migrate. They must be in the same location as the destination. Up to 50 resources can be migrated in one batch. |

## Methods

### BatchMigrateResourcesRequest

```
BatchMigrateResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MigrationService.BatchMigrateResources.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborQuery.NumericFilter.Operator -->

# Class Operator (1.134.0)

`Operator(value)`


Datapoints for which Operator is true relative to the query’s Value field will be allowlisted.

## Enums |
|
|---|---|
Name |
Description |
`OPERATOR_UNSPECIFIED` |
Unspecified operator. |
`LESS` |
Entities are eligible if their value is < the=""> |
`LESS_EQUAL` |
Entities are eligible if their value is <= the=""> |
`EQUAL` |
Entities are eligible if their value is == the query's. |
`GREATER_EQUAL` |
Entities are eligible if their value is >= the query's. |
`GREATER` |
Entities are eligible if their value is > the query's. |
`NOT_EQUAL` |
Entities are eligible if their value is != the query's. |

## Methods

### Operator

`Operator(value)`


Datapoints for which Operator is true relative to the query’s Value field will be allowlisted.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCancelPipelineJobsRequest -->

# Class BatchCancelPipelineJobsRequest (1.134.0)

```
BatchCancelPipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchCancelPipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: `projects/{project}/locations/{location}`
|
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}`
|

## Methods

### BatchCancelPipelineJobsRequest

```
BatchCancelPipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchCancelPipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureNoiseSigma.NoiseSigmaForFeature -->

# Class NoiseSigmaForFeature (1.134.0)

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The name of the input feature for which noise sigma is provided. The features are defined in [explanation metadata inputs][google.cloud.aiplatform.v1.ExplanationMetadata.inputs]. |
`sigma` |
`float`
This represents the standard deviation of the Gaussian kernel that will be used to add noise to the feature prior to computing gradients. Similar to noise_sigma but represents the noise added to the current feature. Defaults to 0.1. |

## Methods

### NoiseSigmaForFeature

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookExecutionJobRequest -->

# Class CreateNotebookExecutionJobRequest (1.134.0)

```
CreateNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.CreateNotebookExecutionJob]

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the NotebookExecutionJob. Format: `projects/{project}/locations/{location}`
|
`notebook_execution_job` |
Required. The NotebookExecutionJob to create. |
`notebook_execution_job_id` |
`str`
Optional. User specified ID for the NotebookExecutionJob. |

## Methods

### CreateNotebookExecutionJobRequest

```
CreateNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.CreateNotebookExecutionJob]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.ExportFormat -->

# Class ExportFormat (1.134.0)

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Output only. The ID of the export format. The possible format IDs are: - `tflite` Used for Android mobile devices.
- `edgetpu-tflite` Used for `Edge
TPU |
`exportable_contents` |
`MutableSequence[`
Output only. The content of this Model that may be exported. |

## Classes

### ExportableContent

`ExportableContent(value)`


The Model content that can be exported.

## Methods

### ExportFormat

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs.ModelType -->

# Class ModelType (1.134.0)

A model best tailored to be used within Google Cloud, and which cannot be exported. Expected to have a higher latency, but should also have a higher prediction quality than other cloud models.

CLOUD_LOW_LATENCY_1

A model best tailored to be used within Google Cloud, and which cannot be exported. Expected to have a low latency, but may have lower prediction quality than other cloud models.

MOBILE_TF_LOW_LATENCY_1

A model that, in addition to being available within Google Cloud can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

MOBILE_TF_VERSATILE_1

A model that, in addition to being available within Google Cloud can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards.

MOBILE_TF_HIGH_ACCURACY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards. Expected to have a higher latency, but should also have a higher prediction quality than other mobile models.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpecialistPool -->

# Class SpecialistPool (1.134.0)

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the SpecialistPool. |
`display_name` |
`str`
Required. The user-defined name of the SpecialistPool. The name can be up to 128 characters long and can consist of any UTF-8 characters. This field should be unique on project-level. |
`specialist_managers_count` |
`int`
Output only. The number of managers in this SpecialistPool. |
`specialist_manager_emails` |
`MutableSequence[str]`
The email addresses of the managers in the SpecialistPool. |
`pending_data_labeling_jobs` |
`MutableSequence[str]`
Output only. The resource name of the pending data labeling jobs. |
`specialist_worker_emails` |
`MutableSequence[str]`
The email addresses of workers in the SpecialistPool. |

## Methods

### SpecialistPool

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionInputs -->

# Class AutoMlImageObjectDetectionInputs (1.134.0)

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`budget_milli_node_hours` |
`int`
The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node_hour = actual_hour \*
number_of_nodes_involved. For modelType
`cloud` \ (default), the budget must be between 20,000 and
900,000 milli node hours, inclusive. The default value is
216,000 which represents one day in wall time, considering 9
nodes are used. For model types `mobile-tf-low-latency-1` ,
`mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` the
training budget must be between 1,000 and 100,000 milli node
hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.
|
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Object Detection might stop training before the entire training budget has been used. |

## Classes

### ModelType

`ModelType(value)`


## Methods

### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore -->

# Class Featurestore (1.134.0)

```
Featurestore(
featurestore_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Managed featurestore resource for Vertex AI.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### Featurestore

```
Featurestore(
featurestore_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed featurestore given a featurestore resource name or a featurestore ID.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='projects/123/locations/us-central1/featurestores/my_featurestore_id'
)
or
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id'
)
```


Parameters |
|
|---|---|
Name |
Description |
`featurestore_name` |
`str`
Required. A fully-qualified featurestore resource name or a featurestore ID. Example: "projects/123/locations/us-central1/featurestores/my_featurestore_id" or "my_featurestore_id" when project and location are initialized or passed. |
`project` |
`str`
Optional. Project to retrieve featurestore from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve featurestore from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Featurestore. Overrides credentials set in aiplatform.init. |

### batch_serve_to_bq

```
batch_serve_to_bq(
bq_destination_output_uri: str,
serving_feature_ids: typing.Dict[str, typing.List[str]],
read_instances_uri: str,
pass_through_fields: typing.Optional[typing.List[str]] = None,
feature_destination_fields: typing.Optional[typing.Dict[str, str]] = None,
start_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
serve_request_timeout: typing.Optional[float] = None,
sync: bool = True,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Batch serves feature values to BigQuery destination

Exceptions |
|
|---|---|
Type |
Description |
`NotFound` |
if the BigQuery destination Dataset does not exist. |
`FailedPrecondition` |
if the BigQuery destination Dataset/Table is in a different project. |

Returns |
|
|---|---|
Type |
Description |
`Featurestore` |
The featurestore resource object batch read feature values from. |

### batch_serve_to_df

```
batch_serve_to_df(
serving_feature_ids: typing.Dict[str, typing.List[str]],
read_instances_df: pd.DataFrame,
pass_through_fields: typing.Optional[typing.List[str]] = None,
feature_destination_fields: typing.Optional[typing.Dict[str, str]] = None,
start_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
serve_request_timeout: typing.Optional[float] = None,
bq_dataset_id: typing.Optional[str] = None,
) -> pd.DataFrame
```


Batch serves feature values to pandas DataFrame

Parameters |
|
|---|---|
Name |
Description |
`serving_feature_ids` |
`Dict[str, List[str]]`
Required. A user defined dictionary to define the entity_types and their features for batch serve/read. The keys of the dictionary are the serving entity_type ids and the values are lists of serving feature ids in each entity_type. .. rubric:: Example serving_feature_ids = { 'my_entity_type_id_1': ['feature_id_1_1', 'feature_id_1_2'], 'my_entity_type_id_2': ['feature_id_2_1', 'feature_id_2_2'], } |
`read_instances_df` |
`pd.DataFrame`
Required. Read_instances_df is a pandas DataFrame containing the read instances. Each read instance should consist of exactly one read timestamp and one or more entity IDs identifying entities of the corresponding EntityTypes whose Features are requested. Each output instance contains Feature values of requested entities concatenated together as of the read time. An example read_instances_df may be pd.DataFrame( data=[ { "my_entity_type_id_1": "my_entity_type_id_1_entity_1", "my_entity_type_id_2": "my_entity_type_id_2_entity_1", "timestamp": "2020-01-01T10:00:00.123Z" ], ) An example batch_serve_output_df may be pd.DataFrame( data=[ { "my_entity_type_id_1": "my_entity_type_id_1_entity_1", "my_entity_type_id_2": "my_entity_type_id_2_entity_1", "foo": "feature_id_1_1_feature_value", "feature_id_1_2": "feature_id_1_2_feature_value", "feature_id_2_1": "feature_id_2_1_feature_value", "bar": "feature_id_2_2_feature_value", "timestamp": "2020-01-01T10:00:00.123Z" ], ) Timestamp in each read instance must be millisecond-aligned. The columns can be in any order. Values in the timestamp column must use the RFC 3339 format, e.g. |
`pass_through_fields` |
`List[str]`
Optional. When not empty, the specified fields in the read_instances source will be joined as-is in the output, in addition to those fields from the Featurestore Entity. For BigQuery source, the type of the pass-through values will be automatically inferred. For CSV source, the pass-through values will be passed as opaque bytes. |
`feature_destination_fields` |
`Dict[str, str]`
Optional. A user defined dictionary to map a feature's fully qualified resource name to its destination field name. If the destination field name is not defined, the feature ID will be used as its destination field name. .. rubric:: Example feature_destination_fields = { 'projects/123/locations/us-central1/featurestores/fs_id/entityTypes/et_id1/features/f_id11': 'foo', 'projects/123/locations/us-central1/featurestores/fs_id/entityTypes/et_id2/features/f_id22': 'bar', } |
`serve_request_timeout` |
`float`
Optional. The timeout for the serve request in seconds. |
`bq_dataset_id` |
`str`
Optional. The full dataset ID for the BigQuery dataset to use for temporarily staging data. If specified, caller must have |
`start_time` |
`timestamp_pb2.Timestamp`
Optional. Excludes Feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in Feature Store. Timestamp, if present, must not have higher than millisecond precision. |

Returns |
|
|---|---|
Type |
Description |
`pd.DataFrame` |
The pandas DataFrame containing feature values from batch serving. |

### batch_serve_to_gcs

```
batch_serve_to_gcs(
gcs_destination_output_uri_prefix: str,
gcs_destination_type: str,
serving_feature_ids: typing.Dict[str, typing.List[str]],
read_instances_uri: str,
pass_through_fields: typing.Optional[typing.List[str]] = None,
feature_destination_fields: typing.Optional[typing.Dict[str, str]] = None,
start_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
serve_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Batch serves feature values to GCS destination

Exceptions |
|
|---|---|
Type |
Description |
`ValueErro` |
if gcs_destination_type is not supported.: |

Returns |
|
|---|---|
Type |
Description |
`Featurestore` |
The featurestore resource object batch read feature values from. |

### create

```
create(
featurestore_id: str,
online_store_fixed_node_count: typing.Optional[int] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Creates a Featurestore resource.

Example Usage:

```
my_featurestore = aiplatform.Featurestore.create(
featurestore_id='my_featurestore_id',
)
```


### create_entity_type

```
create_entity_type(
entity_type_id: str,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.entity_type.EntityType
```


Creates an EntityType resource in this Featurestore.

Example Usage:

```
my_featurestore = aiplatform.Featurestore.create(
featurestore_id='my_featurestore_id'
)
my_entity_type = my_featurestore.create_entity_type(
entity_type_id='my_entity_type_id',
)
```


Parameters |
|
|---|---|
Name |
Description |
`entity_type_id` |
`str`
Required. The ID to use for the EntityType, which will become the final component of the EntityType's resource name. This value may be up to 60 characters, and valid characters are |
`description` |
`str`
Optional. Description of the EntityType. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your EntityTypes. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`sync` |
`bool`
Optional. Whether to execute this creation synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### delete

`delete(sync: bool = True, force: bool = False) -> None`


Deletes this Featurestore resource. If force is set to True, all entityTypes in this Featurestore will be deleted prior to featurestore deletion, and all features in each entityType will be deleted prior to each entityType deletion.

WARNING: This deletion is permanent.

### delete_entity_types

```
delete_entity_types(
entity_type_ids: typing.List[str], sync: bool = True, force: bool = False
) -> None
```


Deletes entity_type resources in this Featurestore given their entity_type IDs. WARNING: This deletion is permanent.

### get_entity_type

```
get_entity_type(
entity_type_id: str,
) -> google.cloud.aiplatform.featurestore.entity_type.EntityType
```


Retrieves an existing managed entityType in this Featurestore.

Parameter |
|
|---|---|
Name |
Description |
`entity_type_id` |
`str`
Required. The managed entityType resource ID in this Featurestore. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
parent: typing.Optional[str] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


List all instances of this Vertex AI Resource.

Example Usage:

aiplatform.BatchPredictionJobs.list( filter='state="JOB_STATE_SUCCEEDED" AND display_name="my_job"', )

aiplatform.Model.list(order_by="create_time desc, display_name")

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: |
`project` |
`str`
Optional. Project to retrieve list from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve list from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve list. Overrides credentials set in aiplatform.init. |
`parent` |
`str`
Optional. The parent resource name if any to retrieve list from. |

### list_entity_types

```
list_entity_types(
filter: typing.Optional[str] = None, order_by: typing.Optional[str] = None
) -> typing.List[google.cloud.aiplatform.featurestore.entity_type.EntityType]
```


Lists existing managed entityType resources in this Featurestore.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id',
)
my_featurestore.list_entity_types()
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. Lists the EntityTypes that match the filter expression. The following filters are supported: - |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
labels: typing.Optional[typing.Dict[str, str]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Updates an existing managed featurestore resource.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id',
)
my_featurestore.update(
labels={'update my key': 'update my value'},
)
```


Parameters |
|
|---|---|
Name |
Description |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Featurestores. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

### update_online_store

```
update_online_store(
fixed_node_count: int,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Updates the online store of an existing managed featurestore resource.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id',
)
my_featurestore.update_online_store(
fixed_node_count=2,
)
```


Parameters |
|
|---|---|
Name |
Description |
`fixed_node_count` |
`int`
Required. Config for online serving resources, can only update the node count to >= 1. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

### wait

`wait()`


Helper method that blocks until all futures are complete.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricInstance -->

# Class PointwiseMetricInstance (1.134.0)

`PointwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pointwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`json_instance` |
`str`
Instance specified as a json string. String key-value pairs are expected in the json_instance to render PointwiseMetricSpec.instance_prompt_template. This field is a member of `oneof` _ `instance` .
|
`content_map_instance` |
Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content. This field is a member of `oneof` _ `instance` .
|

## Methods

### PointwiseMetricInstance

`PointwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pointwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringTabularStats -->

# Class ModelMonitoringTabularStats (1.134.0)

`ModelMonitoringTabularStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of data points that describes the time-varying values of a tabular metric.

## Attributes |
|
|---|---|
Name |
Description |
`stats_name` |
`str`
The stats name. |
`objective_type` |
`str`
One of the supported monitoring objectives: `raw-feature-drift` `prediction-output-drift`
`feature-attribution`
|
`data_points` |
`MutableSequence[`
The data points of this time series. When listing time series, points are returned in reverse time order. |

## Methods

### ModelMonitoringTabularStats

`ModelMonitoringTabularStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of data points that describes the time-varying values of a tabular metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataResponse -->

# Class ImportDataResponse (1.134.0)

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.

## Methods

### ImportDataResponse

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataResponse -->

# Class ImportDataResponse (1.134.0)

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.

## Methods

### ImportDataResponse

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchDeletePipelineJobsRequest -->

# Class BatchDeletePipelineJobsRequest (1.134.0)

```
BatchDeletePipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchDeletePipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: `projects/{project}/locations/{location}`
|
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}`
|

## Methods

### BatchDeletePipelineJobsRequest

```
BatchDeletePipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchDeletePipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelSourceInfo -->

# Class ModelSourceInfo (1.134.0)

`ModelSourceInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Detail description of the source information of the model.

## Attributes |
|
|---|---|
Name |
Description |
`source_type` |
Type of the model source. |
`copy` |
`bool`
If this Model is copy of another Model. If true then source_type pertains to the original. |

## Classes

### ModelSourceType

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.

## Methods

### ModelSourceInfo

`ModelSourceInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Detail description of the source information of the model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataConfig -->

# Class ExportDataConfig (1.134.0)

`ExportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes what part of the Dataset is to be exported, the destination of the export and how to export.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`gcs_destination` |
The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: `export-data-`
where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601
format. All export output will be written into that
directory. Inside that directory, annotations with the same
schema will be grouped into sub directories which are named
with the corresponding annotations' schema title. Inside
these sub directories, a schema.yaml will be created to
describe the output format.
This field is a member of `oneof` _ `destination` .
|
`fraction_split` |
Split based on fractions defining the size of each set. This field is a member of `oneof` _ `split` .
|
`annotations_filter` |
`str`
An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in ListAnnotations. |

## Methods

### ExportDataConfig

`ExportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes what part of the Dataset is to be exported, the destination of the export and how to export.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesRequest.StatsAnomaliesObjective -->

# Class StatsAnomaliesObjective (1.134.0)

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

## Attribute |
|
|---|---|
Name |
Description |
`top_feature_count` |
`int`
If set, all attribution scores between SearchModelDeploymentMonitoringStatsAnomaliesRequest.start_time and SearchModelDeploymentMonitoringStatsAnomaliesRequest.end_time are fetched, and page token doesn't take effect in this case. Only used to retrieve attribution score for the top Features which has the highest attribution score in the latest monitoring run. |

## Methods

### StatsAnomaliesObjective

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomOutput -->

# Class CustomOutput (1.134.0)

`CustomOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for custom output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`raw_outputs` |
Output only. List of raw output strings. This field is a member of `oneof` _ `custom_output` .
|

## Methods

### CustomOutput

`CustomOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for custom output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsRequest -->

# Class BatchCancelPipelineJobsRequest (1.134.0)

```
BatchCancelPipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchCancelPipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: `projects/{project}/locations/{location}`
|
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}`
|

## Methods

### BatchCancelPipelineJobsRequest

```
BatchCancelPipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchCancelPipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup.ServiceAgentType -->

# Class ServiceAgentType (1.134.0)

`ServiceAgentType(value)`


Service agent type used during jobs under a FeatureGroup.

## Enums |
|
|---|---|
Name |
Description |
`SERVICE_AGENT_TYPE_UNSPECIFIED` |
By default, the project-level Vertex AI Service Agent is enabled. |
`SERVICE_AGENT_TYPE_PROJECT` |
Specifies the project-level Vertex AI Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents). |
`SERVICE_AGENT_TYPE_FEATURE_GROUP` |
Enable a FeatureGroup service account to be created by Vertex AI and output in the field `service_account_email`. This service account will be used to read from the source BigQuery table during jobs under a FeatureGroup. |

## Methods

### ServiceAgentType

`ServiceAgentType(value)`


Service agent type used during jobs under a FeatureGroup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportDataResponse -->

# Class ExportDataResponse (1.134.0)

`ExportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ExportData.

## Attributes |
|
|---|---|
Name |
Description |
`exported_files` |
`MutableSequence[str]`
All of the files that are exported in this export operation. For custom code training export, only three (training, validation and test) Cloud Storage paths in wildcard format are populated (for example, gs://.../training-\*). |
`data_stats` |
Only present for custom code training export use case. Records data stats, i.e., train/validation/test item/annotation counts calculated during the export operation. |

## Methods

### ExportDataResponse

`ExportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ExportData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedIndexRequest -->

# Class MutateDeployedIndexRequest (1.134.0)

`MutateDeployedIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.MutateDeployedIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`deployed_index` |
Required. The DeployedIndex to be updated within the IndexEndpoint. Currently, the updatable fields are DeployedIndex.automatic_resources and DeployedIndex.dedicated_resources |

## Methods

### MutateDeployedIndexRequest

`MutateDeployedIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.MutateDeployedIndex.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeContextsRequest -->

# Class PurgeContextsRequest (1.134.0)

`PurgeContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeContexts.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The metadata store to purge Contexts from. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`filter` |
`str`
Required. A required filter matching the Contexts to be purged. E.g., `update_time <=>` .
|
`force` |
`bool`
Optional. Flag to indicate to actually perform the purge. If `force` is set to false, the method will return a sample
of Context names that would be deleted.
|

## Methods

### PurgeContextsRequest

`PurgeContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeContexts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UnmanagedContainerModel -->

# Class UnmanagedContainerModel (1.134.0)

`UnmanagedContainerModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains model information necessary to perform batch prediction without requiring a full model import.

## Attributes |
|
|---|---|
Name |
Description |
`artifact_uri` |
`str`
The path to the directory containing the Model artifact and any of its supporting files. |
`predict_schemata` |
Contains the schemata used in Model's predictions and explanations |
`container_spec` |
Input only. The specification of the container that is to be used when deploying this Model. |

## Methods

### UnmanagedContainerModel

`UnmanagedContainerModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains model information necessary to perform batch prediction without requiring a full model import.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient -->

# Class VertexRagServiceClient (1.134.0)

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for retrieving relevant contexts.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### VertexRagServiceClient

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagServiceTransport,Callable[..., VertexRagServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If mutual TLS transport creation failed for any reason. |

### __exit__

`__exit__(type, value, traceback)`


Releases underlying transport's resources.

### augment_prompt

```
augment_prompt(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptRequest.Model
] = None,
vertex_rag_store: typing.Optional[
google.cloud.aiplatform_v1.types.tool.VertexRagStore
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptResponse
```


Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_augment_prompt():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AugmentPromptRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AugmentPromptRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[augment_prompt](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceClient_augment_prompt)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for AugmentPrompt. |
`parent` |
`str`
Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: |
`model` |
Optional. Metadata of the backend deployed model. This corresponds to the |
`vertex_rag_store` |
Optional. Retrieves contexts from the Vertex RagStore. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for AugmentPrompt. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### corroborate_content

```
corroborate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.CorroborateContentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
content: typing.Optional[google.cloud.aiplatform_v1.types.content.Content] = None,
facts: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1.types.vertex_rag_service.Fact]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.CorroborateContentResponse
```


Given an input text, it returns a score that evaluates the factuality of the text. It also extracts and returns claims from the text and provides supporting facts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_corroborate_content():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CorroborateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorroborateContentRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[corroborate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceClient_corroborate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for CorroborateContent. |
`parent` |
`str`
Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: |
`content` |
Optional. Input content to corroborate, only text format is supported for now. This corresponds to the |
`facts` |
`MutableSequence[`
Optional. Facts used to generate the text can also be used to corroborate the text. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for CorroborateContent. |

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Deprecated. Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### retrieve_contexts

```
retrieve_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.RetrieveContextsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
query: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_service.RagQuery
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.RetrieveContextsResponse
```


Retrieves relevant contexts for a query.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_retrieve_contexts():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
query = aiplatform_v1.[RagQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagQuery.html)()
query.text = "text_value"
request = aiplatform_v1.[RetrieveContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrieveContextsRequest.html)(
parent="parent_value",
query=query,
)
# Make the request
response = client.[retrieve_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceClient_retrieve_contexts)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VertexRagService.RetrieveContexts. |
`parent` |
`str`
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: |
`query` |
Required. Single RAG retrieve query. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VertexRagService.RetrieveContexts. |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient -->

# Class VizierServiceAsyncClient (1.134.0)

```
VizierServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Vertex AI Vizier API.

Vertex AI Vizier is a service to solve blackbox optimization problems, such as tuning machine learning hyperparameters and searching over deep learning architectures.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`VizierServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### VizierServiceAsyncClient

```
VizierServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vizier service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VizierServiceTransport,Callable[..., VizierServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the VizierServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTlsChannelError` |
If mutual TLS transport creation failed for any reason. |

### add_trial_measurement

```
add_trial_measurement(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.AddTrialMeasurementRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Adds a measurement of the objective metrics to a Trial. This measurement is assumed to have been taken before the Trial is complete.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_add_trial_measurement():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AddTrialMeasurementRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddTrialMeasurementRequest.html)(
trial_name="trial_name_value",
)
# Make the request
response = await client.[add_trial_measurement](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_add_trial_measurement)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.AddTrialMeasurement. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### check_trial_early_stopping_state

```
check_trial_early_stopping_state(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CheckTrialEarlyStoppingStateRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Checks whether a Trial should stop or not. Returns a long-running operation. When the operation is successful, it will contain a xref_CheckTrialEarlyStoppingStateResponse.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_check_trial_early_stopping_state():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CheckTrialEarlyStoppingStateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CheckTrialEarlyStoppingStateRequest.html)(
trial_name="trial_name_value",
)
# Make the request
operation = client.[check_trial_early_stopping_state](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_check_trial_early_stopping_state)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CheckTrialEarlyStoppingState. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be CheckTrialEarlyStoppingStateResponse Response message for VizierService.CheckTrialEarlyStoppingState. |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### complete_trial

```
complete_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CompleteTrialRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Marks a Trial as complete.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_complete_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CompleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CompleteTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[complete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_complete_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CompleteTrial. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### create_study

```
create_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CreateStudyRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
study: typing.Optional[google.cloud.aiplatform_v1.types.study.Study] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Study
```


Creates a Study. A resource name will be generated after creation of the Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
study = aiplatform_v1.[Study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Study.html)()
study.display_name = "display_name_value"
study.study_spec.metrics.metric_id = "metric_id_value"
study.study_spec.metrics.goal = "MINIMIZE"
study.study_spec.parameters.double_value_spec.min_value = 0.96
study.study_spec.parameters.double_value_spec.max_value = 0.962
study.study_spec.parameters.parameter_id = "parameter_id_value"
request = aiplatform_v1.[CreateStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateStudyRequest.html)(
parent="parent_value",
study=study,
)
# Make the request
response = await client.[create_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_create_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CreateStudy. |
`parent` |
Required. The resource name of the Location to create the CustomJob in. Format: |
`study` |
Required. The Study configuration used to create the Study. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### create_trial

```
create_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CreateTrialRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
trial: typing.Optional[google.cloud.aiplatform_v1.types.study.Trial] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Adds a user provided Trial to a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTrialRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_create_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CreateTrial. |
`parent` |
Required. The resource name of the Study to create the Trial in. Format: |
`trial` |
Required. The Trial to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### custom_job_path

`custom_job_path(project: str, location: str, custom_job: str) -> str`


Returns a fully-qualified custom_job string.

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### delete_study

```
delete_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.DeleteStudyRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteStudyRequest.html)(
name="name_value",
)
# Make the request
await client.[delete_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_delete_study)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.DeleteStudy. |
`name` |
Required. The name of the Study resource to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### delete_trial

```
delete_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.DeleteTrialRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTrialRequest.html)(
name="name_value",
)
# Make the request
await client.[delete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_delete_trial)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.DeleteTrial. |
`name` |
Required. The Trial's name. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### get_study

```
get_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.GetStudyRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Study
```


Gets a Study by name.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetStudyRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_get_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.GetStudy. |
`name` |
Required. The name of the Study resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport
]
```


Returns an appropriate transport class.

Parameter |
|
|---|---|
Name |
Description |
`label` |
`typing.Optional[str]`
The name of the desired transport. If none is provided, then the first transport in the registry is used. |

### get_trial

```
get_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.GetTrialRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Gets a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_get_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.GetTrial. |
`name` |
Required. The name of the Trial resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### list_optimal_trials

```
list_optimal_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.ListOptimalTrialsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vizier_service.ListOptimalTrialsResponse
```


Lists the pareto-optimal Trials for multi-objective Study or the
optimal Trials for single-objective Study. The definition of
pareto-optimal can be checked in wiki page.
[https://en.wikipedia.org/wiki/Pareto_efficiency](https://en.wikipedia.org/wiki/Pareto_efficiency)

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_optimal_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListOptimalTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListOptimalTrialsRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[list_optimal_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_list_optimal_trials)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListOptimalTrials. |
`parent` |
Required. The name of the Study that the optimal Trial belongs to. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListOptimalTrials. |

### list_studies

```
list_studies(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.vizier_service.pagers.ListStudiesAsyncPager
```


Lists all the studies in a region for an associated project.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_studies():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListStudiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_studies](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_list_studies)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListStudies. |
`parent` |
Required. The resource name of the Location to list the Study from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListStudies. Iterating over this object will yield results and resolve additional pages automatically. |

### list_trials

```
list_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsAsyncPager
```


Lists the Trials associated with a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_list_trials)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListTrials. |
`parent` |
Required. The resource name of the Study to list the Trial from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListTrials. Iterating over this object will yield results and resolve additional pages automatically. |

### lookup_study

```
lookup_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.LookupStudyRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Study
```


Looks a study up using the user-defined display_name field instead of the fully qualified resource name.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_lookup_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[LookupStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LookupStudyRequest.html)(
parent="parent_value",
display_name="display_name_value",
)
# Make the request
response = await client.[lookup_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_lookup_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.LookupStudy. |
`parent` |
Required. The resource name of the Location to get the Study from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_custom_job_path

`parse_custom_job_path(path: str) -> typing.Dict[str, str]`


Parses a custom_job path into its component segments.

### parse_study_path

`parse_study_path(path: str) -> typing.Dict[str, str]`


Parses a study path into its component segments.

### parse_trial_path

`parse_trial_path(path: str) -> typing.Dict[str, str]`


Parses a trial path into its component segments.

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### stop_trial

```
stop_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.StopTrialRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Stops a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_stop_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StopTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StopTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[stop_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_stop_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.StopTrial. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### study_path

`study_path(project: str, location: str, study: str) -> str`


Returns a fully-qualified study string.

### suggest_trials

```
suggest_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.SuggestTrialsRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Adds one or more Trials to a Study, with parameter values suggested by Vertex AI Vizier. Returns a long-running operation associated with the generation of Trial suggestions. When this long-running operation succeeds, it will contain a xref_SuggestTrialsResponse.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_suggest_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SuggestTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SuggestTrialsRequest.html)(
parent="parent_value",
suggestion_count=1744,
client_id="client_id_value",
)
# Make the request
operation = client.[suggest_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_suggest_trials)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.SuggestTrials. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be SuggestTrialsResponse Response message for VizierService.SuggestTrials. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### trial_path

`trial_path(project: str, location: str, study: str, trial: str) -> str`


Returns a fully-qualified trial string.

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PersistentResource -->

# Class PersistentResource (1.134.0)

`PersistentResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. Resource name of a PersistentResource. |
`display_name` |
`str`
Optional. The display name of the PersistentResource. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`resource_pools` |
`MutableSequence[`
Required. The spec of the pools of different resources. |
`state` |
Output only. The detailed state of a Study. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when persistent resource's state is `STOPPING` or `ERROR` .
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the PersistentResource was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the PersistentResource for the first time entered the `RUNNING` state.
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the PersistentResource was most recently updated. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize PersistentResource. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`network` |
`str`
Optional. The full name of the Compute Engine `network ` __
to peered with Vertex AI to host the persistent resources.
For example, `projects/12345/global/networks/myVPC` .
`Format ` __
is of the form
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in `12345` , and
{network} is a network name.
To specify this field, you must have already `configured VPC
Network Peering for Vertex
AI |
`psc_interface_config` |
Optional. Configuration for PSC-I for PersistentResource. |
`encryption_spec` |
Optional. Customer-managed encryption key spec for a PersistentResource. If set, this PersistentResource and all sub-resources of this PersistentResource will be secured by this key. |
`resource_runtime_spec` |
Optional. Persistent Resource runtime spec. For example, used for Ray cluster configuration. |
`resource_runtime` |
Output only. Runtime information of the Persistent Resource. |
`reserved_ip_ranges` |
`MutableSequence[str]`
Optional. A list of names for the reserved IP ranges under the VPC network that can be used for this persistent resource. If set, we will deploy the persistent resource within the provided IP ranges. Otherwise, the persistent resource is deployed to any IP ranges under the provided VPC network. Example: ['vertex-ai-ip-range']. |

## Classes

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
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

### State

`State(value)`


Describes the PersistentResource state.

## Methods

### PersistentResource

`PersistentResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionInputs.ModelType -->

# Class ModelType (1.134.0)

A model best tailored to be used within Google Cloud, and which cannot be exported. Expected to have a higher latency, but should also have a higher prediction quality than other cloud models.

CLOUD_LOW_LATENCY_1

A model best tailored to be used within Google Cloud, and which cannot be exported. Expected to have a low latency, but may have lower prediction quality than other cloud models.

MOBILE_TF_LOW_LATENCY_1

A model that, in addition to being available within Google Cloud can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

MOBILE_TF_VERSATILE_1

A model that, in addition to being available within Google Cloud can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards.

MOBILE_TF_HIGH_ACCURACY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards. Expected to have a higher latency, but should also have a higher prediction quality than other mobile models.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingMetadata -->

# Class AutoMlForecastingMetadata (1.134.0)

`AutoMlForecastingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Forecasting.

## Attribute |
|
|---|---|
Name |
Description |
`train_cost_milli_node_hours` |
`int`
Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget. |

## Methods

### AutoMlForecastingMetadata

`AutoMlForecastingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Forecasting.

### AutoMlForecastingMetadata

`AutoMlForecastingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Forecasting.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PostStartupScriptConfig -->

# Class PostStartupScriptConfig (1.134.0)

`PostStartupScriptConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Post startup script config.

## Attributes |
|
|---|---|
Name |
Description |
`post_startup_script` |
`str`
Optional. Post startup script to run after runtime is started. |
`post_startup_script_url` |
`str`
Optional. Post startup script url to download. Example: `gs://bucket/script.sh`
|
`post_startup_script_behavior` |
Optional. Post startup script behavior that defines download and execution behavior. |

## Classes

### PostStartupScriptBehavior

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post startup script behavior.

## Methods

### PostStartupScriptConfig

`PostStartupScriptConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Post startup script config.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelSourceInfo -->

# Class ModelSourceInfo (1.134.0)

`ModelSourceInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Detail description of the source information of the model.

## Attributes |
|
|---|---|
Name |
Description |
`source_type` |
Type of the model source. |
`copy` |
`bool`
If this Model is copy of another Model. If true then source_type pertains to the original. |

## Classes

### ModelSourceType

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.

## Methods

### ModelSourceInfo

`ModelSourceInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Detail description of the source information of the model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResumeScheduleRequest -->

# Class ResumeScheduleRequest (1.134.0)

`ResumeScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ResumeSchedule.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource to be resumed. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|
`catch_up` |
`bool`
Optional. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. This will also update Schedule.catch_up field. Default to false. |

## Methods

### ResumeScheduleRequest

`ResumeScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ResumeSchedule.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesRequest.StatsAnomaliesObjective -->

# Class StatsAnomaliesObjective (1.134.0)

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

## Attribute |
|
|---|---|
Name |
Description |
`top_feature_count` |
`int`
If set, all attribution scores between SearchModelDeploymentMonitoringStatsAnomaliesRequest.start_time and SearchModelDeploymentMonitoringStatsAnomaliesRequest.end_time are fetched, and page token doesn't take effect in this case. Only used to retrieve attribution score for the top Features which has the highest attribution score in the latest monitoring run. |

## Methods

### StatsAnomaliesObjective

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsResponse -->

# Class ListHyperparameterTuningJobsResponse (1.134.0)

```
ListHyperparameterTuningJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListHyperparameterTuningJobs

## Attributes |
|
|---|---|
Name |
Description |
`hyperparameter_tuning_jobs` |
`MutableSequence[`
List of HyperparameterTuningJobs in the requested page. HyperparameterTuningJob.trials of the jobs will be not be returned. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListHyperparameterTuningJobsRequest.page_token to obtain that page. |

## Methods

### ListHyperparameterTuningJobsResponse

```
ListHyperparameterTuningJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListHyperparameterTuningJobs

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tensor -->

# Class Tensor (1.134.0)

`Tensor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A tensor value type.

## Attributes |
|
|---|---|
Name |
Description |
`dtype` |
The data type of tensor. |
`shape` |
`MutableSequence[int]`
Shape of the tensor. |
`bool_val` |
`MutableSequence[bool]`
Type specific representations that make it easy to create tensor protos in all languages. Only the representation corresponding to "dtype" can be set. The values hold the flattened representation of the tensor in row major order. BOOL |
`string_val` |
`MutableSequence[str]`
STRING |
`bytes_val` |
`MutableSequence[bytes]`
STRING |
`float_val` |
`MutableSequence[float]`
FLOAT |
`double_val` |
`MutableSequence[float]`
DOUBLE |
`int_val` |
`MutableSequence[int]`
INT_8 INT_16 INT_32 |
`int64_val` |
`MutableSequence[int]`
INT64 |
`uint_val` |
`MutableSequence[int]`
UINT8 UINT16 UINT32 |
`uint64_val` |
`MutableSequence[int]`
UINT64 |
`list_val` |
`MutableSequence[google.cloud.aiplatform_v1.types.Tensor]`
A list of tensor values. |
`struct_val` |
`MutableMapping[str, google.cloud.aiplatform_v1.types.Tensor]`
A map of string to tensor. |
`tensor_val` |
`bytes`
Serialized raw tensor content. |

## Classes

### DataType

`DataType(value)`


Data type of the tensor.

### StructValEntry

`StructValEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
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

## Methods

### Tensor

`Tensor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A tensor value type.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployModelRequest -->

# Class DeployModelRequest (1.134.0)

`DeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeployModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to deploy a Model. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model` |
Required. The DeployedModel to be created within the Endpoint. Note that Endpoint.traffic_split must be updated for the DeployedModel to start receiving traffic, either as part of this call, or via EndpointService.UpdateEndpoint. |
`traffic_split` |
`MutableMapping[str, int]`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If this field is non-empty, then the Endpoint's traffic_split will be overwritten with it. To refer to the ID of the just being deployed Model, a "0" should be used, and the actual ID of the new DeployedModel will be filled in its place by this method. The traffic percentage values must add up to 100. If this field is empty, then the Endpoint's traffic_split is not updated. |

## Classes

### TrafficSplitEntry

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
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

## Methods

### DeployModelRequest

`DeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeployModel.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineContextSpec.MemoryBankConfig -->

# Class MemoryBankConfig (1.134.0)

`MemoryBankConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for a Memory Bank.

## Attributes |
|
|---|---|
Name |
Description |
`generation_config` |
Optional. Configuration for how to generate memories for the Memory Bank. |
`similarity_search_config` |
Optional. Configuration for how to perform similarity search on memories. If not set, the Memory Bank will use the default embedding model `text-embedding-005` .
|
`ttl_config` |
Optional. Configuration for automatic TTL ("time-to-live") of the memories in the Memory Bank. If not set, TTL will not be applied automatically. The TTL can be explicitly set by modifying the `expire_time` of each Memory resource.
|

## Classes

### GenerationConfig

`GenerationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how to generate memories.

### SimilaritySearchConfig

`SimilaritySearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how to perform similarity search on memories.

### TtlConfig

`TtlConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for automatically setting the TTL ("time-to-live") of the memories in the Memory Bank.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### MemoryBankConfig

`MemoryBankConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for a Memory Bank.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureNoiseSigma.NoiseSigmaForFeature -->

# Class NoiseSigmaForFeature (1.134.0)

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The name of the input feature for which noise sigma is provided. The features are defined in [explanation metadata inputs][google.cloud.aiplatform.v1beta1.ExplanationMetadata.inputs]. |
`sigma` |
`float`
This represents the standard deviation of the Gaussian kernel that will be used to add noise to the feature prior to computing gradients. Similar to noise_sigma but represents the noise added to the current feature. Defaults to 0.1. |

## Methods

### NoiseSigmaForFeature

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UnmanagedContainerModel -->

# Class UnmanagedContainerModel (1.134.0)

`UnmanagedContainerModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains model information necessary to perform batch prediction without requiring a full model import.

## Attributes |
|
|---|---|
Name |
Description |
`artifact_uri` |
`str`
The path to the directory containing the Model artifact and any of its supporting files. |
`predict_schemata` |
Contains the schemata used in Model's predictions and explanations |
`container_spec` |
Input only. The specification of the container that is to be used when deploying this Model. |

## Methods

### UnmanagedContainerModel

`UnmanagedContainerModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains model information necessary to perform batch prediction without requiring a full model import.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelOperationMetadata.OutputInfo -->

# Class OutputInfo (1.134.0)

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes the output of the ExportModel. Supplements ExportModelRequest.OutputConfig.

## Attributes |
|
|---|---|
Name |
Description |
`artifact_output_uri` |
`str`
Output only. If the Model artifact is being exported to Google Cloud Storage this is the full path of the directory created, into which the Model files are being written to. |
`image_output_uri` |
`str`
Output only. If the Model image is being exported to Google Container Registry or Artifact Registry this is the full path of the image created. |

## Methods

### OutputInfo

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes the output of the ExportModel. Supplements ExportModelRequest.OutputConfig.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextSentimentPredictionInstance -->

# Class TextSentimentPredictionInstance (1.134.0)

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The text snippet to make the predictions on. |
`mime_type` |
`str`
The MIME type of the text snippet. The supported MIME types are listed below. - text/plain |

## Methods

### TextSentimentPredictionInstance

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.

### TextSentimentPredictionInstance

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeContextsRequest -->

# Class PurgeContextsRequest (1.134.0)

`PurgeContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeContexts.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The metadata store to purge Contexts from. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`filter` |
`str`
Required. A required filter matching the Contexts to be purged. E.g., `update_time <=>` .
|
`force` |
`bool`
Optional. Flag to indicate to actually perform the purge. If `force` is set to false, the method will return a sample
of Context names that would be deleted.
|

## Methods

### PurgeContextsRequest

`PurgeContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeContexts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.Serializer -->

# Class Serializer (1.134.0)

`Serializer()`


Interface to implement serialization and deserialization for prediction.

## Methods

### deserialize

`deserialize(data: typing.Any, content_type: typing.Optional[str]) -> typing.Any`


Deserializes the request data. Invoked before predict.

Parameters |
|
|---|---|
Name |
Description |
`data` |
`Any`
Required. The request data sent to the application. |
`content_type` |
`str`
Optional. The specified content type of the request. |

### serialize

`serialize(prediction: typing.Any, accept: typing.Optional[str]) -> typing.Any`


Serializes the prediction results. Invoked after predict.

Parameters |
|
|---|---|
Name |
Description |
`prediction` |
`Any`
Required. The generated prediction to be sent back to clients. |
`accept` |
`str`
Optional. The specified content type of the response. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation -->

# Class Transformation (1.134.0)

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Classes

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The value converted to float32.

The z_score of the value.

log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

z_score of log(value+1) when the value is greater than or equal to

- Otherwise, this transformation is not applied and the value is considered a missing value.

A boolean value that indicates whether the value is valid.


### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The text as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.


### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


## Methods

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborSearchOperationMetadata.RecordError -->

# Class RecordError (1.134.0)

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`error_type` |
The error type of this record. |
`error_message` |
`str`
A human-readable message that is shown to the user to help them fix the error. Note that this message may change from time to time, your code should check against error_type as the source of truth. |
`source_gcs_uri` |
`str`
Cloud Storage URI pointing to the original file in user's bucket. |
`embedding_id` |
`str`
Empty if the embedding id is failed to parse. |
`raw_record` |
`str`
The original content of this record. |

## Classes

### RecordErrorType

`RecordErrorType(value)`


## Methods

### RecordError

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CheckTrialEarlyStoppingStateMetatdata -->

# Class CheckTrialEarlyStoppingStateMetatdata (1.134.0)

```
CheckTrialEarlyStoppingStateMetatdata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


This message will be placed in the metadata field of a google.longrunning.Operation associated with a CheckTrialEarlyStoppingState request.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for suggesting Trials. |
`study` |
`str`
The name of the Study that the Trial belongs to. |
`trial` |
`str`
The Trial name. |

## Methods

### CheckTrialEarlyStoppingStateMetatdata

```
CheckTrialEarlyStoppingStateMetatdata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


This message will be placed in the metadata field of a google.longrunning.Operation associated with a CheckTrialEarlyStoppingState request.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelRequest -->

# Class DeployModelRequest (1.134.0)

`DeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeployModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to deploy a Model. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model` |
Required. The DeployedModel to be created within the Endpoint. Note that Endpoint.traffic_split must be updated for the DeployedModel to start receiving traffic, either as part of this call, or via EndpointService.UpdateEndpoint. |
`traffic_split` |
`MutableMapping[str, int]`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If this field is non-empty, then the Endpoint's traffic_split will be overwritten with it. To refer to the ID of the just being deployed Model, a "0" should be used, and the actual ID of the new DeployedModel will be filled in its place by this method. The traffic percentage values must add up to 100. If this field is empty, then the Endpoint's traffic_split is not updated. |

## Classes

### TrafficSplitEntry

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
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

## Methods

### DeployModelRequest

`DeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeployModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient -->

# Class VertexRagServiceClient (1.134.0)

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for retrieving relevant contexts.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### VertexRagServiceClient

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagServiceTransport,Callable[..., VertexRagServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If mutual TLS transport creation failed for any reason. |

### __exit__

`__exit__(type, value, traceback)`


Releases underlying transport's resources.

### augment_prompt

```
augment_prompt(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptRequest.Model
] = None,
vertex_rag_store: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tool.VertexRagStore
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptResponse
```


Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_augment_prompt():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AugmentPromptRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AugmentPromptRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[augment_prompt](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceClient_augment_prompt)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for AugmentPrompt. |
`parent` |
`str`
Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: |
`model` |
Optional. Metadata of the backend deployed model. This corresponds to the |
`vertex_rag_store` |
Optional. Retrieves contexts from the Vertex RagStore. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for AugmentPrompt. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### corroborate_content

```
corroborate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.CorroborateContentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
content: typing.Optional[
google.cloud.aiplatform_v1beta1.types.content.Content
] = None,
facts: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.Fact
]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.CorroborateContentResponse
)
```


Given an input text, it returns a score that evaluates the factuality of the text. It also extracts and returns claims from the text and provides supporting facts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_corroborate_content():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CorroborateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[corroborate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceClient_corroborate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for CorroborateContent. |
`parent` |
`str`
Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: |
`content` |
Optional. Input content to corroborate, only text format is supported for now. This corresponds to the |
`facts` |
`MutableSequence[`
Optional. Facts used to generate the text can also be used to corroborate the text. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for CorroborateContent. |

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Deprecated. Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### retrieve_contexts

```
retrieve_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RetrieveContextsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
query: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RagQuery
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RetrieveContextsResponse
```


Retrieves relevant contexts for a query.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_retrieve_contexts():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
query = aiplatform_v1beta1.[RagQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagQuery.html)()
query.text = "text_value"
request = aiplatform_v1beta1.[RetrieveContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsRequest.html)(
parent="parent_value",
query=query,
)
# Make the request
response = client.[retrieve_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceClient_retrieve_contexts)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VertexRagService.RetrieveContexts. |
`parent` |
`str`
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: |
`query` |
Required. Single RAG retrieve query. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VertexRagService.RetrieveContexts. |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse -->

# Class SearchMigratableResourcesResponse (1.135.0)

```
SearchMigratableResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MigrationService.SearchMigratableResources.

## Attributes |
|
|---|---|
Name |
Description |
`migratable_resources` |
`MutableSequence[`
All migratable resources that can be migrated to the location specified in the request. |
`next_page_token` |
`str`
The standard next-page token. The migratable_resources may not fill page_size in SearchMigratableResourcesRequest even when there are subsequent pages. |

## Methods

### SearchMigratableResourcesResponse

```
SearchMigratableResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MigrationService.SearchMigratableResources.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model.ExportFormat -->

# Class ExportFormat (1.135.0)

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Output only. The ID of the export format. The possible format IDs are: - `tflite` Used for Android mobile devices.
- `edgetpu-tflite` Used for `Edge
TPU |
`exportable_contents` |
`MutableSequence[`
Output only. The content of this Model that may be exported. |

## Classes

### ExportableContent

`ExportableContent(value)`


The Model content that can be exported.

## Methods

### ExportFormat

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest.SimpleRetrievalParams -->

# Class SimpleRetrievalParams (1.135.0)

`SimpleRetrievalParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for simple (non-similarity search) retrieval.

## Attributes |
|
|---|---|
Name |
Description |
`page_size` |
`int`
Optional. The maximum number of memories to return. The service may return fewer than this value. If unspecified, at most 3 memories will be returned. The maximum value is 100; values above 100 will be coerced to 100. |
`page_token` |
`str`
Optional. A page token, received from a previous `RetrieveMemories` call. Provide this to retrieve the
subsequent page.
|

## Methods

### SimpleRetrievalParams

`SimpleRetrievalParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for simple (non-similarity search) retrieval.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNotebookExecutionJobRequest -->

# Class CreateNotebookExecutionJobRequest (1.135.0)

```
CreateNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.CreateNotebookExecutionJob]

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the NotebookExecutionJob. Format: `projects/{project}/locations/{location}`
|
`notebook_execution_job` |
Required. The NotebookExecutionJob to create. |
`notebook_execution_job_id` |
`str`
Optional. User specified ID for the NotebookExecutionJob. |

## Methods

### CreateNotebookExecutionJobRequest

```
CreateNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.CreateNotebookExecutionJob]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectRawPredictRequest -->

# Class DirectRawPredictRequest (1.135.0)

`DirectRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.DirectRawPredict.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform predictions. Format: `/namespace.Service/Method/` Example:
`/tensorflow.serving.PredictionService/Predict`
|
`input` |
`bytes`
The prediction input. |

## Methods

### DirectRawPredictRequest

`DirectRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.DirectRawPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AcceptPublisherModelEulaRequest -->

# Class AcceptPublisherModelEulaRequest (1.135.0)

```
AcceptPublisherModelEulaRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelGardenService.AcceptPublisherModelEula.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The project requesting access for named model. The format is `projects/{project}` .
|
`publisher_model` |
`str`
Required. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisher_model}` , or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}`
|

## Methods

### AcceptPublisherModelEulaRequest

```
AcceptPublisherModelEulaRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelGardenService.AcceptPublisherModelEula.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs -->

# Class AutoMlImageObjectDetectionInputs (1.135.0)

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`budget_milli_node_hours` |
`int`
The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node_hour = actual_hour \*
number_of_nodes_involved. For modelType
`cloud` \ (default), the budget must be between 20,000 and
900,000 milli node hours, inclusive. The default value is
216,000 which represents one day in wall time, considering 9
nodes are used. For model types `mobile-tf-low-latency-1` ,
`mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` the
training budget must be between 1,000 and 100,000 milli node
hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.
|
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Object Detection might stop training before the entire training budget has been used. |

## Classes

### ModelType

`ModelType(value)`


## Methods

### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AggregationResult -->

# Class AggregationResult (1.135.0)

`AggregationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The aggregation result for a single metric.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`pointwise_metric_result` |
Result for pointwise metric. This field is a member of `oneof` _ `aggregation_result` .
|
`pairwise_metric_result` |
Result for pairwise metric. This field is a member of `oneof` _ `aggregation_result` .
|
`exact_match_metric_value` |
Results for exact match metric. This field is a member of `oneof` _ `aggregation_result` .
|
`bleu_metric_value` |
Results for bleu metric. This field is a member of `oneof` _ `aggregation_result` .
|
`rouge_metric_value` |
Results for rouge metric. This field is a member of `oneof` _ `aggregation_result` .
|
`aggregation_metric` |
Aggregation metric. |

## Methods

### AggregationResult

`AggregationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The aggregation result for a single metric.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseMetricInstance -->

# Class PairwiseMetricInstance (1.135.0)

`PairwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pairwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`json_instance` |
`str`
Instance specified as a json string. String key-value pairs are expected in the json_instance to render PairwiseMetricSpec.instance_prompt_template. This field is a member of `oneof` _ `instance` .
|
`content_map_instance` |
Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content. This field is a member of `oneof` _ `instance` .
|

## Methods

### PairwiseMetricInstance

`PairwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pairwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportEvaluatedAnnotationsRequest -->

# Class BatchImportEvaluatedAnnotationsRequest (1.135.0)

```
BatchImportEvaluatedAnnotationsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.BatchImportEvaluatedAnnotations

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the parent ModelEvaluationSlice resource. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}/slices/{slice}`
|
`evaluated_annotations` |
`MutableSequence[`
Required. Evaluated annotations resource to be imported. |

## Methods

### BatchImportEvaluatedAnnotationsRequest

```
BatchImportEvaluatedAnnotationsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.BatchImportEvaluatedAnnotations

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchDeletePipelineJobsRequest -->

# Class BatchDeletePipelineJobsRequest (1.135.0)

```
BatchDeletePipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchDeletePipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: `projects/{project}/locations/{location}`
|
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}`
|

## Methods

### BatchDeletePipelineJobsRequest

```
BatchDeletePipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchDeletePipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpecialistPool -->

# Class SpecialistPool (1.135.0)

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the SpecialistPool. |
`display_name` |
`str`
Required. The user-defined name of the SpecialistPool. The name can be up to 128 characters long and can consist of any UTF-8 characters. This field should be unique on project-level. |
`specialist_managers_count` |
`int`
Output only. The number of managers in this SpecialistPool. |
`specialist_manager_emails` |
`MutableSequence[str]`
The email addresses of the managers in the SpecialistPool. |
`pending_data_labeling_jobs` |
`MutableSequence[str]`
Output only. The resource name of the pending data labeling jobs. |
`specialist_worker_emails` |
`MutableSequence[str]`
The email addresses of workers in the SpecialistPool. |

## Methods

### SpecialistPool

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesRequest -->

# Class BatchMigrateResourcesRequest (1.135.0)

```
BatchMigrateResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MigrationService.BatchMigrateResources.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location of the migrated resource will live in. Format: `projects/{project}/locations/{location}`
|
`migrate_resource_requests` |
`MutableSequence[`
Required. The request messages specifying the resources to migrate. They must be in the same location as the destination. Up to 50 resources can be migrated in one batch. |

## Methods

### BatchMigrateResourcesRequest

```
BatchMigrateResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MigrationService.BatchMigrateResources.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborQuery.NumericFilter.Operator -->

# Class Operator (1.135.0)

`Operator(value)`


Datapoints for which Operator is true relative to the query’s Value field will be allowlisted.

## Enums |
|
|---|---|
Name |
Description |
`OPERATOR_UNSPECIFIED` |
Unspecified operator. |
`LESS` |
Entities are eligible if their value is < the=""> |
`LESS_EQUAL` |
Entities are eligible if their value is <= the=""> |
`EQUAL` |
Entities are eligible if their value is == the query's. |
`GREATER_EQUAL` |
Entities are eligible if their value is >= the query's. |
`GREATER` |
Entities are eligible if their value is > the query's. |
`NOT_EQUAL` |
Entities are eligible if their value is != the query's. |

## Methods

### Operator

`Operator(value)`


Datapoints for which Operator is true relative to the query’s Value field will be allowlisted.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCancelPipelineJobsRequest -->

# Class BatchCancelPipelineJobsRequest (1.135.0)

```
BatchCancelPipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchCancelPipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: `projects/{project}/locations/{location}`
|
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}`
|

## Methods

### BatchCancelPipelineJobsRequest

```
BatchCancelPipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchCancelPipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureNoiseSigma.NoiseSigmaForFeature -->

# Class NoiseSigmaForFeature (1.135.0)

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The name of the input feature for which noise sigma is provided. The features are defined in [explanation metadata inputs][google.cloud.aiplatform.v1.ExplanationMetadata.inputs]. |
`sigma` |
`float`
This represents the standard deviation of the Gaussian kernel that will be used to add noise to the feature prior to computing gradients. Similar to noise_sigma but represents the noise added to the current feature. Defaults to 0.1. |

## Methods

### NoiseSigmaForFeature

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookExecutionJobRequest -->

# Class CreateNotebookExecutionJobRequest (1.135.0)

```
CreateNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.CreateNotebookExecutionJob]

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the NotebookExecutionJob. Format: `projects/{project}/locations/{location}`
|
`notebook_execution_job` |
Required. The NotebookExecutionJob to create. |
`notebook_execution_job_id` |
`str`
Optional. User specified ID for the NotebookExecutionJob. |

## Methods

### CreateNotebookExecutionJobRequest

```
CreateNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.CreateNotebookExecutionJob]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.ExportFormat -->

# Class ExportFormat (1.135.0)

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Output only. The ID of the export format. The possible format IDs are: - `tflite` Used for Android mobile devices.
- `edgetpu-tflite` Used for `Edge
TPU |
`exportable_contents` |
`MutableSequence[`
Output only. The content of this Model that may be exported. |

## Classes

### ExportableContent

`ExportableContent(value)`


The Model content that can be exported.

## Methods

### ExportFormat

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs.ModelType -->

# Class ModelType (1.135.0)

A model best tailored to be used within Google Cloud, and which cannot be exported. Expected to have a higher latency, but should also have a higher prediction quality than other cloud models.

CLOUD_LOW_LATENCY_1

A model best tailored to be used within Google Cloud, and which cannot be exported. Expected to have a low latency, but may have lower prediction quality than other cloud models.

MOBILE_TF_LOW_LATENCY_1

A model that, in addition to being available within Google Cloud can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

MOBILE_TF_VERSATILE_1

A model that, in addition to being available within Google Cloud can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards.

MOBILE_TF_HIGH_ACCURACY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards. Expected to have a higher latency, but should also have a higher prediction quality than other mobile models.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-28 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpecialistPool -->

# Class SpecialistPool (1.135.0)

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the SpecialistPool. |
`display_name` |
`str`
Required. The user-defined name of the SpecialistPool. The name can be up to 128 characters long and can consist of any UTF-8 characters. This field should be unique on project-level. |
`specialist_managers_count` |
`int`
Output only. The number of managers in this SpecialistPool. |
`specialist_manager_emails` |
`MutableSequence[str]`
The email addresses of the managers in the SpecialistPool. |
`pending_data_labeling_jobs` |
`MutableSequence[str]`
Output only. The resource name of the pending data labeling jobs. |
`specialist_worker_emails` |
`MutableSequence[str]`
The email addresses of workers in the SpecialistPool. |

## Methods

### SpecialistPool

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionInputs -->

# Class AutoMlImageObjectDetectionInputs (1.135.0)

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`budget_milli_node_hours` |
`int`
The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node_hour = actual_hour \*
number_of_nodes_involved. For modelType
`cloud` \ (default), the budget must be between 20,000 and
900,000 milli node hours, inclusive. The default value is
216,000 which represents one day in wall time, considering 9
nodes are used. For model types `mobile-tf-low-latency-1` ,
`mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` the
training budget must be between 1,000 and 100,000 milli node
hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.
|
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Object Detection might stop training before the entire training budget has been used. |

## Classes

### ModelType

`ModelType(value)`


## Methods

### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricInstance -->

# Class PointwiseMetricInstance (1.135.0)

`PointwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pointwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`json_instance` |
`str`
Instance specified as a json string. String key-value pairs are expected in the json_instance to render PointwiseMetricSpec.instance_prompt_template. This field is a member of `oneof` _ `instance` .
|
`content_map_instance` |
Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content. This field is a member of `oneof` _ `instance` .
|

## Methods

### PointwiseMetricInstance

`PointwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pointwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringTabularStats -->

# Class ModelMonitoringTabularStats (1.135.0)

`ModelMonitoringTabularStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of data points that describes the time-varying values of a tabular metric.

## Attributes |
|
|---|---|
Name |
Description |
`stats_name` |
`str`
The stats name. |
`objective_type` |
`str`
One of the supported monitoring objectives: `raw-feature-drift` `prediction-output-drift`
`feature-attribution`
|
`data_points` |
`MutableSequence[`
The data points of this time series. When listing time series, points are returned in reverse time order. |

## Methods

### ModelMonitoringTabularStats

`ModelMonitoringTabularStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of data points that describes the time-varying values of a tabular metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataResponse -->

# Class ImportDataResponse (1.135.0)

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.

## Methods

### ImportDataResponse

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataResponse -->

# Class ImportDataResponse (1.135.0)

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.

## Methods

### ImportDataResponse

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore -->

# Class Featurestore (1.135.0)

```
Featurestore(
featurestore_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Managed featurestore resource for Vertex AI.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### Featurestore

```
Featurestore(
featurestore_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed featurestore given a featurestore resource name or a featurestore ID.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='projects/123/locations/us-central1/featurestores/my_featurestore_id'
)
or
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id'
)
```


Parameters |
|
|---|---|
Name |
Description |
`featurestore_name` |
`str`
Required. A fully-qualified featurestore resource name or a featurestore ID. Example: "projects/123/locations/us-central1/featurestores/my_featurestore_id" or "my_featurestore_id" when project and location are initialized or passed. |
`project` |
`str`
Optional. Project to retrieve featurestore from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve featurestore from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Featurestore. Overrides credentials set in aiplatform.init. |

### batch_serve_to_bq

```
batch_serve_to_bq(
bq_destination_output_uri: str,
serving_feature_ids: typing.Dict[str, typing.List[str]],
read_instances_uri: str,
pass_through_fields: typing.Optional[typing.List[str]] = None,
feature_destination_fields: typing.Optional[typing.Dict[str, str]] = None,
start_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
serve_request_timeout: typing.Optional[float] = None,
sync: bool = True,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Batch serves feature values to BigQuery destination

Exceptions |
|
|---|---|
Type |
Description |
`NotFound` |
if the BigQuery destination Dataset does not exist. |
`FailedPrecondition` |
if the BigQuery destination Dataset/Table is in a different project. |

Returns |
|
|---|---|
Type |
Description |
`Featurestore` |
The featurestore resource object batch read feature values from. |

### batch_serve_to_df

```
batch_serve_to_df(
serving_feature_ids: typing.Dict[str, typing.List[str]],
read_instances_df: pd.DataFrame,
pass_through_fields: typing.Optional[typing.List[str]] = None,
feature_destination_fields: typing.Optional[typing.Dict[str, str]] = None,
start_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
serve_request_timeout: typing.Optional[float] = None,
bq_dataset_id: typing.Optional[str] = None,
) -> pd.DataFrame
```


Batch serves feature values to pandas DataFrame

Parameters |
|
|---|---|
Name |
Description |
`serving_feature_ids` |
`Dict[str, List[str]]`
Required. A user defined dictionary to define the entity_types and their features for batch serve/read. The keys of the dictionary are the serving entity_type ids and the values are lists of serving feature ids in each entity_type. .. rubric:: Example serving_feature_ids = { 'my_entity_type_id_1': ['feature_id_1_1', 'feature_id_1_2'], 'my_entity_type_id_2': ['feature_id_2_1', 'feature_id_2_2'], } |
`read_instances_df` |
`pd.DataFrame`
Required. Read_instances_df is a pandas DataFrame containing the read instances. Each read instance should consist of exactly one read timestamp and one or more entity IDs identifying entities of the corresponding EntityTypes whose Features are requested. Each output instance contains Feature values of requested entities concatenated together as of the read time. An example read_instances_df may be pd.DataFrame( data=[ { "my_entity_type_id_1": "my_entity_type_id_1_entity_1", "my_entity_type_id_2": "my_entity_type_id_2_entity_1", "timestamp": "2020-01-01T10:00:00.123Z" ], ) An example batch_serve_output_df may be pd.DataFrame( data=[ { "my_entity_type_id_1": "my_entity_type_id_1_entity_1", "my_entity_type_id_2": "my_entity_type_id_2_entity_1", "foo": "feature_id_1_1_feature_value", "feature_id_1_2": "feature_id_1_2_feature_value", "feature_id_2_1": "feature_id_2_1_feature_value", "bar": "feature_id_2_2_feature_value", "timestamp": "2020-01-01T10:00:00.123Z" ], ) Timestamp in each read instance must be millisecond-aligned. The columns can be in any order. Values in the timestamp column must use the RFC 3339 format, e.g. |
`pass_through_fields` |
`List[str]`
Optional. When not empty, the specified fields in the read_instances source will be joined as-is in the output, in addition to those fields from the Featurestore Entity. For BigQuery source, the type of the pass-through values will be automatically inferred. For CSV source, the pass-through values will be passed as opaque bytes. |
`feature_destination_fields` |
`Dict[str, str]`
Optional. A user defined dictionary to map a feature's fully qualified resource name to its destination field name. If the destination field name is not defined, the feature ID will be used as its destination field name. .. rubric:: Example feature_destination_fields = { 'projects/123/locations/us-central1/featurestores/fs_id/entityTypes/et_id1/features/f_id11': 'foo', 'projects/123/locations/us-central1/featurestores/fs_id/entityTypes/et_id2/features/f_id22': 'bar', } |
`serve_request_timeout` |
`float`
Optional. The timeout for the serve request in seconds. |
`bq_dataset_id` |
`str`
Optional. The full dataset ID for the BigQuery dataset to use for temporarily staging data. If specified, caller must have |
`start_time` |
`timestamp_pb2.Timestamp`
Optional. Excludes Feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in Feature Store. Timestamp, if present, must not have higher than millisecond precision. |

Returns |
|
|---|---|
Type |
Description |
`pd.DataFrame` |
The pandas DataFrame containing feature values from batch serving. |

### batch_serve_to_gcs

```
batch_serve_to_gcs(
gcs_destination_output_uri_prefix: str,
gcs_destination_type: str,
serving_feature_ids: typing.Dict[str, typing.List[str]],
read_instances_uri: str,
pass_through_fields: typing.Optional[typing.List[str]] = None,
feature_destination_fields: typing.Optional[typing.Dict[str, str]] = None,
start_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
serve_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Batch serves feature values to GCS destination

Exceptions |
|
|---|---|
Type |
Description |
`ValueErro` |
if gcs_destination_type is not supported.: |

Returns |
|
|---|---|
Type |
Description |
`Featurestore` |
The featurestore resource object batch read feature values from. |

### create

```
create(
featurestore_id: str,
online_store_fixed_node_count: typing.Optional[int] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Creates a Featurestore resource.

Example Usage:

```
my_featurestore = aiplatform.Featurestore.create(
featurestore_id='my_featurestore_id',
)
```


### create_entity_type

```
create_entity_type(
entity_type_id: str,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.entity_type.EntityType
```


Creates an EntityType resource in this Featurestore.

Example Usage:

```
my_featurestore = aiplatform.Featurestore.create(
featurestore_id='my_featurestore_id'
)
my_entity_type = my_featurestore.create_entity_type(
entity_type_id='my_entity_type_id',
)
```


Parameters |
|
|---|---|
Name |
Description |
`entity_type_id` |
`str`
Required. The ID to use for the EntityType, which will become the final component of the EntityType's resource name. This value may be up to 60 characters, and valid characters are |
`description` |
`str`
Optional. Description of the EntityType. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your EntityTypes. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`sync` |
`bool`
Optional. Whether to execute this creation synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### delete

`delete(sync: bool = True, force: bool = False) -> None`


Deletes this Featurestore resource. If force is set to True, all entityTypes in this Featurestore will be deleted prior to featurestore deletion, and all features in each entityType will be deleted prior to each entityType deletion.

WARNING: This deletion is permanent.

### delete_entity_types

```
delete_entity_types(
entity_type_ids: typing.List[str], sync: bool = True, force: bool = False
) -> None
```


Deletes entity_type resources in this Featurestore given their entity_type IDs. WARNING: This deletion is permanent.

### get_entity_type

```
get_entity_type(
entity_type_id: str,
) -> google.cloud.aiplatform.featurestore.entity_type.EntityType
```


Retrieves an existing managed entityType in this Featurestore.

Parameter |
|
|---|---|
Name |
Description |
`entity_type_id` |
`str`
Required. The managed entityType resource ID in this Featurestore. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
parent: typing.Optional[str] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


List all instances of this Vertex AI Resource.

Example Usage:

aiplatform.BatchPredictionJobs.list( filter='state="JOB_STATE_SUCCEEDED" AND display_name="my_job"', )

aiplatform.Model.list(order_by="create_time desc, display_name")

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: |
`project` |
`str`
Optional. Project to retrieve list from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve list from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve list. Overrides credentials set in aiplatform.init. |
`parent` |
`str`
Optional. The parent resource name if any to retrieve list from. |

### list_entity_types

```
list_entity_types(
filter: typing.Optional[str] = None, order_by: typing.Optional[str] = None
) -> typing.List[google.cloud.aiplatform.featurestore.entity_type.EntityType]
```


Lists existing managed entityType resources in this Featurestore.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id',
)
my_featurestore.list_entity_types()
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. Lists the EntityTypes that match the filter expression. The following filters are supported: - |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
labels: typing.Optional[typing.Dict[str, str]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Updates an existing managed featurestore resource.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id',
)
my_featurestore.update(
labels={'update my key': 'update my value'},
)
```


Parameters |
|
|---|---|
Name |
Description |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Featurestores. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

### update_online_store

```
update_online_store(
fixed_node_count: int,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.featurestore.Featurestore
```


Updates the online store of an existing managed featurestore resource.

Example Usage:

```
my_featurestore = aiplatform.Featurestore(
featurestore_name='my_featurestore_id',
)
my_featurestore.update_online_store(
fixed_node_count=2,
)
```


Parameters |
|
|---|---|
Name |
Description |
`fixed_node_count` |
`int`
Required. Config for online serving resources, can only update the node count to >= 1. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

### wait

`wait()`


Helper method that blocks until all futures are complete.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchDeletePipelineJobsRequest -->

# Class BatchDeletePipelineJobsRequest (1.135.0)

```
BatchDeletePipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchDeletePipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: `projects/{project}/locations/{location}`
|
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}`
|

## Methods

### BatchDeletePipelineJobsRequest

```
BatchDeletePipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchDeletePipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelSourceInfo -->

# Class ModelSourceInfo (1.135.0)

`ModelSourceInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Detail description of the source information of the model.

## Attributes |
|
|---|---|
Name |
Description |
`source_type` |
Type of the model source. |
`copy` |
`bool`
If this Model is copy of another Model. If true then source_type pertains to the original. |

## Classes

### ModelSourceType

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.

## Methods

### ModelSourceInfo

`ModelSourceInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Detail description of the source information of the model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataConfig -->

# Class ExportDataConfig (1.135.0)

`ExportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes what part of the Dataset is to be exported, the destination of the export and how to export.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`gcs_destination` |
The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: `export-data-`
where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601
format. All export output will be written into that
directory. Inside that directory, annotations with the same
schema will be grouped into sub directories which are named
with the corresponding annotations' schema title. Inside
these sub directories, a schema.yaml will be created to
describe the output format.
This field is a member of `oneof` _ `destination` .
|
`fraction_split` |
Split based on fractions defining the size of each set. This field is a member of `oneof` _ `split` .
|
`annotations_filter` |
`str`
An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in ListAnnotations. |

## Methods

### ExportDataConfig

`ExportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes what part of the Dataset is to be exported, the destination of the export and how to export.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesRequest.StatsAnomaliesObjective -->

# Class StatsAnomaliesObjective (1.135.0)

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

## Attribute |
|
|---|---|
Name |
Description |
`top_feature_count` |
`int`
If set, all attribution scores between SearchModelDeploymentMonitoringStatsAnomaliesRequest.start_time and SearchModelDeploymentMonitoringStatsAnomaliesRequest.end_time are fetched, and page token doesn't take effect in this case. Only used to retrieve attribution score for the top Features which has the highest attribution score in the latest monitoring run. |

## Methods

### StatsAnomaliesObjective

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomOutput -->

# Class CustomOutput (1.135.0)

`CustomOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for custom output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`raw_outputs` |
Output only. List of raw output strings. This field is a member of `oneof` _ `custom_output` .
|

## Methods

### CustomOutput

`CustomOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for custom output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsRequest -->

# Class BatchCancelPipelineJobsRequest (1.135.0)

```
BatchCancelPipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchCancelPipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: `projects/{project}/locations/{location}`
|
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}`
|

## Methods

### BatchCancelPipelineJobsRequest

```
BatchCancelPipelineJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.BatchCancelPipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup.ServiceAgentType -->

# Class ServiceAgentType (1.135.0)

`ServiceAgentType(value)`


Service agent type used during jobs under a FeatureGroup.

## Enums |
|
|---|---|
Name |
Description |
`SERVICE_AGENT_TYPE_UNSPECIFIED` |
By default, the project-level Vertex AI Service Agent is enabled. |
`SERVICE_AGENT_TYPE_PROJECT` |
Specifies the project-level Vertex AI Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents). |
`SERVICE_AGENT_TYPE_FEATURE_GROUP` |
Enable a FeatureGroup service account to be created by Vertex AI and output in the field `service_account_email`. This service account will be used to read from the source BigQuery table during jobs under a FeatureGroup. |

## Methods

### ServiceAgentType

`ServiceAgentType(value)`


Service agent type used during jobs under a FeatureGroup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportDataResponse -->

# Class ExportDataResponse (1.135.0)

`ExportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ExportData.

## Attributes |
|
|---|---|
Name |
Description |
`exported_files` |
`MutableSequence[str]`
All of the files that are exported in this export operation. For custom code training export, only three (training, validation and test) Cloud Storage paths in wildcard format are populated (for example, gs://.../training-\*). |
`data_stats` |
Only present for custom code training export use case. Records data stats, i.e., train/validation/test item/annotation counts calculated during the export operation. |

## Methods

### ExportDataResponse

`ExportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ExportData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedIndexRequest -->

# Class MutateDeployedIndexRequest (1.135.0)

`MutateDeployedIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.MutateDeployedIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`deployed_index` |
Required. The DeployedIndex to be updated within the IndexEndpoint. Currently, the updatable fields are DeployedIndex.automatic_resources and DeployedIndex.dedicated_resources |

## Methods

### MutateDeployedIndexRequest

`MutateDeployedIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.MutateDeployedIndex.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeContextsRequest -->

# Class PurgeContextsRequest (1.135.0)

`PurgeContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeContexts.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The metadata store to purge Contexts from. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`filter` |
`str`
Required. A required filter matching the Contexts to be purged. E.g., `update_time <=>` .
|
`force` |
`bool`
Optional. Flag to indicate to actually perform the purge. If `force` is set to false, the method will return a sample
of Context names that would be deleted.
|

## Methods

### PurgeContextsRequest

`PurgeContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeContexts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UnmanagedContainerModel -->

# Class UnmanagedContainerModel (1.135.0)

`UnmanagedContainerModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains model information necessary to perform batch prediction without requiring a full model import.

## Attributes |
|
|---|---|
Name |
Description |
`artifact_uri` |
`str`
The path to the directory containing the Model artifact and any of its supporting files. |
`predict_schemata` |
Contains the schemata used in Model's predictions and explanations |
`container_spec` |
Input only. The specification of the container that is to be used when deploying this Model. |

## Methods

### UnmanagedContainerModel

`UnmanagedContainerModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains model information necessary to perform batch prediction without requiring a full model import.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PersistentResource -->

# Class PersistentResource (1.135.0)

`PersistentResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. Resource name of a PersistentResource. |
`display_name` |
`str`
Optional. The display name of the PersistentResource. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`resource_pools` |
`MutableSequence[`
Required. The spec of the pools of different resources. |
`state` |
Output only. The detailed state of a Study. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when persistent resource's state is `STOPPING` or `ERROR` .
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the PersistentResource was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the PersistentResource for the first time entered the `RUNNING` state.
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the PersistentResource was most recently updated. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize PersistentResource. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`network` |
`str`
Optional. The full name of the Compute Engine `network ` __
to peered with Vertex AI to host the persistent resources.
For example, `projects/12345/global/networks/myVPC` .
`Format ` __
is of the form
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in `12345` , and
{network} is a network name.
To specify this field, you must have already `configured VPC
Network Peering for Vertex
AI |
`psc_interface_config` |
Optional. Configuration for PSC-I for PersistentResource. |
`encryption_spec` |
Optional. Customer-managed encryption key spec for a PersistentResource. If set, this PersistentResource and all sub-resources of this PersistentResource will be secured by this key. |
`resource_runtime_spec` |
Optional. Persistent Resource runtime spec. For example, used for Ray cluster configuration. |
`resource_runtime` |
Output only. Runtime information of the Persistent Resource. |
`reserved_ip_ranges` |
`MutableSequence[str]`
Optional. A list of names for the reserved IP ranges under the VPC network that can be used for this persistent resource. If set, we will deploy the persistent resource within the provided IP ranges. Otherwise, the persistent resource is deployed to any IP ranges under the provided VPC network. Example: ['vertex-ai-ip-range']. |

## Classes

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
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

### State

`State(value)`


Describes the PersistentResource state.

## Methods

### PersistentResource

`PersistentResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient -->

# Class VertexRagServiceClient (1.135.0)

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for retrieving relevant contexts.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### VertexRagServiceClient

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagServiceTransport,Callable[..., VertexRagServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If mutual TLS transport creation failed for any reason. |

### __exit__

`__exit__(type, value, traceback)`


Releases underlying transport's resources.

### augment_prompt

```
augment_prompt(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptRequest.Model
] = None,
vertex_rag_store: typing.Optional[
google.cloud.aiplatform_v1.types.tool.VertexRagStore
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptResponse
```


Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_augment_prompt():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AugmentPromptRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AugmentPromptRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[augment_prompt](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceClient_augment_prompt)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for AugmentPrompt. |
`parent` |
`str`
Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: |
`model` |
Optional. Metadata of the backend deployed model. This corresponds to the |
`vertex_rag_store` |
Optional. Retrieves contexts from the Vertex RagStore. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for AugmentPrompt. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### corroborate_content

```
corroborate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.CorroborateContentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
content: typing.Optional[google.cloud.aiplatform_v1.types.content.Content] = None,
facts: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1.types.vertex_rag_service.Fact]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.CorroborateContentResponse
```


Given an input text, it returns a score that evaluates the factuality of the text. It also extracts and returns claims from the text and provides supporting facts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_corroborate_content():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CorroborateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorroborateContentRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[corroborate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceClient_corroborate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for CorroborateContent. |
`parent` |
`str`
Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: |
`content` |
Optional. Input content to corroborate, only text format is supported for now. This corresponds to the |
`facts` |
`MutableSequence[`
Optional. Facts used to generate the text can also be used to corroborate the text. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for CorroborateContent. |

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Deprecated. Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### retrieve_contexts

```
retrieve_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.RetrieveContextsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
query: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_service.RagQuery
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.RetrieveContextsResponse
```


Retrieves relevant contexts for a query.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_retrieve_contexts():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
query = aiplatform_v1.[RagQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagQuery.html)()
query.text = "text_value"
request = aiplatform_v1.[RetrieveContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrieveContextsRequest.html)(
parent="parent_value",
query=query,
)
# Make the request
response = client.[retrieve_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceClient_retrieve_contexts)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VertexRagService.RetrieveContexts. |
`parent` |
`str`
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: |
`query` |
Required. Single RAG retrieve query. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VertexRagService.RetrieveContexts. |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient -->

# Class VertexRagServiceClient (1.135.0)

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for retrieving relevant contexts.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### VertexRagServiceClient

```
VertexRagServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagServiceTransport,Callable[..., VertexRagServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If mutual TLS transport creation failed for any reason. |

### __exit__

`__exit__(type, value, traceback)`


Releases underlying transport's resources.

### augment_prompt

```
augment_prompt(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptRequest.Model
] = None,
vertex_rag_store: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tool.VertexRagStore
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptResponse
```


Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_augment_prompt():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AugmentPromptRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AugmentPromptRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[augment_prompt](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceClient_augment_prompt)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for AugmentPrompt. |
`parent` |
`str`
Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: |
`model` |
Optional. Metadata of the backend deployed model. This corresponds to the |
`vertex_rag_store` |
Optional. Retrieves contexts from the Vertex RagStore. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for AugmentPrompt. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### corroborate_content

```
corroborate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.CorroborateContentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
content: typing.Optional[
google.cloud.aiplatform_v1beta1.types.content.Content
] = None,
facts: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.Fact
]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.CorroborateContentResponse
)
```


Given an input text, it returns a score that evaluates the factuality of the text. It also extracts and returns claims from the text and provides supporting facts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_corroborate_content():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CorroborateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[corroborate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceClient_corroborate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for CorroborateContent. |
`parent` |
`str`
Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: |
`content` |
Optional. Input content to corroborate, only text format is supported for now. This corresponds to the |
`facts` |
`MutableSequence[`
Optional. Facts used to generate the text can also be used to corroborate the text. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for CorroborateContent. |

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VertexRagServiceClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Deprecated. Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### retrieve_contexts

```
retrieve_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RetrieveContextsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
query: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RagQuery
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RetrieveContextsResponse
```


Retrieves relevant contexts for a query.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_retrieve_contexts():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html)()
# Initialize request argument(s)
query = aiplatform_v1beta1.[RagQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagQuery.html)()
query.text = "text_value"
request = aiplatform_v1beta1.[RetrieveContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsRequest.html)(
parent="parent_value",
query=query,
)
# Make the request
response = client.[retrieve_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceClient_retrieve_contexts)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VertexRagService.RetrieveContexts. |
`parent` |
`str`
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: |
`query` |
Required. Single RAG retrieve query. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VertexRagService.RetrieveContexts. |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient -->

# Class VizierServiceAsyncClient (1.135.0)

```
VizierServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Vertex AI Vizier API.

Vertex AI Vizier is a service to solve blackbox optimization problems, such as tuning machine learning hyperparameters and searching over deep learning architectures.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`VizierServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### VizierServiceAsyncClient

```
VizierServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vizier service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VizierServiceTransport,Callable[..., VizierServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the VizierServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTlsChannelError` |
If mutual TLS transport creation failed for any reason. |

### add_trial_measurement

```
add_trial_measurement(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.AddTrialMeasurementRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Adds a measurement of the objective metrics to a Trial. This measurement is assumed to have been taken before the Trial is complete.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_add_trial_measurement():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AddTrialMeasurementRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddTrialMeasurementRequest.html)(
trial_name="trial_name_value",
)
# Make the request
response = await client.[add_trial_measurement](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_add_trial_measurement)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.AddTrialMeasurement. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### check_trial_early_stopping_state

```
check_trial_early_stopping_state(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CheckTrialEarlyStoppingStateRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Checks whether a Trial should stop or not. Returns a long-running operation. When the operation is successful, it will contain a xref_CheckTrialEarlyStoppingStateResponse.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_check_trial_early_stopping_state():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CheckTrialEarlyStoppingStateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CheckTrialEarlyStoppingStateRequest.html)(
trial_name="trial_name_value",
)
# Make the request
operation = client.[check_trial_early_stopping_state](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_check_trial_early_stopping_state)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CheckTrialEarlyStoppingState. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be CheckTrialEarlyStoppingStateResponse Response message for VizierService.CheckTrialEarlyStoppingState. |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### complete_trial

```
complete_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CompleteTrialRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Marks a Trial as complete.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_complete_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CompleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CompleteTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[complete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_complete_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CompleteTrial. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### create_study

```
create_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CreateStudyRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
study: typing.Optional[google.cloud.aiplatform_v1.types.study.Study] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Study
```


Creates a Study. A resource name will be generated after creation of the Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
study = aiplatform_v1.[Study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Study.html)()
study.display_name = "display_name_value"
study.study_spec.metrics.metric_id = "metric_id_value"
study.study_spec.metrics.goal = "MINIMIZE"
study.study_spec.parameters.double_value_spec.min_value = 0.96
study.study_spec.parameters.double_value_spec.max_value = 0.962
study.study_spec.parameters.parameter_id = "parameter_id_value"
request = aiplatform_v1.[CreateStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateStudyRequest.html)(
parent="parent_value",
study=study,
)
# Make the request
response = await client.[create_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_create_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CreateStudy. |
`parent` |
Required. The resource name of the Location to create the CustomJob in. Format: |
`study` |
Required. The Study configuration used to create the Study. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### create_trial

```
create_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.CreateTrialRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
trial: typing.Optional[google.cloud.aiplatform_v1.types.study.Trial] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Adds a user provided Trial to a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTrialRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_create_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.CreateTrial. |
`parent` |
Required. The resource name of the Study to create the Trial in. Format: |
`trial` |
Required. The Trial to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### custom_job_path

`custom_job_path(project: str, location: str, custom_job: str) -> str`


Returns a fully-qualified custom_job string.

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### delete_study

```
delete_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.DeleteStudyRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteStudyRequest.html)(
name="name_value",
)
# Make the request
await client.[delete_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_delete_study)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.DeleteStudy. |
`name` |
Required. The name of the Study resource to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### delete_trial

```
delete_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.DeleteTrialRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTrialRequest.html)(
name="name_value",
)
# Make the request
await client.[delete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_delete_trial)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.DeleteTrial. |
`name` |
Required. The Trial's name. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`VizierServiceAsyncClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### get_study

```
get_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.GetStudyRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Study
```


Gets a Study by name.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetStudyRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_get_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.GetStudy. |
`name` |
Required. The name of the Study resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.vizier_service.transports.base.VizierServiceTransport
]
```


Returns an appropriate transport class.

Parameter |
|
|---|---|
Name |
Description |
`label` |
`typing.Optional[str]`
The name of the desired transport. If none is provided, then the first transport in the registry is used. |

### get_trial

```
get_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.GetTrialRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Gets a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_get_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.GetTrial. |
`name` |
Required. The name of the Trial resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### list_optimal_trials

```
list_optimal_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.ListOptimalTrialsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vizier_service.ListOptimalTrialsResponse
```


Lists the pareto-optimal Trials for multi-objective Study or the
optimal Trials for single-objective Study. The definition of
pareto-optimal can be checked in wiki page.
[https://en.wikipedia.org/wiki/Pareto_efficiency](https://en.wikipedia.org/wiki/Pareto_efficiency)

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_optimal_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListOptimalTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListOptimalTrialsRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[list_optimal_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_list_optimal_trials)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListOptimalTrials. |
`parent` |
Required. The name of the Study that the optimal Trial belongs to. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListOptimalTrials. |

### list_studies

```
list_studies(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.vizier_service.pagers.ListStudiesAsyncPager
```


Lists all the studies in a region for an associated project.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_studies():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListStudiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_studies](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_list_studies)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListStudies. |
`parent` |
Required. The resource name of the Location to list the Study from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListStudies. Iterating over this object will yield results and resolve additional pages automatically. |

### list_trials

```
list_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsAsyncPager
```


Lists the Trials associated with a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_list_trials)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.ListTrials. |
`parent` |
Required. The resource name of the Study to list the Trial from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for VizierService.ListTrials. Iterating over this object will yield results and resolve additional pages automatically. |

### lookup_study

```
lookup_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.LookupStudyRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Study
```


Looks a study up using the user-defined display_name field instead of the fully qualified resource name.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_lookup_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[LookupStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LookupStudyRequest.html)(
parent="parent_value",
display_name="display_name_value",
)
# Make the request
response = await client.[lookup_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_lookup_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.LookupStudy. |
`parent` |
Required. The resource name of the Location to get the Study from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Study. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_custom_job_path

`parse_custom_job_path(path: str) -> typing.Dict[str, str]`


Parses a custom_job path into its component segments.

### parse_study_path

`parse_study_path(path: str) -> typing.Dict[str, str]`


Parses a study path into its component segments.

### parse_trial_path

`parse_trial_path(path: str) -> typing.Dict[str, str]`


Parses a trial path into its component segments.

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### stop_trial

```
stop_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.StopTrialRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.study.Trial
```


Stops a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_stop_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StopTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StopTrialRequest.html)(
name="name_value",
)
# Make the request
response = await client.[stop_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_stop_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.StopTrial. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### study_path

`study_path(project: str, location: str, study: str) -> str`


Returns a fully-qualified study string.

### suggest_trials

```
suggest_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vizier_service.SuggestTrialsRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Adds one or more Trials to a Study, with parameter values suggested by Vertex AI Vizier. Returns a long-running operation associated with the generation of Trial suggestions. When this long-running operation succeeds, it will contain a xref_SuggestTrialsResponse.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_suggest_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SuggestTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SuggestTrialsRequest.html)(
parent="parent_value",
suggestion_count=1744,
client_id="client_id_value",
)
# Make the request
operation = client.[suggest_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceAsyncClient_suggest_trials)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VizierService.SuggestTrials. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be SuggestTrialsResponse Response message for VizierService.SuggestTrials. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### trial_path

`trial_path(project: str, location: str, study: str, trial: str) -> str`


Returns a fully-qualified trial string.

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionInputs.ModelType -->

# Class ModelType (1.135.0)

A model best tailored to be used within Google Cloud, and which cannot be exported. Expected to have a higher latency, but should also have a higher prediction quality than other cloud models.

CLOUD_LOW_LATENCY_1

A model best tailored to be used within Google Cloud, and which cannot be exported. Expected to have a low latency, but may have lower prediction quality than other cloud models.

MOBILE_TF_LOW_LATENCY_1

A model that, in addition to being available within Google Cloud can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

MOBILE_TF_VERSATILE_1

A model that, in addition to being available within Google Cloud can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards.

MOBILE_TF_HIGH_ACCURACY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) and used on a mobile or edge device with TensorFlow afterwards. Expected to have a higher latency, but should also have a higher prediction quality than other mobile models.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-28 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingMetadata -->

# Class AutoMlForecastingMetadata (1.135.0)

`AutoMlForecastingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Forecasting.

## Attribute |
|
|---|---|
Name |
Description |
`train_cost_milli_node_hours` |
`int`
Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget. |

## Methods

### AutoMlForecastingMetadata

`AutoMlForecastingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Forecasting.

### AutoMlForecastingMetadata

`AutoMlForecastingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Forecasting.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PostStartupScriptConfig -->

# Class PostStartupScriptConfig (1.135.0)

`PostStartupScriptConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Post startup script config.

## Attributes |
|
|---|---|
Name |
Description |
`post_startup_script` |
`str`
Optional. Post startup script to run after runtime is started. |
`post_startup_script_url` |
`str`
Optional. Post startup script url to download. Example: `gs://bucket/script.sh`
|
`post_startup_script_behavior` |
Optional. Post startup script behavior that defines download and execution behavior. |

## Classes

### PostStartupScriptBehavior

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post startup script behavior.

## Methods

### PostStartupScriptConfig

`PostStartupScriptConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Post startup script config.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelSourceInfo -->

# Class ModelSourceInfo (1.135.0)

`ModelSourceInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Detail description of the source information of the model.

## Attributes |
|
|---|---|
Name |
Description |
`source_type` |
Type of the model source. |
`copy` |
`bool`
If this Model is copy of another Model. If true then source_type pertains to the original. |

## Classes

### ModelSourceType

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.

## Methods

### ModelSourceInfo

`ModelSourceInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Detail description of the source information of the model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResumeScheduleRequest -->

# Class ResumeScheduleRequest (1.135.0)

`ResumeScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ResumeSchedule.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource to be resumed. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|
`catch_up` |
`bool`
Optional. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. This will also update Schedule.catch_up field. Default to false. |

## Methods

### ResumeScheduleRequest

`ResumeScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ResumeSchedule.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesRequest.StatsAnomaliesObjective -->

# Class StatsAnomaliesObjective (1.135.0)

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

## Attribute |
|
|---|---|
Name |
Description |
`top_feature_count` |
`int`
If set, all attribution scores between SearchModelDeploymentMonitoringStatsAnomaliesRequest.start_time and SearchModelDeploymentMonitoringStatsAnomaliesRequest.end_time are fetched, and page token doesn't take effect in this case. Only used to retrieve attribution score for the top Features which has the highest attribution score in the latest monitoring run. |

## Methods

### StatsAnomaliesObjective

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsResponse -->

# Class ListHyperparameterTuningJobsResponse (1.135.0)

```
ListHyperparameterTuningJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListHyperparameterTuningJobs

## Attributes |
|
|---|---|
Name |
Description |
`hyperparameter_tuning_jobs` |
`MutableSequence[`
List of HyperparameterTuningJobs in the requested page. HyperparameterTuningJob.trials of the jobs will be not be returned. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListHyperparameterTuningJobsRequest.page_token to obtain that page. |

## Methods

### ListHyperparameterTuningJobsResponse

```
ListHyperparameterTuningJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListHyperparameterTuningJobs

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tensor -->

# Class Tensor (1.135.0)

`Tensor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A tensor value type.

## Attributes |
|
|---|---|
Name |
Description |
`dtype` |
The data type of tensor. |
`shape` |
`MutableSequence[int]`
Shape of the tensor. |
`bool_val` |
`MutableSequence[bool]`
Type specific representations that make it easy to create tensor protos in all languages. Only the representation corresponding to "dtype" can be set. The values hold the flattened representation of the tensor in row major order. BOOL |
`string_val` |
`MutableSequence[str]`
STRING |
`bytes_val` |
`MutableSequence[bytes]`
STRING |
`float_val` |
`MutableSequence[float]`
FLOAT |
`double_val` |
`MutableSequence[float]`
DOUBLE |
`int_val` |
`MutableSequence[int]`
INT_8 INT_16 INT_32 |
`int64_val` |
`MutableSequence[int]`
INT64 |
`uint_val` |
`MutableSequence[int]`
UINT8 UINT16 UINT32 |
`uint64_val` |
`MutableSequence[int]`
UINT64 |
`list_val` |
`MutableSequence[google.cloud.aiplatform_v1.types.Tensor]`
A list of tensor values. |
`struct_val` |
`MutableMapping[str, google.cloud.aiplatform_v1.types.Tensor]`
A map of string to tensor. |
`tensor_val` |
`bytes`
Serialized raw tensor content. |

## Classes

### DataType

`DataType(value)`


Data type of the tensor.

### StructValEntry

`StructValEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
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

## Methods

### Tensor

`Tensor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A tensor value type.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployModelRequest -->

# Class DeployModelRequest (1.135.0)

`DeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeployModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to deploy a Model. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model` |
Required. The DeployedModel to be created within the Endpoint. Note that Endpoint.traffic_split must be updated for the DeployedModel to start receiving traffic, either as part of this call, or via EndpointService.UpdateEndpoint. |
`traffic_split` |
`MutableMapping[str, int]`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If this field is non-empty, then the Endpoint's traffic_split will be overwritten with it. To refer to the ID of the just being deployed Model, a "0" should be used, and the actual ID of the new DeployedModel will be filled in its place by this method. The traffic percentage values must add up to 100. If this field is empty, then the Endpoint's traffic_split is not updated. |

## Classes

### TrafficSplitEntry

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
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

## Methods

### DeployModelRequest

`DeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeployModel.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineContextSpec.MemoryBankConfig -->

# Class MemoryBankConfig (1.135.0)

`MemoryBankConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for a Memory Bank.

## Attributes |
|
|---|---|
Name |
Description |
`generation_config` |
Optional. Configuration for how to generate memories for the Memory Bank. |
`similarity_search_config` |
Optional. Configuration for how to perform similarity search on memories. If not set, the Memory Bank will use the default embedding model `text-embedding-005` .
|
`ttl_config` |
Optional. Configuration for automatic TTL ("time-to-live") of the memories in the Memory Bank. If not set, TTL will not be applied automatically. The TTL can be explicitly set by modifying the `expire_time` of each Memory resource.
|

## Classes

### GenerationConfig

`GenerationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how to generate memories.

### SimilaritySearchConfig

`SimilaritySearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how to perform similarity search on memories.

### TtlConfig

`TtlConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for automatically setting the TTL ("time-to-live") of the memories in the Memory Bank.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### MemoryBankConfig

`MemoryBankConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for a Memory Bank.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureNoiseSigma.NoiseSigmaForFeature -->

# Class NoiseSigmaForFeature (1.135.0)

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The name of the input feature for which noise sigma is provided. The features are defined in [explanation metadata inputs][google.cloud.aiplatform.v1beta1.ExplanationMetadata.inputs]. |
`sigma` |
`float`
This represents the standard deviation of the Gaussian kernel that will be used to add noise to the feature prior to computing gradients. Similar to noise_sigma but represents the noise added to the current feature. Defaults to 0.1. |

## Methods

### NoiseSigmaForFeature

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UnmanagedContainerModel -->

# Class UnmanagedContainerModel (1.135.0)

`UnmanagedContainerModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains model information necessary to perform batch prediction without requiring a full model import.

## Attributes |
|
|---|---|
Name |
Description |
`artifact_uri` |
`str`
The path to the directory containing the Model artifact and any of its supporting files. |
`predict_schemata` |
Contains the schemata used in Model's predictions and explanations |
`container_spec` |
Input only. The specification of the container that is to be used when deploying this Model. |

## Methods

### UnmanagedContainerModel

`UnmanagedContainerModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains model information necessary to perform batch prediction without requiring a full model import.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelOperationMetadata.OutputInfo -->

# Class OutputInfo (1.135.0)

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes the output of the ExportModel. Supplements ExportModelRequest.OutputConfig.

## Attributes |
|
|---|---|
Name |
Description |
`artifact_output_uri` |
`str`
Output only. If the Model artifact is being exported to Google Cloud Storage this is the full path of the directory created, into which the Model files are being written to. |
`image_output_uri` |
`str`
Output only. If the Model image is being exported to Google Container Registry or Artifact Registry this is the full path of the image created. |

## Methods

### OutputInfo

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes the output of the ExportModel. Supplements ExportModelRequest.OutputConfig.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextSentimentPredictionInstance -->

# Class TextSentimentPredictionInstance (1.135.0)

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The text snippet to make the predictions on. |
`mime_type` |
`str`
The MIME type of the text snippet. The supported MIME types are listed below. - text/plain |

## Methods

### TextSentimentPredictionInstance

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.

### TextSentimentPredictionInstance

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeContextsRequest -->

# Class PurgeContextsRequest (1.135.0)

`PurgeContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeContexts.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The metadata store to purge Contexts from. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`filter` |
`str`
Required. A required filter matching the Contexts to be purged. E.g., `update_time <=>` .
|
`force` |
`bool`
Optional. Flag to indicate to actually perform the purge. If `force` is set to false, the method will return a sample
of Context names that would be deleted.
|

## Methods

### PurgeContextsRequest

`PurgeContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeContexts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.Serializer -->

# Class Serializer (1.135.0)

`Serializer()`


Interface to implement serialization and deserialization for prediction.

## Methods

### deserialize

`deserialize(data: typing.Any, content_type: typing.Optional[str]) -> typing.Any`


Deserializes the request data. Invoked before predict.

Parameters |
|
|---|---|
Name |
Description |
`data` |
`Any`
Required. The request data sent to the application. |
`content_type` |
`str`
Optional. The specified content type of the request. |

### serialize

`serialize(prediction: typing.Any, accept: typing.Optional[str]) -> typing.Any`


Serializes the prediction results. Invoked after predict.

Parameters |
|
|---|---|
Name |
Description |
`prediction` |
`Any`
Required. The generated prediction to be sent back to clients. |
`accept` |
`str`
Optional. The specified content type of the response. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation -->

# Class Transformation (1.135.0)

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Classes

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The value converted to float32.

The z_score of the value.

log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

z_score of log(value+1) when the value is greater than or equal to

- Otherwise, this transformation is not applied and the value is considered a missing value.

A boolean value that indicates whether the value is valid.


### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The text as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.


### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


## Methods

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborSearchOperationMetadata.RecordError -->

# Class RecordError (1.135.0)

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`error_type` |
The error type of this record. |
`error_message` |
`str`
A human-readable message that is shown to the user to help them fix the error. Note that this message may change from time to time, your code should check against error_type as the source of truth. |
`source_gcs_uri` |
`str`
Cloud Storage URI pointing to the original file in user's bucket. |
`embedding_id` |
`str`
Empty if the embedding id is failed to parse. |
`raw_record` |
`str`
The original content of this record. |

## Classes

### RecordErrorType

`RecordErrorType(value)`


## Methods

### RecordError

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CheckTrialEarlyStoppingStateMetatdata -->

# Class CheckTrialEarlyStoppingStateMetatdata (1.135.0)

```
CheckTrialEarlyStoppingStateMetatdata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


This message will be placed in the metadata field of a google.longrunning.Operation associated with a CheckTrialEarlyStoppingState request.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for suggesting Trials. |
`study` |
`str`
The name of the Study that the Trial belongs to. |
`trial` |
`str`
The Trial name. |

## Methods

### CheckTrialEarlyStoppingStateMetatdata

```
CheckTrialEarlyStoppingStateMetatdata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


This message will be placed in the metadata field of a google.longrunning.Operation associated with a CheckTrialEarlyStoppingState request.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelRequest -->

# Class DeployModelRequest (1.135.0)

`DeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeployModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to deploy a Model. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model` |
Required. The DeployedModel to be created within the Endpoint. Note that Endpoint.traffic_split must be updated for the DeployedModel to start receiving traffic, either as part of this call, or via EndpointService.UpdateEndpoint. |
`traffic_split` |
`MutableMapping[str, int]`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If this field is non-empty, then the Endpoint's traffic_split will be overwritten with it. To refer to the ID of the just being deployed Model, a "0" should be used, and the actual ID of the new DeployedModel will be filled in its place by this method. The traffic percentage values must add up to 100. If this field is empty, then the Endpoint's traffic_split is not updated. |

## Classes

### TrafficSplitEntry

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
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

## Methods

### DeployModelRequest

`DeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeployModel.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResumeScheduleRequest -->

# Class ResumeScheduleRequest (1.135.0)

`ResumeScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ResumeSchedule.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource to be resumed. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|
`catch_up` |
`bool`
Optional. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. This will also update Schedule.catch_up field. Default to false. |

## Methods

### ResumeScheduleRequest

`ResumeScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ResumeSchedule.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse -->

# Class ListHyperparameterTuningJobsResponse (1.135.0)

```
ListHyperparameterTuningJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListHyperparameterTuningJobs

## Attributes |
|
|---|---|
Name |
Description |
`hyperparameter_tuning_jobs` |
`MutableSequence[`
List of HyperparameterTuningJobs in the requested page. HyperparameterTuningJob.trials of the jobs will be not be returned. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListHyperparameterTuningJobsRequest.page_token to obtain that page. |

## Methods

### ListHyperparameterTuningJobsResponse

```
ListHyperparameterTuningJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListHyperparameterTuningJobs

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service -->

# Package featurestore_service (1.135.0)

API documentation for `aiplatform_v1beta1.services.featurestore_service`

package.

## Classes

[FeaturestoreServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient)

The service that handles CRUD and List for resources for Featurestore.

[FeaturestoreServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient)

The service that handles CRUD and List for resources for Featurestore.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers)

API documentation for `aiplatform_v1beta1.services.featurestore_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PostStartupScriptConfig -->

# Class PostStartupScriptConfig (1.135.0)

`PostStartupScriptConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Post-startup script config.

## Attributes |
|
|---|---|
Name |
Description |
`post_startup_script` |
`str`
Optional. Post-startup script to run after runtime is started. |
`post_startup_script_url` |
`str`
Optional. Post-startup script url to download. Example: https://bucket/script.sh |
`post_startup_script_behavior` |
Optional. Post-startup script behavior that defines download and execution behavior. |

## Classes

### PostStartupScriptBehavior

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post-startup script behavior.

## Methods

### PostStartupScriptConfig

`PostStartupScriptConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Post-startup script config.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardTimeSeries -->

# Class TensorboardTimeSeries (1.135.0)

```
TensorboardTimeSeries(
tensorboard_time_series_name: str,
tensorboard_id: typing.Optional[str] = None,
tensorboard_experiment_id: typing.Optional[str] = None,
tensorboard_run_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Managed tensorboard resource for Vertex AI.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### TensorboardTimeSeries

```
TensorboardTimeSeries(
tensorboard_time_series_name: str,
tensorboard_id: typing.Optional[str] = None,
tensorboard_experiment_id: typing.Optional[str] = None,
tensorboard_run_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing tensorboard time series given a tensorboard time series name or ID.

Example Usage:

```
tb_ts = aiplatform.TensorboardTimeSeries(
tensorboard_time_series_name="projects/123/locations/us-central1/tensorboards/456/experiments/789/run/1011/timeSeries/mse"
)
tb_ts = aiplatform.TensorboardTimeSeries(
tensorboard_time_series_name= "mse",
tensorboard_id = "456",
tensorboard_experiment_id = "789"
tensorboard_run_id = "1011"
)
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_time_series_name` |
`str`
Required. A fully-qualified tensorboard time series resource name or resource ID. Example: "projects/123/locations/us-central1/tensorboards/456/experiments/789/run/1011/timeSeries/mse" or "mse" when tensorboard_id, tensorboard_experiment_id, tensorboard_run_id are passed and project and location are initialized or passed. |
`tensorboard_id` |
`str`
Optional. A tensorboard resource ID. |
`tensorboard_experiment_id` |
`str`
Optional. A tensorboard experiment resource ID. |
`tensorboard_run_id` |
`str`
Optional. A tensorboard run resource ID. |
`project` |
`str`
Optional. Project to retrieve tensorboard from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve tensorboard from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Tensorboard. Overrides credentials set in aiplatform.init. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
if only one of tensorboard_id or tensorboard_experiment_id is provided. |

### create

```
create(
display_name: str,
tensorboard_run_name: str,
tensorboard_id: typing.Optional[str] = None,
tensorboard_experiment_id: typing.Optional[str] = None,
value_type: typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_time_series.TensorboardTimeSeries.ValueType,
str,
] = "SCALAR",
plugin_name: str = "scalars",
plugin_data: typing.Optional[bytes] = None,
description: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.tensorboard.tensorboard_resource.TensorboardTimeSeries
```


Creates a new tensorboard time series.

Example Usage:

```
tb_ts = aiplatform.TensorboardTimeSeries.create(
display_name='my display name',
tensorboard_run_name='my-run'
tensorboard_id='456'
tensorboard_experiment_id='my-experiment'
description='my description',
labels={
'key1': 'value1',
'key2': 'value2'
}
)
```


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. User provided name of this TensorboardTimeSeries. This value should be unique among all TensorboardTimeSeries resources belonging to the same TensorboardRun resource (parent resource). |
`tensorboard_run_name` |
`str`
Required. The resource name or ID of the TensorboardRun to create the TensorboardTimeseries in. Resource name format: |
`tensorboard_id` |
`str`
Optional. The resource ID of the Tensorboard to create the TensorboardTimeSeries in. |
`tensorboard_experiment_id` |
`str`
Optional. The ID of the TensorboardExperiment to create the TensorboardTimeSeries in. |
`value_type` |
`Union[gca_tensorboard_time_series.TensorboardTimeSeries.ValueType, str]`
Optional. Type of TensorboardTimeSeries value. One of 'SCALAR', 'TENSOR', 'BLOB_SEQUENCE'. |
`plugin_name` |
`str`
Optional. Name of the plugin this time series pertain to. |
`plugin_data` |
`bytes`
Optional. Data of the current plugin, with the size limited to 65KB. |
`description` |
`str`
Optional. Description of this TensorboardTimeseries. |
`project` |
`str`
Optional. Project to upload this model to. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to upload this model to. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`TensorboardTimeSeries` |
The TensorboardTimeSeries resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### list

```
list(
tensorboard_run_name: str,
tensorboard_id: typing.Optional[str] = None,
tensorboard_experiment_id: typing.Optional[str] = None,
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[
google.cloud.aiplatform.tensorboard.tensorboard_resource.TensorboardTimeSeries
]
```


List all instances of TensorboardTimeSeries in TensorboardRun.

Example Usage:

```
aiplatform.TensorboardTimeSeries.list(
tensorboard_run_name='projects/my-project/locations/us-central1/tensorboards/123/experiments/my-experiment/runs/my-run'
)
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_run_name` |
`str`
Required. The resource name or ID of the TensorboardRun to list the TensorboardTimeseries from. Resource name format: |
`tensorboard_id` |
`str`
Optional. The resource ID of the Tensorboard to list the TensorboardTimeSeries from. |
`tensorboard_experiment_id` |
`str`
Optional. The ID of the TensorboardExperiment to list the TensorboardTimeSeries from. |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: |
`project` |
`str`
Optional. Project to retrieve list from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve list from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve list. Overrides credentials set in aiplatform.init. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RawOutput -->

# Class RawOutput (1.135.0)

`RawOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Raw output.

## Attribute |
|
|---|---|
Name |
Description |
`raw_output` |
`MutableSequence[str]`
Output only. Raw output string. |

## Methods

### RawOutput

`RawOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Raw output.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Modality -->

# Class Modality (1.135.0)

`Modality(value)`


Content Part modality

## Enums |
|
|---|---|
Name |
Description |
`MODALITY_UNSPECIFIED` |
Unspecified modality. |
`TEXT` |
Plain text. |
`IMAGE` |
Image. |
`VIDEO` |
Video. |
`AUDIO` |
Audio. |
`DOCUMENT` |
Document, e.g. PDF. |

## Methods

### Modality

`Modality(value)`


Content Part modality

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BleuMetricValue -->

# Class BleuMetricValue (1.135.0)

`BleuMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Bleu metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Bleu score. This field is a member of `oneof` _ `_score` .
|

## Methods

### BleuMetricValue

`BleuMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Bleu metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest.MigrateDataLabelingDatasetConfig.MigrateDataLabelingAnnotatedDatasetConfig -->

# Class MigrateDataLabelingAnnotatedDatasetConfig (1.135.0)

```
MigrateDataLabelingAnnotatedDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating AnnotatedDataset in datalabeling.googleapis.com to Vertex AI's SavedQuery.

## Attribute |
|
|---|---|
Name |
Description |
`annotated_dataset` |
`str`
Required. Full resource name of data labeling AnnotatedDataset. Format: `projects/{project}/datasets/{dataset}/annotatedDatasets/{annotated_dataset}` .
|

## Methods

### MigrateDataLabelingAnnotatedDatasetConfig

```
MigrateDataLabelingAnnotatedDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating AnnotatedDataset in datalabeling.googleapis.com to Vertex AI's SavedQuery.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SafetyInstance -->

# Class SafetyInstance (1.135.0)

`SafetyInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for safety instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|

## Methods

### SafetyInstance

`SafetyInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for safety instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineTaskExecutorDetail -->

# Class PipelineTaskExecutorDetail (1.135.0)

`PipelineTaskExecutorDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime detail of a pipeline executor.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`container_detail` |
Output only. The detailed info for a container executor. This field is a member of `oneof` _ `details` .
|
`custom_job_detail` |
Output only. The detailed info for a custom job executor. This field is a member of `oneof` _ `details` .
|

## Classes

### ContainerDetail

`ContainerDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The detail of a container execution. It contains the job names of the lifecycle of a container execution.

### CustomJobDetail

`CustomJobDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The detailed info for a custom job executor.

## Methods

### PipelineTaskExecutorDetail

`PipelineTaskExecutorDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime detail of a pipeline executor.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteContextRequest -->

# Class DeleteContextRequest (1.135.0)

`DeleteContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteContext.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Context to delete. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`force` |
`bool`
The force deletion semantics is still undefined. Users should not use this field. |
`etag` |
`str`
Optional. The etag of the Context to delete. If this is provided, it must match the server's etag. Otherwise, the request will fail with a FAILED_PRECONDITION. |

## Methods

### DeleteContextRequest

`DeleteContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteContext.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateScheduleRequest -->

# Class UpdateScheduleRequest (1.135.0)

`UpdateScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.UpdateSchedule.

## Attributes |
|
|---|---|
Name |
Description |
`schedule` |
Required. The Schedule which replaces the resource on the server. The following restrictions will be applied: - The scheduled request type cannot be changed. - The non-empty fields cannot be unset. - The output_only fields will be ignored if specified. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateScheduleRequest

`UpdateScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.UpdateSchedule.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers -->

# Module pagers (1.135.0)

API documentation for `aiplatform_v1.services.metadata_service.pagers`

module.

## Classes

[ListArtifactsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListArtifactsAsyncPager)

```
ListArtifactsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_artifacts`

requests.

This class thinly wraps an initial
[ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse) object, and
provides an `__aiter__`

method to iterate through its
`artifacts`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListArtifacts`

requests and continue to iterate
through the `artifacts`

field on the
corresponding responses.

All the usual [ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListArtifactsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListArtifactsPager)

```
ListArtifactsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_artifacts`

requests.

This class thinly wraps an initial
[ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse) object, and
provides an `__iter__`

method to iterate through its
`artifacts`

field.

If there are more pages, the `__iter__`

method will make additional
`ListArtifacts`

requests and continue to iterate
through the `artifacts`

field on the
corresponding responses.

All the usual [ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListContextsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListContextsAsyncPager)

```
ListContextsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_contexts`

requests.

This class thinly wraps an initial
[ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse) object, and
provides an `__aiter__`

method to iterate through its
`contexts`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListContexts`

requests and continue to iterate
through the `contexts`

field on the
corresponding responses.

All the usual [ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListContextsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListContextsPager)

```
ListContextsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_contexts`

requests.

This class thinly wraps an initial
[ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse) object, and
provides an `__iter__`

method to iterate through its
`contexts`

field.

If there are more pages, the `__iter__`

method will make additional
`ListContexts`

requests and continue to iterate
through the `contexts`

field on the
corresponding responses.

All the usual [ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListExecutionsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListExecutionsAsyncPager)

```
ListExecutionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_executions`

requests.

This class thinly wraps an initial
[ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`executions`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListExecutions`

requests and continue to iterate
through the `executions`

field on the
corresponding responses.

All the usual [ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListExecutionsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListExecutionsPager)

```
ListExecutionsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_executions`

requests.

This class thinly wraps an initial
[ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse) object, and
provides an `__iter__`

method to iterate through its
`executions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListExecutions`

requests and continue to iterate
through the `executions`

field on the
corresponding responses.

All the usual [ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListMetadataSchemasAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataSchemasAsyncPager)

```
ListMetadataSchemasAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_metadata_schemas`

requests.

This class thinly wraps an initial
[ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse) object, and
provides an `__aiter__`

method to iterate through its
`metadata_schemas`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListMetadataSchemas`

requests and continue to iterate
through the `metadata_schemas`

field on the
corresponding responses.

All the usual [ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListMetadataSchemasPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataSchemasPager)

```
ListMetadataSchemasPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse,
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_metadata_schemas`

requests.

This class thinly wraps an initial
[ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse) object, and
provides an `__iter__`

method to iterate through its
`metadata_schemas`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMetadataSchemas`

requests and continue to iterate
through the `metadata_schemas`

field on the
corresponding responses.

All the usual [ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListMetadataStoresAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataStoresAsyncPager)

```
ListMetadataStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_metadata_stores`

requests.

This class thinly wraps an initial
[ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`metadata_stores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListMetadataStores`

requests and continue to iterate
through the `metadata_stores`

field on the
corresponding responses.

All the usual [ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListMetadataStoresPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataStoresPager)

```
ListMetadataStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse,
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_metadata_stores`

requests.

This class thinly wraps an initial
[ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`metadata_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMetadataStores`

requests and continue to iterate
through the `metadata_stores`

field on the
corresponding responses.

All the usual [ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.
