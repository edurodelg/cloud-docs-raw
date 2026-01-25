---
merged_at: 2026-01-25T21:47:44.404207
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesmigration_servicemigrationserviceclient_googl_0a63db.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesmigration_servicemigrationserviceclient_google_355d0b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmigration_servicemigrationserviceclient_googlec_b535f8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmigration_servicemigrationserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient -->

# Class MigrationServiceClient (1.134.0)

```
MigrationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service that migrates resources from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

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
`MigrationServiceTransport` |
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

### MigrationServiceClient

```
MigrationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the migration service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MigrationServiceTransport,Callable[..., MigrationServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MigrationServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### annotated_dataset_path

`annotated_dataset_path(project: str, dataset: str, annotated_dataset: str) -> str`


Returns a fully-qualified annotated_dataset string.

### batch_migrate_resources

```
batch_migrate_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.migration_service.BatchMigrateResourcesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
migrate_resource_requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.migration_service.MigrateResourceRequest
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
) -> google.api_core.operation.Operation
```


Batch migrates resources from ml.googleapis.com, automl.googleapis.com, and datalabeling.googleapis.com to Vertex AI.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_migrate_resources():
# Create a client
client = aiplatform_v1.
```[MigrationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html)()
# Initialize request argument(s)
migrate_resource_requests = aiplatform_v1.[MigrateResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest.html)()
migrate_resource_requests.migrate_ml_engine_model_version_config.endpoint = "endpoint_value"
migrate_resource_requests.migrate_ml_engine_model_version_config.model_version = "model_version_value"
migrate_resource_requests.migrate_ml_engine_model_version_config.model_display_name = "model_display_name_value"
request = aiplatform_v1.[BatchMigrateResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchMigrateResourcesRequest.html)(
parent="parent_value",
migrate_resource_requests=migrate_resource_requests,
)
# Make the request
operation = client.[batch_migrate_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html#google_cloud_aiplatform_v1_services_migration_service_MigrationServiceClient_batch_migrate_resources)(request=request)
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
The request object. Request message for MigrationService.BatchMigrateResources. |
`parent` |
`str`
Required. The location of the migrated resource will live in. Format: |
`migrate_resource_requests` |
`MutableSequence[`
Required. The request messages specifying the resources to migrate. They must be in the same location as the destination. Up to 50 resources can be migrated in one batch. This corresponds to the |
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

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

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
`MigrationServiceClient` |
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
`MigrationServiceClient` |
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
`MigrationServiceClient` |
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

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### parse_annotated_dataset_path

`parse_annotated_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a annotated_dataset path into its component segments.

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

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_version_path

`parse_version_path(path: str) -> typing.Dict[str, str]`


Parses a version path into its component segments.

### search_migratable_resources

```
search_migratable_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesRequest,
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
) -> (
google.cloud.aiplatform_v1.services.migration_service.pagers.SearchMigratableResourcesPager
)
```


Searches all of the resources in automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com that can be migrated to Vertex AI's given location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_search_migratable_resources():
# Create a client
client = aiplatform_v1.
```[MigrationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SearchMigratableResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[search_migratable_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html#google_cloud_aiplatform_v1_services_migration_service_MigrationServiceClient_search_migratable_resources)(request=request)
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
The request object. Request message for MigrationService.SearchMigratableResources. |
`parent` |
`str`
Required. The location that the migratable resources should be searched from. It's the Vertex AI location that the resources can be migrated to, not the resources' original location. Format: |
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
Response message for MigrationService.SearchMigratableResources. Iterating over this object will yield results and resolve additional pages automatically. |

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

### version_path

`version_path(project: str, model: str, version: str) -> str`


Returns a fully-qualified version string.

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesreasoning_engine_execution_servicereasoningengineexecutionserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient -->

# Class ReasoningEngineExecutionServiceAsyncClient (1.134.0)

```
ReasoningEngineExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for executing queries on Reasoning Engine.

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
`ReasoningEngineExecutionServiceTransport` |
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

### ReasoningEngineExecutionServiceAsyncClient

```
ReasoningEngineExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the reasoning engine execution service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ReasoningEngineExecutionServiceTransport,Callable[..., ReasoningEngineExecutionServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ReasoningEngineExecutionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport
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

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### query_reasoning_engine

```
query_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_execution_service.QueryReasoningEngineRequest,
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
) -> (
google.cloud.aiplatform_v1beta1.types.reasoning_engine_execution_service.QueryReasoningEngineResponse
)
```


Queries using a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_query_reasoning_engine():
# Create a client
client = aiplatform_v1beta1.
```[ReasoningEngineExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[QueryReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
response = await client.[query_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_reasoning_engine_execution_service_ReasoningEngineExecutionServiceAsyncClient_query_reasoning_engine)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [ReasoningEngineExecutionService.Query][]. |
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
Response message for [ReasoningEngineExecutionService.Query][] |

### reasoning_engine_path

`reasoning_engine_path(project: str, location: str, reasoning_engine: str) -> str`


Returns a fully-qualified reasoning_engine string.

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

### stream_query_reasoning_engine

```
stream_query_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_execution_service.StreamQueryReasoningEngineRequest,
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
) -> typing.Awaitable[typing.AsyncIterable[google.api.httpbody_pb2.HttpBody]]
```


Streams queries using a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_stream_query_reasoning_engine():
# Create a client
client = aiplatform_v1beta1.
```[ReasoningEngineExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamQueryReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamQueryReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
stream = await client.[stream_query_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_reasoning_engine_execution_service_ReasoningEngineExecutionServiceAsyncClient_stream_query_reasoning_engine)(request=request)
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [ReasoningEngineExecutionService.StreamQuery][]. |
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
`AsyncIterable[google.api.httpbody_pb2.HttpBody]` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicespipeline_servicepipelineserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient -->

# Class PipelineServiceClient (1.134.0)

```
PipelineServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### PipelineServiceClient

```
PipelineServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.pipeline_service.transports.base.PipelineServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the pipeline service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the PipelineServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.cloud.aiplatform_v1.types.pipeline_service.BatchCancelPipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch cancel PipelineJobs. Firstly the server will check if all the jobs are in non-terminal states, and skip the jobs that are already terminated. If the operation failed, none of the pipeline jobs are cancelled. The server will poll the states of all the pipeline jobs periodically to check the cancellation status. This operation will return an LRO.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_cancel_pipeline_jobs():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[BatchCancelPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCancelPipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_cancel_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_batch_cancel_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchCancelPipelineJobs. |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: |
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
An object representing a long-running operation. The result type for the operation will be
|

### batch_delete_pipeline_jobs

```
batch_delete_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.BatchDeletePipelineJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
names: typing.Optional[typing.MutableSequence[str]] = None,
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


Batch deletes PipelineJobs The Operation is atomic. If it fails, none of the PipelineJobs are deleted. If it succeeds, all of the PipelineJobs are deleted.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_delete_pipeline_jobs():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[BatchDeletePipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchDeletePipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_delete_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_batch_delete_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchDeletePipelineJobs. |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: |
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

### cancel_pipeline_job

```
cancel_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.CancelPipelineJobRequest,
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
from google.cloud import aiplatform_v1
def sample_cancel_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelPipelineJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_cancel_pipeline_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CancelPipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
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
google.cloud.aiplatform_v1.types.pipeline_service.CancelTrainingPipelineRequest,
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
from google.cloud import aiplatform_v1
def sample_cancel_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_cancel_training_pipeline)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CancelTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline to cancel. Format: |
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

### context_path

`context_path(project: str, location: str, metadata_store: str, context: str) -> str`


Returns a fully-qualified context string.

### create_pipeline_job

```
create_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.CreatePipelineJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
pipeline_job: typing.Optional[
google.cloud.aiplatform_v1.types.pipeline_job.PipelineJob
] = None,
pipeline_job_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.pipeline_job.PipelineJob
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
from google.cloud import aiplatform_v1
def sample_create_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreatePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreatePipelineJobRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_create_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CreatePipelineJob. |
`parent` |
`str`
Required. The resource name of the Location to create the PipelineJob in. Format: |
`pipeline_job` |
Required. The PipelineJob to create. This corresponds to the |
`pipeline_job_id` |
`str`
The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated. This value should be less than 128 characters, and valid characters are |
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
An instance of a machine learning PipelineJob. |

### create_training_pipeline

```
create_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.CreateTrainingPipelineRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
training_pipeline: typing.Optional[
google.cloud.aiplatform_v1.types.training_pipeline.TrainingPipeline
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.training_pipeline.TrainingPipeline
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
from google.cloud import aiplatform_v1
def sample_create_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
training_pipeline = aiplatform_v1.[TrainingPipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TrainingPipeline.html)()
training_pipeline.display_name = "display_name_value"
training_pipeline.training_task_definition = "training_task_definition_value"
training_pipeline.training_task_inputs.null_value = "NULL_VALUE"
request = aiplatform_v1.[CreateTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTrainingPipelineRequest.html)(
parent="parent_value",
training_pipeline=training_pipeline,
)
# Make the request
response = client.[create_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_create_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CreateTrainingPipeline. |
`parent` |
`str`
Required. The resource name of the Location to create the TrainingPipeline in. Format: |
`training_pipeline` |
Required. The TrainingPipeline to create. This corresponds to the |
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

### delete_pipeline_job

```
delete_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.DeletePipelineJobRequest,
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
) -> google.api_core.operation.Operation
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
from google.cloud import aiplatform_v1
def sample_delete_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeletePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeletePipelineJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_delete_pipeline_job)(request=request)
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
The request object. Request message for PipelineService.DeletePipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob resource to be deleted. Format: |
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
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_training_pipeline

```
delete_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.DeleteTrainingPipelineRequest,
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
) -> google.api_core.operation.Operation
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
from google.cloud import aiplatform_v1
def sample_delete_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_delete_training_pipeline)(request=request)
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
The request object. Request message for PipelineService.DeleteTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline resource to be deleted. Format: |
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
`PipelineServiceClient` |
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
`PipelineServiceClient` |
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
`PipelineServiceClient` |
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

### get_pipeline_job

```
get_pipeline_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.GetPipelineJobRequest,
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
) -> google.cloud.aiplatform_v1.types.pipeline_job.PipelineJob
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
from google.cloud import aiplatform_v1
def sample_get_pipeline_job():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetPipelineJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_get_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.GetPipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob resource. Format: |
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
An instance of a machine learning PipelineJob. |

### get_training_pipeline

```
get_training_pipeline(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.GetTrainingPipelineRequest,
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
) -> google.cloud.aiplatform_v1.types.training_pipeline.TrainingPipeline
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
from google.cloud import aiplatform_v1
def sample_get_training_pipeline():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_get_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.GetTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline resource. Format: |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

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

### list_pipeline_jobs

```
list_pipeline_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsRequest,
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
) -> google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListPipelineJobsPager
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
from google.cloud import aiplatform_v1
def sample_list_pipeline_jobs():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_list_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.ListPipelineJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the PipelineJobs from. Format: |
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
Response message for PipelineService.ListPipelineJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_training_pipelines

```
list_training_pipelines(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesRequest,
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
) -> (
google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListTrainingPipelinesPager
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
from google.cloud import aiplatform_v1
def sample_list_training_pipelines():
# Create a client
client = aiplatform_v1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTrainingPipelinesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_training_pipelines](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1_services_pipeline_service_PipelineServiceClient_list_training_pipelines)(request=request)
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
The request object. Request message for PipelineService.ListTrainingPipelines. |
`parent` |
`str`
Required. The resource name of the Location to list the TrainingPipelines from. Format: |
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

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typesupdatefeatureonlinestorerequest_googlecl_f65ad7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesupdatefeatureonlinestorerequest_googleclo_96fe7c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesupdatefeatureonlinestorerequest_googleclou_2e71af.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesupdatefeatureonlinestorerequest_googlecloud_f2146b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdatefeatureonlinestorerequest_googleclouda_febf87.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatefeatureonlinestorerequest_googlecloudai_5305a8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatefeatureonlinestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureOnlineStoreRequest -->

# Class UpdateFeatureOnlineStoreRequest (1.134.0)

```
UpdateFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.UpdateFeatureOnlineStore.

## Attributes |
|
|---|---|
Name |
Description |
`feature_online_store` |
Required. The FeatureOnlineStore's `name` field is used to
identify the FeatureOnlineStore to be updated. Format:
`projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureOnlineStore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `description`
- `bigtable`
- `bigtable.auto_scaling`
- `bigtable.enable_multi_region_replica`
|

## Methods

### UpdateFeatureOnlineStoreRequest

```
UpdateFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.UpdateFeatureOnlineStore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureonlinestorededicatedservingendpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.DedicatedServingEndpoint -->

# Class DedicatedServingEndpoint (1.134.0)

`DedicatedServingEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The dedicated serving endpoint for this FeatureOnlineStore. Only need to set when you choose Optimized storage type. Public endpoint is provisioned by default.

## Attributes |
|
|---|---|
Name |
Description |
`public_endpoint_domain_name` |
`str`
Output only. This field will be populated with the domain name to use for this FeatureOnlineStore |
`private_service_connect_config` |
Optional. Private service connect config. The private service connection is available only for Optimized storage type, not for embedding management now. If PrivateServiceConnectConfig.enable_private_service_connect set to true, customers will use private service connection to send request. Otherwise, the connection will set to public endpoint. |
`service_attachment` |
`str`
Output only. The name of the service attachment resource. Populated if private service connect is enabled and after FeatureViewSync is created. |

## Methods

### DedicatedServingEndpoint

`DedicatedServingEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The dedicated serving endpoint for this FeatureOnlineStore. Only need to set when you choose Optimized storage type. Public endpoint is provisioned by default.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgroundednessspec_googlecloudaiplatform_v1bet_e8ed32.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgroundednessspec_googlecloudaiplatform_v1beta_e98b64.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgroundednessspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundednessSpec -->

# Class GroundednessSpec (1.134.0)

`GroundednessSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness metric.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### GroundednessSpec

`GroundednessSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfetchfeaturevaluesrequestformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchFeatureValuesRequest.Format -->

# Class Format (1.134.0)

`Format(value)`


Format of the response data.

## Enums |
|
|---|---|
Name |
Description |
`FORMAT_UNSPECIFIED` |
Not set. Will be treated as the KeyValue format. |
`KEY_VALUE` |
Return response data in key-value format. |
`PROTO_STRUCT` |
Return response data in proto Struct format. |

## Methods

### Format

`Format(value)`


Format of the response data.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessummarizationhelpfulnessinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationHelpfulnessInstance -->

# Class SummarizationHelpfulnessInstance (1.134.0)

```
SummarizationHelpfulnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|
`reference` |
`str`
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`context` |
`str`
Required. Text to be summarized. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Optional. Summarization prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### SummarizationHelpfulnessInstance

```
SummarizationHelpfulnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesvertexaisearchdatastorespec_googlecloudaipla_29ed8e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesvertexaisearchdatastorespec_googlecloudaiplat_74a7bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesvertexaisearchdatastorespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VertexAISearch.DataStoreSpec -->

# Class DataStoreSpec (1.134.0)

`DataStoreSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Define data stores within engine to filter on in a search
call and configurations for those data stores. For more
information, see
[https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec](https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec)

## Attributes |
|
|---|---|
Name |
Description |
`data_store` |
`str`
Full resource name of DataStore, such as Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`
|
`filter` |
`str`
Optional. Filter specification to filter documents in the data store specified by data_store field. For more information on filtering, see `Filtering ` __
|

## Methods

### DataStoreSpec

`DataStoreSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Define data stores within engine to filter on in a search
call and configurations for those data stores. For more
information, see
[https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec](https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelevaluationslicesliceslicespecvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluationSlice.Slice.SliceSpec.Value -->

# Class Value (1.134.0)

`Value(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Single value that supports strings and floats.

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
`string_value` |
`str`
String type. This field is a member of `oneof` _ `kind` .
|
`float_value` |
`float`
Float type. This field is a member of `oneof` _ `kind` .
|

## Methods

### Value

`Value(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Single value that supports strings and floats.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerssearchmodeldeploymentmonitoringstatsanomaliespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesPager -->

# Class SearchModelDeploymentMonitoringStatsAnomaliesPager (1.134.0)

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


A pager for iterating through `search_model_deployment_monitoring_stats_anomalies`

requests.

This class thinly wraps an initial
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
provides an `__iter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchModelDeploymentMonitoringStatsAnomalies`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchModelDeploymentMonitoringStatsAnomaliesPager

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesrougeinput_googlecloudaiplatform_v1typespresets_b3482a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesrougeinput_googlecloudaiplatform_v1typespresetsq_d2bdfa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesrougeinput_googlecloudaiplatform_v1typespresetsqu_ec9bf7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesrougeinput_googlecloudaiplatform_v1typespresetsque_633234.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesrougeinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RougeInput -->

# Class RougeInput (1.134.0)

`RougeInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for rouge metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for rouge score metric. |
`instances` |
`MutableSequence[`
Required. Repeated rouge instances. |

## Methods

### RougeInput

`RougeInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for rouge metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespresetsquery.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Presets.Query -->

# Class Query (1.134.0)

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off

## Enums |
|
|---|---|
Name |
Description |
`PRECISE` |
More precise neighbors as a trade-off against slower response. |
`FAST` |
Faster response as a trade-off against less precise neighbors. |

## Methods

### Query

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbatchmigrateresourcesoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesOperationMetadata -->

# Class BatchMigrateResourcesOperationMetadata (1.134.0)

```
BatchMigrateResourcesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for MigrationService.BatchMigrateResources.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |
`partial_results` |
`MutableSequence[`
Partial results that reflect the latest migration operation progress. |

## Classes

### PartialResult

`PartialResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a partial result in batch migration operation for one MigrateResourceRequest.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### BatchMigrateResourcesOperationMetadata

```
BatchMigrateResourcesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for MigrationService.BatchMigrateResources.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmetadataschema_googlecloudaiplatform_v1beta1typesv_226962.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmetadataschema.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetadataSchema -->

# Class MetadataSchema (1.134.0)

`MetadataSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general MetadataSchema.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the MetadataSchema. |
`schema_version` |
`str`
The version of the MetadataSchema. The version's format must match the following regular expression: `^[0-9]+` .][0-9]`+` .][0-9]`+$` , which would allow to
order/compare different versions. Example: 1.0.0, 1.0.1,
etc.
|
`schema` |
`str`
Required. The raw YAML string representation of the MetadataSchema. The combination of [MetadataSchema.version] and the schema name given by `title` in
[MetadataSchema.schema] must be unique within a
MetadataStore.
The schema is defined as an OpenAPI 3.0.2 `MetadataSchema
Object |
`schema_type` |
The type of the MetadataSchema. This is a property that identifies which metadata types will use the MetadataSchema. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MetadataSchema was created. |
`description` |
`str`
Description of the Metadata Schema |

## Classes

### MetadataSchemaType

`MetadataSchemaType(value)`


Describes the type of the MetadataSchema.

## Methods

### MetadataSchema

`MetadataSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general MetadataSchema.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Value -->

# Class Value (1.134.0)

`Value(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value is the value of the field.

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
`int_value` |
`int`
An integer value. This field is a member of `oneof` _ `value` .
|
`double_value` |
`float`
A double value. This field is a member of `oneof` _ `value` .
|
`string_value` |
`str`
A string value. This field is a member of `oneof` _ `value` .
|

## Methods

### Value

`Value(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value is the value of the field.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesexportfeaturevaluesresponse_googlecloudaiplatfor_b4a8dd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesexportfeaturevaluesresponse_googlecloudaiplatform_7754db.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexportfeaturevaluesresponse_googlecloudaiplatform__f32869.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportfeaturevaluesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFeatureValuesResponse -->

# Class ExportFeatureValuesResponse (1.134.0)

`ExportFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ExportFeatureValues.

## Methods

### ExportFeatureValuesResponse

`ExportFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ExportFeatureValues.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolcomputeruseenvironment.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tool.ComputerUse.Environment -->

# Class Environment (1.134.0)

`Environment(value)`


Represents the environment being operated, such as a web browser.

## Enums |
|
|---|---|
Name |
Description |
`ENVIRONMENT_UNSPECIFIED` |
Defaults to browser. |
`ENVIRONMENT_BROWSER` |
Operates in a web browser. |

## Methods

### Environment

`Environment(value)`


Represents the environment being operated, such as a web browser.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmigrateresourcerequestmigratedatalabelingdatasetconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest.MigrateDataLabelingDatasetConfig -->

# Class MigrateDataLabelingDatasetConfig (1.134.0)

```
MigrateDataLabelingDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
`str`
Required. Full resource name of data labeling Dataset. Format: `projects/{project}/datasets/{dataset}` .
|
`dataset_display_name` |
`str`
Optional. Display name of the Dataset in Vertex AI. System will pick a display name if unspecified. |
`migrate_data_labeling_annotated_dataset_configs` |
`MutableSequence[`
Optional. Configs for migrating AnnotatedDataset in datalabeling.googleapis.com to Vertex AI's SavedQuery. The specified AnnotatedDatasets have to belong to the datalabeling Dataset. |

## Classes

### MigrateDataLabelingAnnotatedDatasetConfig

```
MigrateDataLabelingAnnotatedDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating AnnotatedDataset in datalabeling.googleapis.com to Vertex AI's SavedQuery.

## Methods

### MigrateDataLabelingDatasetConfig

```
MigrateDataLabelingDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesembedcontentresponseembedding_googlecloudaiplatfo_655e4f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesembedcontentresponseembedding_googlecloudaiplatfor_96f243.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesembedcontentresponseembedding.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EmbedContentResponse.Embedding -->

# Class Embedding (1.134.0)

`Embedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of floats representing an embedding.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Embedding vector values. |

## Methods

### Embedding

`Embedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of floats representing an embedding.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexactmatchspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExactMatchSpec -->

# Class ExactMatchSpec (1.134.0)

`ExactMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for exact match metric - returns 1 if prediction and reference exactly matches, otherwise 0.

## Methods

### ExactMatchSpec

`ExactMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for exact match metric - returns 1 if prediction and reference exactly matches, otherwise 0.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesreadfeaturevaluesresponsefeaturedescriptor_go_2c0fc5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadfeaturevaluesresponsefeaturedescriptor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadFeatureValuesResponse.FeatureDescriptor -->

# Class FeatureDescriptor (1.134.0)

`FeatureDescriptor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for requested Features.

## Attribute |
|
|---|---|
Name |
Description |
`id` |
`str`
Feature ID. |

## Methods

### FeatureDescriptor

`FeatureDescriptor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for requested Features.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmetricxinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetricxInput -->

# Class MetricxInput (1.134.0)

`MetricxInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for MetricX metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for Metricx metric. |
`instance` |
Required. Metricx instance. |

## Methods

### MetricxInput

`MetricxInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for MetricX metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmigration_servicemigrationserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceClient -->

# Class MigrationServiceClient (1.134.0)

```
MigrationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.migration_service.transports.base.MigrationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.migration_service.transports.base.MigrationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service that migrates resources from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

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
`MigrationServiceTransport` |
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

### MigrationServiceClient

```
MigrationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.migration_service.transports.base.MigrationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.migration_service.transports.base.MigrationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the migration service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MigrationServiceTransport,Callable[..., MigrationServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MigrationServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### annotated_dataset_path

`annotated_dataset_path(project: str, dataset: str, annotated_dataset: str) -> str`


Returns a fully-qualified annotated_dataset string.

### batch_migrate_resources

```
batch_migrate_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.migration_service.BatchMigrateResourcesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
migrate_resource_requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.migration_service.MigrateResourceRequest
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
) -> google.api_core.operation.Operation
```


Batch migrates resources from ml.googleapis.com, automl.googleapis.com, and datalabeling.googleapis.com to Vertex AI.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_batch_migrate_resources():
# Create a client
client = aiplatform_v1beta1.
```[MigrationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceClient.html)()
# Initialize request argument(s)
migrate_resource_requests = aiplatform_v1beta1.[MigrateResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest.html)()
migrate_resource_requests.migrate_ml_engine_model_version_config.endpoint = "endpoint_value"
migrate_resource_requests.migrate_ml_engine_model_version_config.model_version = "model_version_value"
migrate_resource_requests.migrate_ml_engine_model_version_config.model_display_name = "model_display_name_value"
request = aiplatform_v1beta1.[BatchMigrateResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesRequest.html)(
parent="parent_value",
migrate_resource_requests=migrate_resource_requests,
)
# Make the request
operation = client.[batch_migrate_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceClient.html#google_cloud_aiplatform_v1beta1_services_migration_service_MigrationServiceClient_batch_migrate_resources)(request=request)
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
The request object. Request message for MigrationService.BatchMigrateResources. |
`parent` |
`str`
Required. The location of the migrated resource will live in. Format: |
`migrate_resource_requests` |
`MutableSequence[`
Required. The request messages specifying the resources to migrate. They must be in the same location as the destination. Up to 50 resources can be migrated in one batch. This corresponds to the |
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

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

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
`MigrationServiceClient` |
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
`MigrationServiceClient` |
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
`MigrationServiceClient` |
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

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### parse_annotated_dataset_path

`parse_annotated_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a annotated_dataset path into its component segments.

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

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_version_path

`parse_version_path(path: str) -> typing.Dict[str, str]`


Parses a version path into its component segments.

### search_migratable_resources

```
search_migratable_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
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
) -> (
google.cloud.aiplatform_v1beta1.services.migration_service.pagers.SearchMigratableResourcesPager
)
```


Searches all of the resources in automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com that can be migrated to Vertex AI's given location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_search_migratable_resources():
# Create a client
client = aiplatform_v1beta1.
```[MigrationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SearchMigratableResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[search_migratable_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceClient.html#google_cloud_aiplatform_v1beta1_services_migration_service_MigrationServiceClient_search_migratable_resources)(request=request)
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
The request object. Request message for MigrationService.SearchMigratableResources. |
`parent` |
`str`
Required. The location that the migratable resources should be searched from. It's the Vertex AI location that the resources can be migrated to, not the resources' original location. Format: |
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
Response message for MigrationService.SearchMigratableResources. Iterating over this object will yield results and resolve additional pages automatically. |

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

### version_path

`version_path(project: str, model: str, version: str) -> str`


Returns a fully-qualified version string.

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicevertexragdataserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient -->

# Class VertexRagDataServiceAsyncClient (1.134.0)

```
VertexRagDataServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing user data for RAG.

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
`VertexRagDataServiceTransport` |
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

### VertexRagDataServiceAsyncClient

```
VertexRagDataServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag data service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagDataServiceTransport,Callable[..., VertexRagDataServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagDataServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_rag_corpus

```
create_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.CreateRagCorpusRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
rag_corpus: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
] = None,
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


Creates a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_corpus = aiplatform_v1beta1.[RagCorpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.html)()
rag_corpus.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateRagCorpusRequest.html)(
parent="parent_value",
rag_corpus=rag_corpus,
)
# Make the request
operation = client.[create_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_create_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.CreateRagCorpus. |
`parent` |
Required. The resource name of the Location to create the RagCorpus in. Format: |
`rag_corpus` |
Required. The RagCorpus to create. This corresponds to the |
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

### delete_rag_corpus

```
delete_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.DeleteRagCorpusRequest,
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


Deletes a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagCorpusRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_delete_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.DeleteRagCorpus. |
`name` |
Required. The name of the RagCorpus resource to be deleted. Format: |
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

### delete_rag_file

```
delete_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.DeleteRagFileRequest,
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


Deletes a RagFile.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagFileRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_delete_rag_file)(request=request)
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
The request object. Request message for VertexRagDataService.DeleteRagFile. |
`name` |
Required. The name of the RagFile resource to be deleted. Format: |
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
`VertexRagDataServiceAsyncClient` |
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
`VertexRagDataServiceAsyncClient` |
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
`VertexRagDataServiceAsyncClient` |
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

### get_rag_corpus

```
get_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagCorpusRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
```


Gets a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagCorpusRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_corpus)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagCorpus |
`name` |
Required. The name of the RagCorpus resource. Format: |
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
A RagCorpus is a RagFile container and a project can have multiple RagCorpora. |

### get_rag_engine_config

```
get_rag_engine_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagEngineConfigRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagEngineConfig
```


Gets a RagEngineConfig.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_rag_engine_config():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagEngineConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagEngineConfigRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_engine_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_engine_config)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagEngineConfig |
`name` |
Required. The name of the RagEngineConfig resource. Format: |
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
Config for RagEngine. |

### get_rag_file

```
get_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagFileRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagFile
```


Gets a RagFile.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagFileRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_file)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagFile |
`name` |
Required. The name of the RagFile resource. Format: |
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
A RagFile contains user data for chunking, embedding and indexing. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport
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

### import_rag_files

