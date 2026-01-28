---
merged_at: 2026-01-28T15:11:44.731430
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient -->

# Class VizierServiceClient (1.134.0)

```
VizierServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### VizierServiceClient

```
VizierServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vizier service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the VizierServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_add_trial_measurement():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AddTrialMeasurementRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddTrialMeasurementRequest.html)(
trial_name="trial_name_value",
)
# Make the request
response = client.[add_trial_measurement](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_add_trial_measurement)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.AddTrialMeasurement. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_check_trial_early_stopping_state():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CheckTrialEarlyStoppingStateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CheckTrialEarlyStoppingStateRequest.html)(
trial_name="trial_name_value",
)
# Make the request
operation = client.[check_trial_early_stopping_state](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_check_trial_early_stopping_state)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CheckTrialEarlyStoppingState. |
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
`google.api_core.operation.Operation` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_complete_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CompleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CompleteTrialRequest.html)(
name="name_value",
)
# Make the request
response = client.[complete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_complete_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CompleteTrial. |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_create_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
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
response = client.[create_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_create_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CreateStudy. |
`parent` |
`str`
Required. The resource name of the Location to create the CustomJob in. Format: |
`study` |
Required. The Study configuration used to create the Study. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_create_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTrialRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_create_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CreateTrial. |
`parent` |
`str`
Required. The resource name of the Study to create the Trial in. Format: |
`trial` |
Required. The Trial to create. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_delete_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteStudyRequest.html)(
name="name_value",
)
# Make the request
client.[delete_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_delete_study)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.DeleteStudy. |
`name` |
`str`
Required. The name of the Study resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
def sample_delete_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTrialRequest.html)(
name="name_value",
)
# Make the request
client.[delete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_delete_trial)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.DeleteTrial. |
`name` |
`str`
Required. The Trial's name. Format: |
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
`VizierServiceClient` |
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
`VizierServiceClient` |
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
`VizierServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetStudyRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_get_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.GetStudy. |
`name` |
`str`
Required. The name of the Study resource. Format: |
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
A message representing a Study. |

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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTrialRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_get_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.GetTrial. |
`name` |
`str`
Required. The name of the Trial resource. Format: |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_list_optimal_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListOptimalTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListOptimalTrialsRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[list_optimal_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_list_optimal_trials)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.ListOptimalTrials. |
`parent` |
`str`
Required. The name of the Study that the optimal Trial belongs to. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.vizier_service.pagers.ListStudiesPager
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
def sample_list_studies():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListStudiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_studies](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_list_studies)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.ListStudies. |
`parent` |
`str`
Required. The resource name of the Location to list the Study from. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsPager
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
def sample_list_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_list_trials)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.ListTrials. |
`parent` |
`str`
Required. The resource name of the Study to list the Trial from. Format: |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_lookup_study():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[LookupStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LookupStudyRequest.html)(
parent="parent_value",
display_name="display_name_value",
)
# Make the request
response = client.[lookup_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_lookup_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.LookupStudy. |
`parent` |
`str`
Required. The resource name of the Location to get the Study from. Format: |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_stop_trial():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StopTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StopTrialRequest.html)(
name="name_value",
)
# Make the request
response = client.[stop_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_stop_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.StopTrial. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_suggest_trials():
# Create a client
client = aiplatform_v1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SuggestTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SuggestTrialsRequest.html)(
parent="parent_value",
suggestion_count=1744,
client_id="client_id_value",
)
# Make the request
operation = client.[suggest_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1_services_vizier_service_VizierServiceClient_suggest_trials)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.SuggestTrials. |
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
`google.api_core.operation.Operation` |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service -->

# Package featurestore_service (1.134.0)

API documentation for `aiplatform_v1.services.featurestore_service`

package.

## Classes

[FeaturestoreServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient)

The service that handles CRUD and List for resources for Featurestore.

[FeaturestoreServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient)

The service that handles CRUD and List for resources for Featurestore.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers)

API documentation for `aiplatform_v1.services.featurestore_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service -->

# Package gen_ai_tuning_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.gen_ai_tuning_service`

package.

## Classes

[GenAiTuningServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient)

A service for creating and managing GenAI Tuning Jobs.

[GenAiTuningServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient)

A service for creating and managing GenAI Tuning Jobs.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.pagers)

API documentation for `aiplatform_v1beta1.services.gen_ai_tuning_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsRequest -->

# Class ListFeatureViewSyncsRequest (1.134.0)

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureView to list FeatureViewSyncs. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|
`filter` |
`str`
Lists the FeatureViewSyncs that match the filter expression. The following filters are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
Examples:
- `create_time > \"2020-01-31T15:30:00.000000Z\"` -->
FeatureViewSyncs created after
2020-01-31T15:30:00.000000Z.
|
`page_size` |
`int`
The maximum number of FeatureViewSyncs to return. The service may return fewer than this value. If unspecified, at most 1000 FeatureViewSyncs will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeatureOnlineStoreAdminService.ListFeatureViewSyncs call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeatureOnlineStoreAdminService.ListFeatureViewSyncs must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `create_time`
|

## Methods

### ListFeatureViewSyncsRequest

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesRequest -->

# Class BatchReadFeatureValuesRequest (1.134.0)

