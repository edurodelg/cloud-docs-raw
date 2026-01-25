---
merged_at: 2026-01-25T12:06:27.754094
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: automated-deployments.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/automated-deployments -->

# Automated deployments for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Automated Deployments streamline the process of setting up a GitHub Action or Azure DevOps Pipeline, making it easy to create a continuous deployment pipeline for your application to Azure Kubernetes Service (AKS). Once connected, every new commit automatically triggers the pipeline, delivering updates to your application seamlessly. You can either bring your own deployment files for quick pipeline creation or generate Dockerfiles and Kubernetes manifests to containerize and deploy non-containerized applications with minimal effort.

## Prerequisites

- A GitHub account or an Azure DevOps organization.
- An AKS cluster. If you don't have one, you can create one using the steps in
[Deploy an Azure Kubernetes Service (AKS) cluster](learn/quick-kubernetes-deploy-portal). - An Azure Container Registry (ACR). If you don't have one, you can create one using the steps in
[Integrate Azure Container Registry (ACR) with an Azure Kubernetes Service (AKS) cluster](cluster-container-registry-integration). - An application to deploy.

### Connect to source code repository

Create an automated deployment workflow and authorize it to connect to the desired source code repository.

- In the Azure portal, navigate to your AKS cluster resource.
- From the service menu, under
**Settings**, select**Automated deployments**>**Create**. - Under
**Repository details**, enter a name for the workflow, then select**GitHub or ADO**for your repository location. - Select
**Authorize access**to connect to the desired repository. - Choose the
**Repository**and**Branch**, and then select**Next**.

### Choose the container image configuration

To get an application ready for Kubernetes, you need to build it into a container image and store it in a container registry. You use a Dockerfile to provide instructions on how to build the container image. If your source code repository doesn't already have a Dockerfile, Automated Deployments can generate one for you. Otherwise, you can use an existing Dockerfile.

Use Automated Deployments to generate a Dockerfile for many languages and frameworks such as Go, C#, Node.js, Python, Java, Gradle, Clojure, PHP, Ruby, Erlang, Swift, and Rust. The language support is built on what's available in [draft.sh](https://draft.sh).

- Select
**Auto-containerize (generate Dockerfile)**for the container configuration. - Select the
**location of where to save the generated Dockerfile**in the repository. - Select the
**application environment**from the list of supported languages and frameworks. - Enter the
**application port**. - Provide the
**Dockerfile build context**path. - Select an existing
**Azure Container Registry**or create a new one. This registry is used to store the built application image.

### Choose the Kubernetes manifest configuration

Note

The Generate Manifests option also supports advanced features like Service Connector integration, auto-generated Ingress resources, and more detailed, customizable Kubernetes manifest files.

An application running on Kubernetes consists of many Kubernetes primitive components. These components describe what container image to use, how many replicas to run, if there's a public IP required to expose the application, etc. For more information, see the official [Kubernetes documentation][kubernetes-documentation]. If your source code repository doesn't already have the basic Kubernetes manifests to deploy, Automated Deployments can generate them for you. Otherwise, you can use a set of existing manifests. You can also choose an existing Helm chart.

If your code repository already has a Dockerfile, you can select it to be used to build the application image.

- Select
**Use existing Kubernetes manifest deployment files**for the deployment options. - Select the
**Kubernetes manifest file or folder**from your repository. - Select
**Next**.

## (Optional) Use a managed ingress and/or Service Connector

When generating Kubernetes manifests with Automated Deployments, you can optionally enable App Routing to set up an ingress controller for your application. You can also use Service Connector to create a new connection or seamlessly integrate your app with an existing Azure service backend.

App Routing provides a fully managed NGINX-based ingress controller out of the box, complete with built-in SSL/TLS encryption using certificates stored in Azure Key Vault and DNS zone management through Azure DNS. When using Automated Deployments, the expose ingress command integrates seamlessly with App Routing, making it easy to expose your application to external traffic under a secure, custom DNS name—with minimal configuration.

- Select the
**Expose ingress**box. - Choose between an
**Existing ingress controller**or a**New ingress controller**. - Choose between using a
**SSL/TLS enabled**or**Insecure**ingress controller. - (Optional) Enter
**Certificate details**if choosing a**SSL/TLS enabled**ingress controller. - Choose between using
**Azure DNS**or a**3rd party provider**. - Enter the
**Azure DNS Zone**and**Subdomain name**.

## (Optional) Add environment variables

Define environment variables for a container in Kubernetes by specifying name-value pairs. Environment variables are important as they help enable easier management of settings, secure handling of sensitive information, and flexibility across environments.

## Review configuration and deploy

Review the configuration for the application, and Kubernetes manifests, then select **Deploy**. A pull request (PR) will be generated against the repository that you selected, so don't navigate away from deployment page.

### Review and merge pull request

When the deployment succeeds, select **View pull request** to view the details of the generated pull request on your code repository.

- Review the changes under
**Files changed**and make any desired edits. - Select
**Merge pull request**to merge the changes into your code repository.

Merging the change runs the GitHub Actions workflow that builds your application into a container image, stores it in Azure Container Registry, and deploys it to the cluster.

### Check the deployed resources

After the pipeline is completed, you can review the created Kubernetes `Service`

in the Azure portal by selecting **Services and ingresses** under the **Kubernetes resources** section of the service menu.

Selecting the **External IP** should open up a new browser page with the running application.

## Delete resources

Once you're done with your cluster, use the following steps to delete it to avoid incurring Azure charges:

- In the Azure portal, navigate to
**Automated deployments** - Select
**...**on the pipeline of your choice. - Select
**Delete**.


---

<!-- DOCUMENTO FUSIONADO: container-network-security-l7-policy-concepts.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-security-l7-policy-concepts -->

# Overview of Layer 7 (L7) policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Network policies are essential for securing Kubernetes clusters by defining and controlling pod communication. They mitigate unauthorized access and potential security breaches by regulating traffic flow. Advanced Container Networking Services strengthens security with [FQDN-based network policies](container-network-security-fqdn-filtering-concepts). Expanding on this foundation, Advanced Container Networking Services now provides L7 policy support, enabling detailed inspection and management of application-level traffic. This advancement enhances both the security and efficiency of network communications within AKS clusters. The offering includes comprehensive support for widely adopted protocols, including HTTP, gRPC, and Kafka.

## Components of L7 policy

**Envoy proxy**: Envoy, part of ACNS security agent acts as the enforcement point for L7 policies. A TPROXY inspects application traffic, comparing it against the defined L7 policies. To enhance scalability and resource management, Envoy is deployed as a separate DaemonSet, decoupled from the Cilium Agent.

## How L7 policy works

When L7 policy enforcement is enabled for an application or pod, outgoing network traffic is first evaluated to determine compliance with the configured application-level rules. The eBPF probe attached to the source pod’s network interface marks the packets, which are then redirected to a node-local Envoy Proxy. This redirection occurs only for pods enforcing L7 policies, ensuring that policy enforcement is applied selectively.

The Envoy proxy, augmented with Cilium network filters, then decides whether to forward the traffic to the destination pod based on policy criteria. If permitted, the traffic proceeds; if not, Envoy returns an appropriate error code to the originating pod. Upon successful authorization, the Envoy proxy facilitates the traffic flow, providing application-level visibility and control. This allows the Cilium agent to enforce detailed network policies within the policy engine. The following diagram illustrates the high-level flow of L7 policy enforcement.

## Monitoring L7 traffic with Hubble and Grafana

To gain insights into L7 traffic flows, specifically HTTP, gRPC, and Kafka, Azure CNI Powered by Cilium leverages Hubble agent, which is enabled by default with Advanced Container Networking Services. Hubble provides detailed flow-level metrics.

To simplify the analysis of these L7 metrics, we provide pre-configured Azure Managed Grafana dashboards. You can find them under the **Dashboards > Azure Managed Prometheus** folder, with filenames like **"Kubernetes/Networking/L7 (Namespace)"** and **"Kubernetes/Networking/L7 (Workload)"**.

These dashboards offer granular visibility into L7 flow data at the cluster, namespace, and workload levels.

Note

These dashboards will only display data if you have this feature enabled on your cluster and have relevant policies applied.
Additionally, the monitoring metrics are **not** required to flow through Envoy, a component of the ACNS security agent. Rather, these metrics are collected by the Hubble agent, which is installed on your cluster as part of the Advanced Container Networking Service's observability feature.

## Key benefits

**Granular Application-Level Control**: L7 policies allow for fine-grained control over network traffic based on application-specific attributes, such as HTTP methods, gRPC paths, and Kafka topics. This extends beyond the basic IP address and port-based control of traditional network policies.

**Enhanced Security**: By inspecting application-level traffic, L7 policies can prevent attacks that exploit vulnerabilities at the application layer. This includes blocking unauthorized access to specific APIs or services. Furthermore, L7 policies are an important component of a Zero Trust security strategy, enabling the enforcement of the principle of least privilege at the application layer.

**Graceful Error Handling**: Unlike L3/L4 policies that typically drop unauthorized traffic silently, L7 policies can return application-level error codes (for example, HTTP 403, Kafka authorization failures), allowing applications to handle errors more gracefully.

**Observability**: With observability enabled for Advanced Container Networking Services and L7 policies applied to your AKS cluster, you can monitor traffic and policy effectiveness using Grafana dashboards.

## Limitations and considerations

- Current feature support relies on Cilium's Layer 7 policy enforcement based on HTTP, HTTPS, gRPC, and Kafka.
- The maximum supported cluster size is up to 1,000 nodes or 40,000 pods, whichever is greater.
- Traffic traversing Envoy proxies do come with latency. Users may experience noticeable latency degradation beyond 3,000 requests per second.
- As part of our observability solution, we provide envoy_http_rq_total metrics. These metrics give the total request count, which could be used to derive requests per seconds (rps).
- During a Cilium upgrade or rollout, existing sessions can be gracefully closed. Applications are expected to handle these interruptions gracefully—typically by implementing retry mechanisms at the connection or request level. New connections initiated during the rollout aren't impacted.
- L7 policy isn't supported by CiliumClusterwideNetworkPolicy(CCNP).
- L7 policy through Advanced Container Networking Services (ACNS) isn't compatible with L7 policies implemented via alternate methods such as Istio. The following table summarizes the supported scenarios.

| Feature/Component | L7 Policies using AKS, Istio - Managed addon |
|---|---|
| K8s network policies by Azure CNI powered by Cilium | Supported |
| L4 (FQDN) Policies by Azure CNI powered by Cilium and ACNS | Supported |
| L7 (HTTP(s)/GRPC/Kafka) Policies by Azure CNI powered by Cilium and ACNS | Not Supported |

## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[L7 policies](how-to-apply-l7-policies)on AKS.Explore how the open source community builds

[Cilium Network Policies](https://docs.cilium.io/en/latest/security/policy/).For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](advanced-container-networking-services-overview#container-network-observability)
