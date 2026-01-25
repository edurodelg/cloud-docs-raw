---
merged_at: 2026-01-25T12:20:14.956751
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesemptydirvolumesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EmptyDirVolumeSource -->

# Class EmptyDirVolumeSource (0.14.0)

`EmptyDirVolumeSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


In memory (tmpfs) ephemeral storage. It is ephemeral in the sense that when the sandbox is taken down, the data is destroyed with it (it does not persist across sandbox runs).

## Attributes |
|
|---|---|
Name |
Description |
`medium` |
The medium on which the data is stored. Acceptable values today is only MEMORY or none. When none, the default will currently be backed by memory but could change over time. +optional |
`size_limit` |
`str`
Limit on the storage usable by this EmptyDir volume. The size limit is also applicable for memory medium. The maximum usage on memory medium EmptyDir would be the minimum value between the SizeLimit specified here and the sum of memory limits of all containers. The default is nil which means that the limit is undefined. More info: https://cloud.google.com/run/docs/configuring/in-memory-volumes#configure-volume. Info in Kubernetes: https://kubernetes.io/docs/concepts/storage/volumes/#emptydir |

## Classes

### Medium

`Medium(value)`


The different types of medium supported for EmptyDir.


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesversiontopath.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VersionToPath -->

# Class VersionToPath (0.14.0)

`VersionToPath(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


VersionToPath maps a specific version of a secret to a relative file to mount to, relative to VolumeMount's mount_path.

## Attributes |
|
|---|---|
Name |
Description |
`path` |
`str`
Required. The relative path of the secret in the container. |
`version` |
`str`
The Cloud Secret Manager secret version. Can be 'latest' for the latest value, or an integer or a secret alias for a specific version. |
`mode` |
`int`
Integer octal mode bits to use on this file, must be a value between 01 and 0777 (octal). If 0 or not set, the Volume's default mode will be used. Notes - Internally, a umask of 0222 will be applied to any non-zero value. - This is an integer representation of the mode bits. So, the octal integer value should look exactly as the chmod numeric notation with a leading zero. Some examples: for chmod 640 (u=rw,g=r), set to 0640 (octal) or 416 (base-10). For chmod 755 (u=rwx,g=rx,o=rx), set to 0755 (octal) or 493 (base-10). - This might be in conflict with other options that affect the file mode, like fsGroup, and the result can be other mode bits set. |
