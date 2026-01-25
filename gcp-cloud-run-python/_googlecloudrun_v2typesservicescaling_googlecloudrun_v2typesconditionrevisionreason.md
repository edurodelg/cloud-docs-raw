---
merged_at: 2026-01-25T12:06:29.176118
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesservicescaling.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceScaling -->

# Class ServiceScaling (0.14.0)

`ServiceScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaling settings applied at the service level rather than at the revision level.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`min_instance_count` |
`int`
Optional. total min instances for the service. This number of instances is divided among all revisions with specified traffic based on the percent of traffic they are receiving. |
`scaling_mode` |
Optional. The scaling mode for the service. |
`max_instance_count` |
`int`
Optional. total max instances for the service. This number of instances is divided among all revisions with specified traffic based on the percent of traffic they are receiving. |
`manual_instance_count` |
`int`
Optional. total instance count for the service in manual scaling mode. This number of instances is divided among all revisions with specified traffic based on the percent of traffic they are receiving. This field is a member of `oneof` _ `_manual_instance_count` .
|

## Classes

### ScalingMode

`ScalingMode(value)`


The scaling mode for the service. If not provided, it defaults to AUTOMATIC.


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