```
import_rag_files(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ImportRagFilesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
import_rag_files_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.ImportRagFilesConfig
] = None,
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


Import files from Google Cloud Storage or Google Drive into a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_import_rag_files():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
import_rag_files_config = aiplatform_v1beta1.[ImportRagFilesConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesConfig.html)()
import_rag_files_config.gcs_source.uris = ['uris_value1', 'uris_value2']
import_rag_files_config.partial_failure_gcs_sink.output_uri_prefix = "output_uri_prefix_value"
import_rag_files_config.import_result_gcs_sink.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[ImportRagFilesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesRequest.html)(
parent="parent_value",
import_rag_files_config=import_rag_files_config,
)
# Make the request
operation = client.[import_rag_files](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_import_rag_files)(request=request)
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
The request object. Request message for VertexRagDataService.ImportRagFiles. |
`parent` |
Required. The name of the RagCorpus resource into which to import files. Format: |
`import_rag_files_config` |
Required. The config for the RagFiles to be synced and imported into the RagCorpus. VertexRagDataService.ImportRagFiles. This corresponds to the |
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

### list_rag_corpora

```
list_rag_corpora(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaRequest,
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
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager
)
```


Lists RagCorpora in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_rag_corpora():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListRagCorporaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_rag_corpora](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_list_rag_corpora)(request=request)
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
The request object. Request message for VertexRagDataService.ListRagCorpora. |
`parent` |
Required. The resource name of the Location from which to list the RagCorpora. Format: |
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
Response message for VertexRagDataService.ListRagCorpora. Iterating over this object will yield results and resolve additional pages automatically. |

### list_rag_files

```
list_rag_files(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesRequest,
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
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagFilesAsyncPager
)
```


Lists RagFiles in a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_rag_files():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListRagFilesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_rag_files](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_list_rag_files)(request=request)
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
The request object. Request message for VertexRagDataService.ListRagFiles. |
`parent` |
Required. The resource name of the RagCorpus from which to list the RagFiles. Format: |
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
Response message for VertexRagDataService.ListRagFiles. Iterating over this object will yield results and resolve additional pages automatically. |

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### parse_rag_engine_config_path

`parse_rag_engine_config_path(path: str) -> typing.Dict[str, str]`


Parses a rag_engine_config path into its component segments.

### parse_rag_file_path

`parse_rag_file_path(path: str) -> typing.Dict[str, str]`


Parses a rag_file path into its component segments.

### parse_secret_version_path

`parse_secret_version_path(path: str) -> typing.Dict[str, str]`


Parses a secret_version path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### rag_engine_config_path

`rag_engine_config_path(project: str, location: str) -> str`


Returns a fully-qualified rag_engine_config string.

### rag_file_path

`rag_file_path(project: str, location: str, rag_corpus: str, rag_file: str) -> str`


Returns a fully-qualified rag_file string.

### secret_version_path

`secret_version_path(project: str, secret: str, secret_version: str) -> str`


Returns a fully-qualified secret_version string.

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

### update_rag_corpus

```
update_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UpdateRagCorpusRequest,
dict,
]
] = None,
*,
rag_corpus: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
] = None,
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


Updates a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_corpus = aiplatform_v1beta1.[RagCorpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.html)()
rag_corpus.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagCorpusRequest.html)(
rag_corpus=rag_corpus,
)
# Make the request
operation = client.[update_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_update_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.UpdateRagCorpus. |
`rag_corpus` |
Required. The RagCorpus which replaces the resource on the server. This corresponds to the |
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

### update_rag_engine_config

```
update_rag_engine_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UpdateRagEngineConfigRequest,
dict,
]
] = None,
*,
rag_engine_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagEngineConfig
] = None,
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


Updates a RagEngineConfig.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_rag_engine_config():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateRagEngineConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagEngineConfigRequest.html)(
)
# Make the request
operation = client.[update_rag_engine_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_update_rag_engine_config)(request=request)
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
The request object. Request message for VertexRagDataService.UpdateRagEngineConfig. |
`rag_engine_config` |
Required. The updated RagEngineConfig. NOTE: Downgrading your RagManagedDb's ComputeTier could temporarily increase request latencies until the operation is fully complete. This corresponds to the |
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

### upload_rag_file

```
upload_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UploadRagFileRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
rag_file: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagFile
] = None,
upload_rag_file_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.UploadRagFileConfig
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UploadRagFileResponse
)
```


Upload a file into a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_upload_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_file = aiplatform_v1beta1.[RagFile](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFile.html)()
rag_file.gcs_source.uris = ['uris_value1', 'uris_value2']
rag_file.display_name = "display_name_value"
request = aiplatform_v1beta1.[UploadRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadRagFileRequest.html)(
parent="parent_value",
rag_file=rag_file,
)
# Make the request
response = await client.[upload_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_upload_rag_file)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.UploadRagFile. |
`parent` |
Required. The name of the RagCorpus resource into which to upload the file. Format: |
`rag_file` |
Required. The RagFile to upload. This corresponds to the |
`upload_rag_file_config` |
Required. The config for the RagFiles to be uploaded into the RagCorpus. VertexRagDataService.UploadRagFile. This corresponds to the |
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
Response message for VertexRagDataService.UploadRagFile. |

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

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1servicesschedule_servicepagers_googlecloudaip_f9ac9a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1servicesschedule_servicepagers_googlecloudaipl_3769d6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesschedule_servicepagers_googlecloudaipla_ade0b9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesschedule_servicepagers_googlecloudaiplat_a8f4c3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesschedule_servicepagers_googlecloudaiplatf_2104c3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesschedule_servicepagers_googlecloudaiplatfo_49bed3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesschedule_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.schedule_service.pagers`

module.

## Classes

[ListSchedulesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.pagers.ListSchedulesAsyncPager)

```
ListSchedulesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
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


A pager for iterating through `list_schedules`

requests.

This class thinly wraps an initial
[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse) object, and
provides an `__aiter__`

method to iterate through its
`schedules`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSchedules`

requests and continue to iterate
through the `schedules`

field on the
corresponding responses.

All the usual [ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListSchedulesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.pagers.ListSchedulesPager)

```
ListSchedulesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
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


A pager for iterating through `list_schedules`

requests.

This class thinly wraps an initial
[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse) object, and
provides an `__iter__`

method to iterate through its
`schedules`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSchedules`

requests and continue to iterate
through the `schedules`

field on the
corresponding responses.