```
BatchReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreService.BatchReadFeatureValues.

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
`csv_read_instances` |
Each read instance consists of exactly one read timestamp and one or more entity IDs identifying entities of the corresponding EntityTypes whose Features are requested. Each output instance contains Feature values of requested entities concatenated together as of the read time. An example read instance may be `foo_entity_id, bar_entity_id, 2020-01-01T10:00:00.123Z` .
An example output instance may be
`foo_entity_id, bar_entity_id, 2020-01-01T10:00:00.123Z, foo_entity_feature1_value, bar_entity_feature2_value` .
Timestamp in each read instance must be millisecond-aligned.
`csv_read_instances` are read instances stored in a
plain-text CSV file. The header should be:
[ENTITY_TYPE_ID1], [ENTITY_TYPE_ID2], ..., timestamp
The columns can be in any order.
Values in the timestamp column must use the RFC 3339 format,
e.g. `2012-07-30T10:43:17.123Z` .
This field is a member of `oneof` _ `read_option` .
|
`bigquery_read_instances` |
Similar to csv_read_instances, but from BigQuery source. This field is a member of `oneof` _ `read_option` .
|
`featurestore` |
`str`
Required. The resource name of the Featurestore from which to query Feature values. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`destination` |
Required. Specifies output location and format. |
`pass_through_fields` |
`MutableSequence[`
When not empty, the specified fields in the \*_read_instances source will be joined as-is in the output, in addition to those fields from the Featurestore Entity. For BigQuery source, the type of the pass-through values will be automatically inferred. For CSV source, the pass-through values will be passed as opaque bytes. |
`entity_type_specs` |
`MutableSequence[`
Required. Specifies EntityType grouping Features to read values of and settings. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Excludes Feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in Feature Store. Timestamp, if present, must not have higher than millisecond precision. |

## Classes

### EntityTypeSpec

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

### PassThroughField

`PassThroughField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describe pass-through fields in read_instance source.

## Methods

### BatchReadFeatureValuesRequest

```
BatchReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreService.BatchReadFeatureValues.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.CategoricalTransformation -->

# Class CategoricalTransformation (1.134.0)

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

## Methods

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringObjectiveConfig -->

# Class ModelDeploymentMonitoringObjectiveConfig (1.134.0)

```
ModelDeploymentMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringObjectiveConfig contains the pair of deployed_model_id to ModelMonitoringObjectiveConfig.

## Attributes |
|
|---|---|
Name |
Description |
`deployed_model_id` |
`str`
The DeployedModel ID of the objective config. |
`objective_config` |
The objective config of for the modelmonitoring job of this deployed model. |

## Methods

### ModelDeploymentMonitoringObjectiveConfig

```
ModelDeploymentMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringObjectiveConfig contains the pair of deployed_model_id to ModelMonitoringObjectiveConfig.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesRequest -->

# Class ListRagFilesRequest (1.134.0)

`ListRagFilesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ListRagFiles.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the RagCorpus from which to list the RagFiles. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListRagFilesResponse.next_page_token of the previous VertexRagDataService.ListRagFiles call. |

## Methods

### ListRagFilesRequest

`ListRagFilesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ListRagFiles.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsRequest -->

# Class ListDataLabelingJobsRequest (1.134.0)

`ListDataLabelingJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListDataLabelingJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. FieldMask represents a set of symbolic field paths. For example, the mask can be `paths: "name"` . The "name" here is a field in
DataLabelingJob. If this field is not set, all fields of the
DataLabelingJob are returned.
|
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order by default. Use `desc` after a field name
for descending.
|

## Methods

### ListDataLabelingJobsRequest

`ListDataLabelingJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListDataLabelingJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetection -->

# Class AutoMlImageObjectDetection (1.134.0)

`AutoMlImageObjectDetection(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

## Attributes |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |
`metadata` |
The metadata information |

## Methods

### AutoMlImageObjectDetection

`AutoMlImageObjectDetection(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

### AutoMlImageObjectDetection

`AutoMlImageObjectDetection(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesRequest -->

# Class ListReasoningEnginesRequest (1.134.0)

`ListReasoningEnginesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ReasoningEngineService.ListReasoningEngines.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the ReasoningEngines from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. The standard list filter. More detail in `AIP-160 ` __.
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |

## Methods

### ListReasoningEnginesRequest

`ListReasoningEnginesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ReasoningEngineService.ListReasoningEngines.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportModelEvaluationSlicesRequest -->

# Class BatchImportModelEvaluationSlicesRequest (1.134.0)

```
BatchImportModelEvaluationSlicesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.BatchImportModelEvaluationSlices

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the parent ModelEvaluation resource. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}`
|
`model_evaluation_slices` |
`MutableSequence[`
Required. Model evaluation slice resource to be imported. |

## Methods

### BatchImportModelEvaluationSlicesRequest

```
BatchImportModelEvaluationSlicesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.BatchImportModelEvaluationSlices

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TrainingConfig -->

# Class TrainingConfig (1.134.0)

`TrainingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems.

## Attribute |
|
|---|---|
Name |
Description |
`timeout_training_milli_hours` |
`int`
The timeout hours for the CMLE training job, expressed in milli hours i.e. 1,000 value in this field means 1 hour. |

## Methods

### TrainingConfig

`TrainingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelRequest -->

# Class ExportModelRequest (1.134.0)

`ExportModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ExportModel.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Model to export. The resource name may contain version id or version alias to specify the version, if no version is specified, the default version will be exported. |
`output_config` |
Required. The desired output location and configuration. |

## Classes

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output configuration for the Model export.

## Methods

### ExportModelRequest

`ExportModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ExportModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tensor.DataType -->

# Class DataType (1.134.0)

`DataType(value)`


Data type of the tensor.

## Enums |
|
|---|---|
Name |
Description |
`DATA_TYPE_UNSPECIFIED` |
Not a legal value for DataType. Used to indicate a DataType field has not been set. |
`BOOL` |
Data types that all computation devices are expected to be capable to support. |
`STRING` |
No description available. |
`FLOAT` |
No description available. |
`DOUBLE` |
No description available. |
`INT8` |
No description available. |
`INT16` |
No description available. |
`INT32` |
No description available. |
`INT64` |
No description available. |
`UINT8` |
No description available. |
`UINT16` |
No description available. |
`UINT32` |
No description available. |
`UINT64` |
No description available. |

## Methods

### DataType

`DataType(value)`


Data type of the tensor.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.CategoricalTransformation -->

# Class CategoricalTransformation (1.134.0)

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


## Methods

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsRequest -->

# Class ListFeatureViewSyncsRequest (1.134.0)

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureView to list FeatureViewSyncs. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|
`filter` |
`str`
Lists the FeatureViewSyncs that match the filter expression. The following filters are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
Examples:
- `create_time > \"2020-01-31T15:30:00.000000Z\"` -->
FeatureViewSyncs created after
2020-01-31T15:30:00.000000Z.
|
`page_size` |
`int`
The maximum number of FeatureViewSyncs to return. The service may return fewer than this value. If unspecified, at most 1000 FeatureViewSyncs will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeatureOnlineStoreAdminService.ListFeatureViewSyncs call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeatureOnlineStoreAdminService.ListFeatureViewSyncs must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `create_time`
|

## Methods

### ListFeatureViewSyncsRequest

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchPredictionJob.OutputConfig -->

# Class OutputConfig (1.134.0)

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the output of BatchPredictionJob. See Model.supported_output_storage_formats for supported output formats, and how predictions are expressed via any of them.

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
`gcs_destination` |
The Cloud Storage location of the directory where the output is to be written to. In the given directory a new directory is created. Its name is `prediction-` , where
timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601 format.
Inside of it files `predictions_0001.` ,
`predictions_0002.` , ...,
`predictions_N.` are created where
depends on chosen
predictions_format,
and N may equal 0001 and depends on the total number of
successfully predicted instances. If the Model has both
instance
and
prediction
schemata defined then each such file contains predictions as
per the
predictions_format.
If prediction for any instance failed (partially or
completely), then an additional `errors_0001.` ,
`errors_0002.` ,..., `errors_N.`
files are created (N depends on total number of failed
predictions). These files contain the failed instances, as
per their schema, followed by an additional `error` field
which as value has `google.rpc.Status][google.rpc.Status]`
containing only `code` and `message` fields.
This field is a member of `oneof` _ `destination` .
|
`bigquery_destination` |
The BigQuery project or dataset location where the output is to be written to. If project is provided, a new dataset is created with name `prediction_` where
is made BigQuery-dataset-name compatible (for example, most
special characters become underscores), and timestamp is in
YYYY_MM_DDThh_mm_ss_sssZ "based on ISO-8601" format. In the
dataset two tables will be created, `predictions` , and
`errors` . If the Model has both
instance
and
prediction
schemata defined then the tables have columns as follows:
The `predictions` table contains instances for which the
prediction succeeded, it has columns as per a concatenation
of the Model's instance and prediction schemata. The
`errors` table contains rows for which the prediction has
failed, it has instance columns, as per the instance schema,
followed by a single "errors" column, which as values has
`google.rpc.Status][google.rpc.Status]` represented as a
STRUCT, and containing only `code` and `message` .
This field is a member of `oneof` _ `destination` .
|
`predictions_format` |
`str`
Required. The format in which Vertex AI gives the predictions, must be one of the [Model's][google.cloud.aiplatform.v1.BatchPredictionJob.model] supported_output_storage_formats. |

## Methods

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the output of BatchPredictionJob. See Model.supported_output_storage_formats for supported output formats, and how predictions are expressed via any of them.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExamplesArrayFilter -->

# Class ExamplesArrayFilter (1.134.0)

`ExamplesArrayFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Filters for examples' array metadata fields. An array field is example metadata where multiple values are attributed to a single example.

## Attributes |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[str]`
Required. The values by which to filter examples. |
`array_operator` |
Required. The operator logic to use for filtering. |

## Classes

### ArrayOperator

`ArrayOperator(value)`


The logic to use for filtering.

## Methods

### ExamplesArrayFilter

`ExamplesArrayFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Filters for examples' array metadata fields. An array field is example metadata where multiple values are attributed to a single example.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryExtensionRequest -->

# Class QueryExtensionRequest (1.134.0)

`QueryExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionExecutionService.QueryExtension.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. Name (identifier) of the extension; Format: `projects/{project}/locations/{location}/extensions/{extension}`
|
`contents` |
`MutableSequence[`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. |

## Methods

### QueryExtensionRequest

`QueryExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionExecutionService.QueryExtension.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoObjectTrackingPredictionResult.Frame -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineTemplateMetadata -->

# Class PipelineTemplateMetadata (1.134.0)

`PipelineTemplateMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pipeline template metadata if PipelineJob.template_uri is from supported template registry. Currently, the only supported registry is Artifact Registry.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`str`
The version_name in artifact registry. Will always be presented in output if the PipelineJob.template_uri is from supported template registry. Format is "sha256:abcdef123456...". |

## Methods

### PipelineTemplateMetadata

`PipelineTemplateMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pipeline template metadata if PipelineJob.template_uri is from supported template registry. Currently, the only supported registry is Artifact Registry.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSpecialistPoolRequest -->

# Class DeleteSpecialistPoolRequest (1.134.0)

`DeleteSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.DeleteSpecialistPool.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the SpecialistPool to delete. Format: `projects/{project}/locations/{location}/specialistPools/{specialist_pool}`
|
`force` |
`bool`
If set to true, any specialist managers in this SpecialistPool will also be deleted. (Otherwise, the request will only work if the SpecialistPool has no specialist managers.) |

## Methods

### DeleteSpecialistPoolRequest

`DeleteSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.DeleteSpecialistPool.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsRequest -->

# Class ListDataLabelingJobsRequest (1.134.0)

`ListDataLabelingJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListDataLabelingJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. FieldMask represents a set of symbolic field paths. For example, the mask can be `paths: "name"` . The "name" here is a field in
DataLabelingJob. If this field is not set, all fields of the
DataLabelingJob are returned.
|
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order by default. Use `desc` after a field name
for descending.
|

## Methods

### ListDataLabelingJobsRequest

`ListDataLabelingJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListDataLabelingJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SavedQuery -->

# Class SavedQuery (1.134.0)

`SavedQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A SavedQuery is a view of the dataset. It references a subset of annotations by problem type and filters.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the SavedQuery. |
`display_name` |
`str`
Required. The user-defined name of the SavedQuery. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Some additional information about the SavedQuery. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this SavedQuery was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when SavedQuery was last updated. |
`annotation_filter` |
`str`
Output only. Filters on the Annotations in the dataset. |
`problem_type` |
`str`
Required. Problem type of the SavedQuery. Allowed values: - IMAGE_CLASSIFICATION_SINGLE_LABEL - IMAGE_CLASSIFICATION_MULTI_LABEL - IMAGE_BOUNDING_POLY - IMAGE_BOUNDING_BOX - TEXT_CLASSIFICATION_SINGLE_LABEL - TEXT_CLASSIFICATION_MULTI_LABEL - TEXT_EXTRACTION - TEXT_SENTIMENT - VIDEO_CLASSIFICATION - VIDEO_OBJECT_TRACKING |
`annotation_spec_count` |
`int`
Output only. Number of AnnotationSpecs in the context of the SavedQuery. |
`etag` |
`str`
Used to perform a consistent read-modify-write update. If not set, a blind "overwrite" update happens. |
`support_automl_training` |
`bool`
Output only. If the Annotations belonging to the SavedQuery can be used for AutoML training. |

## Methods

### SavedQuery

`SavedQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A SavedQuery is a view of the dataset. It references a subset of annotations by problem type and filters.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service -->

# Package reasoning_engine_service (1.134.0)

API documentation for `aiplatform_v1.services.reasoning_engine_service`

package.

## Classes

[ReasoningEngineServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient)

A service for managing Vertex AI's Reasoning Engines.

[ReasoningEngineServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient)

A service for managing Vertex AI's Reasoning Engines.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.pagers)

API documentation for `aiplatform_v1.services.reasoning_engine_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborQuery.NumericFilter.Operator -->

# Class Operator (1.134.0)

`Operator(value)`


Datapoints for which Operator is true relative to the query's Value field will be allowlisted.

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


Datapoints for which Operator is true relative to the query's Value field will be allowlisted.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesResponse -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ManualBatchTuningParameters -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.CategoricalTransformation -->

# Class CategoricalTransformation (1.134.0)

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

## Methods

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoActionRecognition -->

# Class AutoMlVideoActionRecognition (1.134.0)

```
AutoMlVideoActionRecognition(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


A TrainingJob that trains and uploads an AutoML Video Action Recognition Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlVideoActionRecognition

```
AutoMlVideoActionRecognition(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


A TrainingJob that trains and uploads an AutoML Video Action Recognition Model.

### AutoMlVideoActionRecognition

```
AutoMlVideoActionRecognition(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


A TrainingJob that trains and uploads an AutoML Video Action Recognition Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringObjectiveConfig -->

# Class ModelDeploymentMonitoringObjectiveConfig (1.134.0)

```
ModelDeploymentMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringObjectiveConfig contains the pair of deployed_model_id to ModelMonitoringObjectiveConfig.

## Attributes |
|
|---|---|
Name |
Description |
`deployed_model_id` |
`str`
The DeployedModel ID of the objective config. |
`objective_config` |
The objective config of for the modelmonitoring job of this deployed model. |

## Methods

### ModelDeploymentMonitoringObjectiveConfig

```
ModelDeploymentMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringObjectiveConfig contains the pair of deployed_model_id to ModelMonitoringObjectiveConfig.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DirectRawPredictRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesRequest -->

# Class ListReasoningEnginesRequest (1.134.0)

`ListReasoningEnginesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ReasoningEngineService.ListReasoningEngines.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the ReasoningEngines from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. The standard list filter. More detail in `AIP-160 ` __.
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |

## Methods

### ListReasoningEnginesRequest

`ListReasoningEnginesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ReasoningEngineService.ListReasoningEngines.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchPredictionJob.OutputConfig -->

# Class OutputConfig (1.134.0)

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the output of BatchPredictionJob. See Model.supported_output_storage_formats for supported output formats, and how predictions are expressed via any of them.

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
`gcs_destination` |
The Cloud Storage location of the directory where the output is to be written to. In the given directory a new directory is created. Its name is `prediction-` , where
timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601 format.
Inside of it files `predictions_0001.` ,
`predictions_0002.` , ...,
`predictions_N.` are created where
depends on chosen
predictions_format,
and N may equal 0001 and depends on the total number of
successfully predicted instances. If the Model has both
instance
and
prediction
schemata defined then each such file contains predictions as
per the
predictions_format.
If prediction for any instance failed (partially or
completely), then an additional `errors_0001.` ,
`errors_0002.` ,..., `errors_N.`
files are created (N depends on total number of failed
predictions). These files contain the failed instances, as
per their schema, followed by an additional `error` field
which as value has `google.rpc.Status][google.rpc.Status]`
containing only `code` and `message` fields.
This field is a member of `oneof` _ `destination` .
|
`bigquery_destination` |
The BigQuery project or dataset location where the output is to be written to. If project is provided, a new dataset is created with name `prediction_` where
is made BigQuery-dataset-name compatible (for example, most
special characters become underscores), and timestamp is in
YYYY_MM_DDThh_mm_ss_sssZ "based on ISO-8601" format. In the
dataset two tables will be created, `predictions` , and
`errors` . If the Model has both
instance
and
prediction
schemata defined then the tables have columns as follows:
The `predictions` table contains instances for which the
prediction succeeded, it has columns as per a concatenation
of the Model's instance and prediction schemata. The
`errors` table contains rows for which the prediction has
failed, it has instance columns, as per the instance schema,
followed by a single "errors" column, which as values has
`google.rpc.Status][google.rpc.Status]` represented as a
STRUCT, and containing only `code` and `message` .
This field is a member of `oneof` _ `destination` .
|
`predictions_format` |
`str`
Required. The format in which Vertex AI gives the predictions, must be one of the [Model's][google.cloud.aiplatform.v1beta1.BatchPredictionJob.model] supported_output_storage_formats. |

## Methods

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the output of BatchPredictionJob. See Model.supported_output_storage_formats for supported output formats, and how predictions are expressed via any of them.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SavedQuery -->

# Class SavedQuery (1.134.0)

`SavedQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A SavedQuery is a view of the dataset. It references a subset of annotations by problem type and filters.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the SavedQuery. |
`display_name` |
`str`
Required. The user-defined name of the SavedQuery. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Some additional information about the SavedQuery. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this SavedQuery was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when SavedQuery was last updated. |
`annotation_filter` |
`str`
Output only. Filters on the Annotations in the dataset. |
`problem_type` |
`str`
Required. Problem type of the SavedQuery. Allowed values: - IMAGE_CLASSIFICATION_SINGLE_LABEL - IMAGE_CLASSIFICATION_MULTI_LABEL - IMAGE_BOUNDING_POLY - IMAGE_BOUNDING_BOX - TEXT_CLASSIFICATION_SINGLE_LABEL - TEXT_CLASSIFICATION_MULTI_LABEL - TEXT_EXTRACTION - TEXT_SENTIMENT - VIDEO_CLASSIFICATION - VIDEO_OBJECT_TRACKING |
`annotation_spec_count` |
`int`
Output only. Number of AnnotationSpecs in the context of the SavedQuery. |
`etag` |
`str`
Used to perform a consistent read-modify-write update. If not set, a blind "overwrite" update happens. |
`support_automl_training` |
`bool`
Output only. If the Annotations belonging to the SavedQuery can be used for AutoML training. |

## Methods

### SavedQuery

`SavedQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A SavedQuery is a view of the dataset. It references a subset of annotations by problem type and filters.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service -->

# Package index_endpoint_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.index_endpoint_service`

package.

## Classes

[IndexEndpointServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient)

A service for managing Vertex AI's IndexEndpoints.

[IndexEndpointServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient)

A service for managing Vertex AI's IndexEndpoints.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers)

API documentation for `aiplatform_v1beta1.services.index_endpoint_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchImportEvaluatedAnnotationsRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EventActions -->

# Class EventActions (1.134.0)

`EventActions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions are parts of events that are executed by the agent.

## Attributes |
|
|---|---|
Name |
Description |
`skip_summarization` |
`bool`
Optional. If true, it won't call model to summarize function response. Only used for function_response event. |
`state_delta` |
`google.protobuf.struct_pb2.Struct`
Optional. Indicates that the event is updating the state with the given delta. |
`artifact_delta` |
`MutableMapping[str, int]`
Optional. Indicates that the event is updating an artifact. key is the filename, value is the version. |
`escalate` |
`bool`
Optional. The agent is escalating to a higher level agent. |
`requested_auth_configs` |
`google.protobuf.struct_pb2.Struct`
Optional. Will only be set by a tool response indicating tool request euc. Struct key is the function call id since one function call response (from model) could correspond to multiple function calls. Struct value is the required auth config, which can be another struct. |
`transfer_agent` |
`str`
Optional. If set, the event transfers to the specified agent. |

## Classes

### ArtifactDeltaEntry

`ArtifactDeltaEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### EventActions

`EventActions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions are parts of events that are executed by the agent.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportModelRequest -->

# Class ExportModelRequest (1.134.0)

`ExportModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ExportModel.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Model to export. The resource name may contain version id or version alias to specify the version, if no version is specified, the default version will be exported. |
`output_config` |
Required. The desired output location and configuration. |

## Classes

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output configuration for the Model export.

## Methods

### ExportModelRequest

`ExportModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ExportModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrainingConfig -->

# Class TrainingConfig (1.134.0)

`TrainingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems.

## Attribute |
|
|---|---|
Name |
Description |
`timeout_training_milli_hours` |
`int`
The timeout hours for the CMLE training job, expressed in milli hours i.e. 1,000 value in this field means 1 hour. |

## Methods

### TrainingConfig

`TrainingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagContexts.Context -->

# Class Context (1.134.0)

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A context of the query.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`source_uri` |
`str`
If the file is imported from Cloud Storage or Google Drive, source_uri will be original file URI in Cloud Storage or Google Drive; if file is uploaded, source_uri will be file display name. |
`source_display_name` |
`str`
The file display name. |
`text` |
`str`
The text chunk. |
`distance` |
`float`
The distance between the query dense embedding vector and the context text vector. |
`sparse_distance` |
`float`
The distance between the query sparse embedding vector and the context text vector. |
`score` |
`float`
According to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the context and its range depends on the metric type. For example, if the metric type is COSINE_DISTANCE, it represents the distance between the query and the context. The larger the distance, the less relevant the context is to the query. The range is [0, 2], while 0 means the most relevant and 2 means the least relevant. This field is a member of `oneof` _ `_score` .
|
`chunk` |
Context of the retrieved chunk. |

## Methods

### Context

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A context of the query.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service -->

# Package example_store_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.example_store_service`

package.

## Classes

[ExampleStoreServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient)

A service for managing and retrieving few-shot examples.

[ExampleStoreServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceClient)

A service for managing and retrieving few-shot examples.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers)

API documentation for `aiplatform_v1beta1.services.example_store_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTemplateMetadata -->

# Class PipelineTemplateMetadata (1.134.0)

`PipelineTemplateMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pipeline template metadata if PipelineJob.template_uri is from supported template registry. Currently, the only supported registry is Artifact Registry.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`str`
The version_name in artifact registry. Will always be presented in output if the PipelineJob.template_uri is from supported template registry. Format is "sha256:abcdef123456...". |

## Methods

### PipelineTemplateMetadata

`PipelineTemplateMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pipeline template metadata if PipelineJob.template_uri is from supported template registry. Currently, the only supported registry is Artifact Registry.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient -->

# Class PipelineServiceAsyncClient (1.134.0)

```
PipelineServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's pipelines. This
includes both `TrainingPipeline`

resources (used for AutoML and
custom training) and `PipelineJob`

resources (used for Vertex AI
Pipelines).

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
`PipelineServiceTransport` |
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

### PipelineServiceAsyncClient

```
PipelineServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the pipeline service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PipelineServiceTransport,Callable[..., PipelineServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the PipelineServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### artifact_path

```
artifact_path(
project: str, location: str, metadata_store: str, artifact: str
) -> str
```


Returns a fully-qualified artifact string.

### batch_cancel_pipeline_jobs

```
batch_cancel_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.BatchCancelPipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch cancel PipelineJobs. Firstly the server will check if all the jobs are in non-terminal states, and skip the jobs that are already terminated. If the operation failed, none of the pipeline jobs are cancelled. The server will poll the states of all the pipeline jobs periodically to check the cancellation status. This operation will return an LRO.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_batch_cancel_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchCancelPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_cancel_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_batch_cancel_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchCancelPipelineJobs. |
`parent` |
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`:class:`
Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: |
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
An object representing a long-running operation. The result type for the operation will be
|

### batch_delete_pipeline_jobs

```
batch_delete_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.BatchDeletePipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch deletes PipelineJobs The Operation is atomic. If it fails, none of the PipelineJobs are deleted. If it succeeds, all of the PipelineJobs are deleted.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_batch_delete_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchDeletePipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchDeletePipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_delete_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_batch_delete_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchDeletePipelineJobs. |
`parent` |
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`:class:`
Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: |
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
An object representing a long-running operation. The result type for the operation will be
|

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

### cancel_pipeline_job

```
cancel_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CancelPipelineJobRequest,
dict,
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


Cancels a PipelineJob. Starts asynchronous cancellation on the
PipelineJob. The server makes a best effort to cancel the
pipeline, but success is not guaranteed. Clients can use
xref_PipelineService.GetPipelineJob
or other methods to check whether the cancellation succeeded or
whether the pipeline completed despite cancellation. On
successful cancellation, the PipelineJob is not deleted; instead
it becomes a pipeline with a
xref_PipelineJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_PipelineJob.state
is set to `CANCELLED`

.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_cancel_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelPipelineJobRequest.html)(
name="name_value",
)
# Make the request
await client.[cancel_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_cancel_pipeline_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.CancelPipelineJob. |
`name` |
Required. The name of the PipelineJob to cancel. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_training_pipeline

```
cancel_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CancelTrainingPipelineRequest,
dict,
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


Cancels a TrainingPipeline. Starts asynchronous cancellation on
the TrainingPipeline. The server makes a best effort to cancel
the pipeline, but success is not guaranteed. Clients can use
xref_PipelineService.GetTrainingPipeline
or other methods to check whether the cancellation succeeded or
whether the pipeline completed despite cancellation. On
successful cancellation, the TrainingPipeline is not deleted;
instead it becomes a pipeline with a
xref_TrainingPipeline.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_TrainingPipeline.state
is set to `CANCELLED`

.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_cancel_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
await client.[cancel_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_cancel_training_pipeline)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.CancelTrainingPipeline. |
`name` |
Required. The name of the TrainingPipeline to cancel. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
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

### context_path

`context_path(project: str, location: str, metadata_store: str, context: str) -> str`


Returns a fully-qualified context string.

### create_pipeline_job

```
create_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CreatePipelineJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
pipeline_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.pipeline_job.PipelineJob
] = None,
pipeline_job_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.pipeline_job.PipelineJob
```


Creates a PipelineJob. A PipelineJob will run immediately when created.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreatePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePipelineJobRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_create_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.CreatePipelineJob. |
`parent` |
Required. The resource name of the Location to create the PipelineJob in. Format: |
`pipeline_job` |
Required. The PipelineJob to create. This corresponds to the |
`pipeline_job_id` |
The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated. This value should be less than 128 characters, and valid characters are |
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
An instance of a machine learning PipelineJob. |

### create_training_pipeline

```
create_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CreateTrainingPipelineRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
training_pipeline: typing.Optional[
google.cloud.aiplatform_v1beta1.types.training_pipeline.TrainingPipeline
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.training_pipeline.TrainingPipeline
```


Creates a TrainingPipeline. A created TrainingPipeline right away will be attempted to be run.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
training_pipeline = aiplatform_v1beta1.[TrainingPipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrainingPipeline.html)()
training_pipeline.display_name = "display_name_value"
training_pipeline.training_task_definition = "training_task_definition_value"
training_pipeline.training_task_inputs.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[CreateTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTrainingPipelineRequest.html)(
parent="parent_value",
training_pipeline=training_pipeline,
)
# Make the request
response = await client.[create_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_create_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.CreateTrainingPipeline. |
`parent` |
Required. The resource name of the Location to create the TrainingPipeline in. Format: |
`training_pipeline` |
Required. The TrainingPipeline to create. This corresponds to the |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

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

### delete_pipeline_job

```
delete_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.DeletePipelineJobRequest,
dict,
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
) -> google.api_core.operation_async.AsyncOperation
```


Deletes a PipelineJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeletePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePipelineJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_delete_pipeline_job)(request=request)
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
The request object. Request message for PipelineService.DeletePipelineJob. |
`name` |
Required. The name of the PipelineJob resource to be deleted. Format: |
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
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_training_pipeline

```
delete_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.DeleteTrainingPipelineRequest,
dict,
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
) -> google.api_core.operation_async.AsyncOperation
```


Deletes a TrainingPipeline.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_delete_training_pipeline)(request=request)
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
The request object. Request message for PipelineService.DeleteTrainingPipeline. |
`name` |
Required. The name of the TrainingPipeline resource to be deleted. Format: |
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
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### execution_path

```
execution_path(
project: str, location: str, metadata_store: str, execution: str
) -> str
```


Returns a fully-qualified execution string.

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
`PipelineServiceAsyncClient` |
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
`PipelineServiceAsyncClient` |
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
`PipelineServiceAsyncClient` |
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

### get_pipeline_job

```
get_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.GetPipelineJobRequest,
dict,
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
) -> google.cloud.aiplatform_v1beta1.types.pipeline_job.PipelineJob
```


Gets a PipelineJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPipelineJobRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_get_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.GetPipelineJob. |
`name` |
Required. The name of the PipelineJob resource. Format: |
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
An instance of a machine learning PipelineJob. |

### get_training_pipeline

```
get_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.GetTrainingPipelineRequest,
dict,
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
) -> google.cloud.aiplatform_v1beta1.types.training_pipeline.TrainingPipeline
```


Gets a TrainingPipeline.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_get_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.GetTrainingPipeline. |
`name` |
Required. The name of the TrainingPipeline resource. Format: |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport
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

### list_pipeline_jobs

```
list_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsRequest,
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
) -> (
google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListPipelineJobsAsyncPager
)
```


Lists PipelineJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_list_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.ListPipelineJobs. |
`parent` |
Required. The resource name of the Location to list the PipelineJobs from. Format: |
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
Response message for PipelineService.ListPipelineJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_training_pipelines

```
list_training_pipelines(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesRequest,
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
) -> (
google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesAsyncPager
)
```


Lists TrainingPipelines in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_training_pipelines():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTrainingPipelinesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_training_pipelines](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_list_training_pipelines)(request=request)
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
The request object. Request message for PipelineService.ListTrainingPipelines. |
`parent` |
Required. The resource name of the Location to list the TrainingPipelines from. Format: |
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
Response message for PipelineService.ListTrainingPipelines Iterating over this object will yield results and resolve additional pages automatically. |

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### parse_artifact_path

`parse_artifact_path(path: str) -> typing.Dict[str, str]`


Parses a artifact path into its component segments.

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

### parse_context_path

`parse_context_path(path: str) -> typing.Dict[str, str]`


Parses a context path into its component segments.

### parse_custom_job_path

`parse_custom_job_path(path: str) -> typing.Dict[str, str]`


Parses a custom_job path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_training_pipeline_path

`parse_training_pipeline_path(path: str) -> typing.Dict[str, str]`


Parses a training_pipeline path into its component segments.

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

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

### training_pipeline_path

`training_pipeline_path(project: str, location: str, training_pipeline: str) -> str`


Returns a fully-qualified training_pipeline string.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient -->

# Class VizierServiceClient (1.134.0)

```
VizierServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### VizierServiceClient

