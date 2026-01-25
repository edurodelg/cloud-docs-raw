---
merged_at: 2026-01-25T12:06:29.177237
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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
