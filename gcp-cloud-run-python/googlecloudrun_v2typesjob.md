---
source_url: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Job
fetched_at: 2026-01-26T23:10:08.241499
---

# Class Job (0.14.0)

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