---
merged_at: 2026-01-29T15:33:46.861558
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CancelExecutionRequest -->

# Class CancelExecutionRequest (0.15.0)

`CancelExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for deleting an Execution.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Execution to cancel. Format: `projects/{project}/locations/{location}/jobs/{job}/executions/{execution}` ,
where `{project}` can be project id or number.
|
`validate_only` |
`bool`
Indicates that the request should be validated without actually cancelling any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. This may be used to detect modification conflict during updates. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplit -->

# Class InstanceSplit (0.15.0)

str
Revision to which to assign this portion of
instances, if split allocation is by revision.

percent

int
Specifies percent of the instance split to
this Revision. This defaults to zero if
unspecified.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteWorkerPoolRequest -->

# Class DeleteWorkerPoolRequest (0.15.0)

`DeleteWorkerPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message to delete a WorkerPool by its full name.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The full name of the WorkerPool. Format: `projects/{project}/locations/{location}/workerPools/{worker_pool}` ,
where `{project}` can be project id or number.
|
`validate_only` |
`bool`
Optional. Indicates that the request should be validated without actually deleting any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.ExecutionReason -->

# Class ExecutionReason (0.15.0)

`ExecutionReason(value)`


Reasons specific to Execution resource.

## Enums |
|
|---|---|
Name |
Description |
`EXECUTION_REASON_UNDEFINED` |
Default value. |
`JOB_STATUS_SERVICE_POLLING_ERROR` |
Internal system error getting execution status. System will retry. |
`NON_ZERO_EXIT_CODE` |
A task reached its retry limit and the last attempt failed due to the user container exiting with a non-zero exit code. |
`CANCELLED` |
The execution was cancelled by users. |
`CANCELLING` |
The execution is in the process of being cancelled. |
`DELETED` |
The execution was deleted. |
`DELAYED_START_PENDING` |
A delayed execution is waiting for a start time. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateJobRequest -->

# Class CreateJobRequest (0.15.0)

`CreateJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for creating a Job.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location and project in which this Job should be created. Format: projects/{project}/locations/{location}, where {project} can be project id or number. |
`job` |
Required. The Job instance to create. |
`job_id` |
`str`
Required. The unique identifier for the Job. The name of the job becomes {parent}/jobs/{job_id}. |
`validate_only` |
`bool`
Indicates that the request should be validated and default values populated, without persisting the request or creating any resources. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetTaskRequest -->

# Class GetTaskRequest (0.15.0)

Request message for obtaining a Task by its full name.

Attribute

Name

Description

name

str
Required. The full name of the Task.
Format:
projects/{project}/locations/{location}/jobs/{job}/executions/{execution}/tasks/{task}

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetJobRequest -->

# Class GetJobRequest (0.15.0)

Request message for obtaining a Job by its full name.

Attribute

Name

Description

name

str
Required. The full name of the Job.
Format:
projects/{project}/locations/{location}/jobs/{job},
where {project} can be project id or number.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListInstancesRequest -->

# Class ListInstancesRequest (0.15.0)

`ListInstancesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for retrieving a list of Instances.

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
Optional. Maximum number of Instances to return in this call. |
`page_token` |
`str`
Optional. A page token received from a previous call to ListInstances. All other parameters must match. |
`show_deleted` |
`bool`
Optional. If true, returns deleted (but unexpired) resources along with active ones. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Job -->

# Class Job (0.15.0)

`Job(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Job represents the configuration of a single job, which references a container image that is run to completion.

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
`name` |
`str`
The fully qualified name of this Job. Format: projects/{project}/locations/{location}/jobs/{job} |
`uid` |
`str`
Output only. Server assigned unique identifier for the Execution. The value is a UUID4 string and guaranteed to remain unchanged until the resource is deleted. |
`generation` |
`int`
Output only. A number that monotonically increases every time the user modifies the desired state. |
`labels` |
`MutableMapping[str, str]`
Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels. .. raw:: html Cloud Run API v2 does not support labels with |
`annotations` |
`MutableMapping[str, str]`
Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. .. raw:: html Cloud Run API v2 does not support annotations with This field follows Kubernetes annotations' namespacing, limits, and rules. |
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
The launch stage as defined by `Google Cloud Platform Launch Stages |
`binary_authorization` |
Settings for the Binary Authorization feature. |
`template` |
Required. The template used to create executions for this Job. |
`observed_generation` |
`int`
Output only. The generation of this Job. See comments in `reconciling` for additional information on reconciliation
process in Cloud Run.
|
`terminal_condition` |
Output only. The Condition of this Job, containing its readiness status, and detailed error information in case it did not reach the desired state. |
`conditions` |
`MutableSequence[`
Output only. The Conditions of all other associated sub-resources. They contain additional diagnostics information in case the Job does not reach its desired state. See comments in `reconciling` for additional
information on reconciliation process in Cloud Run.
|
`execution_count` |
`int`
Output only. Number of executions created for this job. |
`latest_created_execution` |
Output only. Name of the last created execution. |
`reconciling` |
`bool`
Output only. Returns true if the Job is currently being acted upon by the system to bring it into the desired state. When a new Job is created, or an existing one is updated, Cloud Run will asynchronously perform all necessary steps to bring the Job to the desired state. This process is called reconciliation. While reconciliation is in process, `observed_generation` and `latest_succeeded_execution` ,
will have transient values that might mismatch the intended
state: Once reconciliation is over (and this field is
false), there are two possible outcomes: reconciliation
succeeded and the state matches the Job, or there was an
error, and reconciliation failed. This state can be found in
`terminal_condition.state` .
If reconciliation succeeded, the following fields will
match: `observed_generation` and `generation` ,
`latest_succeeded_execution` and
`latest_created_execution` .
If reconciliation failed, `observed_generation` and
`latest_succeeded_execution` will have the state of the
last succeeded execution or empty for newly created Job.
Additional information on the failure can be found in
`terminal_condition` and `conditions` .
|
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`start_execution_token` |
`str`
A unique string used as a suffix creating a new execution. The Job will become ready when the execution is successfully started. The sum of job name and token length must be fewer than 63 characters. This field is a member of `oneof` _ `create_execution` .
|
`run_execution_token` |
`str`
A unique string used as a suffix for creating a new execution. The Job will become ready when the execution is successfully completed. The sum of job name and token length must be fewer than 63 characters. This field is a member of `oneof` _ `create_execution` .
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