```
VizierServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vizier service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the VizierServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### add_trial_measurement

```
add_trial_measurement(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.AddTrialMeasurementRequest,
dict,
]
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
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
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
from google.cloud import aiplatform_v1beta1
def sample_add_trial_measurement():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AddTrialMeasurementRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddTrialMeasurementRequest.html)(
trial_name="trial_name_value",
)
# Make the request
response = client.[add_trial_measurement](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_add_trial_measurement)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.AddTrialMeasurement. |
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

### check_trial_early_stopping_state

```
check_trial_early_stopping_state(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.CheckTrialEarlyStoppingStateRequest,
dict,
]
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
) -> google.api_core.operation.Operation
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
from google.cloud import aiplatform_v1beta1
def sample_check_trial_early_stopping_state():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CheckTrialEarlyStoppingStateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckTrialEarlyStoppingStateRequest.html)(
trial_name="trial_name_value",
)
# Make the request
operation = client.[check_trial_early_stopping_state](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_check_trial_early_stopping_state)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CheckTrialEarlyStoppingState. |
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
`google.api_core.operation.Operation` |
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
google.cloud.aiplatform_v1beta1.types.vizier_service.CompleteTrialRequest,
dict,
]
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
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
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
from google.cloud import aiplatform_v1beta1
def sample_complete_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CompleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CompleteTrialRequest.html)(
name="name_value",
)
# Make the request
response = client.[complete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_complete_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CompleteTrial. |
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
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### create_study

```
create_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.CreateStudyRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
study: typing.Optional[google.cloud.aiplatform_v1beta1.types.study.Study] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Study
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
from google.cloud import aiplatform_v1beta1
def sample_create_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
study = aiplatform_v1beta1.[Study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Study.html)()
study.display_name = "display_name_value"
study.study_spec.metrics.metric_id = "metric_id_value"
study.study_spec.metrics.goal = "MINIMIZE"
study.study_spec.parameters.double_value_spec.min_value = 0.96
study.study_spec.parameters.double_value_spec.max_value = 0.962
study.study_spec.parameters.parameter_id = "parameter_id_value"
request = aiplatform_v1beta1.[CreateStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateStudyRequest.html)(
parent="parent_value",
study=study,
)
# Make the request
response = client.[create_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_create_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CreateStudy. |
`parent` |
`str`
Required. The resource name of the Location to create the CustomJob in. Format: |
`study` |
Required. The Study configuration used to create the Study. This corresponds to the |
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
A message representing a Study. |

### create_trial

```
create_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.CreateTrialRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
trial: typing.Optional[google.cloud.aiplatform_v1beta1.types.study.Trial] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
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
from google.cloud import aiplatform_v1beta1
def sample_create_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTrialRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_create_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CreateTrial. |
`parent` |
`str`
Required. The resource name of the Study to create the Trial in. Format: |
`trial` |
Required. The Trial to create. This corresponds to the |
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

### delete_study

```
delete_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.DeleteStudyRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
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


Deletes a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteStudyRequest.html)(
name="name_value",
)
# Make the request
client.[delete_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_delete_study)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.DeleteStudy. |
`name` |
`str`
Required. The name of the Study resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
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
google.cloud.aiplatform_v1beta1.types.vizier_service.DeleteTrialRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
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


