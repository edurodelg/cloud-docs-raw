---
merged_at: 2026-01-26T23:13:32.276260
merged_files: 2
---


---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionTemplate -->

# Class RevisionTemplate (0.14.0)

`RevisionTemplate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


RevisionTemplate describes the data a revision should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`revision` |
`str`
Optional. The unique name for the revision. If this field is omitted, it will be automatically generated based on the Service name. |
`labels` |
`MutableMapping[str, str]`
Optional. Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels. .. raw:: html Cloud Run API v2 does not support labels with |
`annotations` |
`MutableMapping[str, str]`
Optional. Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. .. raw:: html Cloud Run API v2 does not support annotations with This field follows Kubernetes annotations' namespacing, limits, and rules. |
`scaling` |
Optional. Scaling settings for this Revision. |
`vpc_access` |
Optional. VPC Access configuration to use for this Revision. For more information, visit https://cloud.google.com/run/docs/configuring/connecting-vpc. |
`timeout` |
`google.protobuf.duration_pb2.Duration`
Optional. Max allowed time for an instance to respond to a request. |
`service_account` |
`str`
Optional. Email address of the IAM service account associated with the revision of the service. The service account represents the identity of the running revision, and determines what permissions the revision has. If not provided, the revision will use the project's default service account. |
`containers` |
`MutableSequence[`
Holds the single container that defines the unit of execution for this Revision. |
`volumes` |
`MutableSequence[`
Optional. A list of Volumes to make available to containers. |
`execution_environment` |
Optional. The sandbox environment to host this Revision. |
`encryption_key` |
`str`
A reference to a customer managed encryption key (CMEK) to use to encrypt this container image. For more information, go to https://cloud.google.com/run/docs/securing/using-cmek |
`max_instance_request_concurrency` |
`int`
Optional. Sets the maximum number of requests that each serving instance can receive. If not specified or 0, concurrency defaults to 80 when requested `CPU >= 1` and
defaults to 1 when requested `CPU <>` .
|
`service_mesh` |
Optional. Enables service mesh connectivity. |
`encryption_key_revocation_action` |
Optional. The action to take if the encryption key is revoked. |
`encryption_key_shutdown_duration` |
`google.protobuf.duration_pb2.Duration`
Optional. If encryption_key_revocation_action is SHUTDOWN, the duration before shutting down all instances. The minimum increment is 1 hour. |
`session_affinity` |
`bool`
Optional. Enable session affinity. |
`health_check_disabled` |
`bool`
Optional. Disables health checking containers during deployment. |
`node_selector` |
Optional. The node selector for the revision template. |
`gpu_zonal_redundancy_disabled` |
`bool`
Optional. True if GPU zonal redundancy is disabled on this revision. This field is a member of `oneof` _ `_gpu_zonal_redundancy_disabled` .
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.State -->

# Class State (0.14.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EnvVarSource -->

# Class EnvVarSource (0.14.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VpcAccess -->

# Class VpcAccess (0.14.0)

`VpcAccess(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


VPC Access settings. For more information on sending traffic
to a VPC network, visit
[https://cloud.google.com/run/docs/configuring/connecting-vpc](https://cloud.google.com/run/docs/configuring/connecting-vpc).

## Attributes |
|
|---|---|
Name |
Description |
`connector` |
`str`
VPC Access connector name. Format: `projects/{project}/locations/{location}/connectors/{connector}` ,
where `{project}` can be project id or number. For more
information on sending traffic to a VPC network via a
connector, visit
https://cloud.google.com/run/docs/configuring/vpc-connectors.
|
`egress` |
Optional. Traffic VPC egress settings. If not provided, it defaults to PRIVATE_RANGES_ONLY. |
`network_interfaces` |
`MutableSequence[`
Optional. Direct VPC egress settings. Currently only single network interface is supported. |

## Classes

### NetworkInterface

`NetworkInterface(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Direct VPC egress settings.

### VpcEgress

`VpcEgress(value)`


Egress options for VPC access.

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Container -->

# Class Container (0.14.0)

`Container(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single application container. This specifies both the container to run, the command to run in the container and the arguments to supply to it. Note that additional arguments can be supplied by the system to the container at runtime.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Name of the container specified as a DNS_LABEL (RFC 1123). |
`image` |
`str`
Required. Name of the container image in Dockerhub, Google Artifact Registry, or Google Container Registry. If the host is not provided, Dockerhub is assumed. |
`source_code` |
Optional. Location of the source. |
`command` |
`MutableSequence[str]`
Entrypoint array. Not executed within a shell. The docker image's ENTRYPOINT is used if this is not provided. |
`args` |
`MutableSequence[str]`
Arguments to the entrypoint. The docker image's CMD is used if this is not provided. |
`env` |
`MutableSequence[`
List of environment variables to set in the container. |
`resources` |
Compute Resource requirements by this container. |
`ports` |
`MutableSequence[`
List of ports to expose from the container. Only a single port can be specified. The specified ports must be listening on all interfaces (0.0.0.0) within the container to be accessible. If omitted, a port number will be chosen and passed to the container through the PORT environment variable for the container to listen on. |
`volume_mounts` |
`MutableSequence[`
Volume to mount into the container's filesystem. |
`working_dir` |
`str`
Container's working directory. If not specified, the container runtime's default will be used, which might be configured in the container image. |
`liveness_probe` |
Periodic probe of container liveness. Container will be restarted if the probe fails. |
`startup_probe` |
Startup probe of application within the container. All other probes are disabled if a startup probe is provided, until it succeeds. Container will not be added to service endpoints if the probe fails. |
`depends_on` |
`MutableSequence[str]`
Names of the containers that must start before this container. |
`base_image_uri` |
`str`
Base image for this container. Only supported for services. If set, it indicates that the service is enrolled into automatic base image update. |
`build_info` |
Output only. The build info of the container image. |
