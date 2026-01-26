---
merged_at: 2026-01-26T20:50:51.812553
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPoolRevisionTemplate -->

# Class WorkerPoolRevisionTemplate (0.14.0)

`WorkerPoolRevisionTemplate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


WorkerPoolRevisionTemplate describes the data a worker pool revision should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`revision` |
`str`
Optional. The unique name for the revision. If this field is omitted, it will be automatically generated based on the WorkerPool name. |
`labels` |
`MutableMapping[str, str]`
Optional. Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels. Cloud Run API v2 does not support labels with `run.googleapis.com` , `cloud.googleapis.com` ,
`serving.knative.dev` , or `autoscaling.knative.dev`
namespaces, and they will be rejected. All system labels in
v1 now have a corresponding field in v2
WorkerPoolRevisionTemplate.
|
`annotations` |
`MutableMapping[str, str]`
Optional. Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. Cloud Run API v2 does not support annotations with `run.googleapis.com` , `cloud.googleapis.com` ,
`serving.knative.dev` , or `autoscaling.knative.dev`
namespaces, and they will be rejected. All system
annotations in v1 now have a corresponding field in v2
WorkerPoolRevisionTemplate.
This field follows Kubernetes annotations' namespacing,
limits, and rules.
|
`vpc_access` |
Optional. VPC Access configuration to use for this Revision. For more information, visit https://cloud.google.com/run/docs/configuring/connecting-vpc. |
`service_account` |
`str`
Optional. Email address of the IAM service account associated with the revision of the service. The service account represents the identity of the running revision, and determines what permissions the revision has. If not provided, the revision will use the project's default service account. |
`containers` |
`MutableSequence[`
Holds list of the containers that defines the unit of execution for this Revision. |
`volumes` |
`MutableSequence[`
Optional. A list of Volumes to make available to containers. |
`encryption_key` |
`str`
A reference to a customer managed encryption key (CMEK) to use to encrypt this container image. For more information, go to https://cloud.google.com/run/docs/securing/using-cmek |
`service_mesh` |
Optional. Enables service mesh connectivity. |
`encryption_key_revocation_action` |
Optional. The action to take if the encryption key is revoked. |
`encryption_key_shutdown_duration` |
`google.protobuf.duration_pb2.Duration`
Optional. If encryption_key_revocation_action is SHUTDOWN, the duration before shutting down all instances. The minimum increment is 1 hour. |
`node_selector` |
Optional. The node selector for the revision template. |
`gpu_zonal_redundancy_disabled` |
`bool`
Optional. True if GPU zonal redundancy is disabled on this worker pool. This field is a member of `oneof` _ `_gpu_zonal_redundancy_disabled` .
|

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildConfig -->

# Class BuildConfig (0.14.0)

`BuildConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the Build step of the function that builds a container from the given source.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The Cloud Build name of the latest successful deployment of the function. |
`source_location` |
`str`
The Cloud Storage bucket URI where the function source code is located. |
`function_target` |
`str`
Optional. The name of the function (as defined in source code) that will be executed. Defaults to the resource name suffix, if not specified. For backward compatibility, if function with given name is not found, then the system will try to use function named "function". |
`image_uri` |
`str`
Optional. Artifact Registry URI to store the built image. |
`base_image` |
`str`
Optional. The base image used to build the function. |
`enable_automatic_updates` |
`bool`
Optional. Sets whether the function will receive automatic base image updates. |
`worker_pool` |
`str`
Optional. Name of the Cloud Build Custom Worker Pool that should be used to build the Cloud Run function. The format of this field is `projects/{project}/locations/{region}/workerPools/{workerPool}`
where `{project}` and `{region}` are the project id and
region respectively where the worker pool is defined and
`{workerPool}` is the short name of the worker pool.
|
`environment_variables` |
`MutableMapping[str, str]`
Optional. User-provided build-time environment variables for the function |
`service_account` |
`str`
Optional. Service account to be used for building the container. The format of this field is `projects/{projectId}/serviceAccounts/{serviceAccountEmail}` .
|

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EnvVar -->

# Class EnvVar (0.14.0)

`EnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


EnvVar represents an environment variable present in a Container.

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
Required. Name of the environment variable. Must not exceed 32768 characters. |
`value` |
`str`
Literal value of the environment variable. Defaults to "", and the maximum length is 32768 bytes. Variable references are not supported in Cloud Run. This field is a member of `oneof` _ `values` .
|
`value_source` |
Source for the environment variable's value. This field is a member of `oneof` _ `values` .
|

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/summary_overview -->

# Cloud Run API

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.builds -->

# Package builds (0.14.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typesinstancesplit_googlecloudrun_v2typesdeleteworkerpoolrequ_bbdd8c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesinstancesplit_googlecloudrun_v2typesdeleteworkerpoolreque_0206ac.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesinstancesplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplit -->

# Class InstanceSplit (0.14.0)

str
Revision to which to assign this portion of
instances, if split allocation is by revision.

percent

int
Specifies percent of the instance split to
this Revision. This defaults to zero if
unspecified.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesdeleteworkerpoolrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteWorkerPoolRequest -->

# Class DeleteWorkerPoolRequest (0.14.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesconditionexecutionreason_googlecloudrun_v2typescreatejobr_9578fc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesconditionexecutionreason.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.ExecutionReason -->

# Class ExecutionReason (0.14.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typescreatejobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateJobRequest -->

# Class CreateJobRequest (0.14.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typesgettaskrequest_googlecloudrun_v2typesgetjobrequest_googl_0a7495.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesgettaskrequest_googlecloudrun_v2typesgetjobrequest.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesgettaskrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetTaskRequest -->

# Class GetTaskRequest (0.14.0)

Request message for obtaining a Task by its full name.

Attribute

Name

Description

name

str
Required. The full name of the Task.
Format:
projects/{project}/locations/{location}/jobs/{job}/executions/{execution}/tasks/{task}

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesgetjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetJobRequest -->

# Class GetJobRequest (0.14.0)

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

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessubmitbuildrequestbuildpacksbuild.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest.BuildpacksBuild -->

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
