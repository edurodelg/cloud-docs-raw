---
merged_at: 2026-01-25T12:06:29.176684
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesvolume.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Volume -->

# Class Volume (0.14.0)

`Volume(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Volume represents a named volume in a container.

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
Required. Volume's name. |
`secret` |
Secret represents a secret that should populate this volume. This field is a member of `oneof` _ `volume_type` .
|
`cloud_sql_instance` |
For Cloud SQL volumes, contains the specific instances that should be mounted. Visit https://cloud.google.com/sql/docs/mysql/connect-run for more information on how to connect Cloud SQL and Cloud Run. This field is a member of `oneof` _ `volume_type` .
|
`empty_dir` |
Ephemeral storage used as a shared volume. This field is a member of `oneof` _ `volume_type` .
|
`nfs` |
For NFS Voumes, contains the path to the nfs Volume This field is a member of `oneof` _ `volume_type` .
|
`gcs` |
Persistent storage backed by a Google Cloud Storage bucket. This field is a member of `oneof` _ `volume_type` .
|


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesresourcerequirements.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ResourceRequirements -->

# Class ResourceRequirements (0.14.0)

`ResourceRequirements(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ResourceRequirements describes the compute resource requirements.

## Attributes |
|
|---|---|
Name |
Description |
`limits` |
`MutableMapping[str, str]`
Only `memory` , `cpu` and `nvidia.com/gpu` keys in the
map are supported.
.. raw:: html
Notes: * The only supported values for CPU are '1', '2', '4', and '8'. Setting 4 CPU requires at least 2Gi of memory. For more information, go to https://cloud.google.com/run/docs/configuring/cpu. * For supported 'memory' values and syntax, go to https://cloud.google.com/run/docs/configuring/memory-limits * The only supported 'nvidia.com/gpu' value is '1'. |
`cpu_idle` |
`bool`
Determines whether CPU is only allocated during requests (true by default). However, if ResourceRequirements is set, the caller must explicitly set this field to true to preserve the default behavior. |
`startup_cpu_boost` |
`bool`
Determines whether CPU should be boosted on startup of a new container instance above the requested CPU threshold, this can help reduce cold-start latency. |

## Classes

### LimitsEntry

`LimitsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
