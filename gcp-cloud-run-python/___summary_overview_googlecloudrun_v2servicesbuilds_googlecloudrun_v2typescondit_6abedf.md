---
merged_at: 2026-01-25T15:25:49.592687
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __summary_overview_googlecloudrun_v2servicesbuilds_googlecloudrun_v2typesconditi_0b52e8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _summary_overview_googlecloudrun_v2servicesbuilds.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: summary_overview.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/summary_overview -->

# Cloud Run API

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicesbuilds.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.builds -->

# Package builds (0.14.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesconditionrevisionreason.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.RevisionReason -->

# Class RevisionReason (0.14.0)

`RevisionReason(value)`


Reasons specific to Revision resource.

## Enums |
|
|---|---|
Name |
Description |
`REVISION_REASON_UNDEFINED` |
Default value. |
`PENDING` |
Revision in Pending state. |
`RESERVE` |
Revision is in Reserve state. |
`RETIRED` |
Revision is Retired. |
`RETIRING` |
Revision is being retired. |
`RECREATING` |
Revision is being recreated. |
`HEALTH_CHECK_CONTAINER_ERROR` |
There was a health check error. |
`CUSTOMIZED_PATH_RESPONSE_PENDING` |
Health check failed due to user error from customized path of the container. System will retry. |
`MIN_INSTANCES_NOT_PROVISIONED` |
A revision with min_instance_count > 0 was created and is reserved, but it was not configured to serve traffic, so it's not live. This can also happen momentarily during traffic migration. |
`ACTIVE_REVISION_LIMIT_REACHED` |
The maximum allowed number of active revisions has been reached. |
`NO_DEPLOYMENT` |
There was no deployment defined. This value is no longer used, but Services created in older versions of the API might contain this value. |
`HEALTH_CHECK_SKIPPED` |
A revision's container has no port specified since the revision is of a manually scaled service with 0 instance count |
`MIN_INSTANCES_WARMING` |
A revision with min_instance_count > 0 was created and is waiting for enough instances to begin a traffic migration. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesvolume__googlecloudrun_v2typesconditionstate_googlecloudr_579c9c.md -->
<!-- URL ORIGINAL: N/A -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesconditionstate_googlecloudrun_v2typesenvvarsource.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesconditionstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.State -->

# Class State (0.14.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesenvvarsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EnvVarSource -->

# Class EnvVarSource (0.14.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
