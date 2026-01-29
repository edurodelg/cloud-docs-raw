---
merged_at: 2026-01-29T15:33:46.863682
merged_files: 2
---


---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPool -->

# Class WorkerPool (0.15.0)

`WorkerPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


WorkerPool acts as a top-level container that manages a set of configurations and revision templates which implement a pull-based workload. WorkerPool exists to provide a singular abstraction which can be access controlled, reasoned about, and which encapsulates software lifecycle decisions such as rollout policy and team resource ownership.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The fully qualified name of this WorkerPool. In CreateWorkerPoolRequest, this field is ignored, and instead composed from CreateWorkerPoolRequest.parent and CreateWorkerPoolRequest.worker_id. Format: `projects/{project}/locations/{location}/workerPools/{worker_id}`
|
`description` |
`str`
User-provided description of the WorkerPool. This field currently has a 512-character limit. |
`uid` |
`str`
Output only. Server assigned unique identifier for the trigger. The value is a UUID4 string and guaranteed to remain unchanged until the resource is deleted. |
`generation` |
`int`
Output only. A number that monotonically increases every time the user modifies the desired state. Please note that unlike v1, this is an int64 value. As with most Google APIs, its JSON representation will be a `string` instead of an
`integer` .
|
`labels` |
`MutableMapping[str, str]`
Optional. Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels. Cloud Run API v2 does not support labels with `run.googleapis.com` , `cloud.googleapis.com` ,
`serving.knative.dev` , or `autoscaling.knative.dev`
namespaces, and they will be rejected. All system labels in
v1 now have a corresponding field in v2 WorkerPool.
|
`annotations` |
`MutableMapping[str, str]`
Optional. Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. Cloud Run API v2 does not support annotations with `run.googleapis.com` , `cloud.googleapis.com` ,
`serving.knative.dev` , or `autoscaling.knative.dev`
namespaces, and they will be rejected in new resources. All
system annotations in v1 now have a corresponding field in
v2 WorkerPool.
.. raw:: html
This field follows Kubernetes annotations' namespacing, limits, and rules. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The creation time. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The last-modified time. |
`delete_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The deletion time. It is only populated as a response to a Delete request. |
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. For a deleted resource, the time after which it will be permamently deleted. |
`creator` |
`str`
Output only. Email address of the authenticated creator. |
`last_modifier` |
`str`
Output only. Email address of the last authenticated modifier. |
`client` |
`str`
Arbitrary identifier for the API client. |
`client_version` |
`str`
Arbitrary version identifier for the API client. |
`launch_stage` |
`google.api.launch_stage_pb2.LaunchStage`
Optional. The launch stage as defined by `Google Cloud Platform Launch Stages |
`binary_authorization` |
Optional. Settings for the Binary Authorization feature. |
`template` |
Required. The template used to create revisions for this WorkerPool. |
`instance_splits` |
`MutableSequence[`
Optional. Specifies how to distribute instances over a collection of Revisions belonging to the WorkerPool. If instance split is empty or not provided, defaults to 100% instances assigned to the latest `Ready` Revision.
|
`scaling` |
Optional. Specifies worker-pool-level scaling settings |
`observed_generation` |
`int`
Output only. The generation of this WorkerPool currently serving workloads. See comments in `reconciling` for
additional information on reconciliation process in Cloud
Run. Please note that unlike v1, this is an int64 value. As
with most Google APIs, its JSON representation will be a
`string` instead of an `integer` .
|
`terminal_condition` |
Output only. The Condition of this WorkerPool, containing its readiness status, and detailed error information in case it did not reach a serving state. See comments in `reconciling` for additional information on reconciliation
process in Cloud Run.
|
`conditions` |
`MutableSequence[`
Output only. The Conditions of all other associated sub-resources. They contain additional diagnostics information in case the WorkerPool does not reach its Serving state. See comments in `reconciling` for
additional information on reconciliation process in Cloud
Run.
|
`latest_ready_revision` |
`str`
Output only. Name of the latest revision that is serving workloads. See comments in `reconciling` for additional
information on reconciliation process in Cloud Run.
|
`latest_created_revision` |
`str`
Output only. Name of the last created revision. See comments in `reconciling` for additional information on
reconciliation process in Cloud Run.
|
`instance_split_statuses` |
`MutableSequence[`
Output only. Detailed status information for corresponding instance splits. See comments in `reconciling` for
additional information on reconciliation process in Cloud
Run.
|
`threat_detection_enabled` |
`bool`
Output only. Indicates whether Cloud Run Threat Detection monitoring is enabled for the parent project of this worker pool. |
`custom_audiences` |
`MutableSequence[str]`
Not supported, and ignored by Cloud Run. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`reconciling` |
`bool`
Output only. Returns true if the WorkerPool is currently being acted upon by the system to bring it into the desired state. When a new WorkerPool is created, or an existing one is updated, Cloud Run will asynchronously perform all necessary steps to bring the WorkerPool to the desired serving state. This process is called reconciliation. While reconciliation is in process, `observed_generation` ,
`latest_ready_revison` , `instance_split_statuses` , and
`uri` will have transient values that might mismatch the
intended state: Once reconciliation is over (and this field
is false), there are two possible outcomes: reconciliation
succeeded and the serving state matches the WorkerPool, or
there was an error, and reconciliation failed. This state
can be found in `terminal_condition.state` .
If reconciliation succeeded, the following fields will
match: `instance_splits` and `instance_split_statuses` ,
`observed_generation` and `generation` ,
`latest_ready_revision` and `latest_created_revision` .
If reconciliation failed, `instance_split_statuses` ,
`observed_generation` , and `latest_ready_revision` will
have the state of the last serving revision, or empty for
newly created WorkerPools. Additional information on the
failure can be found in `terminal_condition` and
`conditions` .
|
`etag` |
`str`
Optional. A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |

## Classes

### AnnotationsEntry

`AnnotationsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition -->

# Class Condition (0.15.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest -->

# Class RunJobRequest (0.15.0)

`RunJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message to create a new Execution of a Job.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The full name of the Job. Format: projects/{project}/locations/{location}/jobs/{job}, where {project} can be project id or number. |
`validate_only` |
`bool`
Indicates that the request should be validated without actually deleting any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |
`overrides` |
Overrides specification for a given execution of a job. If provided, overrides will be applied to update the execution or task spec. |

## Classes

### Overrides

`Overrides(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


RunJob Overrides that contains Execution fields to be overridden.

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateWorkerPoolRequest -->

# Class CreateWorkerPoolRequest (0.15.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Probe -->

# Class Probe (0.15.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TaskTemplate -->

# Class TaskTemplate (0.15.0)

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
