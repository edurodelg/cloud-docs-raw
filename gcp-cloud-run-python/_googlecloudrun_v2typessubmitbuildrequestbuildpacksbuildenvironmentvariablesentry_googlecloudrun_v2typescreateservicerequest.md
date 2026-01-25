---
merged_at: 2026-01-25T12:06:29.172633
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessubmitbuildrequestbuildpacksbuildenvironmentvariablesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest.BuildpacksBuild.EnvironmentVariablesEntry -->

# Class EnvironmentVariablesEntry (0.14.0)

Keys and values corresponding to the fields of the message.

mapping

Union[dict, .Message]

A dictionary or message to be used to determine the values for this message.

ignore_unknown_fields

Optional(bool)

If True, do not raise errors for unknown fields. Only applied if mapping is a mapping type or there are keyword parameters.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typescreateservicerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateServiceRequest -->

# Class CreateServiceRequest (0.14.0)

`CreateServiceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for creating a Service.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location and project in which this service should be created. Format: projects/{project}/locations/{location}, where {project} can be project id or number. Only lowercase characters, digits, and hyphens. |
`service` |
Required. The Service instance to create. |
`service_id` |
`str`
Required. The unique identifier for the Service. It must begin with letter, and cannot end with hyphen; must contain fewer than 50 characters. The name of the service becomes {parent}/services/{service_id}. |
`validate_only` |
`bool`
Indicates that the request should be validated and default values populated, without persisting the request or creating any resources. |
