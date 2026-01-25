---
merged_at: 2026-01-25T12:06:29.149807
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesgrpcaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GRPCAction -->

# Class GRPCAction (0.14.0)

`GRPCAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GRPCAction describes an action involving a GRPC port.

## Attributes |
|
|---|---|
Name |
Description |
`port` |
`int`
Optional. Port number of the gRPC service. Number must be in the range 1 to 65535. If not specified, defaults to the exposed port of the container, which is the value of container.ports[0].containerPort. |
`service` |
`str`
Optional. Service is the name of the service to place in the gRPC HealthCheckRequest (see https://github.com/grpc/grpc/blob/master/doc/health-checking.md ). If this is not specified, the default behavior is defined by gRPC. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typestraffictargetstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTargetStatus -->

# Class TrafficTargetStatus (0.14.0)

int
Specifies percent of the traffic to this
Revision.

tag

str
Indicates the string used in the URI to
exclusively reference this target.

uri

str
Displays the target URI.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
