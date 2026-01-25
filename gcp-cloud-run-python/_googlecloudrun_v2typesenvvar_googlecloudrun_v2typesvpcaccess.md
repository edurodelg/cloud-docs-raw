---
merged_at: 2026-01-25T12:20:14.956383
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesenvvar.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EnvVar -->

# Class EnvVar (0.14.0)

`EnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


EnvVar represents an environment variable present in a Container.

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
Required. Name of the environment variable. Must not exceed 32768 characters. |
`value` |
`str`
Literal value of the environment variable. Defaults to "", and the maximum length is 32768 bytes. Variable references are not supported in Cloud Run. This field is a member of `oneof` _ `values` .
|
`value_source` |
Source for the environment variable's value. This field is a member of `oneof` _ `values` .
|


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesvpcaccess.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VpcAccess -->

# Class VpcAccess (0.14.0)

`VpcAccess(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


VPC Access settings. For more information on sending traffic
to a VPC network, visit
[https://cloud.google.com/run/docs/configuring/connecting-vpc](https://cloud.google.com/run/docs/configuring/connecting-vpc).

## Attributes |
|
|---|---|
Name |
Description |
`connector` |
`str`
VPC Access connector name. Format: `projects/{project}/locations/{location}/connectors/{connector}` ,
where `{project}` can be project id or number. For more
information on sending traffic to a VPC network via a
connector, visit
https://cloud.google.com/run/docs/configuring/vpc-connectors.
|
`egress` |
Optional. Traffic VPC egress settings. If not provided, it defaults to PRIVATE_RANGES_ONLY. |
`network_interfaces` |
`MutableSequence[`
Optional. Direct VPC egress settings. Currently only single network interface is supported. |

## Classes

### NetworkInterface

`NetworkInterface(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Direct VPC egress settings.

### VpcEgress

`VpcEgress(value)`


Egress options for VPC access.