Deletes a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTrialRequest.html)(
name="name_value",
)
# Make the request
client.[delete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_delete_trial)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.DeleteTrial. |
`name` |
`str`
Required. The Trial's name. Format: |
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
`VizierServiceClient` |
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
`VizierServiceClient` |
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
`VizierServiceClient` |
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

### get_study

```
get_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.GetStudyRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Study
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
from google.cloud import aiplatform_v1beta1
def sample_get_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetStudyRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_get_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.GetStudy. |
`name` |
`str`
Required. The name of the Study resource. Format: |
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
A message representing a Study. |

### get_trial

```
get_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.GetTrialRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
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
from google.cloud import aiplatform_v1beta1
def sample_get_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTrialRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_get_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.GetTrial. |
`name` |
`str`
Required. The name of the Trial resource. Format: |
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

### list_optimal_trials

```
list_optimal_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListOptimalTrialsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.vizier_service.ListOptimalTrialsResponse
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
from google.cloud import aiplatform_v1beta1
def sample_list_optimal_trials():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListOptimalTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListOptimalTrialsRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[list_optimal_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_list_optimal_trials)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.ListOptimalTrials. |
`parent` |
`str`
Required. The name of the Study that the optimal Trial belongs to. This corresponds to the |
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
Response message for VizierService.ListOptimalTrials. |

### list_studies

```
list_studies(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListStudiesPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_studies():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListStudiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_studies](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_list_studies)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.ListStudies. |
`parent` |
`str`
Required. The resource name of the Location to list the Study from. Format: |
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
Response message for VizierService.ListStudies. Iterating over this object will yield results and resolve additional pages automatically. |

### list_trials

```
list_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListTrialsPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_trials():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_list_trials)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.ListTrials. |
`parent` |
`str`
Required. The resource name of the Study to list the Trial from. Format: |
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
Response message for VizierService.ListTrials. Iterating over this object will yield results and resolve additional pages automatically. |

### lookup_study

```
lookup_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.LookupStudyRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Study
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
from google.cloud import aiplatform_v1beta1
def sample_lookup_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[LookupStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LookupStudyRequest.html)(
parent="parent_value",
display_name="display_name_value",
)
# Make the request
response = client.[lookup_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_lookup_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.LookupStudy. |
`parent` |
`str`
Required. The resource name of the Location to get the Study from. Format: |
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

### stop_trial

```
stop_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.StopTrialRequest, dict
]
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
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
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
from google.cloud import aiplatform_v1beta1
def sample_stop_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StopTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopTrialRequest.html)(
name="name_value",
)
# Make the request
response = client.[stop_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_stop_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.StopTrial. |
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
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### study_path

`study_path(project: str, location: str, study: str) -> str`


Returns a fully-qualified study string.

### suggest_trials

```
suggest_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.SuggestTrialsRequest,
dict,
]
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
) -> google.api_core.operation.Operation
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
from google.cloud import aiplatform_v1beta1
def sample_suggest_trials():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SuggestTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SuggestTrialsRequest.html)(
parent="parent_value",
suggestion_count=1744,
client_id="client_id_value",
)
# Make the request
operation = client.[suggest_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_suggest_trials)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.SuggestTrials. |
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
`google.api_core.operation.Operation` |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TabularDataset -->

# Class TabularDataset (1.135.0)

```
TabularDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


A managed tabular dataset resource for Vertex AI.

Use this class to work with tabular datasets. You can use a CSV file, BigQuery, or a pandas
[ DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html)
to create a tabular dataset. For more information about paging through
BigQuery data, see

[Read data with BigQuery API using pagination](https://cloud.google.com/bigquery/docs/paging-results). For more information about tabular data, see

[Tabular data](https://cloud.google.com/vertex-ai/docs/training-overview#tabular_data).

The following code shows you how to create and import a tabular dataset with a CSV file.

```
my_dataset = aiplatform.TabularDataset.create(
display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])
```


Contrary to unstructured datasets, creating and importing a tabular dataset can only be done in a single step.

If you create a tabular dataset with a pandas
[ DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html),
you need to use a BigQuery table to stage the data for Vertex AI:

```
my_dataset = aiplatform.TabularDataset.create_from_dataframe(
df_source=my_pandas_dataframe,
staging_path=f"bq://{bq_dataset_id}.table-unique"
)
```


## Properties

### column_names

Retrieve the columns for the dataset by extracting it from the Google Cloud Storage or Google BigQuery source.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
When no valid source is found. |

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

### metadata_schema_uri

The metadata schema uri of this dataset resource.

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### TabularDataset

```
TabularDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed dataset given a dataset name or ID.

Parameters |
|
|---|---|
Name |
Description |
`dataset_name` |
`str`
Required. A fully-qualified dataset resource name or dataset ID. Example: "projects/123/locations/us-central1/datasets/456" or "456" when project and location are initialized or passed. |
`project` |
`str`
Optional project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to retrieve this Dataset. Overrides credentials set in aiplatform.init. |

### create

```
create(
display_name: typing.Optional[str] = None,
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
bq_source: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.tabular_dataset.TabularDataset
```


Creates a tabular dataset.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the dataset. The name must contain 128 or fewer UTF-8 characters. |
`gcs_source` |
`Union[str, Sequence[str]]`
Optional. The URI to one or more Google Cloud Storage buckets that contain your datasets. For example, |
`bq_source` |
`str`
Optional. The URI to a BigQuery table that's used as an input source. For example, |
`project` |
`str`
Optional. The name of the Google Cloud project to which this |
`location` |
`str`
Optional. The Google Cloud region where this dataset is uploaded. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload the |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings that contain metadata that's sent with the request. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Vertex AI Tensorboards. The maximum length of a key and of a value is 64 unicode characters. Labels and keys can contain only lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (system labels are excluded). For more information and examples of using labels, see |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key that's used to protect the dataset. The format of the key is |
`sync` |
`bool`
If |
`create_request_timeout` |
`float`
Optional. The number of seconds for the timeout of the create request. |

Returns |
|
|---|---|
Type |
Description |
`tabular_dataset (TabularDataset)` |
An instantiated representation of the managed `TabularDataset` resource. |

### create_from_dataframe

```
create_from_dataframe(
df_source: pd.DataFrame,
staging_path: str,
bq_schema: typing.Optional[typing.Union[str, bigquery.SchemaField]] = None,
display_name: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> TabularDataset
```


Creates a new tabular dataset from a pandas `DataFrame`

.

Parameters |
|
|---|---|
Name |
Description |
`df_source` |
`pd.DataFrame`
Required. A pandas `TabularDataset` . This method uses the data types from the provided `DataFrame` when the `TabularDataset` is created. |
`staging_path` |
`str`
Required. The BigQuery table used to stage the data for Vertex AI. Because Vertex AI maintains a reference to this source to create the |
`bq_schema` |
`Optional[Union[str, bigquery.SchemaField]]`
Optional. If not set, BigQuery autodetects the schema using the column types of your |
`display_name` |
`str`
Optional. The user-defined name of the |
`project` |
`str`
Optional. The project to upload this dataset to. This overrides the project set using |
`location` |
`str`
Optional. The location to upload this dataset to. This overrides the location set using |
`credentials` |
`auth_credentials.Credentials`
Optional. The custom credentials used to upload this dataset. This overrides credentials set using |

Returns |
|
|---|---|
Type |
Description |
`tabular_dataset (TabularDataset)` |
An instantiated representation of the managed `TabularDataset` resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### export_data

`export_data(output_dir: str) -> typing.Sequence[str]`


Exports data to output dir to GCS.

Parameter |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |

Returns |
|
|---|---|
Type |
Description |
`exported_files (Sequence[str])` |
All of the files that are exported in this export operation. |

### export_data_for_custom_training

```
export_data_for_custom_training(
output_dir: str,
annotation_filter: typing.Optional[str] = None,
saved_query_id: typing.Optional[str] = None,
annotation_schema_uri: typing.Optional[str] = None,
split: typing.Optional[
typing.Union[typing.Dict[str, str], typing.Dict[str, float]]
] = None,
) -> typing.Dict[str, typing.Any]
```


Exports data to output dir to GCS for custom training use case.

Example annotation_schema_uri (image classification): gs://google-cloud-aiplatform/schema/dataset/annotation/image_classification_1.0.0.yaml

Example split (filter split): { "training_filter": "labels.aiplatform.googleapis.com/ml_use=training", "validation_filter": "labels.aiplatform.googleapis.com/ml_use=validation", "test_filter": "labels.aiplatform.googleapis.com/ml_use=test", } Example split (fraction split): { "training_fraction": 0.7, "validation_fraction": 0.2, "test_fraction": 0.1, }

Parameters |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |
`annotation_filter` |
`str`
Optional. An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in |
`saved_query_id` |
`str`
Optional. The ID of a SavedQuery (annotation set) under this Dataset used for filtering Annotations for training. Only used for custom training data export use cases. Only applicable to Datasets that have SavedQueries. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`annotation_schema_uri` |
`str`
Optional. The Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/annotation/, note that the chosen schema must be consistent with metadata_schema_uri of this Dataset. Only used for custom training data export use cases. Only applicable if this Dataset that have DataItems and Annotations. Only Annotations that both match this schema and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both annotations_filter and annotation_schema_uri. |
`split` |
`Union[Dict[str, str], Dict[str, float]]`
The instructions how the export data should be split between the training, validation and test sets. |

