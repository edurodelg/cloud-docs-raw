---
merged_at: 2026-01-26T20:50:51.811498
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typeshttpgetaction_googlecloudrun_v2typesrunjobrequestoverrid_50c660.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typeshttpgetaction_googlecloudrun_v2typesrunjobrequestoverride_5262ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeshttpgetaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.HTTPGetAction -->

# Class HTTPGetAction (0.14.0)

`HTTPGetAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HTTPGetAction describes an action based on HTTP Get requests.

## Attributes |
|
|---|---|
Name |
Description |
`path` |
`str`
Optional. Path to access on the HTTP server. Defaults to '/'. |
`http_headers` |
`MutableSequence[`
Optional. Custom headers to set in the request. HTTP allows repeated headers. |
`port` |
`int`
Optional. Port number to access on the container. Must be in the range 1 to 65535. If not specified, defaults to the exposed port of the container, which is the value of container.ports[0].containerPort. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesrunjobrequestoverridescontaineroverride.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest.Overrides.ContainerOverride -->

# Class ContainerOverride (0.14.0)

`ContainerOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per-container override specification.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The name of the container specified as a DNS_LABEL. |
`args` |
`MutableSequence[str]`
Optional. Arguments to the entrypoint. Will replace existing args for override. |
`env` |
`MutableSequence[`
List of environment variables to set in the container. Will be merged with existing env for override. |
`clear_args` |
`bool`
Optional. True if the intention is to clear out existing args list. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessecretvolumesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SecretVolumeSource -->

# Class SecretVolumeSource (0.14.0)

`SecretVolumeSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The secret's value will be presented as the content of a file whose name is defined in the item path. If no items are defined, the name of the file is the secret.

## Attributes |
|
|---|---|
Name |
Description |
`secret` |
`str`
Required. The name of the secret in Cloud Secret Manager. Format: {secret} if the secret is in the same project. projects/{project}/secrets/{secret} if the secret is in a different project. |
`items` |
`MutableSequence[`
If unspecified, the volume will expose a file whose name is the secret, relative to VolumeMount.mount_path + VolumeMount.sub_path. If specified, the key will be used as the version to fetch from Cloud Secret Manager and the path will be the name of the file exposed in the volume. When items are defined, they must specify a path and a version. |
`default_mode` |
`int`
Integer representation of mode bits to use on created files by default. Must be a value between 0000 and 0777 (octal), defaulting to 0444. Directories within the path are not affected by this setting. Notes - Internally, a umask of 0222 will be applied to any non-zero value. - This is an integer representation of the mode bits. So, the octal integer value should look exactly as the chmod numeric notation with a leading zero. Some examples: for chmod 640 (u=rw,g=r), set to 0640 (octal) or 416 (base-10). For chmod 755 (u=rwx,g=rx,o=rx), set to 0755 (octal) or 493 (base-10). - This might be in conflict with other options that affect the file mode, like fsGroup, and the result can be other mode bits set. This might be in conflict with other options that affect the file mode, like fsGroup, and as a result, other mode bits could be set. |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typesdeleteservicerequest_googlecloudrun_v2typeshttpheader__g_5729dc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesdeleteservicerequest_googlecloudrun_v2typeshttpheader.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesdeleteservicerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteServiceRequest -->

# Class DeleteServiceRequest (0.14.0)

`DeleteServiceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message to delete a Service by its full name.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The full name of the Service. Format: projects/{project}/locations/{location}/services/{service}, where {project} can be project id or number. |
`validate_only` |
`bool`
Indicates that the request should be validated without actually deleting any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeshttpheader.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.HTTPHeader -->

# Class HTTPHeader (0.14.0)

HTTPHeader describes a custom header to be used in HTTP
probes

Attributes

Name

Description

name

str
Required. The header field name

value

str
Optional. The header field value

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typeslistjobsrequest_googlecloudrun_v2typesgrpcaction.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeslistjobsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsRequest -->

# Class ListJobsRequest (0.14.0)

`ListJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for retrieving a list of Jobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location and project to list resources on. Format: projects/{project}/locations/{location}, where {project} can be project id or number. |
`page_size` |
`int`
Maximum number of Jobs to return in this call. |
`page_token` |
`str`
A page token received from a previous call to ListJobs. All other parameters must match. |
`show_deleted` |
`bool`
If true, returns deleted (but unexpired) resources along with active ones. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesgrpcaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GRPCAction -->

# Class GRPCAction (0.14.0)

`GRPCAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GRPCAction describes an action involving a GRPC port.

## Attributes |
|
|---|---|
Name |
Description |
`port` |
`int`
Optional. Port number of the gRPC service. Number must be in the range 1 to 65535. If not specified, defaults to the exposed port of the container, which is the value of container.ports[0].containerPort. |
`service` |
`str`
Optional. Service is the name of the service to place in the gRPC HealthCheckRequest (see https://github.com/grpc/grpc/blob/master/doc/health-checking.md ). If this is not specified, the default behavior is defined by gRPC. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition -->

# Class Condition (0.14.0)

`Condition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a status condition for a resource.

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
`type_` |
`str`
type is used to communicate the status of the reconciliation process. See also: https://github.com/knative/serving/blob/main/docs/spec/errors.md#error-conditions-and-reporting Types common to all resources include: - "Ready": True when the Resource is ready. |
`state` |
State of the condition. |
`message` |
`str`
Human readable message indicating details about the current status. |
`last_transition_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Last time the condition transitioned from one status to another. |
`severity` |
How to interpret failures of this condition, one of Error, Warning, Info |
`reason` |
Output only. A common (service-level) reason for this condition. This field is a member of `oneof` _ `reasons` .
|
`revision_reason` |
Output only. A reason for the revision condition. This field is a member of `oneof` _ `reasons` .
|
`execution_reason` |
Output only. A reason for the execution condition. This field is a member of `oneof` _ `reasons` .
|

## Classes

### CommonReason

`CommonReason(value)`


Reasons common to all types of conditions.

### ExecutionReason

`ExecutionReason(value)`


Reasons specific to Execution resource.

### RevisionReason

`RevisionReason(value)`


Reasons specific to Revision resource.

### Severity

`Severity(value)`


Represents the severity of the condition failures.

### State

`State(value)`


Represents the possible Condition states.

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Probe -->

# Class Probe (0.14.0)

`Probe(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

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
`initial_delay_seconds` |
`int`
Optional. Number of seconds after the container has started before the probe is initiated. Defaults to 0 seconds. Minimum value is 0. Maximum value for liveness probe is 3600. Maximum value for startup probe is 240. |
`timeout_seconds` |
`int`
Optional. Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1. Maximum value is 3600. Must be smaller than period_seconds. |
`period_seconds` |
`int`
Optional. How often (in seconds) to perform the probe. Default to 10 seconds. Minimum value is 1. Maximum value for liveness probe is 3600. Maximum value for startup probe is 240. Must be greater or equal than timeout_seconds. |
`failure_threshold` |
`int`
Optional. Minimum consecutive failures for the probe to be considered failed after having succeeded. Defaults to 3. Minimum value is 1. |
`http_get` |
Optional. HTTPGet specifies the http request to perform. Exactly one of httpGet, tcpSocket, or grpc must be specified. This field is a member of `oneof` _ `probe_type` .
|
`tcp_socket` |
Optional. TCPSocket specifies an action involving a TCP port. Exactly one of httpGet, tcpSocket, or grpc must be specified. This field is a member of `oneof` _ `probe_type` .
|
`grpc` |
Optional. GRPC specifies an action involving a gRPC port. Exactly one of httpGet, tcpSocket, or grpc must be specified. This field is a member of `oneof` _ `probe_type` .
|

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateWorkerPoolRequest -->

# Class CreateWorkerPoolRequest (0.14.0)

`CreateWorkerPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for creating a WorkerPool.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location and project in which this worker pool should be created. Format: `projects/{project}/locations/{location}` , where
`{project}` can be project id or number. Only lowercase
characters, digits, and hyphens.
|
`worker_pool` |
Required. The WorkerPool instance to create. |
`worker_pool_id` |
`str`
Required. The unique identifier for the WorkerPool. It must begin with letter, and cannot end with hyphen; must contain fewer than 50 characters. The name of the worker pool becomes `{parent}/workerPools/{worker_pool_id}` .
|
`validate_only` |
`bool`
Optional. Indicates that the request should be validated and default values populated, without persisting the request or creating any resources. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VpcAccess.NetworkInterface -->

# Class NetworkInterface (0.14.0)

`NetworkInterface(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Direct VPC egress settings.

## Attributes |
|
|---|---|
Name |
Description |
`network` |
`str`
Optional. The VPC network that the Cloud Run resource will be able to send traffic to. At least one of network or subnetwork must be specified. If both network and subnetwork are specified, the given VPC subnetwork must belong to the given VPC network. If network is not specified, it will be looked up from the subnetwork. |
`subnetwork` |
`str`
Optional. The VPC subnetwork that the Cloud Run resource will get IPs from. At least one of network or subnetwork must be specified. If both network and subnetwork are specified, the given VPC subnetwork must belong to the given VPC network. If subnetwork is not specified, the subnetwork with the same name with the network will be used. |
`tags` |
`MutableSequence[str]`
Optional. Network tags applied to this Cloud Run resource. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TaskTemplate -->

# Class TaskTemplate (0.14.0)

`TaskTemplate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TaskTemplate describes the data a task should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`containers` |
`MutableSequence[`
Holds the single container that defines the unit of execution for this task. |
`volumes` |
`MutableSequence[`
Optional. A list of Volumes to make available to containers. |
`max_retries` |
`int`
Number of retries allowed per Task, before marking this Task failed. Defaults to 3. This field is a member of `oneof` _ `retries` .
|
`timeout` |
`google.protobuf.duration_pb2.Duration`
Optional. Max allowed time duration the Task may be active before the system will actively try to mark it failed and kill associated containers. This applies per attempt of a task, meaning each retry can run for the full timeout. Defaults to 600 seconds. |
`service_account` |
`str`
Optional. Email address of the IAM service account associated with the Task of a Job. The service account represents the identity of the running task, and determines what permissions the task has. If not provided, the task will use the project's default service account. |
`execution_environment` |
Optional. The execution environment being used to host this Task. |
`encryption_key` |
`str`
A reference to a customer managed encryption key (CMEK) to use to encrypt this container image. For more information, go to https://cloud.google.com/run/docs/securing/using-cmek |
`vpc_access` |
Optional. VPC Access configuration to use for this Task. For more information, visit https://cloud.google.com/run/docs/configuring/connecting-vpc. |
`node_selector` |
Optional. The node selector for the task template. |
`gpu_zonal_redundancy_disabled` |
`bool`
Optional. True if GPU zonal redundancy is disabled on this task template. This field is a member of `oneof` _ `_gpu_zonal_redundancy_disabled` .
|
