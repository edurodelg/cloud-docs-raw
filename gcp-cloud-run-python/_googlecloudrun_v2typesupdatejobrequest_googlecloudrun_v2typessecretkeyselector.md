---
merged_at: 2026-01-25T12:20:14.937605
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesupdatejobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateJobRequest -->

# Class UpdateJobRequest (0.14.0)

`UpdateJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for updating a Job.

## Attributes |
|
|---|---|
Name |
Description |
`job` |
Required. The Job to be updated. |
`validate_only` |
`bool`
Indicates that the request should be validated and default values populated, without persisting the request or updating any resources. |
`allow_missing` |
`bool`
Optional. If set to true, and if the Job does not exist, it will create a new one. Caller must have both create and update permissions for this call if this is set to true. |


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