Returns |
|
|---|---|
Type |
Description |
`export_data_response (Dict)` |
Response message for DatasetService.ExportData in Dictionary format. |

### import_data

`import_data()`


Upload data to existing managed dataset.

Parameters |
|
|---|---|
Name |
Description |
`gcs_source` |
`Union[str, Sequence[str]]`
Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see |
`import_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing the import format. Validation will be done against the schema. The schema is defined as an |
`data_item_labels` |
`Dict`
Labels that will be applied to newly imported DataItems. If an identical DataItem as one being imported already exists in the Dataset, then these labels will be appended to these of the already existing one, and if labels with identical key is imported before, the old label value will be overwritten. If two DataItems are identical in the same import data operation, the labels will be combined and if key collision happens in this case, one of the values will be picked randomly. Two DataItems are considered identical if their content bytes are identical (e.g. image bytes or pdf bytes). These labels will be overridden by Annotation labels specified inside index file referenced by |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`import_request_timeout` |
`float`
Optional. The timeout for the import request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Instantiated representation of the managed dataset resource. |

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


List all instances of this Dataset resource.

Example Usage:

aiplatform.TabularDataset.list( filter='labels.my_key="my_value"', order_by='display_name' )

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

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
*,
display_name: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
description: typing.Optional[str] = None,
update_request_timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.datasets.dataset._Dataset
```


Update the dataset. Updatable fields:

`display_name`

`description`

`labels`


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the Dataset. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See |
`description` |
`str`
Optional. The description of the Dataset. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Updated dataset. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Feature.MonitoringStatsAnomaly.Objective -->

# Class Objective (1.135.0)

`Objective(value)`


If the objective in the request is both Import Feature Analysis and Snapshot Analysis, this objective could be one of them. Otherwise, this objective should be the same as the objective in the request.

## Enums |
|
|---|---|
Name |
Description |
`OBJECTIVE_UNSPECIFIED` |
If it's OBJECTIVE_UNSPECIFIED, monitoring_stats will be empty. |
`IMPORT_FEATURE_ANALYSIS` |
Stats are generated by Import Feature Analysis. |
`SNAPSHOT_ANALYSIS` |
Stats are generated by Snapshot Analysis. |

## Methods

### Objective

`Objective(value)`


If the objective in the request is both Import Feature Analysis and Snapshot Analysis, this objective could be one of them. Otherwise, this objective should be the same as the objective in the request.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchImportModelEvaluationSlicesRequest -->

# Class BatchImportModelEvaluationSlicesRequest (1.135.0)

```
BatchImportModelEvaluationSlicesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.BatchImportModelEvaluationSlices

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the parent ModelEvaluation resource. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}`
|
`model_evaluation_slices` |
`MutableSequence[`
Required. Model evaluation slice resource to be imported. |

## Methods

### BatchImportModelEvaluationSlicesRequest

```
BatchImportModelEvaluationSlicesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.BatchImportModelEvaluationSlices

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tensor.DataType -->

# Class DataType (1.135.0)

`DataType(value)`


Data type of the tensor.

## Enums |
|
|---|---|
Name |
Description |
`DATA_TYPE_UNSPECIFIED` |
Not a legal value for DataType. Used to indicate a DataType field has not been set. |
`BOOL` |
Data types that all computation devices are expected to be capable to support. |
`STRING` |
No description available. |
`FLOAT` |
No description available. |
`DOUBLE` |
No description available. |
`INT8` |
No description available. |
`INT16` |
No description available. |
`INT32` |
No description available. |
`INT64` |
No description available. |
`UINT8` |
No description available. |
`UINT16` |
No description available. |
`UINT32` |
No description available. |
`UINT64` |
No description available. |

## Methods

### DataType

`DataType(value)`


Data type of the tensor.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateSpecialistPoolOperationMetadata -->

# Class UpdateSpecialistPoolOperationMetadata (1.135.0)

```
UpdateSpecialistPoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation metadata for SpecialistPoolService.UpdateSpecialistPool.

## Attributes |
|
|---|---|
Name |
Description |
`specialist_pool` |
`str`
Output only. The name of the SpecialistPool to which the specialists are being added. Format: `projects/{project_id}/locations/{location_id}/specialistPools/{specialist_pool}`
|
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateSpecialistPoolOperationMetadata

```
UpdateSpecialistPoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation metadata for SpecialistPoolService.UpdateSpecialistPool.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VeoTuningSpec -->

# Class VeoTuningSpec (1.135.0)

`VeoTuningSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning Spec for Veo Model Tuning.

## Attributes |
|
|---|---|
Name |
Description |
`training_dataset_uri` |
`str`
Required. Training dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset. |
`validation_dataset_uri` |
`str`
Optional. Validation dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset. |
`hyper_parameters` |
Optional. Hyperparameters for Veo. |

## Methods

### VeoTuningSpec

`VeoTuningSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning Spec for Veo Model Tuning.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteSpecialistPoolRequest -->

# Class DeleteSpecialistPoolRequest (1.135.0)

`DeleteSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.DeleteSpecialistPool.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the SpecialistPool to delete. Format: `projects/{project}/locations/{location}/specialistPools/{specialist_pool}`
|
`force` |
`bool`
If set to true, any specialist managers in this SpecialistPool will also be deleted. (Otherwise, the request will only work if the SpecialistPool has no specialist managers.) |

## Methods

### DeleteSpecialistPoolRequest

`DeleteSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.DeleteSpecialistPool.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeArtifact -->

# Class RuntimeArtifact (1.135.0)

`RuntimeArtifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of a runtime artifact.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The name of an artifact. |
`type_` |
The type of the artifact. |
`uri` |
`str`
The URI of the artifact. |
`properties` |
`MutableMapping[str, `
The properties of the artifact. Deprecated. Use RuntimeArtifact.metadata instead. |
`custom_properties` |
`MutableMapping[str, `
The custom properties of the artifact. Deprecated. Use RuntimeArtifact.metadata instead. |
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Artifact. |

## Classes

### CustomPropertiesEntry

`CustomPropertiesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### PropertiesEntry

`PropertiesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### RuntimeArtifact

`RuntimeArtifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of a runtime artifact.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesRequest -->

# Class BatchReadFeatureValuesRequest (1.135.0)

```
BatchReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreService.BatchReadFeatureValues.

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
`csv_read_instances` |
Each read instance consists of exactly one read timestamp and one or more entity IDs identifying entities of the corresponding EntityTypes whose Features are requested. Each output instance contains Feature values of requested entities concatenated together as of the read time. An example read instance may be `foo_entity_id, bar_entity_id, 2020-01-01T10:00:00.123Z` .
An example output instance may be
`foo_entity_id, bar_entity_id, 2020-01-01T10:00:00.123Z, foo_entity_feature1_value, bar_entity_feature2_value` .
Timestamp in each read instance must be millisecond-aligned.
`csv_read_instances` are read instances stored in a
plain-text CSV file. The header should be:
[ENTITY_TYPE_ID1], [ENTITY_TYPE_ID2], ..., timestamp
The columns can be in any order.
Values in the timestamp column must use the RFC 3339 format,
e.g. `2012-07-30T10:43:17.123Z` .
This field is a member of `oneof` _ `read_option` .
|
`bigquery_read_instances` |
Similar to csv_read_instances, but from BigQuery source. This field is a member of `oneof` _ `read_option` .
|
`featurestore` |
`str`
Required. The resource name of the Featurestore from which to query Feature values. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`destination` |
Required. Specifies output location and format. |
`pass_through_fields` |
`MutableSequence[`
When not empty, the specified fields in the \*_read_instances source will be joined as-is in the output, in addition to those fields from the Featurestore Entity. For BigQuery source, the type of the pass-through values will be automatically inferred. For CSV source, the pass-through values will be passed as opaque bytes. |
`entity_type_specs` |
`MutableSequence[`
Required. Specifies EntityType grouping Features to read values of and settings. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Excludes Feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in Feature Store. Timestamp, if present, must not have higher than millisecond precision. |

## Classes

### EntityTypeSpec

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

### PassThroughField

`PassThroughField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describe pass-through fields in read_instance source.

## Methods

### BatchReadFeatureValuesRequest

```
BatchReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreService.BatchReadFeatureValues.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service -->

# Package featurestore_service (1.135.0)

API documentation for `aiplatform_v1.services.featurestore_service`

package.

## Classes

[FeaturestoreServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient)

The service that handles CRUD and List for resources for Featurestore.

[FeaturestoreServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient)

The service that handles CRUD and List for resources for Featurestore.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers)

API documentation for `aiplatform_v1.services.featurestore_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service -->

# Package gen_ai_tuning_service (1.135.0)

API documentation for `aiplatform_v1beta1.services.gen_ai_tuning_service`

package.

## Classes

[GenAiTuningServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient)

A service for creating and managing GenAI Tuning Jobs.

[GenAiTuningServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient)

A service for creating and managing GenAI Tuning Jobs.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.pagers)

API documentation for `aiplatform_v1beta1.services.gen_ai_tuning_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsRequest -->

# Class ListFeatureViewSyncsRequest (1.135.0)

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureView to list FeatureViewSyncs. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|
`filter` |
`str`
Lists the FeatureViewSyncs that match the filter expression. The following filters are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
Examples:
- `create_time > \"2020-01-31T15:30:00.000000Z\"` -->
FeatureViewSyncs created after
2020-01-31T15:30:00.000000Z.
|
`page_size` |
`int`
The maximum number of FeatureViewSyncs to return. The service may return fewer than this value. If unspecified, at most 1000 FeatureViewSyncs will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeatureOnlineStoreAdminService.ListFeatureViewSyncs call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeatureOnlineStoreAdminService.ListFeatureViewSyncs must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `create_time`
|

## Methods

### ListFeatureViewSyncsRequest

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesRequest -->

# Class BatchReadFeatureValuesRequest (1.135.0)

