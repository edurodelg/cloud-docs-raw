---
merged_at: 2026-01-25T12:06:29.174963
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesupdateworkerpoolrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateWorkerPoolRequest -->

# Class UpdateWorkerPoolRequest (0.14.0)

`UpdateWorkerPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for updating a worker pool.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. The list of fields to be updated. |
`worker_pool` |
Required. The WorkerPool to be updated. |
`validate_only` |
`bool`
Optional. Indicates that the request should be validated and default values populated, without persisting the request or updating any resources. |
`allow_missing` |
`bool`
Optional. If set to true, and if the WorkerPool does not exist, it will create a new one. The caller must have 'run.workerpools.create' permissions if this is set to true and the WorkerPool does not exist. |
`force_new_revision` |
`bool`
Optional. If set to true, a new revision will be created from the template even if the system doesn't detect any changes from the previously deployed revision. This may be useful for cases where the underlying resources need to be recreated or reinitialized. For example if the image is specified by label, but the underlying image digest has changed) or if the container performs deployment initialization work that needs to be performed again. |
