---
merged_at: 2026-01-25T12:06:29.173816
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesvpcaccessnetworkinterface.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VpcAccess.NetworkInterface -->

# Class NetworkInterface (0.14.0)

`NetworkInterface(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Direct VPC egress settings.

## Attributes |
|
|---|---|
Name |
Description |
`network` |
`str`
Optional. The VPC network that the Cloud Run resource will be able to send traffic to. At least one of network or subnetwork must be specified. If both network and subnetwork are specified, the given VPC subnetwork must belong to the given VPC network. If network is not specified, it will be looked up from the subnetwork. |
`subnetwork` |
`str`
Optional. The VPC subnetwork that the Cloud Run resource will get IPs from. At least one of network or subnetwork must be specified. If both network and subnetwork are specified, the given VPC subnetwork must belong to the given VPC network. If subnetwork is not specified, the subnetwork with the same name with the network will be used. |
`tags` |
`MutableSequence[str]`
Optional. Network tags applied to this Cloud Run resource. |


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
