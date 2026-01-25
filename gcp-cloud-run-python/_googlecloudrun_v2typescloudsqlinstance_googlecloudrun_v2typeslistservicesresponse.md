---
merged_at: 2026-01-25T12:06:29.156412
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typescloudsqlinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CloudSqlInstance -->

# Class CloudSqlInstance (0.14.0)

`CloudSqlInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a set of Cloud SQL instances. Each one will be available
under /cloudsql/[instance]. Visit
[https://cloud.google.com/sql/docs/mysql/connect-run](https://cloud.google.com/sql/docs/mysql/connect-run) for more
information on how to connect Cloud SQL and Cloud Run.

## Attribute |
|
|---|---|
Name |
Description |
`instances` |
`MutableSequence[str]`
The Cloud SQL instance connection names, as can be found in https://console.cloud.google.com/sql/instances. Visit https://cloud.google.com/sql/docs/mysql/connect-run for more information on how to connect Cloud SQL and Cloud Run. Format: {project}:{location}:{instance} |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeslistservicesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse -->

# Class ListServicesResponse (0.14.0)

str
A token indicating there are more items than page_size. Use
it in the next ListServices request to continue.

unreachable

MutableSequence[str]
Output only. For global requests, returns the
list of regions that could not be reached within
the deadline.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
