---
merged_at: 2026-01-25T12:06:29.177781
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typescondition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition -->

# Class Condition (0.14.0)

`Condition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a status condition for a resource.

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
`type_` |
`str`
type is used to communicate the status of the reconciliation process. See also: https://github.com/knative/serving/blob/main/docs/spec/errors.md#error-conditions-and-reporting Types common to all resources include: - "Ready": True when the Resource is ready. |
`state` |
State of the condition. |
`message` |
`str`
Human readable message indicating details about the current status. |
`last_transition_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Last time the condition transitioned from one status to another. |
`severity` |
How to interpret failures of this condition, one of Error, Warning, Info |
`reason` |
Output only. A common (service-level) reason for this condition. This field is a member of `oneof` _ `reasons` .
|
`revision_reason` |
Output only. A reason for the revision condition. This field is a member of `oneof` _ `reasons` .
|
`execution_reason` |
Output only. A reason for the execution condition. This field is a member of `oneof` _ `reasons` .
|

## Classes

### CommonReason

`CommonReason(value)`


Reasons common to all types of conditions.

### ExecutionReason

`ExecutionReason(value)`


Reasons specific to Execution resource.

### RevisionReason

`RevisionReason(value)`


Reasons specific to Revision resource.

### Severity

`Severity(value)`


Represents the severity of the condition failures.

### State

`State(value)`


Represents the possible Condition states.


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesprobe.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Probe -->

# Class Probe (0.14.0)

`Probe(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

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
`initial_delay_seconds` |
`int`
Optional. Number of seconds after the container has started before the probe is initiated. Defaults to 0 seconds. Minimum value is 0. Maximum value for liveness probe is 3600. Maximum value for startup probe is 240. |
`timeout_seconds` |
`int`
Optional. Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1. Maximum value is 3600. Must be smaller than period_seconds. |
`period_seconds` |
`int`
Optional. How often (in seconds) to perform the probe. Default to 10 seconds. Minimum value is 1. Maximum value for liveness probe is 3600. Maximum value for startup probe is 240. Must be greater or equal than timeout_seconds. |
`failure_threshold` |
`int`
Optional. Minimum consecutive failures for the probe to be considered failed after having succeeded. Defaults to 3. Minimum value is 1. |
`http_get` |
Optional. HTTPGet specifies the http request to perform. Exactly one of httpGet, tcpSocket, or grpc must be specified. This field is a member of `oneof` _ `probe_type` .
|
`tcp_socket` |
Optional. TCPSocket specifies an action involving a TCP port. Exactly one of httpGet, tcpSocket, or grpc must be specified. This field is a member of `oneof` _ `probe_type` .
|
`grpc` |
Optional. GRPC specifies an action involving a gRPC port. Exactly one of httpGet, tcpSocket, or grpc must be specified. This field is a member of `oneof` _ `probe_type` .
|
