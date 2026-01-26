---
merged_at: 2026-01-26T20:50:51.810160
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildConfig.EnvironmentVariablesEntry -->

# Class EnvironmentVariablesEntry (0.14.0)

Keys and values corresponding to the fields of the message.

mapping

Union[dict, .Message]

A dictionary or message to be used to determine the values for this message.

ignore_unknown_fields

Optional(bool)

If True, do not raise errors for unknown fields. Only applied if mapping is a mapping type or there are keyword parameters.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionReference.CompletionStatus -->

# Class CompletionStatus (0.14.0)

The default value. This value is used if the state is omitted.

EXECUTION_SUCCEEDED

Job execution has succeeded.

EXECUTION_FAILED

Job execution has failed.

EXECUTION_RUNNING

Job execution is running normally.

EXECUTION_PENDING

Waiting for backing resources to be provisioned.

EXECUTION_CANCELLED

Job execution has been cancelled by the user.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GCSVolumeSource -->

# Class GCSVolumeSource (0.14.0)

Represents a volume backed by a Cloud Storage bucket using
Cloud Storage FUSE.

Attributes

Name

Description

bucket

str
Cloud Storage Bucket name.

read_only

bool
If true, the volume will be mounted as read
only for all mounts.

mount_options

MutableSequence[str]
A list of additional flags to pass to the
gcsfuse CLI. Options should be specified without
the leading "--".

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest.BuildpacksBuild.EnvironmentVariablesEntry -->

# Class EnvironmentVariablesEntry (0.14.0)

Keys and values corresponding to the fields of the message.

mapping

Union[dict, .Message]

A dictionary or message to be used to determine the values for this message.

ignore_unknown_fields

Optional(bool)

If True, do not raise errors for unknown fields. Only applied if mapping is a mapping type or there are keyword parameters.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest.BuildpacksBuild -->

# Class BuildpacksBuild (0.14.0)

`BuildpacksBuild(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Build the source using Buildpacks.

## Attributes |
|
|---|---|
Name |
Description |
`runtime` |
`str`
The runtime name, e.g. 'go113'. Leave blank for generic builds. |
`function_target` |
`str`
Optional. Name of the function target if the source is a function source. Required for function builds. |
`cache_image_uri` |
`str`
Optional. cache_image_uri is the GCR/AR URL where the cache image will be stored. cache_image_uri is optional and omitting it will disable caching. This URL must be stable across builds. It is used to derive a build-specific temporary URL by substituting the tag with the build ID. The build will clean up the temporary image on a best-effort basis. |
`base_image` |
`str`
Optional. The base image to use for the build. |
`environment_variables` |
`MutableMapping[str, str]`
Optional. User-provided build-time environment variables. |
`enable_automatic_updates` |
`bool`
Optional. Whether or not the application container will be enrolled in automatic base image updates. When true, the application will be built on a scratch base image, so the base layers can be appended at run time. |
`project_descriptor` |
`str`
Optional. project_descriptor stores the path to the project descriptor file. When empty, it means that there is no project descriptor file in the source. |

## Classes

### EnvironmentVariablesEntry

`EnvironmentVariablesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateServiceRequest -->

# Class CreateServiceRequest (0.14.0)

`CreateServiceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for creating a Service.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location and project in which this service should be created. Format: projects/{project}/locations/{location}, where {project} can be project id or number. Only lowercase characters, digits, and hyphens. |
`service` |
Required. The Service instance to create. |
`service_id` |
`str`
Required. The unique identifier for the Service. It must begin with letter, and cannot end with hyphen; must contain fewer than 50 characters. The name of the service becomes {parent}/services/{service_id}. |
`validate_only` |
`bool`
Indicates that the request should be validated and default values populated, without persisting the request or creating any resources. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest -->

# Class RunJobRequest (0.14.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPool -->

# Class WorkerPool (0.14.0)

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
