---
merged_at: 2026-01-25T15:25:49.593665
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __multiprocessing_googlecloudrun_v2typessourcecodecloudstoragesource__googleclou_adc707.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _multiprocessing_googlecloudrun_v2typessourcecodecloudstoragesource.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: multiprocessing.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/multiprocessing -->

# Multiprocessing

**NOTE**: Because this client uses [ grpc](https://grpc.github.io/grpc/python/grpc.html#module-grpc) library, it is safe to
share instances across threads. In multiprocessing scenarios, the best
practice is to create client instances

*after*the invocation of

[by](https://docs.python.org/3/library/os.html#os.fork)

`os.fork()`

[or](https://docs.python.org/3/library/multiprocessing.html#multiprocessing.pool.Pool)

`multiprocessing.pool.Pool`

[.](https://docs.python.org/3/library/multiprocessing.html#multiprocessing.Process)

`multiprocessing.Process`


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessourcecodecloudstoragesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SourceCode.CloudStorageSource -->

# Class CloudStorageSource (0.14.0)

int
Optional. The Cloud Storage object
generation.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesnfsvolumesource_googlecloudrun_v2typesworkerpoolscaling.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesnfsvolumesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.NFSVolumeSource -->

# Class NFSVolumeSource (0.14.0)

bool
If true, the volume will be mounted as read
only for all mounts.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesworkerpoolscaling.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPoolScaling -->

# Class WorkerPoolScaling (0.14.0)

`WorkerPoolScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Worker pool scaling settings.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`manual_instance_count` |
`int`
Optional. The total number of instances in manual scaling mode. This field is a member of `oneof` _ `_manual_instance_count` .
|


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesresourcerequirements__googlecloudrun_v2typessubmitbuildre_1c8127.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typessubmitbuildrequestdockerbuild_googlecloudrun_v2typesrevis_084149.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessubmitbuildrequestdockerbuild.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest.DockerBuild -->

# Class DockerBuild (0.14.0)

Build the source using Docker. This means the source has a
Dockerfile.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesrevisionscalingstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionScalingStatus -->

# Class RevisionScalingStatus (0.14.0)

int
The current number of min instances
provisioned for this revision.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
