---
merged_at: 2026-01-25T12:06:29.186565
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesworkerpool.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPool -->

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


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesservice.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Service -->

# Class Service (0.14.0)

`Service(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Service acts as a top-level container that manages a set of configurations and revision templates which implement a network service. Service exists to provide a singular abstraction which can be access controlled, reasoned about, and which encapsulates software lifecycle decisions such as rollout policy and team resource ownership.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. The fully qualified name of this Service. In CreateServiceRequest, this field is ignored, and instead composed from CreateServiceRequest.parent and CreateServiceRequest.service_id. Format: projects/{project}/locations/{location}/services/{service_id} |
`description` |
`str`
User-provided description of the Service. This field currently has a 512-character limit. |
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
Optional. Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels. .. raw:: html Cloud Run API v2 does not support labels with |
`annotations` |
`MutableMapping[str, str]`
Optional. Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. .. raw:: html Cloud Run API v2 does not support annotations with This field follows Kubernetes annotations' namespacing, limits, and rules. |
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
Output only. For a deleted resource, the time after which it will be permanently deleted. |
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
`ingress` |
Optional. Provides the ingress settings for this Service. On output, returns the currently observed ingress settings, or INGRESS_TRAFFIC_UNSPECIFIED if no revision is active. |
`launch_stage` |
`google.api.launch_stage_pb2.LaunchStage`
Optional. The launch stage as defined by `Google Cloud Platform Launch Stages |
`binary_authorization` |
Optional. Settings for the Binary Authorization feature. |
`template` |
Required. The template used to create revisions for this Service. |
`traffic` |
`MutableSequence[`
Optional. Specifies how to distribute traffic over a collection of Revisions belonging to the Service. If traffic is empty or not provided, defaults to 100% traffic to the latest `Ready` Revision.
|
`scaling` |
Optional. Specifies service-level scaling settings |
`invoker_iam_disabled` |
`bool`
Optional. Disables IAM permission check for run.routes.invoke for callers of this service. For more information, visit https://cloud.google.com/run/docs/securing/managing-access#invoker_check. |
`default_uri_disabled` |
`bool`
Optional. Disables public resolution of the default URI of this service. |
`urls` |
`MutableSequence[str]`
Output only. All URLs serving traffic for this Service. |
`iap_enabled` |
`bool`
Optional. IAP settings on the Service. |
`multi_region_settings` |
Optional. Settings for multi-region deployment. |
`custom_audiences` |
`MutableSequence[str]`
One or more custom audiences that you want this service to support. Specify each custom audience as the full URL in a string. The custom audiences are encoded in the token and used to authenticate requests. For more information, see https://cloud.google.com/run/docs/configuring/custom-audiences. |
`observed_generation` |
`int`
Output only. The generation of this Service currently serving traffic. See comments in `reconciling` for
additional information on reconciliation process in Cloud
Run. Please note that unlike v1, this is an int64 value. As
with most Google APIs, its JSON representation will be a
`string` instead of an `integer` .
|
`terminal_condition` |
Output only. The Condition of this Service, containing its readiness status, and detailed error information in case it did not reach a serving state. See comments in `reconciling` for additional information on reconciliation
process in Cloud Run.
|
`conditions` |
`MutableSequence[`
Output only. The Conditions of all other associated sub-resources. They contain additional diagnostics information in case the Service does not reach its Serving state. See comments in `reconciling` for additional
information on reconciliation process in Cloud Run.
|
`latest_ready_revision` |
`str`
Output only. Name of the latest revision that is serving traffic. See comments in `reconciling` for additional
information on reconciliation process in Cloud Run.
|
`latest_created_revision` |
`str`
Output only. Name of the last created revision. See comments in `reconciling` for additional information on
reconciliation process in Cloud Run.
|
`traffic_statuses` |
`MutableSequence[`
Output only. Detailed status information for corresponding traffic targets. See comments in `reconciling` for
additional information on reconciliation process in Cloud
Run.
|
`uri` |
`str`
Output only. The main URI in which this Service is serving traffic. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`threat_detection_enabled` |
`bool`
Output only. True if Cloud Run Threat Detection monitoring is enabled for the parent project of this Service. |
`build_config` |
Optional. Configuration for building a Cloud Run function. |
`reconciling` |
`bool`
Output only. Returns true if the Service is currently being acted upon by the system to bring it into the desired state. When a new Service is created, or an existing one is updated, Cloud Run will asynchronously perform all necessary steps to bring the Service to the desired serving state. This process is called reconciliation. While reconciliation is in process, `observed_generation` ,
`latest_ready_revision` , `traffic_statuses` , and `uri`
will have transient values that might mismatch the intended
state: Once reconciliation is over (and this field is
false), there are two possible outcomes: reconciliation
succeeded and the serving state matches the Service, or
there was an error, and reconciliation failed. This state
can be found in `terminal_condition.state` .
If reconciliation succeeded, the following fields will
match: `traffic` and `traffic_statuses` ,
`observed_generation` and `generation` ,
`latest_ready_revision` and `latest_created_revision` .
If reconciliation failed, `traffic_statuses` ,
`observed_generation` , and `latest_ready_revision` will
have the state of the last serving revision, or empty for
newly created Services. Additional information on the
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

### MultiRegionSettings

`MultiRegionSettings(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Settings for multi-region deployment.
