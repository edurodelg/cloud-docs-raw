---
merged_at: 2026-01-25T12:20:14.959469
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesbuildconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildConfig -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typescontainer.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Container -->

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
