---
merged_at: 2026-01-25T12:06:29.140559
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessecretkeyselector.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SecretKeySelector -->

# Class SecretKeySelector (0.14.0)

`SecretKeySelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SecretEnvVarSource represents a source for the value of an EnvVar.

## Attributes |
|
|---|---|
Name |
Description |
`secret` |
`str`
Required. The name of the secret in Cloud Secret Manager. Format: {secret_name} if the secret is in the same project. projects/{project}/secrets/{secret_name} if the secret is in a different project. |
`version` |
`str`
The Cloud Secret Manager secret version. Can be 'latest' for the latest version, an integer for a specific version, or a version alias. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesservicemesh.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceMesh -->

# Class ServiceMesh (0.14.0)

str
The Mesh resource name. Format:
projects/{project}/locations/global/meshes/{mesh}, where
{project} can be project id or number.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