```
BatchReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreService.BatchReadFeatureValues.

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
`csv_read_instances` |
Each read instance consists of exactly one read timestamp and one or more entity IDs identifying entities of the corresponding EntityTypes whose Features are requested. Each output instance contains Feature values of requested entities concatenated together as of the read time. An example read instance may be `foo_entity_id, bar_entity_id, 2020-01-01T10:00:00.123Z` .
An example output instance may be
`foo_entity_id, bar_entity_id, 2020-01-01T10:00:00.123Z, foo_entity_feature1_value, bar_entity_feature2_value` .
Timestamp in each read instance must be millisecond-aligned.
`csv_read_instances` are read instances stored in a
plain-text CSV file. The header should be:
[ENTITY_TYPE_ID1], [ENTITY_TYPE_ID2], ..., timestamp
The columns can be in any order.
Values in the timestamp column must use the RFC 3339 format,
e.g. `2012-07-30T10:43:17.123Z` .
This field is a member of `oneof` _ `read_option` .
|
`bigquery_read_instances` |
Similar to csv_read_instances, but from BigQuery source. This field is a member of `oneof` _ `read_option` .
|
`featurestore` |
`str`
Required. The resource name of the Featurestore from which to query Feature values. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`destination` |
Required. Specifies output location and format. |
`pass_through_fields` |
`MutableSequence[`
When not empty, the specified fields in the \*_read_instances source will be joined as-is in the output, in addition to those fields from the Featurestore Entity. For BigQuery source, the type of the pass-through values will be automatically inferred. For CSV source, the pass-through values will be passed as opaque bytes. |
`entity_type_specs` |
`MutableSequence[`
Required. Specifies EntityType grouping Features to read values of and settings. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Excludes Feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in Feature Store. Timestamp, if present, must not have higher than millisecond precision. |

## Classes

### EntityTypeSpec

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

### PassThroughField

`PassThroughField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describe pass-through fields in read_instance source.

## Methods

### BatchReadFeatureValuesRequest

```
BatchReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreService.BatchReadFeatureValues.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.CategoricalTransformation -->

# Class CategoricalTransformation (1.135.0)

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

## Methods

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringObjectiveConfig -->

# Class ModelDeploymentMonitoringObjectiveConfig (1.135.0)

```
ModelDeploymentMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringObjectiveConfig contains the pair of deployed_model_id to ModelMonitoringObjectiveConfig.

## Attributes |
|
|---|---|
Name |
Description |
`deployed_model_id` |
`str`
The DeployedModel ID of the objective config. |
`objective_config` |
The objective config of for the modelmonitoring job of this deployed model. |

## Methods

### ModelDeploymentMonitoringObjectiveConfig

```
ModelDeploymentMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringObjectiveConfig contains the pair of deployed_model_id to ModelMonitoringObjectiveConfig.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesRequest -->

# Class ListRagFilesRequest (1.135.0)

`ListRagFilesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ListRagFiles.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the RagCorpus from which to list the RagFiles. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListRagFilesResponse.next_page_token of the previous VertexRagDataService.ListRagFiles call. |

## Methods

### ListRagFilesRequest

`ListRagFilesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ListRagFiles.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsRequest -->

# Class ListDataLabelingJobsRequest (1.135.0)

`ListDataLabelingJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListDataLabelingJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. FieldMask represents a set of symbolic field paths. For example, the mask can be `paths: "name"` . The "name" here is a field in
DataLabelingJob. If this field is not set, all fields of the
DataLabelingJob are returned.
|
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order by default. Use `desc` after a field name
for descending.
|

## Methods

### ListDataLabelingJobsRequest

`ListDataLabelingJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListDataLabelingJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetection -->

# Class AutoMlImageObjectDetection (1.135.0)

`AutoMlImageObjectDetection(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

## Attributes |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |
`metadata` |
The metadata information |

## Methods

### AutoMlImageObjectDetection

`AutoMlImageObjectDetection(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

### AutoMlImageObjectDetection

`AutoMlImageObjectDetection(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesRequest -->

# Class ListReasoningEnginesRequest (1.135.0)

`ListReasoningEnginesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ReasoningEngineService.ListReasoningEngines.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the ReasoningEngines from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. The standard list filter. More detail in `AIP-160 ` __.
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |

## Methods

### ListReasoningEnginesRequest

`ListReasoningEnginesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ReasoningEngineService.ListReasoningEngines.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportModelEvaluationSlicesRequest -->

# Class BatchImportModelEvaluationSlicesRequest (1.135.0)

```
BatchImportModelEvaluationSlicesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.BatchImportModelEvaluationSlices

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the parent ModelEvaluation resource. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}`
|
`model_evaluation_slices` |
`MutableSequence[`
Required. Model evaluation slice resource to be imported. |

## Methods

### BatchImportModelEvaluationSlicesRequest

```
BatchImportModelEvaluationSlicesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.BatchImportModelEvaluationSlices

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TrainingConfig -->

# Class TrainingConfig (1.135.0)

`TrainingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems.

## Attribute |
|
|---|---|
Name |
Description |
`timeout_training_milli_hours` |
`int`
The timeout hours for the CMLE training job, expressed in milli hours i.e. 1,000 value in this field means 1 hour. |

## Methods

### TrainingConfig

`TrainingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelRequest -->

# Class ExportModelRequest (1.135.0)

`ExportModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ExportModel.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Model to export. The resource name may contain version id or version alias to specify the version, if no version is specified, the default version will be exported. |
`output_config` |
Required. The desired output location and configuration. |

## Classes

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output configuration for the Model export.

## Methods

### ExportModelRequest

`ExportModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ExportModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tensor.DataType -->

# Class DataType (1.135.0)

`DataType(value)`


Data type of the tensor.

## Enums |
|
|---|---|
Name |
Description |
`DATA_TYPE_UNSPECIFIED` |
Not a legal value for DataType. Used to indicate a DataType field has not been set. |
`BOOL` |
Data types that all computation devices are expected to be capable to support. |
`STRING` |
No description available. |
`FLOAT` |
No description available. |
`DOUBLE` |
No description available. |
`INT8` |
No description available. |
`INT16` |
No description available. |
`INT32` |
No description available. |
`INT64` |
No description available. |
`UINT8` |
No description available. |
`UINT16` |
No description available. |
`UINT32` |
No description available. |
`UINT64` |
No description available. |

## Methods

### DataType

`DataType(value)`


Data type of the tensor.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.CategoricalTransformation -->

# Class CategoricalTransformation (1.135.0)

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


## Methods

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsRequest -->

# Class ListFeatureViewSyncsRequest (1.135.0)

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureView to list FeatureViewSyncs. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|
`filter` |
`str`
Lists the FeatureViewSyncs that match the filter expression. The following filters are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
Examples:
- `create_time > \"2020-01-31T15:30:00.000000Z\"` -->
FeatureViewSyncs created after
2020-01-31T15:30:00.000000Z.
|
`page_size` |
`int`
The maximum number of FeatureViewSyncs to return. The service may return fewer than this value. If unspecified, at most 1000 FeatureViewSyncs will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeatureOnlineStoreAdminService.ListFeatureViewSyncs call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeatureOnlineStoreAdminService.ListFeatureViewSyncs must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `create_time`
|

## Methods

### ListFeatureViewSyncsRequest

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchPredictionJob.OutputConfig -->

# Class OutputConfig (1.135.0)

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the output of BatchPredictionJob. See Model.supported_output_storage_formats for supported output formats, and how predictions are expressed via any of them.

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
`gcs_destination` |
The Cloud Storage location of the directory where the output is to be written to. In the given directory a new directory is created. Its name is `prediction-` , where
timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601 format.
Inside of it files `predictions_0001.` ,
`predictions_0002.` , ...,
`predictions_N.` are created where
depends on chosen
predictions_format,
and N may equal 0001 and depends on the total number of
successfully predicted instances. If the Model has both
instance
and
prediction
schemata defined then each such file contains predictions as
per the
predictions_format.
If prediction for any instance failed (partially or
completely), then an additional `errors_0001.` ,
`errors_0002.` ,..., `errors_N.`
files are created (N depends on total number of failed
predictions). These files contain the failed instances, as
per their schema, followed by an additional `error` field
which as value has `google.rpc.Status][google.rpc.Status]`
containing only `code` and `message` fields.
This field is a member of `oneof` _ `destination` .
|
`bigquery_destination` |
The BigQuery project or dataset location where the output is to be written to. If project is provided, a new dataset is created with name `prediction_` where
is made BigQuery-dataset-name compatible (for example, most
special characters become underscores), and timestamp is in
YYYY_MM_DDThh_mm_ss_sssZ "based on ISO-8601" format. In the
dataset two tables will be created, `predictions` , and
`errors` . If the Model has both
instance
and
prediction
schemata defined then the tables have columns as follows:
The `predictions` table contains instances for which the
prediction succeeded, it has columns as per a concatenation
of the Model's instance and prediction schemata. The
`errors` table contains rows for which the prediction has
failed, it has instance columns, as per the instance schema,
followed by a single "errors" column, which as values has
`google.rpc.Status][google.rpc.Status]` represented as a
STRUCT, and containing only `code` and `message` .
This field is a member of `oneof` _ `destination` .
|
`predictions_format` |
`str`
Required. The format in which Vertex AI gives the predictions, must be one of the [Model's][google.cloud.aiplatform.v1.BatchPredictionJob.model] supported_output_storage_formats. |

## Methods

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the output of BatchPredictionJob. See Model.supported_output_storage_formats for supported output formats, and how predictions are expressed via any of them.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExamplesArrayFilter -->

# Class ExamplesArrayFilter (1.135.0)

`ExamplesArrayFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Filters for examples' array metadata fields. An array field is example metadata where multiple values are attributed to a single example.

## Attributes |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[str]`
Required. The values by which to filter examples. |
`array_operator` |
Required. The operator logic to use for filtering. |

## Classes

### ArrayOperator

`ArrayOperator(value)`


The logic to use for filtering.

## Methods

### ExamplesArrayFilter

`ExamplesArrayFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Filters for examples' array metadata fields. An array field is example metadata where multiple values are attributed to a single example.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryExtensionRequest -->

# Class QueryExtensionRequest (1.135.0)

`QueryExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionExecutionService.QueryExtension.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. Name (identifier) of the extension; Format: `projects/{project}/locations/{location}/extensions/{extension}`
|
`contents` |
`MutableSequence[`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. |

## Methods

### QueryExtensionRequest

`QueryExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionExecutionService.QueryExtension.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoObjectTrackingPredictionResult.Frame -->

# Class Frame (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineTemplateMetadata -->

# Class PipelineTemplateMetadata (1.135.0)

`PipelineTemplateMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pipeline template metadata if PipelineJob.template_uri is from supported template registry. Currently, the only supported registry is Artifact Registry.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`str`
The version_name in artifact registry. Will always be presented in output if the PipelineJob.template_uri is from supported template registry. Format is "sha256:abcdef123456...". |

## Methods

### PipelineTemplateMetadata

`PipelineTemplateMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pipeline template metadata if PipelineJob.template_uri is from supported template registry. Currently, the only supported registry is Artifact Registry.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSpecialistPoolRequest -->

# Class DeleteSpecialistPoolRequest (1.135.0)

`DeleteSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.DeleteSpecialistPool.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the SpecialistPool to delete. Format: `projects/{project}/locations/{location}/specialistPools/{specialist_pool}`
|
`force` |
`bool`
If set to true, any specialist managers in this SpecialistPool will also be deleted. (Otherwise, the request will only work if the SpecialistPool has no specialist managers.) |

## Methods

### DeleteSpecialistPoolRequest

`DeleteSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.DeleteSpecialistPool.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsRequest -->

# Class ListDataLabelingJobsRequest (1.135.0)

`ListDataLabelingJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListDataLabelingJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. FieldMask represents a set of symbolic field paths. For example, the mask can be `paths: "name"` . The "name" here is a field in
DataLabelingJob. If this field is not set, all fields of the
DataLabelingJob are returned.
|
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order by default. Use `desc` after a field name
for descending.
|

## Methods

### ListDataLabelingJobsRequest

`ListDataLabelingJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListDataLabelingJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient -->

# Class PipelineServiceAsyncClient (1.135.0)

```
PipelineServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's pipelines. This
includes both `TrainingPipeline`

resources (used for AutoML and
custom training) and `PipelineJob`

resources (used for Vertex AI
Pipelines).

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
`PipelineServiceTransport` |
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

### PipelineServiceAsyncClient

```
PipelineServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the pipeline service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PipelineServiceTransport,Callable[..., PipelineServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the PipelineServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### artifact_path

```
artifact_path(
project: str, location: str, metadata_store: str, artifact: str
) -> str
```


Returns a fully-qualified artifact string.

### batch_cancel_pipeline_jobs

```
batch_cancel_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.BatchCancelPipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch cancel PipelineJobs. Firstly the server will check if all the jobs are in non-terminal states, and skip the jobs that are already terminated. If the operation failed, none of the pipeline jobs are cancelled. The server will poll the states of all the pipeline jobs periodically to check the cancellation status. This operation will return an LRO.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_batch_cancel_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchCancelPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_cancel_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_batch_cancel_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchCancelPipelineJobs. |
`parent` |
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`:class:`
Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: |
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
An object representing a long-running operation. The result type for the operation will be
|

### batch_delete_pipeline_jobs

```
batch_delete_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.BatchDeletePipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch deletes PipelineJobs The Operation is atomic. If it fails, none of the PipelineJobs are deleted. If it succeeds, all of the PipelineJobs are deleted.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_batch_delete_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchDeletePipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchDeletePipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_delete_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_batch_delete_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchDeletePipelineJobs. |
`parent` |
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`:class:`
Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: |
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
An object representing a long-running operation. The result type for the operation will be
|

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

### cancel_pipeline_job

```
cancel_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CancelPipelineJobRequest,
dict,
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


Cancels a PipelineJob. Starts asynchronous cancellation on the
PipelineJob. The server makes a best effort to cancel the
pipeline, but success is not guaranteed. Clients can use
xref_PipelineService.GetPipelineJob
or other methods to check whether the cancellation succeeded or
whether the pipeline completed despite cancellation. On
successful cancellation, the PipelineJob is not deleted; instead
it becomes a pipeline with a
xref_PipelineJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_PipelineJob.state
is set to `CANCELLED`

.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_cancel_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelPipelineJobRequest.html)(
name="name_value",
)
# Make the request
await client.[cancel_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_cancel_pipeline_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.CancelPipelineJob. |
`name` |
Required. The name of the PipelineJob to cancel. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_training_pipeline

```
cancel_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CancelTrainingPipelineRequest,
dict,
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


Cancels a TrainingPipeline. Starts asynchronous cancellation on
the TrainingPipeline. The server makes a best effort to cancel
the pipeline, but success is not guaranteed. Clients can use
xref_PipelineService.GetTrainingPipeline
or other methods to check whether the cancellation succeeded or
whether the pipeline completed despite cancellation. On
successful cancellation, the TrainingPipeline is not deleted;
instead it becomes a pipeline with a
xref_TrainingPipeline.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_TrainingPipeline.state
is set to `CANCELLED`

.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_cancel_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
await client.[cancel_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_cancel_training_pipeline)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.CancelTrainingPipeline. |
`name` |
Required. The name of the TrainingPipeline to cancel. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
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

### context_path

`context_path(project: str, location: str, metadata_store: str, context: str) -> str`


Returns a fully-qualified context string.

### create_pipeline_job

```
create_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CreatePipelineJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
pipeline_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.pipeline_job.PipelineJob
] = None,
pipeline_job_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.pipeline_job.PipelineJob
```


Creates a PipelineJob. A PipelineJob will run immediately when created.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreatePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePipelineJobRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_create_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.CreatePipelineJob. |
`parent` |
Required. The resource name of the Location to create the PipelineJob in. Format: |
`pipeline_job` |
Required. The PipelineJob to create. This corresponds to the |
`pipeline_job_id` |
The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated. This value should be less than 128 characters, and valid characters are |
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
An instance of a machine learning PipelineJob. |

### create_training_pipeline

```
create_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.CreateTrainingPipelineRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
training_pipeline: typing.Optional[
google.cloud.aiplatform_v1beta1.types.training_pipeline.TrainingPipeline
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.training_pipeline.TrainingPipeline
```


Creates a TrainingPipeline. A created TrainingPipeline right away will be attempted to be run.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
training_pipeline = aiplatform_v1beta1.[TrainingPipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrainingPipeline.html)()
training_pipeline.display_name = "display_name_value"
training_pipeline.training_task_definition = "training_task_definition_value"
training_pipeline.training_task_inputs.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[CreateTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTrainingPipelineRequest.html)(
parent="parent_value",
training_pipeline=training_pipeline,
)
# Make the request
response = await client.[create_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_create_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.CreateTrainingPipeline. |
`parent` |
Required. The resource name of the Location to create the TrainingPipeline in. Format: |
`training_pipeline` |
Required. The TrainingPipeline to create. This corresponds to the |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

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

### delete_pipeline_job

```
delete_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.DeletePipelineJobRequest,
dict,
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
) -> google.api_core.operation_async.AsyncOperation
```


Deletes a PipelineJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeletePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePipelineJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_delete_pipeline_job)(request=request)
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
The request object. Request message for PipelineService.DeletePipelineJob. |
`name` |
Required. The name of the PipelineJob resource to be deleted. Format: |
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
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_training_pipeline

```
delete_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.DeleteTrainingPipelineRequest,
dict,
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
) -> google.api_core.operation_async.AsyncOperation
```


Deletes a TrainingPipeline.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_delete_training_pipeline)(request=request)
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
The request object. Request message for PipelineService.DeleteTrainingPipeline. |
`name` |
Required. The name of the TrainingPipeline resource to be deleted. Format: |
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
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### execution_path

```
execution_path(
project: str, location: str, metadata_store: str, execution: str
) -> str
```


Returns a fully-qualified execution string.

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
`PipelineServiceAsyncClient` |
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
`PipelineServiceAsyncClient` |
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
`PipelineServiceAsyncClient` |
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

### get_pipeline_job

```
get_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.GetPipelineJobRequest,
dict,
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
) -> google.cloud.aiplatform_v1beta1.types.pipeline_job.PipelineJob
```


Gets a PipelineJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPipelineJobRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_get_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.GetPipelineJob. |
`name` |
Required. The name of the PipelineJob resource. Format: |
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
An instance of a machine learning PipelineJob. |

### get_training_pipeline

```
get_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.GetTrainingPipelineRequest,
dict,
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
) -> google.cloud.aiplatform_v1beta1.types.training_pipeline.TrainingPipeline
```


Gets a TrainingPipeline.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_get_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PipelineService.GetTrainingPipeline. |
`name` |
Required. The name of the TrainingPipeline resource. Format: |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.pipeline_service.transports.base.PipelineServiceTransport
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

### list_pipeline_jobs

```
list_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsRequest,
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
) -> (
google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListPipelineJobsAsyncPager
)
```


Lists PipelineJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_list_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.ListPipelineJobs. |
`parent` |
Required. The resource name of the Location to list the PipelineJobs from. Format: |
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
Response message for PipelineService.ListPipelineJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_training_pipelines

```
list_training_pipelines(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesRequest,
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
) -> (
google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesAsyncPager
)
```


Lists TrainingPipelines in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_training_pipelines():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTrainingPipelinesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_training_pipelines](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceAsyncClient_list_training_pipelines)(request=request)
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
The request object. Request message for PipelineService.ListTrainingPipelines. |
`parent` |
Required. The resource name of the Location to list the TrainingPipelines from. Format: |
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
Response message for PipelineService.ListTrainingPipelines Iterating over this object will yield results and resolve additional pages automatically. |

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### parse_artifact_path

`parse_artifact_path(path: str) -> typing.Dict[str, str]`


Parses a artifact path into its component segments.

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

### parse_context_path

`parse_context_path(path: str) -> typing.Dict[str, str]`


Parses a context path into its component segments.

### parse_custom_job_path

`parse_custom_job_path(path: str) -> typing.Dict[str, str]`


Parses a custom_job path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_training_pipeline_path

`parse_training_pipeline_path(path: str) -> typing.Dict[str, str]`


Parses a training_pipeline path into its component segments.

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

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

### training_pipeline_path

`training_pipeline_path(project: str, location: str, training_pipeline: str) -> str`


Returns a fully-qualified training_pipeline string.

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SavedQuery -->

# Class SavedQuery (1.135.0)

`SavedQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A SavedQuery is a view of the dataset. It references a subset of annotations by problem type and filters.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the SavedQuery. |
`display_name` |
`str`
Required. The user-defined name of the SavedQuery. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Some additional information about the SavedQuery. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this SavedQuery was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when SavedQuery was last updated. |
`annotation_filter` |
`str`
Output only. Filters on the Annotations in the dataset. |
`problem_type` |
`str`
Required. Problem type of the SavedQuery. Allowed values: - IMAGE_CLASSIFICATION_SINGLE_LABEL - IMAGE_CLASSIFICATION_MULTI_LABEL - IMAGE_BOUNDING_POLY - IMAGE_BOUNDING_BOX - TEXT_CLASSIFICATION_SINGLE_LABEL - TEXT_CLASSIFICATION_MULTI_LABEL - TEXT_EXTRACTION - TEXT_SENTIMENT - VIDEO_CLASSIFICATION - VIDEO_OBJECT_TRACKING |
`annotation_spec_count` |
`int`
Output only. Number of AnnotationSpecs in the context of the SavedQuery. |
`etag` |
`str`
Used to perform a consistent read-modify-write update. If not set, a blind "overwrite" update happens. |
`support_automl_training` |
`bool`
Output only. If the Annotations belonging to the SavedQuery can be used for AutoML training. |

