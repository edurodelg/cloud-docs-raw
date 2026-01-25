---
merged_at: 2026-01-25T12:06:29.174395
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesemptydirvolumesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EmptyDirVolumeSource -->

# Class EmptyDirVolumeSource (0.14.0)

`EmptyDirVolumeSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


In memory (tmpfs) ephemeral storage. It is ephemeral in the sense that when the sandbox is taken down, the data is destroyed with it (it does not persist across sandbox runs).

## Attributes |
|
|---|---|
Name |
Description |
`medium` |
The medium on which the data is stored. Acceptable values today is only MEMORY or none. When none, the default will currently be backed by memory but could change over time. +optional |
`size_limit` |
`str`
Limit on the storage usable by this EmptyDir volume. The size limit is also applicable for memory medium. The maximum usage on memory medium EmptyDir would be the minimum value between the SizeLimit specified here and the sum of memory limits of all containers. The default is nil which means that the limit is undefined. More info: https://cloud.google.com/run/docs/configuring/in-memory-volumes#configure-volume. Info in Kubernetes: https://kubernetes.io/docs/concepts/storage/volumes/#emptydir |

## Classes

### Medium

`Medium(value)`


The different types of medium supported for EmptyDir.
