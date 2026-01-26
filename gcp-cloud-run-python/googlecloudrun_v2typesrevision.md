---
source_url: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Revision
fetched_at: 2026-01-26T23:10:56.023687
---

# Class Revision (0.14.0)

`Revision(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Revision is an immutable snapshot of code and configuration. A Revision references a container image. Revisions are only created by updates to its parent Service.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The unique name of this Revision. |
`uid` |
`str`
Output only. Server assigned unique identifier for the Revision. The value is a UUID4 string and guaranteed to remain unchanged until the resource is deleted. |
`generation` |
`int`
Output only. A number that monotonically increases every time the user modifies the desired state. |
`labels` |
`MutableMapping[str, str]`
Output only. Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels. |
`annotations` |
`MutableMapping[str, str]`
Output only. Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The creation time. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The last-modified time. |
`delete_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. For a deleted resource, the deletion time. It is only populated as a response to a Delete request. |
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. For a deleted resource, the time after which it will be permamently deleted. It is only populated as a response to a Delete request. |
`launch_stage` |
`google.api.launch_stage_pb2.LaunchStage`
The least stable launch stage needed to create this resource, as defined by `Google Cloud Platform Launch Stages |
`service` |
`str`
Output only. The name of the parent service. |
`scaling` |
Scaling settings for this revision. |
`vpc_access` |
VPC Access configuration for this Revision. For more information, visit https://cloud.google.com/run/docs/configuring/connecting-vpc. |
`max_instance_request_concurrency` |
`int`
Sets the maximum number of requests that each serving instance can receive. |
`timeout` |
`google.protobuf.duration_pb2.Duration`
Max allowed time for an instance to respond to a request. |
`service_account` |
`str`
Email address of the IAM service account associated with the revision of the service. The service account represents the identity of the running revision, and determines what permissions the revision has. |
`containers` |
`MutableSequence[`
Holds the single container that defines the unit of execution for this Revision. |
`volumes` |
`MutableSequence[`
A list of Volumes to make available to containers. |
`execution_environment` |
The execution environment being used to host this Revision. |
`encryption_key` |
`str`
A reference to a customer managed encryption key (CMEK) to use to encrypt this container image. For more information, go to https://cloud.google.com/run/docs/securing/using-cmek |
`service_mesh` |
Enables service mesh connectivity. |
`encryption_key_revocation_action` |
The action to take if the encryption key is revoked. |
`encryption_key_shutdown_duration` |
`google.protobuf.duration_pb2.Duration`
If encryption_key_revocation_action is SHUTDOWN, the duration before shutting down all instances. The minimum increment is 1 hour. |
`reconciling` |
`bool`
Output only. Indicates whether the resource's reconciliation is still in progress. See comments in `Service.reconciling` for additional information on
reconciliation process in Cloud Run.
|
`conditions` |
`MutableSequence[`
Output only. The Condition of this Revision, containing its readiness status, and detailed error information in case it did not reach a serving state. |
`observed_generation` |
`int`
Output only. The generation of this Revision currently serving traffic. See comments in `reconciling` for
additional information on reconciliation process in Cloud
Run.
|
`log_uri` |
`str`
Output only. The Google Console URI to obtain logs for the Revision. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`session_affinity` |
`bool`
Enable session affinity. |
`scaling_status` |
Output only. The current effective scaling settings for the revision. |
`node_selector` |
The node selector for the revision. |
`gpu_zonal_redundancy_disabled` |
`bool`
Optional. Output only. True if GPU zonal redundancy is disabled on this revision. This field is a member of `oneof` _ `_gpu_zonal_redundancy_disabled` .
|
`creator` |
`str`
Output only. Email address of the authenticated creator. |
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