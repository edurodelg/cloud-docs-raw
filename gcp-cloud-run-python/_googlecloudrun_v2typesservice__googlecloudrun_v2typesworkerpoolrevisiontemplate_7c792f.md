---
merged_at: 2026-01-29T15:33:46.864144
merged_files: 2
---


---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Service -->

# Class Service (0.15.0)

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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPoolRevisionTemplate -->

# Class WorkerPoolRevisionTemplate (0.15.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VpcAccess.NetworkInterface -->

# Class NetworkInterface (0.15.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EnvVar -->

# Class EnvVar (0.15.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildConfig -->

# Class BuildConfig (0.15.0)

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