All the usual [ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescachedcontent.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CachedContent -->

# Class CachedContent (1.134.0)

`CachedContent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A resource used in LLM queries for users to explicitly specify what to cache and how to cache.

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
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Timestamp of when this resource is considered expired. This is *always* provided on output, regardless of what was sent on input. This field is a member of `oneof` _ `expiration` .
|
`ttl` |
`google.protobuf.duration_pb2.Duration`
Input only. The TTL for this resource. The expiration time is computed: now + TTL. This field is a member of `oneof` _ `expiration` .
|
`name` |
`str`
Immutable. Identifier. The server-generated resource name of the cached content Format: projects/{project}/locations/{location}/cachedContents/{cached_content} |
`display_name` |
`str`
Optional. Immutable. The user-generated meaningful display name of the cached content. |
`model` |
`str`
Immutable. The name of the `Model` to use for cached
content. Currently, only the published Gemini base models
are supported, in form of
projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL}
|
`system_instruction` |
Optional. Input only. Immutable. Developer set system instruction. Currently, text only |
`contents` |
`MutableSequence[`
Optional. Input only. Immutable. The content to cache |
`tools` |
`MutableSequence[`
Optional. Input only. Immutable. A list of `Tools` the
model may use to generate the next response
|
`tool_config` |
Optional. Input only. Immutable. Tool config. This config is shared for all tools |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Creation time of the cache entry. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. When the cache entry was last updated in UTC time. |
`usage_metadata` |
Output only. Metadata on the usage of the cached content. |
`encryption_spec` |
Input only. Immutable. Customer-managed encryption key spec for a `CachedContent` . If set, this `CachedContent` and
all its sub-resources will be secured by this key.
|

## Classes

### UsageMetadata

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata on the usage of the cached content.

## Methods

### CachedContent

`CachedContent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A resource used in LLM queries for users to explicitly specify what to cache and how to cache.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesendpoint_servicepagers_googlecloudaiplatfo_d0a05c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesendpoint_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.endpoint_service.pagers`

module.

## Classes

[ListEndpointsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers.ListEndpointsAsyncPager)

```
ListEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
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


A pager for iterating through `list_endpoints`

requests.

This class thinly wraps an initial
[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse) object, and
provides an `__aiter__`

method to iterate through its
`endpoints`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEndpoints`

requests and continue to iterate
through the `endpoints`

field on the
corresponding responses.

All the usual [ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListEndpointsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers.ListEndpointsPager)

```
ListEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
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


A pager for iterating through `list_endpoints`

requests.

This class thinly wraps an initial
[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`endpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListEndpoints`

requests and continue to iterate
through the `endpoints`

field on the
corresponding responses.

All the usual [ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdedicatedresources.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DedicatedResources -->

# Class DedicatedResources (1.134.0)

`DedicatedResources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A description of resources that are dedicated to a DeployedModel, and that need a higher degree of manual configuration.

## Attributes |
|
|---|---|
Name |
Description |
`machine_spec` |
Required. Immutable. The specification of a single machine used by the prediction. |
`min_replica_count` |
`int`
Required. Immutable. The minimum number of machine replicas this DeployedModel will be always deployed on. This value must be greater than or equal to 1. If traffic against the DeployedModel increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed. |
`max_replica_count` |
`int`
Immutable. The maximum number of replicas this DeployedModel may be deployed on when the traffic against it increases. If the requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale the model to that many replicas is guaranteed (barring service outages). If traffic against the DeployedModel increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, will use min_replica_count as the default value. The value of this field impacts the charge against Vertex CPU and GPU quotas. Specifically, you will be charged for (max_replica_count \* number of cores in the selected machine type) and (max_replica_count \* number of GPUs per replica in the selected machine type). |
`required_replica_count` |
`int`
Optional. Number of required available replicas for the deployment to succeed. This field is only needed when partial model deployment/mutation is desired. If set, the model deploy/mutate operation will succeed once available_replica_count reaches required_replica_count, and the rest of the replicas will be retried. If not set, the default required_replica_count will be min_replica_count. |
`autoscaling_metric_specs` |
`MutableSequence[`
Immutable. The metric specifications that overrides a resource utilization metric (CPU utilization, accelerator's duty cycle, and so on) target value (default to 60 if not set). At most one entry is allowed per metric. If machine_spec.accelerator_count is above 0, the autoscaling will be based on both CPU utilization and accelerator's duty cycle metrics and scale up when either metrics exceeds its target value while scale down if both metrics are under their target value. The default target value is 60 for both metrics. If machine_spec.accelerator_count is 0, the autoscaling will be based on CPU utilization metric only with default target value 60 if not explicitly set. For example, in the case of Online Prediction, if you want to override target CPU utilization to 80, you should set autoscaling_metric_specs.metric_name to `aiplatform.googleapis.com/prediction/online/cpu/utilization`
and
autoscaling_metric_specs.target
to `80` .
|
`spot` |
`bool`
Optional. If true, schedule the deployment workload on `spot VMs |

## Methods

### DedicatedResources

`DedicatedResources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A description of resources that are dedicated to a DeployedModel, and that need a higher degree of manual configuration.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesquestionansweringqualityinstance__googlecloudaip_5a4d18.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesquestionansweringqualityinstance__googlecloudaipl_97fa65.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesquestionansweringqualityinstance__googlecloudaipla_341666.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesquestionansweringqualityinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringQualityInstance -->

# Class QuestionAnsweringQualityInstance (1.134.0)

```
QuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|
`reference` |
`str`
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`context` |
`str`
Required. Text to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. Question Answering prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringQualityInstance

```
QuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexactmatchspec_googlecloudaiplatform_v1beta1t_4b3a1b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexactmatchspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchSpec -->

# Class ExactMatchSpec (1.134.0)

`ExactMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for exact match metric - returns 1 if prediction and reference exactly matches, otherwise 0.

## Methods

### ExactMatchSpec

`ExactMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for exact match metric - returns 1 if prediction and reference exactly matches, otherwise 0.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesembedcontentresponseembedding.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EmbedContentResponse.Embedding -->

# Class Embedding (1.134.0)

`Embedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of floats representing an embedding.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Embedding vector values. |

## Methods

### Embedding

`Embedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of floats representing an embedding.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespublishermodelcalltoactionviewrestapi_googlecloud_7b9691.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespublishermodelcalltoactionviewrestapi_googleclouda_922089.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespublishermodelcalltoactionviewrestapi.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.ViewRestApi -->

# Class ViewRestApi (1.134.0)

`ViewRestApi(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rest API docs.

## Attributes |
|
|---|---|
Name |
Description |
`documentations` |
`MutableSequence[`
Required. |
`title` |
`str`
Required. The title of the view rest API. |

## Methods

### ViewRestApi

`ViewRestApi(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rest API docs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesraylogsspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RayLogsSpec -->

# Class RayLogsSpec (1.134.0)

`RayLogsSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the Ray OSS Logs.

## Attribute |
|
|---|---|
Name |
Description |
`disabled` |
`bool`
Optional. Flag to disable the export of Ray OSS logs to Cloud Logging. |

## Methods

### RayLogsSpec

`RayLogsSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the Ray OSS Logs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragembeddingmodelconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagEmbeddingModelConfig -->

# Class RagEmbeddingModelConfig (1.134.0)

`RagEmbeddingModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the embedding model to use for RAG.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`vertex_prediction_endpoint` |
The Vertex AI Prediction Endpoint that either refers to a publisher model or an endpoint that is hosting a 1P fine-tuned text embedding model. Endpoints hosting non-1P fine-tuned text embedding models are currently not supported. This is used for dense vector search. This field is a member of `oneof` _ `model_config` .
|

## Classes

### VertexPredictionEndpoint

`VertexPredictionEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config representing a model hosted on Vertex Prediction Endpoint.

## Methods

### RagEmbeddingModelConfig

`RagEmbeddingModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the embedding model to use for RAG.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesjob_servicepagerssearchmodeldeploymentmonitorin_8fa8a1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerssearchmodeldeploymentmonitoringstatsanomaliesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager -->

# Class SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager (1.134.0)

```
SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


A pager for iterating through `search_model_deployment_monitoring_stats_anomalies`

requests.

This class thinly wraps an initial
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
provides an `__aiter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchModelDeploymentMonitoringStatsAnomalies`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager

```
SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescachedcontent.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CachedContent -->

# Class CachedContent (1.134.0)

`CachedContent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A resource used in LLM queries for users to explicitly specify what to cache and how to cache.

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
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Timestamp of when this resource is considered expired. This is *always* provided on output, regardless of what was sent on input. This field is a member of `oneof` _ `expiration` .
|
`ttl` |
`google.protobuf.duration_pb2.Duration`
Input only. The TTL for this resource. The expiration time is computed: now + TTL. This field is a member of `oneof` _ `expiration` .
|
`name` |
`str`
Immutable. Identifier. The server-generated resource name of the cached content Format: projects/{project}/locations/{location}/cachedContents/{cached_content} |
`display_name` |
`str`
Optional. Immutable. The user-generated meaningful display name of the cached content. |
`model` |
`str`
Immutable. The name of the `Model` to use for cached
content. Currently, only the published Gemini base models
are supported, in form of
projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL}
|
`system_instruction` |
Optional. Input only. Immutable. Developer set system instruction. Currently, text only |
`contents` |
`MutableSequence[`
Optional. Input only. Immutable. The content to cache |
`tools` |
`MutableSequence[`
Optional. Input only. Immutable. A list of `Tools` the
model may use to generate the next response
|
`tool_config` |
Optional. Input only. Immutable. Tool config. This config is shared for all tools |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Creation time of the cache entry. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. When the cache entry was last updated in UTC time. |
`usage_metadata` |
Output only. Metadata on the usage of the cached content. |
`encryption_spec` |
Input only. Immutable. Customer-managed encryption key spec for a `CachedContent` . If set, this `CachedContent` and
all its sub-resources will be secured by this key.
|

## Classes

### UsageMetadata

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata on the usage of the cached content.

## Methods

### CachedContent

`CachedContent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A resource used in LLM queries for users to explicitly specify what to cache and how to cache.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformautomltexttrainingjob___googlecloudaiplatform_v1beta1servi_bdf948.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformautomltexttrainingjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTextTrainingJob -->

# Class AutoMLTextTrainingJob (1.134.0)

```
AutoMLTextTrainingJob(
display_name: str,
prediction_type: str,
multi_label: bool = False,
sentiment_max: int = 10,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Constructs a AutoML Text Training Job.

## Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of this TrainingPipeline. |
`prediction_type` |
`str`
The type of prediction the Model is to produce, one of: "classification" - A classification model analyzes text data and returns a list of categories that apply to the text found in the data. Vertex AI offers both single-label and multi-label text classification models. "extraction" - An entity extraction model inspects text data for known entities referenced in the data and labels those entities in the text. "sentiment" - A sentiment analysis model inspects text data and identifies the prevailing emotional opinion within it, especially to determine a writer's attitude as positive, negative, or neutral. |
`multi_label` |
`bool`
Required and only applicable for text classification task. If false, a single-label (multi-class) Model will be trained (i.e. assuming that for each text snippet just up to one annotation may be applicable). If true, a multi-label Model will be trained (i.e. assuming that for each text snippet multiple annotations may be applicable). |
`sentiment_max` |
`int`
Required and only applicable for sentiment task. A sentiment is expressed as an integer ordinal, where higher value means a more positive sentiment. The range of sentiments that will be used is between 0 and sentimentMax (inclusive on both ends), and all the values in the range must be represented in the dataset before a model can be created. Only the Annotations with this sentimentMax will be used for training. sentimentMax value must be between 1 and 10 (inclusive). |
`project` |
`str`
Optional. Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |

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

## Methods

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
dataset: google.cloud.aiplatform.datasets.text_dataset.TextDataset,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
training_filter_split: typing.Optional[str] = None,
validation_filter_split: typing.Optional[str] = None,
test_filter_split: typing.Optional[str] = None,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Model
```


Runs the training job and returns a model.

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
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TextDataset`
Required. The dataset within the same Project from which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. |
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
`model_display_name` |
`str`
Optional. The display name of the managed Vertex AI Model. The name can be up to 128 characters long and can consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
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
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run or is waiting to run. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource. |

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesmemory_bank_servicepagers___googlecloudai_440f6a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmemory_bank_servicepagers___googlecloudaip_0cc9c9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmemory_bank_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.memory_bank_service.pagers`

module.

## Classes

[ListMemoriesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers.ListMemoriesAsyncPager)

```
ListMemoriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesRequest,
response: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
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


A pager for iterating through `list_memories`

requests.

This class thinly wraps an initial
[ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse) object, and
provides an `__aiter__`

method to iterate through its
`memories`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListMemories`

requests and continue to iterate
through the `memories`

field on the
corresponding responses.

All the usual [ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListMemoriesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers.ListMemoriesPager)

```
ListMemoriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesRequest,
response: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
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


A pager for iterating through `list_memories`

requests.

This class thinly wraps an initial
[ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse) object, and
provides an `__iter__`

method to iterate through its
`memories`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMemories`

requests and continue to iterate
through the `memories`

field on the
corresponding responses.

All the usual [ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodeldeploymentmonitoringbigquerytablelogsource_g_4b7839.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodeldeploymentmonitoringbigquerytablelogsource_go_26e418.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodeldeploymentmonitoringbigquerytablelogsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringBigQueryTable.LogSource -->

# Class LogSource (1.134.0)

`LogSource(value)`


Indicates where does the log come from.

## Enums |
|
|---|---|
Name |
Description |
`LOG_SOURCE_UNSPECIFIED` |
Unspecified source. |
`TRAINING` |
Logs coming from Training dataset. |
`SERVING` |
Logs coming from Serving traffic. |

## Methods

### LogSource

`LogSource(value)`


Indicates where does the log come from.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragvectordbconfigpinecone.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig.Pinecone -->

# Class Pinecone (1.134.0)

`Pinecone(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Pinecone.

## Attribute |
|
|---|---|
Name |
Description |
`index_name` |
`str`
Pinecone index name. This value cannot be changed after it's set. |

## Methods

### Pinecone

`Pinecone(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Pinecone.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescsvdestination_googlecloudaiplatform_v1beta1typesp_081fe1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescsvdestination.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CsvDestination -->

# Class CsvDestination (1.134.0)

`CsvDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The storage details for CSV output content.

## Attribute |
|
|---|---|
Name |
Description |
`gcs_destination` |
Required. Google Cloud Storage location. |

## Methods

### CsvDestination

`CsvDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The storage details for CSV output content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinetaskrerunconfigartifactlist.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskRerunConfig.ArtifactList -->

# Class ArtifactList (1.134.0)

`ArtifactList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of artifact metadata.

## Attribute |
|
|---|---|
Name |
Description |
`artifacts` |
`MutableSequence[`
Optional. A list of artifact metadata. |

## Methods

### ArtifactList

`ArtifactList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of artifact metadata.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistmodelversionsrequest_googlecloudaiplatform_v1_8700d7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistmodelversionsrequest_googlecloudaiplatform_v1t_898811.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmodelversionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionsRequest -->

# Class ListModelVersionsRequest (1.134.0)

`ListModelVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModelVersions.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the model to list versions for. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via next_page_token of the previous ListModelVersions call. |
`filter` |
`str`
An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- \`labels.key:\* or labels:key - key existence
- A key including a space must be quoted.
`labels."a key"` .
Some examples:
- `labels.myKey="myValue"`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `create_time`
- `update_time`
Example: `update_time asc, create_time desc` .
|

## Methods

### ListModelVersionsRequest

`ListModelVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModelVersions.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgeneratecontentresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentResponse -->

# Class GenerateContentResponse (1.134.0)

`GenerateContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for [PredictionService.GenerateContent].

## Attributes |
|
|---|---|
Name |
Description |
`candidates` |
`MutableSequence[`
Output only. Generated candidates. |
`model_version` |
`str`
Output only. The model version used to generate the response. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the request is made to the server. |
`response_id` |
`str`
Output only. response_id is used to identify each response. It is the encoding of the event_id. |
`prompt_feedback` |
Output only. Content filter results for a prompt sent in the request. Note: Sent only in the first stream chunk. Only happens when no candidates were generated due to content violations. |
`usage_metadata` |
Usage metadata about the response(s). |

## Classes

### PromptFeedback

`PromptFeedback(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content filter results for a prompt sent in the request.

### UsageMetadata

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Usage metadata about response(s).

## Methods

### GenerateContentResponse

`GenerateContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for [PredictionService.GenerateContent].


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesquestionansweringqualityinstance__googlecloud_2ad4cd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquestionansweringqualityinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringQualityInstance -->

# Class QuestionAnsweringQualityInstance (1.134.0)

```
QuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|
`reference` |
`str`
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`context` |
`str`
Required. Text to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. Question Answering prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringQualityInstance

```
QuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeseventtype_googlecloudaiplatform_v1beta1typesstartn_e660af.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeseventtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Event.Type -->

# Class Type (1.134.0)

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Unspecified whether input or output of the Execution. |
`INPUT` |
An input of the Execution. |
`OUTPUT` |
An output of the Execution. |

## Methods

### Type

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstartnotebookruntimeresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeResponse -->

# Class StartNotebookRuntimeResponse (1.134.0)

```
StartNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.StartNotebookRuntime.

## Methods

### StartNotebookRuntimeResponse

```
StartNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.StartNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typesremovecontextchildrenresponse_googlecloudaipl_d72821.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesremovecontextchildrenresponse_googlecloudaipla_f1a4f4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesremovecontextchildrenresponse_googlecloudaiplat_3e9daf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesremovecontextchildrenresponse_googlecloudaiplatf_730a9c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesremovecontextchildrenresponse_googlecloudaiplatfo_bdcef5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesremovecontextchildrenresponse_googlecloudaiplatfor_eaee63.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesremovecontextchildrenresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RemoveContextChildrenResponse -->

# Class RemoveContextChildrenResponse (1.134.0)

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.

## Methods

### RemoveContextChildrenResponse

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespresetsquery.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Presets.Query -->

# Class Query (1.134.0)

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off

## Enums |
|
|---|---|
Name |
Description |
`PRECISE` |
More precise neighbors as a trade-off against slower response. |
`FAST` |
Faster response as a trade-off against less precise neighbors. |

## Methods

### Query

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Value -->

# Class Value (1.134.0)

`Value(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value is the value of the field.

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
`int_value` |
`int`
An integer value. This field is a member of `oneof` _ `value` .
|
`double_value` |
`float`
A double value. This field is a member of `oneof` _ `value` .
|
`string_value` |
`str`
A string value. This field is a member of `oneof` _ `value` .
|

## Methods

### Value

`Value(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value is the value of the field.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesdeployedindexdeploymenttier_googlecloudaiplatform_6e1e30.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeployedindexdeploymenttier_googlecloudaiplatform__5078da.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployedindexdeploymenttier.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedIndex.DeploymentTier -->

# Class DeploymentTier (1.134.0)

`DeploymentTier(value)`


Tiers encapsulate serving time attributes like latency and throughput.

## Enums |
|
|---|---|
Name |
Description |
`DEPLOYMENT_TIER_UNSPECIFIED` |
Default deployment tier. |
`STORAGE` |
Optimized for costs. |

## Methods

### DeploymentTier

`DeploymentTier(value)`


Tiers encapsulate serving time attributes like latency and throughput.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinetaskdetailartifactlist.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskDetail.ArtifactList -->

# Class ArtifactList (1.134.0)

`ArtifactList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of artifact metadata.

## Attribute |
|
|---|---|
Name |
Description |
`artifacts` |
`MutableSequence[`
Output only. A list of artifact metadata. |

## Methods

### ArtifactList

`ArtifactList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of artifact metadata.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesretrievecontextsrequestvertexragstore.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrieveContextsRequest.VertexRagStore -->

# Class VertexRagStore (1.134.0)

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The data source for Vertex RagStore.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`rag_resources` |
`MutableSequence[`
Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support. |
`vector_distance_threshold` |
`float`
Optional. Only return contexts with vector distance smaller than the threshold. This field is a member of `oneof` _ `_vector_distance_threshold` .
|

## Classes

### RagResource

`RagResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of the Rag resource.

## Methods

### VertexRagStore

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The data source for Vertex RagStore.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesmetricxinput_googlecloudaiplatform_v1beta1t_a3f5ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmetricxinput_googlecloudaiplatform_v1beta1ty_c673f2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmetricxinput_googlecloudaiplatform_v1beta1typ_9bfc13.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmetricxinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxInput -->

# Class MetricxInput (1.134.0)

`MetricxInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for MetricX metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for Metricx metric. |
`instance` |
Required. Metricx instance. |

## Methods

### MetricxInput

`MetricxInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for MetricX metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringbigquerytablelogsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringBigQueryTable.LogSource -->

# Class LogSource (1.134.0)

`LogSource(value)`


Indicates where does the log come from.

## Enums |
|
|---|---|
Name |
Description |
`LOG_SOURCE_UNSPECIFIED` |
Unspecified source. |
`TRAINING` |
Logs coming from Training dataset. |
`SERVING` |
Logs coming from Serving traffic. |

## Methods

### LogSource

`LogSource(value)`


Indicates where does the log come from.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstartnotebookruntimeresponse_googlecloudaiplatform_5957bb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstartnotebookruntimeresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StartNotebookRuntimeResponse -->

# Class StartNotebookRuntimeResponse (1.134.0)

```
StartNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.StartNotebookRuntime.

## Methods

### StartNotebookRuntimeResponse

```
StartNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.StartNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescsvdestination.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CsvDestination -->

# Class CsvDestination (1.134.0)

`CsvDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The storage details for CSV output content.

## Attribute |
|
|---|---|
Name |
Description |
`gcs_destination` |
Required. Google Cloud Storage location. |

## Methods

### CsvDestination

`CsvDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The storage details for CSV output content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragvectordbconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig -->

# Class RagVectorDbConfig (1.134.0)

`RagVectorDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vector DB to use for RAG.

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
`rag_managed_db` |
The config for the RAG-managed Vector DB. This field is a member of `oneof` _ `vector_db` .
|
`weaviate` |
The config for the Weaviate. This field is a member of `oneof` _ `vector_db` .
|
`pinecone` |
The config for the Pinecone. This field is a member of `oneof` _ `vector_db` .
|
`vertex_feature_store` |
The config for the Vertex Feature Store. This field is a member of `oneof` _ `vector_db` .
|
`vertex_vector_search` |
The config for the Vertex Vector Search. This field is a member of `oneof` _ `vector_db` .
|
`rag_managed_vertex_vector_search` |
The config for the RAG-managed Vertex Vector Search 2.0. This field is a member of `oneof` _ `vector_db` .
|
`api_auth` |
Authentication config for the chosen Vector DB. |
`rag_embedding_model_config` |
Optional. Immutable. The embedding model config of the Vector DB. |

## Classes

### Pinecone

`Pinecone(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Pinecone.

### RagManagedDb

`RagManagedDb(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the default RAG-managed Vector DB.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### RagManagedVertexVectorSearch

```
RagManagedVertexVectorSearch(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for the RAG-managed Vertex Vector Search 2.0.

### VertexFeatureStore

`VertexFeatureStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Feature Store.

### VertexVectorSearch

`VertexVectorSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Vector Search.

### Weaviate

`Weaviate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Weaviate.

## Methods

### RagVectorDbConfig

`RagVectorDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vector DB to use for RAG.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdeployment_resource_pool_servicepagers_googlecl_69e566.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdeployment_resource_pool_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.deployment_resource_pool_service.pagers`

module.

## Classes

[ListDeploymentResourcePoolsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsAsyncPager)

```
ListDeploymentResourcePoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse
],
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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


A pager for iterating through `list_deployment_resource_pools`

requests.

This class thinly wraps an initial
[ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsResponse) object, and
provides an `__aiter__`

method to iterate through its
`deployment_resource_pools`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDeploymentResourcePools`

requests and continue to iterate
through the `deployment_resource_pools`

field on the
corresponding responses.

All the usual [ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDeploymentResourcePoolsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsPager)

```
ListDeploymentResourcePoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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


A pager for iterating through `list_deployment_resource_pools`

requests.

This class thinly wraps an initial
[ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`deployment_resource_pools`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDeploymentResourcePools`

requests and continue to iterate
through the `deployment_resource_pools`

field on the
corresponding responses.

All the usual [ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[QueryDeployedModelsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsAsyncPager)

```
QueryDeployedModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse
],
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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


A pager for iterating through `query_deployed_models`

requests.

This class thinly wraps an initial
[QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse) object, and
provides an `__aiter__`

method to iterate through its
`deployed_models`

field.

If there are more pages, the `__aiter__`

method will make additional
`QueryDeployedModels`

requests and continue to iterate
through the `deployed_models`

field on the
corresponding responses.

All the usual [QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[QueryDeployedModelsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsPager)

```
QueryDeployedModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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


A pager for iterating through `query_deployed_models`

requests.

This class thinly wraps an initial
[QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`deployed_models`

field.

If there are more pages, the `__iter__`

method will make additional
`QueryDeployedModels`

requests and continue to iterate
through the `deployed_models`

field on the
corresponding responses.

All the usual [QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudyspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec -->

# Class StudySpec (1.134.0)

`StudySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents specification of a Study.

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
`decay_curve_stopping_spec` |
The automated early stopping spec using decay curve rule. This field is a member of `oneof` _ `automated_stopping_spec` .
|
`median_automated_stopping_spec` |
The automated early stopping spec using median rule. This field is a member of `oneof` _ `automated_stopping_spec` .
|
`convex_stop_config` |
Deprecated. The automated early stopping using convex stopping rule. This field is a member of `oneof` _ `automated_stopping_spec` .
|
`convex_automated_stopping_spec` |
The automated early stopping spec using convex stopping rule. This field is a member of `oneof` _ `automated_stopping_spec` .
|
`metrics` |
`MutableSequence[`
Required. Metric specs for the Study. |
`parameters` |
`MutableSequence[`
Required. The set of parameters to tune. |
`algorithm` |
The search algorithm specified for the Study. |
`observation_noise` |
The observation noise level of the study. Currently only supported by the Vertex AI Vizier service. Not supported by HyperparameterTuningJob or TrainingPipeline. |
`measurement_selection_type` |
Describe which measurement selection type will be used |
`transfer_learning_config` |
The configuration info/options for transfer learning. Currently supported for Vertex AI Vizier service, not HyperParameterTuningJob |
`study_stopping_config` |
Conditions for automated stopping of a Study. Enable automated stopping by configuring at least one condition. This field is a member of `oneof` _ `_study_stopping_config` .
|

## Classes

### Algorithm

`Algorithm(value)`


The available search algorithms for the Study.

### ConvexAutomatedStoppingSpec

`ConvexAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for ConvexAutomatedStoppingSpec. When there are enough completed trials (configured by min_measurement_count), for pending trials with enough measurements and steps, the policy first computes an overestimate of the objective value at max_num_steps according to the slope of the incomplete objective value curve. No prediction can be made if the curve is completely flat. If the overestimation is worse than the best objective value of the completed trials, this pending trial will be early-stopped, but a last measurement will be added to the pending trial with max_num_steps and predicted objective value from the autoregression model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ConvexStopConfig

`ConvexStopConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for ConvexStopPolicy.

### DecayCurveAutomatedStoppingSpec

```
DecayCurveAutomatedStoppingSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The decay curve automated stopping rule builds a Gaussian Process Regressor to predict the final objective value of a Trial based on the already completed Trials and the intermediate measurements of the current Trial. Early stopping is requested for the current Trial if there is very low probability to exceed the optimal value found so far.

### MeasurementSelectionType

`MeasurementSelectionType(value)`


This indicates which measurement to use if/when the service automatically selects the final measurement from previously reported intermediate measurements. Choose this based on two considerations: A) Do you expect your measurements to monotonically improve? If so, choose LAST_MEASUREMENT. On the other hand, if you're in a situation where your system can "over-train" and you expect the performance to get better for a while but then start declining, choose BEST_MEASUREMENT. B) Are your measurements significantly noisy and/or irreproducible? If so, BEST_MEASUREMENT will tend to be over-optimistic, and it may be better to choose LAST_MEASUREMENT. If both or neither of (A) and (B) apply, it doesn't matter which selection type is chosen.

### MedianAutomatedStoppingSpec

`MedianAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The median automated stopping rule stops a pending Trial if the Trial's best objective_value is strictly below the median 'performance' of all completed Trials reported up to the Trial's last measurement. Currently, 'performance' refers to the running average of the objective values reported by the Trial in each measurement.

### MetricSpec

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ObservationNoise

`ObservationNoise(value)`


Describes the noise level of the repeated observations.

"Noisy" means that the repeated observations with the same Trial parameters may lead to different metric evaluations.

### ParameterSpec

`ParameterSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single parameter to optimize.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### StudyStoppingConfig

`StudyStoppingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration (stopping conditions) for automated stopping of a Study. Conditions include trial budgets, time budgets, and convergence detection.

### TransferLearningConfig

`TransferLearningConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This contains flag for manually disabling transfer learning for a study. The names of prior studies being used for transfer learning (if any) are also listed here.

## Methods

### StudySpec

`StudySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents specification of a Study.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _prediction_a-z0-9-061a-z0-9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: prediction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/prediction -->

# Vertex AI SDK for Python

## Gemini API and Generative AI on Vertex AI

**NOTE**: For Gemini API and Generative AI on Vertex AI, please reference [Vertex Generative AI SDK for Python](https://cloud.google.com/vertex-ai/generative-ai/docs/reference/python/latest)

[Vertex AI](https://cloud.google.com/vertex-ai/docs): Google Vertex AI is an integrated suite of machine learning tools and services for building and using ML models with AutoML or custom code. It offers both novices and experts the best workbench for the entire machine learning development lifecycle.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-aiplatform
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-aiplatform
```


#### Supported Python Versions

Python >= 3.8

#### Deprecated Python Versions

Python <= 3.7.

The last version of this library compatible with Python 3.6 is google-cloud-aiplatform==1.12.1.

### Overview

This section provides a brief overview of the Vertex AI SDK for Python. You can also reference the notebooks in [vertex-ai-samples](https://github.com/GoogleCloudPlatform/vertex-ai-samples/tree/main/notebooks/community/sdk) for examples.

All publicly available SDK features can be found in the `google/cloud/aiplatform`

directory.
Under the hood, Vertex SDK builds on top of GAPIC, which stands for Google API CodeGen.
The GAPIC library code sits in `google/cloud/aiplatform_v1`

and `google/cloud/aiplatform_v1beta1`

,
and it is auto-generated from Google’s service proto files.

For most developers’ programmatic needs, they can follow these steps to figure out which libraries to import:

Look through

`google/cloud/aiplatform`

first – Vertex SDK’s APIs will almost always be easier to use and more concise comparing with GAPICIf the feature that you are looking for cannot be found there, look through

`aiplatform_v1`

to see if it’s available in GAPICIf it is still in beta phase, it will be available in

`aiplatform_v1beta1`


If none of the above scenarios could help you find the right tools for your task, please feel free to open a github issue and send us a feature request.

#### Importing

Vertex AI SDK resource based functionality can be used by importing the following namespace:

```
from google.cloud import aiplatform
```


#### Initialization

Initialize the SDK to store common configurations that you use with the SDK.

```
aiplatform.init(
# your Google Cloud Project ID or number
# environment default used is not set
project='my-project',
# the Vertex AI region you will use
# defaults to us-central1
location='us-central1',
# Google Cloud Storage bucket in same region as location
# used to stage artifacts
staging_bucket='gs://my_staging_bucket',
# custom google.auth.credentials.Credentials
# environment default credentials used if not set
credentials=my_credentials,
# customer managed encryption key resource name
# will be applied to all Vertex AI resources if set
encryption_spec_key_name=my_encryption_key_name,
# the name of the experiment to use to track
# logged metrics and parameters
experiment='my-experiment',
# description of the experiment above
experiment_description='my experiment description'
)
```


#### Datasets

Vertex AI provides managed tabular, text, image, and video datasets. In the SDK, datasets can be used downstream to train models.

To create a tabular dataset:

```
my_dataset = aiplatform.TabularDataset.create(
display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])
```


You can also create and import a dataset in separate steps:

```
from google.cloud import aiplatform
my_dataset = aiplatform.TextDataset.create(
display_name="my-dataset")
my_dataset.import_data(
gcs_source=['gs://path/to/my/dataset.csv'],
import_schema_uri=aiplatform.schema.dataset.ioformat.text.multi_label_classification
)
```


To get a previously created Dataset:

```
dataset = aiplatform.ImageDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
```


Vertex AI supports a variety of dataset schemas. References to these schemas are available under the
`aiplatform.schema.dataset`

namespace. For more information on the supported dataset schemas please refer to the
[Preparing data docs](https://cloud.google.com/ai-platform-unified/docs/datasets/prepare).

#### Training

The Vertex AI SDK for Python allows you train Custom and AutoML Models.

You can train custom models using a custom Python script, custom Python package, or container.

**Preparing Your Custom Code**

Vertex AI custom training enables you to train on Vertex AI datasets and produce Vertex AI models. To do so your script must adhere to the following contract:

It must read datasets from the environment variables populated by the training service:

```
os.environ['AIP_DATA_FORMAT'] # provides format of data
os.environ['AIP_TRAINING_DATA_URI'] # uri to training split
os.environ['AIP_VALIDATION_DATA_URI'] # uri to validation split
os.environ['AIP_TEST_DATA_URI'] # uri to test split
```


Please visit [Using a managed dataset in a custom training application](https://cloud.google.com/vertex-ai/docs/training/using-managed-datasets) for a detailed overview.

It must write the model artifact to the environment variable populated by the training service:

```
os.environ['AIP_MODEL_DIR']
```


**Running Training**

```
job = aiplatform.CustomTrainingJob(
display_name="my-training-job",
script_path="training_script.py",
container_uri="us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-2:latest",
requirements=["gcsfs==0.7.1"],
model_serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
model = job.run(my_dataset,
replica_count=1,
machine_type="n1-standard-4",
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


In the code block above my_dataset is managed dataset created in the Dataset section above. The model variable is a managed Vertex AI model that can be deployed or exported.

## AutoMLs

The Vertex AI SDK for Python supports AutoML tabular, image, text, video, and forecasting.

To train an AutoML tabular model:

```
dataset = aiplatform.TabularDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
job = aiplatform.AutoMLTabularTrainingJob(
display_name="train-automl",
optimization_prediction_type="regression",
optimization_objective="minimize-rmse",
)
model = job.run(
dataset=dataset,
target_column="target_column_name",
training_fraction_split=0.6,
validation_fraction_split=0.2,
test_fraction_split=0.2,
budget_milli_node_hours=1000,
model_display_name="my-automl-model",
disable_early_stopping=False,
)
```


## Models

To get a model:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
```


To upload a model:

```
model = aiplatform.Model.upload(
display_name='my-model',
artifact_uri="gs://python/to/my/model/dir",
serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
```


To deploy a model:

```
endpoint = model.deploy(machine_type="n1-standard-4",
min_replica_count=1,
max_replica_count=5
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


Please visit [Importing models to Vertex AI](https://cloud.google.com/vertex-ai/docs/general/import-model) for a detailed overview:

## Model Evaluation

The Vertex AI SDK for Python currently supports getting model evaluation metrics for all AutoML models.

To list all model evaluations for a model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
evaluations = model.list_model_evaluations()
```


To get the model evaluation resource for a given model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
# returns the first evaluation with no arguments, you can also pass the evaluation ID
evaluation = model.get_model_evaluation()
eval_metrics = evaluation.metrics
```


You can also create a reference to your model evaluation directly by passing in the resource name of the model evaluation:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name='projects/my-project/locations/us-central1/models/{MODEL_ID}/evaluations/{EVALUATION_ID}')
```


Alternatively, you can create a reference to your evaluation by passing in the model and evaluation IDs:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name={EVALUATION_ID},
model_id={MODEL_ID})
```


## Batch Prediction

To create a batch prediction job:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
batch_prediction_job = model.batch_predict(
job_display_name='my-batch-prediction-job',
instances_format='csv',
machine_type='n1-standard-4',
gcs_source=['gs://path/to/my/file.csv'],
gcs_destination_prefix='gs://path/to/my/batch_prediction/results/',
service_account='my-sa@my-project.iam.gserviceaccount.com'
)
```


You can also create a batch prediction job asynchronously by including the sync=False argument:

```
batch_prediction_job = model.batch_predict(..., sync=False)
# wait for resource to be created
batch_prediction_job.wait_for_resource_creation()
# get the state
batch_prediction_job.state
# block until job is complete
batch_prediction_job.wait()
```


## Endpoints

To create an endpoint:

```
endpoint = aiplatform.Endpoint.create(display_name='my-endpoint')
```


To deploy a model to a created endpoint:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
endpoint.deploy(model,
min_replica_count=1,
max_replica_count=5,
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


To get predictions from endpoints:

```
endpoint.predict(instances=[[6.7, 3.1, 4.7, 1.5], [4.6, 3.1, 1.5, 0.2]])
```


To undeploy models from an endpoint:

```
endpoint.undeploy_all()
```


To delete an endpoint:

```
endpoint.delete()
```


## Pipelines

To create a Vertex AI Pipeline run and monitor until completion:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Execute pipeline in Vertex AI and monitor until completion
pl.run(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
# Whether this function call should be synchronous (wait for pipeline run to finish before terminating)
# or asynchronous (return immediately)
sync=True
)
```


To create a Vertex AI Pipeline without monitoring until completion, use submit instead of run:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Submit the Pipeline to Vertex AI
pl.submit(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
)
```


## Explainable AI: Get Metadata

To get metadata in dictionary format from TensorFlow 1 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v1 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder(
'gs://python/to/my/model/dir', tags=[tf.saved_model.tag_constants.SERVING]
)
generated_md = builder.get_metadata()
```


To get metadata in dictionary format from TensorFlow 2 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v2 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder('gs://python/to/my/model/dir')
generated_md = builder.get_metadata()
```


To use Explanation Metadata in endpoint deployment and model upload:

```
explanation_metadata = builder.get_metadata_protobuf()
# To deploy a model to an endpoint with explanation
model.deploy(..., explanation_metadata=explanation_metadata)
# To deploy a model to a created endpoint with explanation
endpoint.deploy(..., explanation_metadata=explanation_metadata)
# To upload a model with explanation
aiplatform.Model.upload(..., explanation_metadata=explanation_metadata)
```


## Cloud Profiler

Cloud Profiler allows you to profile your remote Vertex AI Training jobs on demand and visualize the results in Vertex AI Tensorboard.

To start using the profiler with TensorFlow, update your training script to include the following:

```
from google.cloud.aiplatform.training_utils import cloud_profiler
...
cloud_profiler.init()
```


Next, run the job with with a Vertex AI TensorBoard instance. For full details on how to do this, visit [https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview](https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview)

Finally, visit your TensorBoard in your Google Cloud Console, navigate to the “Profile” tab, and click the Capture Profile button. This will allow users to capture profiling statistics for the running jobs.

### Next Steps

Read the

[Client Library Documentation](https://cloud.google.com/python/docs/reference/aiplatform/latest)for Vertex AI API to see other available methods on the client.Read the

[Vertex AI API Product documentation](https://cloud.google.com/vertex-ai/docs)to learn more about the product and see How-to Guides.View this

[README](https://github.com/googleapis/google-cloud-python/blob/main/README.rst)to see the full list of Cloud APIs that we cover.


---

<!-- DOCUMENTO FUSIONADO: a-z0-9-061a-z0-9.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/[a-z0-9-]{0,61}[a-z0-9] -->

# Vertex AI SDK for Python

## Gemini API and Generative AI on Vertex AI

**NOTE**: For Gemini API and Generative AI on Vertex AI, please reference [Vertex Generative AI SDK for Python](https://cloud.google.com/vertex-ai/generative-ai/docs/reference/python/latest)

[Vertex AI](https://cloud.google.com/vertex-ai/docs): Google Vertex AI is an integrated suite of machine learning tools and services for building and using ML models with AutoML or custom code. It offers both novices and experts the best workbench for the entire machine learning development lifecycle.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-aiplatform
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-aiplatform
```


#### Supported Python Versions

Python >= 3.8

#### Deprecated Python Versions

Python <= 3.7.

The last version of this library compatible with Python 3.6 is google-cloud-aiplatform==1.12.1.

### Overview

This section provides a brief overview of the Vertex AI SDK for Python. You can also reference the notebooks in [vertex-ai-samples](https://github.com/GoogleCloudPlatform/vertex-ai-samples/tree/main/notebooks/community/sdk) for examples.

All publicly available SDK features can be found in the `google/cloud/aiplatform`

directory.
Under the hood, Vertex SDK builds on top of GAPIC, which stands for Google API CodeGen.
The GAPIC library code sits in `google/cloud/aiplatform_v1`

and `google/cloud/aiplatform_v1beta1`

,
and it is auto-generated from Google’s service proto files.

For most developers’ programmatic needs, they can follow these steps to figure out which libraries to import:

Look through

`google/cloud/aiplatform`

first – Vertex SDK’s APIs will almost always be easier to use and more concise comparing with GAPICIf the feature that you are looking for cannot be found there, look through

`aiplatform_v1`

to see if it’s available in GAPICIf it is still in beta phase, it will be available in

`aiplatform_v1beta1`


If none of the above scenarios could help you find the right tools for your task, please feel free to open a github issue and send us a feature request.

#### Importing

Vertex AI SDK resource based functionality can be used by importing the following namespace:

```
from google.cloud import aiplatform
```


#### Initialization

Initialize the SDK to store common configurations that you use with the SDK.

```
aiplatform.init(
# your Google Cloud Project ID or number
# environment default used is not set
project='my-project',
# the Vertex AI region you will use
# defaults to us-central1
location='us-central1',
# Google Cloud Storage bucket in same region as location
# used to stage artifacts
staging_bucket='gs://my_staging_bucket',
# custom google.auth.credentials.Credentials
# environment default credentials used if not set
credentials=my_credentials,
# customer managed encryption key resource name
# will be applied to all Vertex AI resources if set
encryption_spec_key_name=my_encryption_key_name,
# the name of the experiment to use to track
# logged metrics and parameters
experiment='my-experiment',
# description of the experiment above
experiment_description='my experiment description'
)
```


#### Datasets

Vertex AI provides managed tabular, text, image, and video datasets. In the SDK, datasets can be used downstream to train models.

To create a tabular dataset:

```
my_dataset = aiplatform.TabularDataset.create(
display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])
```


You can also create and import a dataset in separate steps:

```
from google.cloud import aiplatform
my_dataset = aiplatform.TextDataset.create(
display_name="my-dataset")
my_dataset.import_data(
gcs_source=['gs://path/to/my/dataset.csv'],
import_schema_uri=aiplatform.schema.dataset.ioformat.text.multi_label_classification
)
```


To get a previously created Dataset:

```
dataset = aiplatform.ImageDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
```


Vertex AI supports a variety of dataset schemas. References to these schemas are available under the
`aiplatform.schema.dataset`

namespace. For more information on the supported dataset schemas please refer to the
[Preparing data docs](https://cloud.google.com/ai-platform-unified/docs/datasets/prepare).

#### Training

The Vertex AI SDK for Python allows you train Custom and AutoML Models.

You can train custom models using a custom Python script, custom Python package, or container.

**Preparing Your Custom Code**

Vertex AI custom training enables you to train on Vertex AI datasets and produce Vertex AI models. To do so your script must adhere to the following contract:

It must read datasets from the environment variables populated by the training service:

```
os.environ['AIP_DATA_FORMAT'] # provides format of data
os.environ['AIP_TRAINING_DATA_URI'] # uri to training split
os.environ['AIP_VALIDATION_DATA_URI'] # uri to validation split
os.environ['AIP_TEST_DATA_URI'] # uri to test split
```


Please visit [Using a managed dataset in a custom training application](https://cloud.google.com/vertex-ai/docs/training/using-managed-datasets) for a detailed overview.

It must write the model artifact to the environment variable populated by the training service:

```
os.environ['AIP_MODEL_DIR']
```


**Running Training**

```
job = aiplatform.CustomTrainingJob(
display_name="my-training-job",
script_path="training_script.py",
container_uri="us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-2:latest",
requirements=["gcsfs==0.7.1"],
model_serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
model = job.run(my_dataset,
replica_count=1,
machine_type="n1-standard-4",
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


In the code block above my_dataset is managed dataset created in the Dataset section above. The model variable is a managed Vertex AI model that can be deployed or exported.

## AutoMLs

The Vertex AI SDK for Python supports AutoML tabular, image, text, video, and forecasting.

To train an AutoML tabular model:

```
dataset = aiplatform.TabularDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
job = aiplatform.AutoMLTabularTrainingJob(
display_name="train-automl",
optimization_prediction_type="regression",
optimization_objective="minimize-rmse",
)
model = job.run(
dataset=dataset,
target_column="target_column_name",
training_fraction_split=0.6,
validation_fraction_split=0.2,
test_fraction_split=0.2,
budget_milli_node_hours=1000,
model_display_name="my-automl-model",
disable_early_stopping=False,
)
```


## Models

To get a model:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
```


To upload a model:

```
model = aiplatform.Model.upload(
display_name='my-model',
artifact_uri="gs://python/to/my/model/dir",
serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
```


To deploy a model:

```
endpoint = model.deploy(machine_type="n1-standard-4",
min_replica_count=1,
max_replica_count=5
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


Please visit [Importing models to Vertex AI](https://cloud.google.com/vertex-ai/docs/general/import-model) for a detailed overview:

## Model Evaluation

The Vertex AI SDK for Python currently supports getting model evaluation metrics for all AutoML models.

To list all model evaluations for a model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
evaluations = model.list_model_evaluations()
```


To get the model evaluation resource for a given model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
# returns the first evaluation with no arguments, you can also pass the evaluation ID
evaluation = model.get_model_evaluation()
eval_metrics = evaluation.metrics
```


You can also create a reference to your model evaluation directly by passing in the resource name of the model evaluation:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name='projects/my-project/locations/us-central1/models/{MODEL_ID}/evaluations/{EVALUATION_ID}')
```


Alternatively, you can create a reference to your evaluation by passing in the model and evaluation IDs:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name={EVALUATION_ID},
model_id={MODEL_ID})
```


## Batch Prediction

To create a batch prediction job:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
batch_prediction_job = model.batch_predict(
job_display_name='my-batch-prediction-job',
instances_format='csv',
machine_type='n1-standard-4',
gcs_source=['gs://path/to/my/file.csv'],
gcs_destination_prefix='gs://path/to/my/batch_prediction/results/',
service_account='my-sa@my-project.iam.gserviceaccount.com'
)
```


You can also create a batch prediction job asynchronously by including the sync=False argument:

```
batch_prediction_job = model.batch_predict(..., sync=False)
# wait for resource to be created
batch_prediction_job.wait_for_resource_creation()
# get the state
batch_prediction_job.state
# block until job is complete
batch_prediction_job.wait()
```


## Endpoints

To create an endpoint:

```
endpoint = aiplatform.Endpoint.create(display_name='my-endpoint')
```


To deploy a model to a created endpoint:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
endpoint.deploy(model,
min_replica_count=1,
max_replica_count=5,
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


To get predictions from endpoints:

```
endpoint.predict(instances=[[6.7, 3.1, 4.7, 1.5], [4.6, 3.1, 1.5, 0.2]])
```


To undeploy models from an endpoint:

```
endpoint.undeploy_all()
```


To delete an endpoint:

```
endpoint.delete()
```


## Pipelines

To create a Vertex AI Pipeline run and monitor until completion:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Execute pipeline in Vertex AI and monitor until completion
pl.run(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
# Whether this function call should be synchronous (wait for pipeline run to finish before terminating)
# or asynchronous (return immediately)
sync=True
)
```


To create a Vertex AI Pipeline without monitoring until completion, use submit instead of run:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Submit the Pipeline to Vertex AI
pl.submit(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
)
```


## Explainable AI: Get Metadata

To get metadata in dictionary format from TensorFlow 1 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v1 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder(
'gs://python/to/my/model/dir', tags=[tf.saved_model.tag_constants.SERVING]
)
generated_md = builder.get_metadata()
```


To get metadata in dictionary format from TensorFlow 2 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v2 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder('gs://python/to/my/model/dir')
generated_md = builder.get_metadata()
```


To use Explanation Metadata in endpoint deployment and model upload:

```
explanation_metadata = builder.get_metadata_protobuf()
# To deploy a model to an endpoint with explanation
model.deploy(..., explanation_metadata=explanation_metadata)
# To deploy a model to a created endpoint with explanation
endpoint.deploy(..., explanation_metadata=explanation_metadata)
# To upload a model with explanation
aiplatform.Model.upload(..., explanation_metadata=explanation_metadata)
```


## Cloud Profiler

Cloud Profiler allows you to profile your remote Vertex AI Training jobs on demand and visualize the results in Vertex AI Tensorboard.

To start using the profiler with TensorFlow, update your training script to include the following:

```
from google.cloud.aiplatform.training_utils import cloud_profiler
...
cloud_profiler.init()
```


Next, run the job with with a Vertex AI TensorBoard instance. For full details on how to do this, visit [https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview](https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview)

Finally, visit your TensorBoard in your Google Cloud Console, navigate to the “Profile” tab, and click the Capture Profile button. This will allow users to capture profiling statistics for the running jobs.

### Next Steps

Read the

[Client Library Documentation](https://cloud.google.com/python/docs/reference/aiplatform/latest)for Vertex AI API to see other available methods on the client.Read the

[Vertex AI API Product documentation](https://cloud.google.com/vertex-ai/docs)to learn more about the product and see How-to Guides.View this

[README](https://github.com/googleapis/google-cloud-python/blob/main/README.rst)to see the full list of Cloud APIs that we cover.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicespipeline_servicepipelineserviceclient______7af6ca.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicespipeline_servicepipelineserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient -->

# Class PipelineServiceClient (1.134.0)

```
PipelineServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### PipelineServiceClient

```
PipelineServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the pipeline service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the PipelineServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_batch_cancel_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchCancelPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_cancel_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_batch_cancel_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchCancelPipelineJobs. |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_batch_delete_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchDeletePipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchDeletePipelineJobsRequest.html)(
parent="parent_value",
names=['names_value1', 'names_value2'],
)
# Make the request
operation = client.[batch_delete_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_batch_delete_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.BatchDeletePipelineJobs. |
`parent` |
`str`
Required. The name of the PipelineJobs' parent resource. Format: |
`names` |
`MutableSequence[str]`
Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_cancel_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelPipelineJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_cancel_pipeline_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CancelPipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
def sample_cancel_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_cancel_training_pipeline)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CancelTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline to cancel. Format: |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_create_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreatePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePipelineJobRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_create_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CreatePipelineJob. |
`parent` |
`str`
Required. The resource name of the Location to create the PipelineJob in. Format: |
`pipeline_job` |
Required. The PipelineJob to create. This corresponds to the |
`pipeline_job_id` |
`str`
The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated. This value should be less than 128 characters, and valid characters are |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_create_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
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
response = client.[create_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_create_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.CreateTrainingPipeline. |
`parent` |
`str`
Required. The resource name of the Location to create the TrainingPipeline in. Format: |
`training_pipeline` |
Required. The TrainingPipeline to create. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeletePipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePipelineJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_delete_pipeline_job)(request=request)
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
The request object. Request message for PipelineService.DeletePipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob resource to be deleted. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_delete_training_pipeline)(request=request)
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
The request object. Request message for PipelineService.DeleteTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline resource to be deleted. Format: |
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
`PipelineServiceClient` |
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
`PipelineServiceClient` |
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
`PipelineServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_pipeline_job():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetPipelineJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPipelineJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_pipeline_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_get_pipeline_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.GetPipelineJob. |
`name` |
`str`
Required. The name of the PipelineJob resource. Format: |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_training_pipeline():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTrainingPipelineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTrainingPipelineRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_training_pipeline](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_get_training_pipeline)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PipelineService.GetTrainingPipeline. |
`name` |
`str`
Required. The name of the TrainingPipeline resource. Format: |
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
The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model. |

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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListPipelineJobsPager
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
def sample_list_pipeline_jobs():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListPipelineJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_pipeline_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_list_pipeline_jobs)(request=request)
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
The request object. Request message for PipelineService.ListPipelineJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the PipelineJobs from. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesPager
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
def sample_list_training_pipelines():
# Create a client
client = aiplatform_v1beta1.
```[PipelineServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTrainingPipelinesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_training_pipelines](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.PipelineServiceClient.html#google_cloud_aiplatform_v1beta1_services_pipeline_service_PipelineServiceClient_list_training_pipelines)(request=request)
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
The request object. Request message for PipelineService.ListTrainingPipelines. |
`parent` |
`str`
Required. The resource name of the Location to list the TrainingPipelines from. Format: |
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1servicesgen_ai_tuning_servicepagers__googlecloudaipl_14ef4a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesgen_ai_tuning_servicepagers__googlecloudaipla_1c9cd1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesgen_ai_tuning_servicepagers__googlecloudaiplat_4ae771.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesgen_ai_tuning_servicepagers__googlecloudaiplatf_69fd51.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesgen_ai_tuning_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.gen_ai_tuning_service.pagers`

module.

## Classes

[ListTuningJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers.ListTuningJobsAsyncPager)

```
ListTuningJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse,
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


A pager for iterating through `list_tuning_jobs`

requests.

This class thinly wraps an initial
[ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tuning_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTuningJobs`

requests and continue to iterate
through the `tuning_jobs`

field on the
corresponding responses.

All the usual [ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTuningJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers.ListTuningJobsPager)

```
ListTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse,
],
request: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse,
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


A pager for iterating through `list_tuning_jobs`

requests.

This class thinly wraps an initial
[ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`tuning_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTuningJobs`

requests and continue to iterate
through the `tuning_jobs`

field on the
corresponding responses.

All the usual [ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespipelinetaskexecutordetailcontainerdetail_googlecl_d1a0ca.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespipelinetaskexecutordetailcontainerdetail.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineTaskExecutorDetail.ContainerDetail -->

# Class ContainerDetail (1.134.0)

`ContainerDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The detail of a container execution. It contains the job names of the lifecycle of a container execution.

## Attributes |
|
|---|---|
Name |
Description |
`main_job` |
`str`
Output only. The name of the CustomJob for the main container execution. |
`pre_caching_check_job` |
`str`
Output only. The name of the CustomJob for the pre-caching-check container execution. This job will be available if the PipelineJob.pipeline_spec specifies the `pre_caching_check` hook in the lifecycle
events.
|
`failed_main_jobs` |
`MutableSequence[str]`
Output only. The names of the previously failed CustomJob for the main container executions. The list includes the all attempts in chronological order. |
`failed_pre_caching_check_jobs` |
`MutableSequence[str]`
Output only. The names of the previously failed CustomJob for the pre-caching-check container executions. This job will be available if the PipelineJob.pipeline_spec specifies the `pre_caching_check` hook in the lifecycle
events. The list includes the all attempts in chronological
order.
|

## Methods

### ContainerDetail

`ContainerDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The detail of a container execution. It contains the job names of the lifecycle of a container execution.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestimestampsplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TimestampSplit -->

# Class TimestampSplit (1.134.0)

`TimestampSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on a provided timestamps. The youngest data pieces are assigned to training set, next to validation set, and the oldest to the test set.

Supported only for tabular Datasets.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |
`key` |
`str`
Required. The key is a name of one of the Dataset's data columns. The values of the key (the values in the column) must be in RFC 3339 `date-time` format, where
`time-offset` = `"Z"` (e.g. 1985-04-12T23:20:50.52Z). If
for a piece of data the key is not present or has an invalid
value, that piece is ignored by the pipeline.
|

## Methods

### TimestampSplit

`TimestampSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on a provided timestamps. The youngest data pieces are assigned to training set, next to validation set, and the oldest to the test set.

Supported only for tabular Datasets.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typessupervisedtuningdatasetdistribution_googlecloudai_82165d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessupervisedtuningdatasetdistribution_googlecloudaip_69740b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessupervisedtuningdatasetdistribution.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SupervisedTuningDatasetDistribution -->

# Class SupervisedTuningDatasetDistribution (1.134.0)

```
SupervisedTuningDatasetDistribution(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Dataset distribution for Supervised Tuning.

## Attributes |
|
|---|---|
Name |
Description |
`sum` |
`int`
Output only. Sum of a given population of values. |
`billable_sum` |
`int`
Output only. Sum of a given population of values that are billable. |
`min_` |
`float`
Output only. The minimum of the population values. |
`max_` |
`float`
Output only. The maximum of the population values. |
`mean` |
`float`
Output only. The arithmetic mean of the values in the population. |
`median` |
`float`
Output only. The median of the values in the population. |
`p5` |
`float`
Output only. The 5th percentile of the values in the population. |
`p95` |
`float`
Output only. The 95th percentile of the values in the population. |
`buckets` |
`MutableSequence[`
Output only. Defines the histogram bucket. |

## Classes

### DatasetBucket

`DatasetBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.

## Methods

### SupervisedTuningDatasetDistribution

```
SupervisedTuningDatasetDistribution(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Dataset distribution for Supervised Tuning.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturestoreonlineservingconfigscaling.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Featurestore.OnlineServingConfig.Scaling -->

# Class Scaling (1.134.0)

`Scaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Online serving scaling configuration. If min_node_count and max_node_count are set to the same value, the cluster will be configured with the fixed number of node (no auto-scaling).

## Attributes |
|
|---|---|
Name |
Description |
`min_node_count` |
`int`
Required. The minimum number of nodes to scale down to. Must be greater than or equal to 1. |
`max_node_count` |
`int`
The maximum number of nodes to scale up to. Must be greater than min_node_count, and less than or equal to 10 times of 'min_node_count'. |
`cpu_utilization_target` |
`int`
Optional. The cpu utilization that the Autoscaler should be trying to achieve. This number is on a scale from 0 (no utilization) to 100 (total utilization), and is limited between 10 and 80. When a cluster's CPU utilization exceeds the target that you have set, Bigtable immediately adds nodes to the cluster. When CPU utilization is substantially lower than the target, Bigtable removes nodes. If not set or set to 0, default to 50. |

## Methods

### Scaling

`Scaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Online serving scaling configuration. If min_node_count and max_node_count are set to the same value, the cluster will be configured with the fixed number of node (no auto-scaling).


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfeatureselector_googlecloudaiplatform_v1type_84e799.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureselector_googlecloudaiplatform_v1types_419fb6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureselector.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureSelector -->

# Class FeatureSelector (1.134.0)

`FeatureSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for Features of an EntityType.

## Attribute |
|
|---|---|
Name |
Description |
`id_matcher` |
Required. Matches Features based on ID. |

## Methods

### FeatureSelector

`FeatureSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for Features of an EntityType.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgoogledrivesourceresourceidresourcetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GoogleDriveSource.ResourceId.ResourceType -->

# Class ResourceType (1.134.0)

`ResourceType(value)`


The type of the Google Drive resource.

## Enums |
|
|---|---|
Name |
Description |
`RESOURCE_TYPE_UNSPECIFIED` |
Unspecified resource type. |
`RESOURCE_TYPE_FILE` |
File resource type. |
`RESOURCE_TYPE_FOLDER` |
Folder resource type. |

## Methods

### ResourceType

`ResourceType(value)`


The type of the Google Drive resource.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescoherenceinput_googlecloudaiplatform_v1beta1typese_5b128e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescoherenceinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CoherenceInput -->

# Class CoherenceInput (1.134.0)

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for coherence score metric. |
`instance` |
Required. Coherence instance. |

## Methods

### CoherenceInput

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeseventtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Event.Type -->

# Class Type (1.134.0)

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Unspecified whether input or output of the Execution. |
`INPUT` |
An input of the Execution. |
`OUTPUT` |
An output of the Execution. |

## Methods

### Type

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.


---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest -->

# Vertex AI SDK for Python

## Gemini API and Generative AI on Vertex AI

**NOTE**: For Gemini API and Generative AI on Vertex AI, please reference [Vertex Generative AI SDK for Python](https://cloud.google.com/vertex-ai/generative-ai/docs/reference/python/latest)

[Vertex AI](https://cloud.google.com/vertex-ai/docs): Google Vertex AI is an integrated suite of machine learning tools and services for building and using ML models with AutoML or custom code. It offers both novices and experts the best workbench for the entire machine learning development lifecycle.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-aiplatform
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-aiplatform
```


#### Supported Python Versions

Python >= 3.8

#### Deprecated Python Versions

Python <= 3.7.

The last version of this library compatible with Python 3.6 is google-cloud-aiplatform==1.12.1.

### Overview

This section provides a brief overview of the Vertex AI SDK for Python. You can also reference the notebooks in [vertex-ai-samples](https://github.com/GoogleCloudPlatform/vertex-ai-samples/tree/main/notebooks/community/sdk) for examples.

All publicly available SDK features can be found in the `google/cloud/aiplatform`

directory.
Under the hood, Vertex SDK builds on top of GAPIC, which stands for Google API CodeGen.
The GAPIC library code sits in `google/cloud/aiplatform_v1`

and `google/cloud/aiplatform_v1beta1`

,
and it is auto-generated from Google’s service proto files.

For most developers’ programmatic needs, they can follow these steps to figure out which libraries to import:

Look through

`google/cloud/aiplatform`

first – Vertex SDK’s APIs will almost always be easier to use and more concise comparing with GAPICIf the feature that you are looking for cannot be found there, look through

`aiplatform_v1`

to see if it’s available in GAPICIf it is still in beta phase, it will be available in

`aiplatform_v1beta1`


If none of the above scenarios could help you find the right tools for your task, please feel free to open a github issue and send us a feature request.

#### Importing

Vertex AI SDK resource based functionality can be used by importing the following namespace:

```
from google.cloud import aiplatform
```


#### Initialization

Initialize the SDK to store common configurations that you use with the SDK.

```
aiplatform.init(
# your Google Cloud Project ID or number
# environment default used is not set
project='my-project',
# the Vertex AI region you will use
# defaults to us-central1
location='us-central1',
# Google Cloud Storage bucket in same region as location
# used to stage artifacts
staging_bucket='gs://my_staging_bucket',
# custom google.auth.credentials.Credentials
# environment default credentials used if not set
credentials=my_credentials,
# customer managed encryption key resource name
# will be applied to all Vertex AI resources if set
encryption_spec_key_name=my_encryption_key_name,
# the name of the experiment to use to track
# logged metrics and parameters
experiment='my-experiment',
# description of the experiment above
experiment_description='my experiment description'
)
```


#### Datasets

Vertex AI provides managed tabular, text, image, and video datasets. In the SDK, datasets can be used downstream to train models.

To create a tabular dataset:

```
my_dataset = aiplatform.TabularDataset.create(
display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])
```


You can also create and import a dataset in separate steps:

```
from google.cloud import aiplatform
my_dataset = aiplatform.TextDataset.create(
display_name="my-dataset")
my_dataset.import_data(
gcs_source=['gs://path/to/my/dataset.csv'],
import_schema_uri=aiplatform.schema.dataset.ioformat.text.multi_label_classification
)
```


To get a previously created Dataset:

```
dataset = aiplatform.ImageDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
```


Vertex AI supports a variety of dataset schemas. References to these schemas are available under the
`aiplatform.schema.dataset`

namespace. For more information on the supported dataset schemas please refer to the
[Preparing data docs](https://cloud.google.com/ai-platform-unified/docs/datasets/prepare).

#### Training

The Vertex AI SDK for Python allows you train Custom and AutoML Models.

You can train custom models using a custom Python script, custom Python package, or container.

**Preparing Your Custom Code**

Vertex AI custom training enables you to train on Vertex AI datasets and produce Vertex AI models. To do so your script must adhere to the following contract:

It must read datasets from the environment variables populated by the training service:

```
os.environ['AIP_DATA_FORMAT'] # provides format of data
os.environ['AIP_TRAINING_DATA_URI'] # uri to training split
os.environ['AIP_VALIDATION_DATA_URI'] # uri to validation split
os.environ['AIP_TEST_DATA_URI'] # uri to test split
```


Please visit [Using a managed dataset in a custom training application](https://cloud.google.com/vertex-ai/docs/training/using-managed-datasets) for a detailed overview.

It must write the model artifact to the environment variable populated by the training service:

```
os.environ['AIP_MODEL_DIR']
```


**Running Training**

```
job = aiplatform.CustomTrainingJob(
display_name="my-training-job",
script_path="training_script.py",
container_uri="us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-2:latest",
requirements=["gcsfs==0.7.1"],
model_serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
model = job.run(my_dataset,
replica_count=1,
machine_type="n1-standard-4",
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


In the code block above my_dataset is managed dataset created in the Dataset section above. The model variable is a managed Vertex AI model that can be deployed or exported.

## AutoMLs

The Vertex AI SDK for Python supports AutoML tabular, image, text, video, and forecasting.

To train an AutoML tabular model:

```
dataset = aiplatform.TabularDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
job = aiplatform.AutoMLTabularTrainingJob(
display_name="train-automl",
optimization_prediction_type="regression",
optimization_objective="minimize-rmse",
)
model = job.run(
dataset=dataset,
target_column="target_column_name",
training_fraction_split=0.6,
validation_fraction_split=0.2,
test_fraction_split=0.2,
budget_milli_node_hours=1000,
model_display_name="my-automl-model",
disable_early_stopping=False,
)
```


## Models

To get a model:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
```


To upload a model:

```
model = aiplatform.Model.upload(
display_name='my-model',
artifact_uri="gs://python/to/my/model/dir",
serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
```


To deploy a model:

```
endpoint = model.deploy(machine_type="n1-standard-4",
min_replica_count=1,
max_replica_count=5
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


Please visit [Importing models to Vertex AI](https://cloud.google.com/vertex-ai/docs/general/import-model) for a detailed overview:

## Model Evaluation

The Vertex AI SDK for Python currently supports getting model evaluation metrics for all AutoML models.

To list all model evaluations for a model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
evaluations = model.list_model_evaluations()
```


To get the model evaluation resource for a given model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
# returns the first evaluation with no arguments, you can also pass the evaluation ID
evaluation = model.get_model_evaluation()
eval_metrics = evaluation.metrics
```


You can also create a reference to your model evaluation directly by passing in the resource name of the model evaluation:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name='projects/my-project/locations/us-central1/models/{MODEL_ID}/evaluations/{EVALUATION_ID}')
```


Alternatively, you can create a reference to your evaluation by passing in the model and evaluation IDs:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name={EVALUATION_ID},
model_id={MODEL_ID})
```


## Batch Prediction

To create a batch prediction job:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
batch_prediction_job = model.batch_predict(
job_display_name='my-batch-prediction-job',
instances_format='csv',
machine_type='n1-standard-4',
gcs_source=['gs://path/to/my/file.csv'],
gcs_destination_prefix='gs://path/to/my/batch_prediction/results/',
service_account='my-sa@my-project.iam.gserviceaccount.com'
)
```


You can also create a batch prediction job asynchronously by including the sync=False argument:

```
batch_prediction_job = model.batch_predict(..., sync=False)
# wait for resource to be created
batch_prediction_job.wait_for_resource_creation()
# get the state
batch_prediction_job.state
# block until job is complete
batch_prediction_job.wait()
```


## Endpoints

To create an endpoint:

```
endpoint = aiplatform.Endpoint.create(display_name='my-endpoint')
```


To deploy a model to a created endpoint:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
endpoint.deploy(model,
min_replica_count=1,
max_replica_count=5,
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


To get predictions from endpoints:

```
endpoint.predict(instances=[[6.7, 3.1, 4.7, 1.5], [4.6, 3.1, 1.5, 0.2]])
```


To undeploy models from an endpoint:

```
endpoint.undeploy_all()
```


To delete an endpoint:

```
endpoint.delete()
```


## Pipelines

To create a Vertex AI Pipeline run and monitor until completion:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Execute pipeline in Vertex AI and monitor until completion
pl.run(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
# Whether this function call should be synchronous (wait for pipeline run to finish before terminating)
# or asynchronous (return immediately)
sync=True
)
```


To create a Vertex AI Pipeline without monitoring until completion, use submit instead of run:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Submit the Pipeline to Vertex AI
pl.submit(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
)
```


## Explainable AI: Get Metadata

To get metadata in dictionary format from TensorFlow 1 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v1 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder(
'gs://python/to/my/model/dir', tags=[tf.saved_model.tag_constants.SERVING]
)
generated_md = builder.get_metadata()
```


To get metadata in dictionary format from TensorFlow 2 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v2 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder('gs://python/to/my/model/dir')
generated_md = builder.get_metadata()
```


To use Explanation Metadata in endpoint deployment and model upload:

```
explanation_metadata = builder.get_metadata_protobuf()
# To deploy a model to an endpoint with explanation
model.deploy(..., explanation_metadata=explanation_metadata)
# To deploy a model to a created endpoint with explanation
endpoint.deploy(..., explanation_metadata=explanation_metadata)
# To upload a model with explanation
aiplatform.Model.upload(..., explanation_metadata=explanation_metadata)
```


## Cloud Profiler

Cloud Profiler allows you to profile your remote Vertex AI Training jobs on demand and visualize the results in Vertex AI Tensorboard.

To start using the profiler with TensorFlow, update your training script to include the following:

```
from google.cloud.aiplatform.training_utils import cloud_profiler
...
cloud_profiler.init()
```


Next, run the job with with a Vertex AI TensorBoard instance. For full details on how to do this, visit [https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview](https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview)

Finally, visit your TensorBoard in your Google Cloud Console, navigate to the “Profile” tab, and click the Capture Profile button. This will allow users to capture profiling statistics for the running jobs.

### Next Steps

Read the

[Client Library Documentation](https://cloud.google.com/python/docs/reference/aiplatform/latest)for Vertex AI API to see other available methods on the client.Read the

[Vertex AI API Product documentation](https://cloud.google.com/vertex-ai/docs)to learn more about the product and see How-to Guides.View this

[README](https://github.com/googleapis/google-cloud-python/blob/main/README.rst)to see the full list of Cloud APIs that we cover.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesexportmodelrequestoutputconfig_googlecloudaipla_301efa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesexportmodelrequestoutputconfig_googlecloudaiplat_afc32a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesexportmodelrequestoutputconfig_googlecloudaiplatf_986aa6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexportmodelrequestoutputconfig_googlecloudaiplatfo_0f4596.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportmodelrequestoutputconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelRequest.OutputConfig -->

# Class OutputConfig (1.134.0)

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output configuration for the Model export.

## Attributes |
|
|---|---|
Name |
Description |
`export_format_id` |
`str`
The ID of the format in which the Model must be exported. Each Model lists the [export formats it supports][google.cloud.aiplatform.v1.Model.supported_export_formats]. If no value is provided here, then the first from the list of the Model's supported formats is used by default. |
`artifact_destination` |
The Cloud Storage location where the Model artifact is to be written to. Under the directory given as the destination a new one with name " `model-export-` ",
where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601
format, will be created. Inside, the Model and any of its
supporting files will be written. This field should only be
set when the `exportableContent` field of the
[Model.supported_export_formats] object contains
`ARTIFACT` .
|
`image_destination` |
The Google Container Registry or Artifact Registry uri where the Model container image will be copied to. This field should only be set when the `exportableContent` field of
the [Model.supported_export_formats] object contains
`IMAGE` .
|

## Methods

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output configuration for the Model export.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestimestampsplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TimestampSplit -->

# Class TimestampSplit (1.134.0)

`TimestampSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on a provided timestamps. The youngest data pieces are assigned to training set, next to validation set, and the oldest to the test set.

Supported only for tabular Datasets.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |
`key` |
`str`
Required. The key is a name of one of the Dataset's data columns. The values of the key (the values in the column) must be in RFC 3339 `date-time` format, where
`time-offset` = `"Z"` (e.g. 1985-04-12T23:20:50.52Z). If
for a piece of data the key is not present or has an invalid
value, that piece is ignored by the pipeline.
|

## Methods

### TimestampSplit

`TimestampSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on a provided timestamps. The youngest data pieces are assigned to training set, next to validation set, and the oldest to the test set.

Supported only for tabular Datasets.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessupervisedtuningdatasetdistribution_googleclo_d9f2a9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessupervisedtuningdatasetdistribution.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SupervisedTuningDatasetDistribution -->

# Class SupervisedTuningDatasetDistribution (1.134.0)

```
SupervisedTuningDatasetDistribution(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Dataset distribution for Supervised Tuning.

## Attributes |
|
|---|---|
Name |
Description |
`sum` |
`int`
Output only. Sum of a given population of values. |
`billable_sum` |
`int`
Output only. Sum of a given population of values that are billable. |
`min_` |
`float`
Output only. The minimum of the population values. |
`max_` |
`float`
Output only. The maximum of the population values. |
`mean` |
`float`
Output only. The arithmetic mean of the values in the population. |
`median` |
`float`
Output only. The median of the values in the population. |
`p5` |
`float`
Output only. The 5th percentile of the values in the population. |
`p95` |
`float`
Output only. The 95th percentile of the values in the population. |
`buckets` |
`MutableSequence[`
Output only. Defines the histogram bucket. |

## Classes

### DatasetBucket

`DatasetBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.

## Methods

### SupervisedTuningDatasetDistribution

```
SupervisedTuningDatasetDistribution(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Dataset distribution for Supervised Tuning.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturestoreonlineservingconfigscaling.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Featurestore.OnlineServingConfig.Scaling -->

# Class Scaling (1.134.0)

`Scaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Online serving scaling configuration. If min_node_count and max_node_count are set to the same value, the cluster will be configured with the fixed number of node (no auto-scaling).

## Attributes |
|
|---|---|
Name |
Description |
`min_node_count` |
`int`
Required. The minimum number of nodes to scale down to. Must be greater than or equal to 1. |
`max_node_count` |
`int`
The maximum number of nodes to scale up to. Must be greater than min_node_count, and less than or equal to 10 times of 'min_node_count'. |
`cpu_utilization_target` |
`int`
Optional. The cpu utilization that the Autoscaler should be trying to achieve. This number is on a scale from 0 (no utilization) to 100 (total utilization), and is limited between 10 and 80. When a cluster's CPU utilization exceeds the target that you have set, Bigtable immediately adds nodes to the cluster. When CPU utilization is substantially lower than the target, Bigtable removes nodes. If not set or set to 0, default to 50. |

## Methods

### Scaling

`Scaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Online serving scaling configuration. If min_node_count and max_node_count are set to the same value, the cluster will be configured with the fixed number of node (no auto-scaling).


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesnasjobspec__googlecloudaiplatform_v1beta1typesrem_70b1dc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnasjobspec__googlecloudaiplatform_v1beta1typesremo_580a65.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnasjobspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJobSpec -->

# Class NasJobSpec (1.134.0)

`NasJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a NasJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`multi_trial_algorithm_spec` |
The spec of multi-trial algorithms. This field is a member of `oneof` _ `nas_algorithm_spec` .
|
`resume_nas_job_id` |
`str`
The ID of the existing NasJob in the same Project and Location which will be used to resume search. search_space_spec and nas_algorithm_spec are obtained from previous NasJob hence should not provide them again for this NasJob. |
`search_space_spec` |
`str`
It defines the search space for Neural Architecture Search (NAS). |

## Classes

### MultiTrialAlgorithmSpec

`MultiTrialAlgorithmSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of multi-trial Neural Architecture Search (NAS).

## Methods

### NasJobSpec

`NasJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a NasJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesremovecontextchildrenresponse_googlecloudaipl_737c0d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesremovecontextchildrenresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveContextChildrenResponse -->

# Class RemoveContextChildrenResponse (1.134.0)

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.

## Methods

### RemoveContextChildrenResponse

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescoherenceinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceInput -->

# Class CoherenceInput (1.134.0)

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for coherence score metric. |
`instance` |
Required. Coherence instance. |

## Methods

### CoherenceInput

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmetadataschema__googlecloudaiplatform_v1types_0397cd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmetadataschema.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetadataSchema -->

# Class MetadataSchema (1.134.0)

`MetadataSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general MetadataSchema.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the MetadataSchema. |
`schema_version` |
`str`
The version of the MetadataSchema. The version's format must match the following regular expression: `^[0-9]+` .][0-9]`+` .][0-9]`+$` , which would allow to
order/compare different versions. Example: 1.0.0, 1.0.1,
etc.
|
`schema` |
`str`
Required. The raw YAML string representation of the MetadataSchema. The combination of [MetadataSchema.version] and the schema name given by `title` in
[MetadataSchema.schema] must be unique within a
MetadataStore.
The schema is defined as an OpenAPI 3.0.2 `MetadataSchema
Object |
`schema_type` |
The type of the MetadataSchema. This is a property that identifies which metadata types will use the MetadataSchema. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MetadataSchema was created. |
`description` |
`str`
Description of the Metadata Schema |

## Classes

### MetadataSchemaType

`MetadataSchemaType(value)`


Describes the type of the MetadataSchema.

## Methods

### MetadataSchema

`MetadataSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general MetadataSchema.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesport_googlecloudaiplatform_v1beta1typespresetsmoda_2b2f19.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesport.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Port -->

# Class Port (1.134.0)

`Port(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a network port in a container.

## Attribute |
|
|---|---|
Name |
Description |
`container_port` |
`int`
The number of the port to expose on the pod's IP address. Must be a valid port number, between 1 and 65535 inclusive. |

## Methods

### Port

`Port(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a network port in a container.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespresetsmodality.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Presets.Modality -->

# Class Modality (1.134.0)

`Modality(value)`


Preset option controlling parameters for different modalities

## Enums |
|
|---|---|
Name |
Description |
`MODALITY_UNSPECIFIED` |
Should not be set. Added as a recommended best practice for enums |
`IMAGE` |
IMAGE modality |
`TEXT` |
TEXT modality |
`TABULAR` |
TABULAR modality |

## Methods

### Modality

`Modality(value)`


Preset option controlling parameters for different modalities


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesbleuinput_googlecloudaiplatform_v1beta1typ_5abe24.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesbleuinput_googlecloudaiplatform_v1beta1type_2ef16e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesbleuinput_googlecloudaiplatform_v1beta1types_a09283.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesbleuinput_googlecloudaiplatform_v1beta1typesg_c962d4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbleuinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BleuInput -->

# Class BleuInput (1.134.0)

`BleuInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for bleu metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for bleu score metric. |
`instances` |
`MutableSequence[`
Required. Repeated bleu instances. |

## Methods

### BleuInput

`BleuInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for bleu metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgoogledrivesourceresourceidresourcetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GoogleDriveSource.ResourceId.ResourceType -->

# Class ResourceType (1.134.0)

`ResourceType(value)`


The type of the Google Drive resource.

## Enums |
|
|---|---|
Name |
Description |
`RESOURCE_TYPE_UNSPECIFIED` |
Unspecified resource type. |
`RESOURCE_TYPE_FILE` |
File resource type. |
`RESOURCE_TYPE_FOLDER` |
Folder resource type. |

## Methods

### ResourceType

`ResourceType(value)`


The type of the Google Drive resource.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespublishermodelcalltoactionopennotebooks_googleclou_5cbffb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespublishermodelcalltoactionopennotebooks.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.OpenNotebooks -->

# Class OpenNotebooks (1.134.0)

`OpenNotebooks(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open notebooks.

## Attribute |
|
|---|---|
Name |
Description |
`notebooks` |
`MutableSequence[`
Required. Regional resource references to notebooks. |

## Methods

### OpenNotebooks

`OpenNotebooks(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open notebooks.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragcorpuscorpustypeconfigmemorycorpus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.CorpusTypeConfig.MemoryCorpus -->

# Class MemoryCorpus (1.134.0)

`MemoryCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the memory corpus.

## Attribute |
|
|---|---|
Name |
Description |
`llm_parser` |
The LLM parser to use for the memory corpus. |

## Methods

### MemoryCorpus

`MemoryCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the memory corpus.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistdatasetsrequest_googlecloudaiplatform_v1typesm_7ba4e5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistdatasetsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsRequest -->

# Class ListDatasetsRequest (1.134.0)

`ListDatasetsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasets.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the Dataset's parent resource. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `display_name` : supports = and !=
- `metadata_schema_uri` : supports = and !=
- `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- \`labels.key:\* or labels:key - key existence
- A key including a space must be quoted.
`labels."a key"` .
Some examples:
- `displayName="myDisplayName"`
- `labels.myKey="myValue"`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
|

## Methods

### ListDatasetsRequest

`ListDatasetsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasets.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmetadatastore.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetadataStore -->

# Class MetadataStore (1.134.0)

`MetadataStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a metadata store. Contains a set of metadata that can be queried.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the MetadataStore instance. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MetadataStore was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MetadataStore was last updated. |
`encryption_spec` |
Customer-managed encryption key spec for a Metadata Store. If set, this Metadata Store and all sub-resources of this Metadata Store are secured using this key. |
`description` |
`str`
Description of the MetadataStore. |
`state` |
Output only. State information of the MetadataStore. |
`dataplex_config` |
Optional. Dataplex integration settings. |

## Classes

### DataplexConfig

`DataplexConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents Dataplex integration settings.

### MetadataStoreState

`MetadataStoreState(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents state information for a MetadataStore.

## Methods

### MetadataStore

`MetadataStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a metadata store. Contains a set of metadata that can be queried.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesbatchreadfeaturevaluesresponse_googlecloudaiplat_2769a8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesbatchreadfeaturevaluesresponse_googlecloudaiplatf_6d9192.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesbatchreadfeaturevaluesresponse_googlecloudaiplatfo_e0e667.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchreadfeaturevaluesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesResponse -->

# Class BatchReadFeatureValuesResponse (1.134.0)

```
BatchReadFeatureValuesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeaturestoreService.BatchReadFeatureValues.

## Methods

### BatchReadFeatureValuesResponse

```
BatchReadFeatureValuesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeaturestoreService.BatchReadFeatureValues.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesneighbor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Neighbor -->

# Class Neighbor (1.134.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Neighbors for example-based explanations.

## Attributes |
|
|---|---|
Name |
Description |
`neighbor_id` |
`str`
Output only. The neighbor id. |
`neighbor_distance` |
`float`
Output only. The neighbor distance. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Neighbors for example-based explanations.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnasjobspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobSpec -->

# Class NasJobSpec (1.134.0)

`NasJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a NasJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`multi_trial_algorithm_spec` |
The spec of multi-trial algorithms. This field is a member of `oneof` _ `nas_algorithm_spec` .
|
`resume_nas_job_id` |
`str`
The ID of the existing NasJob in the same Project and Location which will be used to resume search. search_space_spec and nas_algorithm_spec are obtained from previous NasJob hence should not provide them again for this NasJob. |
`search_space_spec` |
`str`
It defines the search space for Neural Architecture Search (NAS). |

## Classes

### MultiTrialAlgorithmSpec

`MultiTrialAlgorithmSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of multi-trial Neural Architecture Search (NAS).

## Methods

### NasJobSpec

`NasJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a NasJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespartnermodeltuningspec_googlecloudaiplatform__90c101.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespartnermodeltuningspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PartnerModelTuningSpec -->

# Class PartnerModelTuningSpec (1.134.0)

`PartnerModelTuningSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning spec for Partner models.

## Attributes |
|
|---|---|
Name |
Description |
`training_dataset_uri` |
`str`
Required. Cloud Storage path to file containing training dataset for tuning. The dataset must be formatted as a JSONL file. |
`validation_dataset_uri` |
`str`
Optional. Cloud Storage path to file containing validation dataset for tuning. The dataset must be formatted as a JSONL file. |
`hyper_parameters` |
`MutableMapping[str, google.protobuf.struct_pb2.Value]`
Hyperparameters for tuning. The accepted hyper_parameters and their valid range of values will differ depending on the base model. |

## Classes

### HyperParametersEntry

`HyperParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### PartnerModelTuningSpec

`PartnerModelTuningSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning spec for Partner models.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesremoveexamplesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveExamplesRequest -->

# Class RemoveExamplesRequest (1.134.0)

`RemoveExamplesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.RemoveExamples.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`stored_contents_example_filter` |
The metadata filters for StoredContentsExamples. This field is a member of `oneof` _ `metadata_filter` .
|
`example_store` |
`str`
Required. The name of the ExampleStore resource that the examples should be removed from. Format: `projects/{project}/locations/{location}/exampleStores/{example_store}`
|
`example_ids` |
`MutableSequence[str]`
Optional. Example IDs to remove. If both metadata filters and Example IDs are specified, the metadata filters will be applied to the specified examples in order to identify which should be removed. |

## Methods

### RemoveExamplesRequest

`RemoveExamplesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.RemoveExamples.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)
