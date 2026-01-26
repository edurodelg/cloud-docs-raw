---
source_url: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Task
fetched_at: 2026-01-26T23:12:11.946114
---

# Class Task (0.14.0)

`Task(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Task represents a single run of a container to completion.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The unique name of this Task. |
`uid` |
`str`
Output only. Server assigned unique identifier for the Task. The value is a UUID4 string and guaranteed to remain unchanged until the resource is deleted. |
`generation` |
`int`
Output only. A number that monotonically increases every time the user modifies the desired state. |
`labels` |
`MutableMapping[str, str]`
Output only. Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels |
`annotations` |
`MutableMapping[str, str]`
Output only. Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Represents time when the task was created by the system. It is not guaranteed to be set in happens-before order across separate operations. |
`scheduled_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Represents time when the task was scheduled to run by the system. It is not guaranteed to be set in happens-before order across separate operations. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Represents time when the task started to run. It is not guaranteed to be set in happens-before order across separate operations. |
`completion_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Represents time when the Task was completed. It is not guaranteed to be set in happens-before order across separate operations. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The last-modified time. |
`delete_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. For a deleted resource, the deletion time. It is only populated as a response to a Delete request. |
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. For a deleted resource, the time after which it will be permamently deleted. It is only populated as a response to a Delete request. |
`job` |
`str`
Output only. The name of the parent Job. |
`execution` |
`str`
Output only. The name of the parent Execution. |
`containers` |
`MutableSequence[`
Holds the single container that defines the unit of execution for this task. |
`volumes` |
`MutableSequence[`
A list of Volumes to make available to containers. |
`max_retries` |
`int`
Number of retries allowed per Task, before marking this Task failed. |
`timeout` |
`google.protobuf.duration_pb2.Duration`
Max allowed time duration the Task may be active before the system will actively try to mark it failed and kill associated containers. This applies per attempt of a task, meaning each retry can run for the full timeout. |
`service_account` |
`str`
Email address of the IAM service account associated with the Task of a Job. The service account represents the identity of the running task, and determines what permissions the task has. If not provided, the task will use the project's default service account. |
`execution_environment` |
The execution environment being used to host this Task. |
`reconciling` |
`bool`
Output only. Indicates whether the resource's reconciliation is still in progress. See comments in `Job.reconciling`
for additional information on reconciliation process in
Cloud Run.
|
`conditions` |
`MutableSequence[`
Output only. The Condition of this Task, containing its readiness status, and detailed error information in case it did not reach the desired state. |
`observed_generation` |
`int`
Output only. The generation of this Task. See comments in `Job.reconciling` for additional information on
reconciliation process in Cloud Run.
|
`index` |
`int`
Output only. Index of the Task, unique per execution, and beginning at 0. |
`retried` |
`int`
Output only. The number of times this Task was retried. Tasks are retried when they fail up to the maxRetries limit. |
`last_attempt_result` |
Output only. Result of the last attempt of this Task. |
`encryption_key` |
`str`
Output only. A reference to a customer managed encryption key (CMEK) to use to encrypt this container image. For more information, go to https://cloud.google.com/run/docs/securing/using-cmek |
`vpc_access` |
Output only. VPC Access configuration to use for this Task. For more information, visit https://cloud.google.com/run/docs/configuring/connecting-vpc. |
`log_uri` |
`str`
Output only. URI where logs for this execution can be found in Cloud Console. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`node_selector` |
Output only. The node selector for the task. |
`gpu_zonal_redundancy_disabled` |
`bool`
Optional. Output only. True if GPU zonal redundancy is disabled on this task. This field is a member of `oneof` _ `_gpu_zonal_redundancy_disabled` .
|
`etag` |
`str`
Output only. A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |

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