## Methods

### SavedQuery

`SavedQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A SavedQuery is a view of the dataset. It references a subset of annotations by problem type and filters.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service -->

# Package reasoning_engine_service (1.135.0)

API documentation for `aiplatform_v1.services.reasoning_engine_service`

package.

## Classes

[ReasoningEngineServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient)

A service for managing Vertex AI's Reasoning Engines.

[ReasoningEngineServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceClient)

A service for managing Vertex AI's Reasoning Engines.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.pagers)

API documentation for `aiplatform_v1.services.reasoning_engine_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborQuery.NumericFilter.Operator -->

# Class Operator (1.135.0)

`Operator(value)`


Datapoints for which Operator is true relative to the query's Value field will be allowlisted.

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


Datapoints for which Operator is true relative to the query's Value field will be allowlisted.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesResponse -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ManualBatchTuningParameters -->

# Class ManualBatchTuningParameters (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.CategoricalTransformation -->

# Class CategoricalTransformation (1.135.0)

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

## Methods

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoActionRecognition -->

# Class AutoMlVideoActionRecognition (1.135.0)

```
AutoMlVideoActionRecognition(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


A TrainingJob that trains and uploads an AutoML Video Action Recognition Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlVideoActionRecognition

```
AutoMlVideoActionRecognition(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


A TrainingJob that trains and uploads an AutoML Video Action Recognition Model.

### AutoMlVideoActionRecognition

```
AutoMlVideoActionRecognition(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


A TrainingJob that trains and uploads an AutoML Video Action Recognition Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringObjectiveConfig -->

# Class ModelDeploymentMonitoringObjectiveConfig (1.135.0)

```
ModelDeploymentMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringObjectiveConfig contains the pair of deployed_model_id to ModelMonitoringObjectiveConfig.

## Attributes |
|
|---|---|
Name |
Description |
`deployed_model_id` |
`str`
The DeployedModel ID of the objective config. |
`objective_config` |
The objective config of for the modelmonitoring job of this deployed model. |

## Methods

### ModelDeploymentMonitoringObjectiveConfig

```
ModelDeploymentMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringObjectiveConfig contains the pair of deployed_model_id to ModelMonitoringObjectiveConfig.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DirectRawPredictRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesRequest -->

# Class ListReasoningEnginesRequest (1.135.0)

`ListReasoningEnginesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ReasoningEngineService.ListReasoningEngines.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the ReasoningEngines from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. The standard list filter. More detail in `AIP-160 ` __.
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |

## Methods

### ListReasoningEnginesRequest

`ListReasoningEnginesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ReasoningEngineService.ListReasoningEngines.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchPredictionJob.OutputConfig -->

# Class OutputConfig (1.135.0)

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the output of BatchPredictionJob. See Model.supported_output_storage_formats for supported output formats, and how predictions are expressed via any of them.

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
`gcs_destination` |
The Cloud Storage location of the directory where the output is to be written to. In the given directory a new directory is created. Its name is `prediction-` , where
timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601 format.
Inside of it files `predictions_0001.` ,
`predictions_0002.` , ...,
`predictions_N.` are created where
depends on chosen
predictions_format,
and N may equal 0001 and depends on the total number of
successfully predicted instances. If the Model has both
instance
and
prediction
schemata defined then each such file contains predictions as
per the
predictions_format.
If prediction for any instance failed (partially or
completely), then an additional `errors_0001.` ,
`errors_0002.` ,..., `errors_N.`
files are created (N depends on total number of failed
predictions). These files contain the failed instances, as
per their schema, followed by an additional `error` field
which as value has `google.rpc.Status][google.rpc.Status]`
containing only `code` and `message` fields.
This field is a member of `oneof` _ `destination` .
|
`bigquery_destination` |
The BigQuery project or dataset location where the output is to be written to. If project is provided, a new dataset is created with name `prediction_` where
is made BigQuery-dataset-name compatible (for example, most
special characters become underscores), and timestamp is in
YYYY_MM_DDThh_mm_ss_sssZ "based on ISO-8601" format. In the
dataset two tables will be created, `predictions` , and
`errors` . If the Model has both
instance
and
prediction
schemata defined then the tables have columns as follows:
The `predictions` table contains instances for which the
prediction succeeded, it has columns as per a concatenation
of the Model's instance and prediction schemata. The
`errors` table contains rows for which the prediction has
failed, it has instance columns, as per the instance schema,
followed by a single "errors" column, which as values has
`google.rpc.Status][google.rpc.Status]` represented as a
STRUCT, and containing only `code` and `message` .
This field is a member of `oneof` _ `destination` .
|
`predictions_format` |
`str`
Required. The format in which Vertex AI gives the predictions, must be one of the [Model's][google.cloud.aiplatform.v1beta1.BatchPredictionJob.model] supported_output_storage_formats. |

## Methods

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the output of BatchPredictionJob. See Model.supported_output_storage_formats for supported output formats, and how predictions are expressed via any of them.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SavedQuery -->

# Class SavedQuery (1.135.0)

`SavedQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A SavedQuery is a view of the dataset. It references a subset of annotations by problem type and filters.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the SavedQuery. |
`display_name` |
`str`
Required. The user-defined name of the SavedQuery. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Some additional information about the SavedQuery. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this SavedQuery was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when SavedQuery was last updated. |
`annotation_filter` |
`str`
Output only. Filters on the Annotations in the dataset. |
`problem_type` |
`str`
Required. Problem type of the SavedQuery. Allowed values: - IMAGE_CLASSIFICATION_SINGLE_LABEL - IMAGE_CLASSIFICATION_MULTI_LABEL - IMAGE_BOUNDING_POLY - IMAGE_BOUNDING_BOX - TEXT_CLASSIFICATION_SINGLE_LABEL - TEXT_CLASSIFICATION_MULTI_LABEL - TEXT_EXTRACTION - TEXT_SENTIMENT - VIDEO_CLASSIFICATION - VIDEO_OBJECT_TRACKING |
`annotation_spec_count` |
`int`
Output only. Number of AnnotationSpecs in the context of the SavedQuery. |
`etag` |
`str`
Used to perform a consistent read-modify-write update. If not set, a blind "overwrite" update happens. |
`support_automl_training` |
`bool`
Output only. If the Annotations belonging to the SavedQuery can be used for AutoML training. |

