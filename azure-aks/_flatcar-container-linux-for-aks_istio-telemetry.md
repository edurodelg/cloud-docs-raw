---
merged_at: 2026-01-25T12:25:33.874630
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: flatcar-container-linux-for-aks.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/flatcar-container-linux-for-aks -->

# Use Flatcar Container Linux for Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of Flatcar Container Linux for AKS, a Cloud Native Compute Foundation (CNCF) project that provides security, reliability, and cross-cloud capabilities. Flatcar Container Linux is available in preview as an OS option on AKS. You can deploy Flatcar Container Linux node pools in a new AKS cluster or add Flatcar Container Linux node pools to your existing clusters. To learn more about Flatcar Container Linux, see the [Flatcar documentation](https://www.flatcar.org/).

## Flatcar Container Linux for AKS benefits

Flatcar uses an immutable OS filesystem, and it eliminates configuration drift and prevents unauthorized changes, ensuring robust protection for your workloads across multiple cloud platforms. Designed for versatility, Flatcar enables cross-cloud deployment, empowering businesses to scale effortlessly and securely.

## Limitations

Flatcar Container Linux for AKS has the following limitations:

[FIPS](enable-fips-nodes)isn't supported with Flatcar Container Linux.[Trusted Launch](use-trusted-launch)isn't supported with Flatcar Container Linux.[Confidential VM sizes](use-cvm)aren't supported with Flatcar Container Linux.- The
`SecurityPatch`

[node OS upgrade channel](auto-upgrade-node-os-image)isn't supported with Flatcar Container Linux. - During preview, AKS doesn't support in-place updates with Flatcar Container Linux.
[Artifact Streaming](artifact-streaming)(preview) isn't supported with Flatcar Container Linux.[Generation 1 VMs](aks-virtual-machine-sizes)aren't supported with Flatcar Container Linux, which means you can't use VM sizes that only support Generation 1.[Pod Sandboxing (preview)](use-pod-sandboxing)isn't supported with Flatcar Container Linux.[Node auto-provisioning](node-autoprovision)isn't supported with Flatcar Container Linux.[Azure Monitor VM(SS) extension](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-portal#:%7E:text=Virtual%20machine%20(VM)%20extension)isn't supported.

Note

If you have an existing cluster with any of the above features enabled, you might not be able to add a node pool using Flatcar Container Linux.

## Get started with Flatcar Container Linux for AKS

To get started using the Flatcar Container Linux for AKS, see the following resources:

- Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using
[Azure CLI](learn/quick-flatcar-deploy-cli) - Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using an
[ARM template](learn/quick-flatcar-deploy-arm-template) - Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool using
[Azure CLI or an ARM template](create-node-pools) - Add a Flatcar Container Linux for AKS (preview) node pool to an existing cluster using
[Azure CLI or an ARM template](create-node-pools)

## OS migrations and upgrades with Flatcar Container Linux

AKS doesn't support in-place migrations from existing Linux clusters or node pools to Flatcar Container Linux clusters or node pools. To migrate existing workloads to Flatcar Container Linux for AKS, you need to recreate your node pools using `--os-sku flatcar`

.

Flatcar Container Linux for AKS releases weekly AKS node images. Versioning follows the AKS date-based format (for example: 202506.13.0). You can check the node images in the release notes and by using the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command to view the

`nodeImageVersion`

. For example:```
az aks nodepool list --resource-group <resource-group-name> --cluster-name <aks-cluster-name> --query '[].{name: name, nodeImageVersion: nodeImageVersion}'
```


Example output:

```
[
{
"name": "nodes",
"nodeImageVersion": "AKSFlatcar-flatcargen2-202508.06.0"
}
]
```


You can check the Flatcar version number (for example: Flatcar 4372.0.1) in the release notes and by using `kubectl get nodes`

command. For example:

```
kubectl get nodes -o wide
```


Example output:

```
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodes-16363508-vmss000000 Ready <none> 2m33s v1.32.6 10.224.0.4 <none> Flatcar Container Linux by Kinvolk 4372.0.1 (Oklo) 6.12.35-flatcar containerd://2.0.4
```


Flatcar's inbuilt automatic A/B update for the OS partition is disabled and only full node image updates are supported.

