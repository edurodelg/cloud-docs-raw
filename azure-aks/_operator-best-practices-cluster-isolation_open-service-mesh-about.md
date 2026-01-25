---
merged_at: 2026-01-25T12:06:27.723054
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: operator-best-practices-cluster-isolation.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-cluster-isolation -->

# Best practices for cluster isolation in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. AKS allows flexibility in how you run multi-tenant clusters and isolate resources. To maximize your investment in Kubernetes, it's important you understand AKS multi-tenancy and isolation features.

This best practices article focuses on isolation for cluster operators. In this article, you learn how to:

- Plan for multi-tenant clusters and separation of resources.
- Use logical or physical isolation in your AKS clusters.

## Design clusters for multi-tenancy

Kubernetes lets you logically isolate teams and workloads in the same cluster. The goal is to provide the least number of privileges scoped to the resources each team needs. A Kubernetes [Namespace](concepts-clusters-workloads#namespaces) creates a logical isolation boundary. Other Kubernetes features and considerations for isolation and multi-tenancy include the following areas:

### Scheduling

*Scheduling* uses basic features like resource quotas and pod disruption budgets. For more information about these features, see [Best practices for basic scheduler features in AKS](operator-best-practices-scheduler).

More advanced scheduler features include:

- Taints and tolerations.
- Node selectors.
- Node and pod affinity or anti-affinity.

For more information about these features, see [Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler).

### Networking

*Networking* uses network policies to control the flow of traffic in and out of pods.

For more information, see [Secure traffic between pods using network policies in AKS](use-network-policies).

### Authentication and authorization

*Authentication and authorization* uses:

- Role-based access control (RBAC).
- Microsoft Entra integration.
- Pod identities.
- Secrets in Azure Key Vault.

For more information about these features, see [Best practices for authentication and authorization in AKS](operator-best-practices-identity).

### Containers

*Containers* include:

- The Azure Policy add-on for AKS to enforce pod security.
- Pod security admission.
- Scanning images and runtime for vulnerabilities.
- Using App Armor or Seccomp (Secure Computing) to restrict container access to the underlying node.

## Logically isolated clusters


Best practice guidanceSeparate teams and projects using

logical isolation. Minimize the number of physical AKS clusters you deploy to isolate teams or applications.

With logical isolation, you can use a single AKS cluster for multiple workloads, teams, or environments. Kubernetes [Namespaces](concepts-clusters-workloads#namespaces) form the logical isolation boundary for workloads and resources.

Logical separation of clusters usually provides a higher pod density than physically isolated clusters, with less excess compute capacity sitting idle in the cluster. When combined with the Kubernetes cluster autoscaler, you can scale the number of nodes up or down to meet demands. This best practice approach minimizes costs by running only the required number of nodes.

Kubernetes environments aren't entirely safe for hostile multi-tenant usage. In a multi-tenant environment, multiple tenants work on a shared infrastructure. If all tenants can't be trusted, you need extra planning to prevent tenants from impacting the security and service of others.

Other security features, like Kubernetes RBAC for nodes, efficiently block exploits. For true security when running hostile multi-tenant workloads, you should only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster and not an individual node.

For these types of hostile multi-tenant workloads, you should use physically isolated clusters.

## Physically isolated clusters


Best practice guidanceMinimize the use of physical isolation for each separate team or application deployment and use

logicalisolation instead.

Physically separating AKS clusters is a common approach to cluster isolation. In this isolation model, teams or workloads are assigned their own AKS cluster. While physical isolation might look like the easiest way to isolate workloads or teams, it adds management and financial overhead. With physically isolated clusters, you must maintain multiple clusters and individually provide access and assign permissions. You're also billed for each individual node.

Physically isolated clusters usually have a low pod density. Since each team or workload has their own AKS cluster, the cluster is often over-provisioned with compute resources. Often, a few pods are scheduled on those nodes. Unclaimed node capacity can't be used for applications or services in development by other teams. These excess resources contribute to the extra costs in physically isolated clusters.

## Next steps

This article focused on cluster isolation. For more information about cluster operations in AKS, see the following best practice articles:


---

<!-- DOCUMENTO FUSIONADO: open-service-mesh-about.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-about -->

# Open Service Mesh (OSM) add-on in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Open Service Mesh (OSM)](https://docs.openservicemesh.io/) is a lightweight, extensible, cloud native service mesh that allows you to uniformly manage, secure, and get out-of-the-box observability features for highly dynamic microservice environments.

OSM runs an Envoy-based control plane on Kubernetes and can be configured with [SMI](https://smi-spec.io/) APIs. OSM works by injecting an Envoy proxy as a sidecar container with each instance of your application. The Envoy proxy contains and executes rules around access control policies, implements routing configuration, and captures metrics. The control plane continually configures the Envoy proxies to ensure policies and routing rules are up to date and proxies are healthy.

Microsoft started the OSM project, but it's now governed by the [Cloud Native Computing Foundation (CNCF)](https://www.cncf.io/).

Warning

Microsoft has announced the retirement of the [Open Service Mesh (OSM) add-on for AKS](https://azure.microsoft.com/updates?id=open-service-mesh-add-on-for-aks-will-be-retired-on-september-30-2027). The upstream OSM project has also been retired by the [Cloud Native Computing Foundation (CNCF)](https://docs.openservicemesh.io/). Identify any existing OSM configurations and migrate them to equivalent Istio configurations. For migration steps, see [Migration guidance for Open Service Mesh (OSM) configurations to Istio](open-service-mesh-istio-migration-guidance).

## Enable the OSM add-on

OSM can be added to your Azure Kubernetes Service (AKS) cluster by enabling the OSM add-on using the [Azure CLI](open-service-mesh-deploy-addon-az-cli) or a [Bicep template](open-service-mesh-deploy-addon-bicep). The OSM add-on provides a fully supported installation of OSM that's integrated with AKS.

Important

Based on the version of Kubernetes your cluster is running, the OSM add-on installs a different version of OSM.

| Kubernetes version | OSM version installed |
|---|---|
| 1.24.0 or greater | 1.2.5 |
| Between 1.23.5 and 1.24.0 | 1.1.3 |
| Below 1.23.5 | 1.0.0 |

Older versions of OSM may not be available for install or be actively supported if the corresponding AKS version has reached end of life. You can check the [AKS Kubernetes release calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar) for information on AKS version support windows.

## Capabilities and features

OSM provides the following capabilities and features:

- Secure service-to-service communication by enabling mutual TLS (mTLS).
- Onboard applications onto the OSM mesh using automatic sidecar injection of Envoy proxy.
- Transparently configure traffic shifting on deployments.
- Define and execute fine-grained access control policies for services.
- Monitor and debug services using observability and insights into application metrics.
- Encrypt communications between service endpoints deployed in the cluster.
- Enable traffic authorization of both HTTP/HTTPS and TCP traffic.
- Configure weighted traffic controls between two or more services for A/B testing or canary deployments.
- Collect and view KPIs from application traffic.
- Integrate with external certificate management.
- Integrate with existing ingress solutions such as
[NGINX](https://github.com/kubernetes/ingress-nginx),[Contour](https://projectcontour.io/), and[Application Routing](app-routing).

For more information on ingress and OSM, see [Using ingress to manage external access to services within the cluster](https://release-v1-2.docs.openservicemesh.io/docs/guides/traffic_management/ingress/) and [Integrate OSM with Contour for ingress](https://release-v1-2.docs.openservicemesh.io/docs/demos/ingress_contour). For an example of how to integrate OSM with ingress controllers using the `networking.k8s.io/v1`

API, see [Ingress with Kubernetes Nginx ingress controller](https://release-v1-2.docs.openservicemesh.io/docs/demos/ingress_k8s_nginx). For more information on using Application Routing, which automatically integrates with OSM, see [Application Routing](app-routing).

## Limitations

The OSM AKS add-on has the following limitations:

- After installation, you must enable Iptables redirection for port IP address and port range exclusion using
`kubectl patch`

. For more information, see[iptables redirection](https://release-v1-2.docs.openservicemesh.io/docs/guides/traffic_management/iptables_redirection/). - Any pods that need access to IMDS, Azure DNS, or the Kubernetes API server must have their IP addresses added to the global list of excluded outbound IP ranges using
[Global outbound IP range exclusions](https://release-v1-2.docs.openservicemesh.io/docs/guides/traffic_management/iptables_redirection/#global-outbound-ip-range-exclusions).

- The add-on doesn't work on AKS clusters that are using
[Istio based service mesh addon for AKS](istio-about).

- OSM doesn't support Windows Server containers.

## Next steps

After enabling the OSM add-on using the [Azure CLI](open-service-mesh-deploy-addon-az-cli) or a [Bicep template](open-service-mesh-deploy-addon-bicep), you can:
