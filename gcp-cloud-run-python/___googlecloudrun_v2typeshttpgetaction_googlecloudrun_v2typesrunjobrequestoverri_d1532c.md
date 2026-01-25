---
merged_at: 2026-01-25T15:25:49.595116
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typeshttpgetaction_googlecloudrun_v2typesrunjobrequestoverrid_50c660.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typeshttpgetaction_googlecloudrun_v2typesrunjobrequestoverride_5262ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeshttpgetaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.HTTPGetAction -->

# Class HTTPGetAction (0.14.0)

`HTTPGetAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HTTPGetAction describes an action based on HTTP Get requests.

## Attributes |
|
|---|---|
Name |
Description |
`path` |
`str`
Optional. Path to access on the HTTP server. Defaults to '/'. |
`http_headers` |
`MutableSequence[`
Optional. Custom headers to set in the request. HTTP allows repeated headers. |
`port` |
`int`
Optional. Port number to access on the container. Must be in the range 1 to 65535. If not specified, defaults to the exposed port of the container, which is the value of container.ports[0].containerPort. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesrunjobrequestoverridescontaineroverride.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest.Overrides.ContainerOverride -->

# Class ContainerOverride (0.14.0)

`ContainerOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per-container override specification.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The name of the container specified as a DNS_LABEL. |
`args` |
`MutableSequence[str]`
Optional. Arguments to the entrypoint. Will replace existing args for override. |
`env` |
`MutableSequence[`
List of environment variables to set in the container. Will be merged with existing env for override. |
`clear_args` |
`bool`
Optional. True if the intention is to clear out existing args list. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessecretvolumesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SecretVolumeSource -->

# Class SecretVolumeSource (0.14.0)

`SecretVolumeSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The secret's value will be presented as the content of a file whose name is defined in the item path. If no items are defined, the name of the file is the secret.

## Attributes |
|
|---|---|
Name |
Description |
`secret` |
`str`
Required. The name of the secret in Cloud Secret Manager. Format: {secret} if the secret is in the same project. projects/{project}/secrets/{secret} if the secret is in a different project. |
`items` |
`MutableSequence[`
If unspecified, the volume will expose a file whose name is the secret, relative to VolumeMount.mount_path + VolumeMount.sub_path. If specified, the key will be used as the version to fetch from Cloud Secret Manager and the path will be the name of the file exposed in the volume. When items are defined, they must specify a path and a version. |
`default_mode` |
`int`
Integer representation of mode bits to use on created files by default. Must be a value between 0000 and 0777 (octal), defaulting to 0444. Directories within the path are not affected by this setting. Notes - Internally, a umask of 0222 will be applied to any non-zero value. - This is an integer representation of the mode bits. So, the octal integer value should look exactly as the chmod numeric notation with a leading zero. Some examples: for chmod 640 (u=rw,g=r), set to 0640 (octal) or 416 (base-10). For chmod 755 (u=rwx,g=rx,o=rx), set to 0755 (octal) or 493 (base-10). - This might be in conflict with other options that affect the file mode, like fsGroup, and the result can be other mode bits set. This might be in conflict with other options that affect the file mode, like fsGroup, and as a result, other mode bits could be set. |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typesdeleteservicerequest_googlecloudrun_v2typeshttpheader__g_5729dc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesdeleteservicerequest_googlecloudrun_v2typeshttpheader.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesdeleteservicerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteServiceRequest -->

# Class DeleteServiceRequest (0.14.0)

`DeleteServiceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message to delete a Service by its full name.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The full name of the Service. Format: projects/{project}/locations/{location}/services/{service}, where {project} can be project id or number. |
`validate_only` |
`bool`
Indicates that the request should be validated without actually deleting any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeshttpheader.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.HTTPHeader -->

# Class HTTPHeader (0.14.0)

HTTPHeader describes a custom header to be used in HTTP
probes

Attributes

Name

Description

name

str
Required. The header field name

value

str
Optional. The header field value

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typeslistjobsrequest_googlecloudrun_v2typesgrpcaction.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeslistjobsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsRequest -->

# Class ListJobsRequest (0.14.0)

`ListJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for retrieving a list of Jobs.

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
Maximum number of Jobs to return in this call. |
`page_token` |
`str`
A page token received from a previous call to ListJobs. All other parameters must match. |
`show_deleted` |
`bool`
If true, returns deleted (but unexpired) resources along with active ones. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesgrpcaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GRPCAction -->

# Class GRPCAction (0.14.0)

`GRPCAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GRPCAction describes an action involving a GRPC port.

## Attributes |
|
|---|---|
Name |
Description |
`port` |
`int`
Optional. Port number of the gRPC service. Number must be in the range 1 to 65535. If not specified, defaults to the exposed port of the container, which is the value of container.ports[0].containerPort. |
`service` |
`str`
Optional. Service is the name of the service to place in the gRPC HealthCheckRequest (see https://github.com/grpc/grpc/blob/master/doc/health-checking.md ). If this is not specified, the default behavior is defined by gRPC. |