## Next steps

To learn more about Flatcar Container Linux, see the [Flatcar documentation](https://www.flatcar.org/).


---

<!-- DOCUMENTO FUSIONADO: istio-telemetry.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-telemetry -->

# Telemetry API for Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Istio can [generate metrics, distributed traces, and access logs](https://istio.io/latest/docs/concepts/observability/) for all workloads in the mesh. The Istio-based service mesh add-on for Azure Kubernetes Service (AKS) provides telemetry customization options through the [shared MeshConfig](istio-meshconfig) and the Istio Telemetry API `v1`

for Istio add-on minor revisions `asm-1-22`

and higher.

Note

While the [Istio MeshConfig](istio-meshconfig) also provides options for configuring telemetry globally across the mesh, the Telemetry API offers more granular control over telemetry settings on a per-service or per-workload basis. As the Istio community continues to invest in the Telemetry API, it is now the preferred method for telemetry configuration. We encourage migrating to the Telemetry API for configuring telemetry to be collected in the mesh.

## Prerequisites

- You must be on revision
`asm-1-22`

or higher. For information on how to perform minor version upgrades, see the[Istio add-on upgrade documentation](istio-upgrade).

## Configure Telemetry resources

The following example demonstrates how Envoy access logging can be enabled across the mesh for the Istio add-on via the Telemetry API using `asm-1-22`

(adjust the revision as needed). For guidance on other Telemetry API customizations for the add-on, see the [Telemetry API support scope](#telemetry-api-support-scope) section and the [Istio documentation](https://istio.io/latest/docs/reference/config/telemetry/).

### Deploy sample applications

Label the namespace for sidecar injection:

```
kubectl label ns default istio.io/rev=asm-1-22
```


Deploy the `sleep`

application and set the `SOURCE_POD`

environment variable:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/sleep/sleep.yaml
export SOURCE_POD=$(kubectl get pod -l app=sleep -o jsonpath={.items..metadata.name})
```


Then, deploy the `httpbin`

application:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/httpbin/httpbin.yaml
```


### Enable Envoy access logging with the Istio Telemetry API

Deploy the following Istio `v1`

Telemetry API resource to enable Envoy access logging for the entire mesh:

```
cat <<EOF | kubectl apply -n aks-istio-system -f -
apiVersion: telemetry.istio.io/v1
kind: Telemetry
metadata:
name: mesh-logging-default
spec:
accessLogging:
- providers:
- name: envoy
EOF
```


### Test access logs

Send a request from `sleep`

to `httpbin`

:

```
kubectl exec "$SOURCE_POD" -c sleep -- curl -sS -v httpbin:8000/status/418
```


Verify that access logs are visible for the `sleep`

pod:

```
kubectl logs -l app=sleep -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.690Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 12 11 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" outbound|8000||httpbin.default.svc.cluster.local 10.244.0.12:53336 10.0.112.220:8000 10.244.0.12:42360 - default
```


Now, verify that access logs are visible for the `httpbin`

pod:

```
kubectl logs -l app=httpbin -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.696Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 2 1 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" inbound|8080|| 127.0.0.6:55401 10.244.0.13:8080 10.244.0.12:53336 outbound_.8000_._.httpbin.default.svc.cluster.local default
```


## Telemetry API support scope

For the Istio service mesh add-on for AKS, Telemetry API fields are classified as `allowed`

, `supported`

, and `blocked`

values. For more information about the Istio add-on's support policy for features and mesh configurations, see the Istio add-on [support policy document](istio-support-policy#allowed-supported-and-blocked-customizations).

The following Telemetry API configurations are either `allowed`

or `supported`

for the Istio add-on. Any field not included in this table is `blocked`

.

Telemetry API Field |
Supported/Allowed |
Notes |
|---|---|---|
`accessLogging.match` |
Supported | - |
`accessLogging.disabled` |
Supported | - |
`accessLogging.providers` |
Allowed | The default `envoy` access log provider is supported. For a managed experience for log collection and querying, see
`allowed` but unsupported. |
`metrics.overrides` |
Supported | - |
`metrics.providers` |
Allowed | Metrics collection with
`allowed` but unsupported. |

`tracing.*`

`allowed`

but unsupported.