## Methods

### SavedQuery

`SavedQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A SavedQuery is a view of the dataset. It references a subset of annotations by problem type and filters.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service -->

# Package index_endpoint_service (1.135.0)

API documentation for `aiplatform_v1beta1.services.index_endpoint_service`

package.

## Classes

[IndexEndpointServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient)

A service for managing Vertex AI's IndexEndpoints.

[IndexEndpointServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient)

A service for managing Vertex AI's IndexEndpoints.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers)

API documentation for `aiplatform_v1beta1.services.index_endpoint_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchImportEvaluatedAnnotationsRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EventActions -->

# Class EventActions (1.135.0)

`EventActions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions are parts of events that are executed by the agent.

## Attributes |
|
|---|---|
Name |
Description |
`skip_summarization` |
`bool`
Optional. If true, it won't call model to summarize function response. Only used for function_response event. |
`state_delta` |
`google.protobuf.struct_pb2.Struct`
Optional. Indicates that the event is updating the state with the given delta. |
`artifact_delta` |
`MutableMapping[str, int]`
Optional. Indicates that the event is updating an artifact. key is the filename, value is the version. |
`escalate` |
`bool`
Optional. The agent is escalating to a higher level agent. |
`requested_auth_configs` |
`google.protobuf.struct_pb2.Struct`
Optional. Will only be set by a tool response indicating tool request euc. Struct key is the function call id since one function call response (from model) could correspond to multiple function calls. Struct value is the required auth config, which can be another struct. |
`transfer_agent` |
`str`
Optional. If set, the event transfers to the specified agent. |

## Classes

### ArtifactDeltaEntry

`ArtifactDeltaEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### EventActions

`EventActions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions are parts of events that are executed by the agent.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportModelRequest -->

# Class ExportModelRequest (1.135.0)

`ExportModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ExportModel.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Model to export. The resource name may contain version id or version alias to specify the version, if no version is specified, the default version will be exported. |
`output_config` |
Required. The desired output location and configuration. |

## Classes

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output configuration for the Model export.

## Methods

### ExportModelRequest

`ExportModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ExportModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrainingConfig -->

# Class TrainingConfig (1.135.0)

`TrainingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems.

## Attribute |
|
|---|---|
Name |
Description |
`timeout_training_milli_hours` |
`int`
The timeout hours for the CMLE training job, expressed in milli hours i.e. 1,000 value in this field means 1 hour. |

## Methods

### TrainingConfig

`TrainingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagContexts.Context -->

# Class Context (1.135.0)

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A context of the query.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`source_uri` |
`str`
If the file is imported from Cloud Storage or Google Drive, source_uri will be original file URI in Cloud Storage or Google Drive; if file is uploaded, source_uri will be file display name. |
`source_display_name` |
`str`
The file display name. |
`text` |
`str`
The text chunk. |
`distance` |
`float`
The distance between the query dense embedding vector and the context text vector. |
`sparse_distance` |
`float`
The distance between the query sparse embedding vector and the context text vector. |
`score` |
`float`
According to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the context and its range depends on the metric type. For example, if the metric type is COSINE_DISTANCE, it represents the distance between the query and the context. The larger the distance, the less relevant the context is to the query. The range is [0, 2], while 0 means the most relevant and 2 means the least relevant. This field is a member of `oneof` _ `_score` .
|
`chunk` |
Context of the retrieved chunk. |

## Methods

### Context

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A context of the query.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service -->

# Package example_store_service (1.135.0)

API documentation for `aiplatform_v1beta1.services.example_store_service`

package.

## Classes

[ExampleStoreServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient)

A service for managing and retrieving few-shot examples.

[ExampleStoreServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceClient)

A service for managing and retrieving few-shot examples.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers)

API documentation for `aiplatform_v1beta1.services.example_store_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTemplateMetadata -->

# Class PipelineTemplateMetadata (1.135.0)

`PipelineTemplateMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pipeline template metadata if PipelineJob.template_uri is from supported template registry. Currently, the only supported registry is Artifact Registry.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`str`
The version_name in artifact registry. Will always be presented in output if the PipelineJob.template_uri is from supported template registry. Format is "sha256:abcdef123456...". |

## Methods

### PipelineTemplateMetadata

`PipelineTemplateMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pipeline template metadata if PipelineJob.template_uri is from supported template registry. Currently, the only supported registry is Artifact Registry.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult.Frame -->

# Class Frame (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ManualBatchTuningParameters -->

# Class ManualBatchTuningParameters (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob -->

# Class CustomPythonPackageTrainingJob (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient -->

# Class VizierServiceClient (1.135.0)

```
VizierServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### VizierServiceClient

```
VizierServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vizier_service.transports.base.VizierServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vizier service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the VizierServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### add_trial_measurement

```
add_trial_measurement(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.AddTrialMeasurementRequest,
dict,
]
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
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
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
from google.cloud import aiplatform_v1beta1
def sample_add_trial_measurement():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AddTrialMeasurementRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddTrialMeasurementRequest.html)(
trial_name="trial_name_value",
)
# Make the request
response = client.[add_trial_measurement](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_add_trial_measurement)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.AddTrialMeasurement. |
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

### check_trial_early_stopping_state

```
check_trial_early_stopping_state(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.CheckTrialEarlyStoppingStateRequest,
dict,
]
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
) -> google.api_core.operation.Operation
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
from google.cloud import aiplatform_v1beta1
def sample_check_trial_early_stopping_state():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CheckTrialEarlyStoppingStateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckTrialEarlyStoppingStateRequest.html)(
trial_name="trial_name_value",
)
# Make the request
operation = client.[check_trial_early_stopping_state](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_check_trial_early_stopping_state)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CheckTrialEarlyStoppingState. |
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
`google.api_core.operation.Operation` |
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
google.cloud.aiplatform_v1beta1.types.vizier_service.CompleteTrialRequest,
dict,
]
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
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
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
from google.cloud import aiplatform_v1beta1
def sample_complete_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CompleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CompleteTrialRequest.html)(
name="name_value",
)
# Make the request
response = client.[complete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_complete_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CompleteTrial. |
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
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### create_study

```
create_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.CreateStudyRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
study: typing.Optional[google.cloud.aiplatform_v1beta1.types.study.Study] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Study
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
from google.cloud import aiplatform_v1beta1
def sample_create_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
study = aiplatform_v1beta1.[Study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Study.html)()
study.display_name = "display_name_value"
study.study_spec.metrics.metric_id = "metric_id_value"
study.study_spec.metrics.goal = "MINIMIZE"
study.study_spec.parameters.double_value_spec.min_value = 0.96
study.study_spec.parameters.double_value_spec.max_value = 0.962
study.study_spec.parameters.parameter_id = "parameter_id_value"
request = aiplatform_v1beta1.[CreateStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateStudyRequest.html)(
parent="parent_value",
study=study,
)
# Make the request
response = client.[create_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_create_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CreateStudy. |
`parent` |
`str`
Required. The resource name of the Location to create the CustomJob in. Format: |
`study` |
Required. The Study configuration used to create the Study. This corresponds to the |
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
A message representing a Study. |

### create_trial

```
create_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.CreateTrialRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
trial: typing.Optional[google.cloud.aiplatform_v1beta1.types.study.Trial] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
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
from google.cloud import aiplatform_v1beta1
def sample_create_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTrialRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_create_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.CreateTrial. |
`parent` |
`str`
Required. The resource name of the Study to create the Trial in. Format: |
`trial` |
Required. The Trial to create. This corresponds to the |
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

### delete_study

```
delete_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.DeleteStudyRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
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


Deletes a Study.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteStudyRequest.html)(
name="name_value",
)
# Make the request
client.[delete_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_delete_study)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.DeleteStudy. |
`name` |
`str`
Required. The name of the Study resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
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
google.cloud.aiplatform_v1beta1.types.vizier_service.DeleteTrialRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
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


Deletes a Trial.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTrialRequest.html)(
name="name_value",
)
# Make the request
client.[delete_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_delete_trial)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.DeleteTrial. |
`name` |
`str`
Required. The Trial's name. Format: |
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
`VizierServiceClient` |
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
`VizierServiceClient` |
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
`VizierServiceClient` |
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

### get_study

```
get_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.GetStudyRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Study
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
from google.cloud import aiplatform_v1beta1
def sample_get_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetStudyRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_get_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.GetStudy. |
`name` |
`str`
Required. The name of the Study resource. Format: |
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
A message representing a Study. |

### get_trial

```
get_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.GetTrialRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
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
from google.cloud import aiplatform_v1beta1
def sample_get_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTrialRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_get_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.GetTrial. |
`name` |
`str`
Required. The name of the Trial resource. Format: |
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

### list_optimal_trials

```
list_optimal_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListOptimalTrialsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.vizier_service.ListOptimalTrialsResponse
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
from google.cloud import aiplatform_v1beta1
def sample_list_optimal_trials():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListOptimalTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListOptimalTrialsRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[list_optimal_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_list_optimal_trials)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.ListOptimalTrials. |
`parent` |
`str`
Required. The name of the Study that the optimal Trial belongs to. This corresponds to the |
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
Response message for VizierService.ListOptimalTrials. |

### list_studies

```
list_studies(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListStudiesPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_studies():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListStudiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_studies](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_list_studies)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.ListStudies. |
`parent` |
`str`
Required. The resource name of the Location to list the Study from. Format: |
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
Response message for VizierService.ListStudies. Iterating over this object will yield results and resolve additional pages automatically. |

### list_trials

```
list_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListTrialsPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_trials():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_list_trials)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.ListTrials. |
`parent` |
`str`
Required. The resource name of the Study to list the Trial from. Format: |
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
Response message for VizierService.ListTrials. Iterating over this object will yield results and resolve additional pages automatically. |

### lookup_study

```
lookup_study(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.LookupStudyRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.study.Study
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
from google.cloud import aiplatform_v1beta1
def sample_lookup_study():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[LookupStudyRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LookupStudyRequest.html)(
parent="parent_value",
display_name="display_name_value",
)
# Make the request
response = client.[lookup_study](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_lookup_study)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.LookupStudy. |
`parent` |
`str`
Required. The resource name of the Location to get the Study from. Format: |
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

### stop_trial

```
stop_trial(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.StopTrialRequest, dict
]
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
) -> google.cloud.aiplatform_v1beta1.types.study.Trial
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
from google.cloud import aiplatform_v1beta1
def sample_stop_trial():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StopTrialRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopTrialRequest.html)(
name="name_value",
)
# Make the request
response = client.[stop_trial](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_stop_trial)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.StopTrial. |
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
A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial. |

### study_path

`study_path(project: str, location: str, study: str) -> str`


Returns a fully-qualified study string.

### suggest_trials

```
suggest_trials(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vizier_service.SuggestTrialsRequest,
dict,
]
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
) -> google.api_core.operation.Operation
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
from google.cloud import aiplatform_v1beta1
def sample_suggest_trials():
# Create a client
client = aiplatform_v1beta1.
```[VizierServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SuggestTrialsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SuggestTrialsRequest.html)(
parent="parent_value",
suggestion_count=1744,
client_id="client_id_value",
)
# Make the request
operation = client.[suggest_trials](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient.html#google_cloud_aiplatform_v1beta1_services_vizier_service_VizierServiceClient_suggest_trials)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VizierService.SuggestTrials. |
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
`google.api_core.operation.Operation` |
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
