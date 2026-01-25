---
merged_at: 2026-01-25T12:25:33.904801
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-paas-services.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-paas-services -->

# Tutorial - Use PaaS services with an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Kubernetes, you can use PaaS services, such as [Azure Service Bus](/en-us/azure/service-bus-messaging/service-bus-messaging-overview), to develop and run your applications.

In this tutorial, you create an Azure Service Bus namespace and queue to test your application. You learn how to:

- Create an Azure Service Bus namespace and queue.
- Update the Kubernetes manifest file to use the Azure Service Bus queue.
- Test the updated application by placing an order.

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, created a Kubernetes cluster, and deployed an application. To complete this tutorial, you need the pre-created `aks-store-quickstart.yaml`

Kubernetes manifest file. This file download was included with the application source code in a previous tutorial. Make sure you cloned the repo and changed directories into the cloned repo. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create environment variables

Create the following environment variables to use for the commands in this tutorial:

`LOC_NAME=westus2 RAND=$RANDOM RG_NAME=myResourceGroup AKS_NAME=myAKSCluster SB_NS=sb-store-demo-$RAND`


## Create Azure Service Bus namespace and queue

In previous tutorials, you used a RabbitMQ container to store orders submitted by the `order-service`

. In this tutorial, you use an Azure Service Bus namespace to provide a scoping container for the Service Bus resources within the application. You also use an Azure Service bus queue to send and receive messages between the application components. For more information on Azure Service Bus, see [Create an Azure Service Bus namespace and queue](/en-us/azure/service-bus-messaging/service-bus-quickstart-cli).

Create an Azure Service Bus namespace using the

command.`az servicebus namespace create`

`az servicebus namespace create --name $SB_NS --resource-group $RG_NAME --location $LOC_NAME`

Create an Azure Service Bus queue using the

command.`az servicebus queue create`

`az servicebus queue create --name orders --resource-group $RG_NAME --namespace-name $SB_NS`

Create an Azure Service Bus authorization rule using the

command.`az servicebus queue authorization-rule create`

`az servicebus queue authorization-rule create \ --name sender \ --namespace-name $SB_NS \ --resource-group $RG_NAME \ --queue-name orders \ --rights Send`

Get the Azure Service Bus credentials for later use by using the

and`az servicebus namespace show`

commands.`az servicebus queue authorization-rule keys list`

`az servicebus namespace show --name $SB_NS --resource-group $RG_NAME --query name -o tsv az servicebus queue authorization-rule keys list --namespace-name $SB_NS --resource-group $RG_NAME --queue-name orders --name sender --query primaryKey -o tsv`


## Update Kubernetes manifest file

Configure

`kubectl`

to connect to your cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Open the

`aks-store-quickstart.yaml`

file in a text editor.Remove the existing

`rabbitmq`

StatefulSet, ConfigMap, and Service sections and replace the existing`order-service`

Deployment section with the following content:`apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: <REPLACE_WITH_YOUR_ACR_NAME>.azurecr.io/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "<REPLACE_WITH_YOUR_SB_NS_HOSTNAME>" # Example: sb-store-demo-123456.servicebus.windows.net - name: ORDER_QUEUE_PORT value: "5671" - name: ORDER_QUEUE_TRANSPORT value: "tls" - name: ORDER_QUEUE_USERNAME value: "sender" - name: ORDER_QUEUE_PASSWORD value: "<REPLACE_WITH_YOUR_SB_SENDER_PASSWORD>" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3`

Note

Directly adding sensitive information, such as API keys, to your Kubernetes manifest files isn't secure and may accidentally get committed to code repositories. We added it here for simplicity. For production workloads, use

[Managed Identity](use-managed-identity)to authenticate with Azure Service Bus or store your secrets in[Azure Key Vault](csi-secrets-store-driver).Save and close the updated

`aks-store-quickstart.yaml`

file.

## Deploy the updated application

Deploy the updated application using the

`kubectl apply`

command.`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the successfully updated resources:

`deployment.apps/order-service configured service/order-service unchanged deployment.apps/product-service unchanged service/product-service unchanged deployment.apps/store-front configured service/store-front unchanged`


## Test the application

### Place a sample order

Get the external IP address of the

`store-front`

service using the`kubectl get service`

command.`kubectl get service store-front`

Navigate to the external IP address of the

`store-front`

service in your browser using`http://<external-ip>`

.Place an order by choosing a product and selecting

**Add to cart**.Select

**Cart**to view your order, and then select**Checkout**.

### View the order in the Azure Service Bus queue

- Navigate to the Azure portal and open the Azure Service Bus namespace you created earlier.
- Under
**Entities**, select**Queues**, and then select the**orders**queue. - In the
**orders**queue, select**Service Bus Explorer**. - Select
**Peek from start**to view the order you submitted.

## Next steps

In this tutorial, you used Azure Service Bus to update and test the sample application. You learned how to:

- Create an Azure Service Bus namespace and queue.
- Update the Kubernetes manifest file to use the Azure Service Bus queue.
- Test the updated application by placing an order.

In the next tutorial, you learn how to scale an application in AKS.
