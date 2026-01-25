---
merged_at: 2026-01-25T12:25:33.884813
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: kubelet-logs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kubelet-logs -->

# Get kubelet logs from Azure Kubernetes Service cluster nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might need to review logs to troubleshoot a problem in your Azure Kubernetes Service (AKS) cluster. You can use tools in the Azure portal to view logs for AKS [main components](monitor-aks-reference#resource-logs) and [cluster containers](/en-us/azure/azure-monitor/containers/container-insights-overview). Occasionally, you might need to get *kubelet* logs from AKS nodes to help you troubleshoot an issue.

This article shows you how to use `journalctl`

to view kubelet logs on an AKS node.

Alternatively, you can collect kubelet logs by using the [syslog collection feature in Container insights in Azure Monitor](https://aka.ms/CISyslog).

## Before you begin

This article assumes that you have an existing AKS cluster. If you need an AKS cluster, create one by using the [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

## Connect to your AKS cluster

To interact with your AKS cluster, first get the cluster credentials by using the Azure CLI:

```
export RESOURCE_GROUP_NAME="<ResourceGroupName>"
export AKS_CLUSTER_NAME="<AKSClusterName>"
az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $AKS_CLUSTER_NAME
```


This command configures kubectl to use the credentials for your AKS cluster.

## Use the kubectl raw command

You can quickly view any node's kubelet logs by using the following command:

```
export NODE_NAME="aks-agentpool-xxxxxxx-0"
kubectl get --raw "/api/v1/nodes/$NODE_NAME/proxy/logs/messages" | grep kubelet
```


Results:

```
I0508 12:26:17.905042 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:27.943494 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:28.920125 8672 server.go:796] GET /stats/summary: (10.370874ms) 200 [[Ruby] 10.244.0.x:52492]
I0508 12:26:37.964650 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
...
```


## Create an SSH connection

You must create a Secure Shell Protocol (SSH) connection with the node you need to view kubelet logs for. To create this connection, complete the steps that are described in [SSH into AKS cluster nodes](ssh).

## Get kubelet logs

After you connect to the node by using `kubectl debug`

, run the following command to pull the kubelet logs:

```
chroot /host
journalctl -u kubelet -o cat
```


Note

For Windows nodes, the log data is in `C:\k`

and can be viewed by using the `more`

command:

```
more C:\k\kubelet.log
```


The following example output shows kubelet log data:

```
I0508 12:26:17.905042 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:27.943494 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:28.920125 8672 server.go:796] GET /stats/summary: (10.370874ms) 200 [[Ruby] 10.244.0.x:52292]
I0508 12:26:37.964650 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:47.996449 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:58.019746 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:05.107680 8672 server.go:796] GET /stats/summary/: (24.853838ms) 200 [[Go-http-client/1.1] 10.244.0.x:44660]
I0508 12:27:08.041736 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:18.068505 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:28.094889 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:38.121346 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:44.015205 8672 server.go:796] GET /stats/summary: (30.236824ms) 200 [[Ruby] 10.244.0.x:52588]
I0508 12:27:48.145640 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:58.178534 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:05.040375 8672 server.go:796] GET /stats/summary/: (27.78503ms) 200 [[Go-http-client/1.1] 10.244.0.x:44660]
I0508 12:28:08.214158 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:18.242160 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:28.274408 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:38.296074 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:48.321952 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:58.344656 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
```


---

<!-- DOCUMENTO FUSIONADO: app-routing-nginx-prometheus.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/app-routing-nginx-prometheus -->

# Monitor the ingress-nginx controller metrics in the application routing add-on with Prometheus and Grafana

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The ingress-nginx controller in the application routing add-on exposes many metrics for requests, the nginx process, and the controller that can be helpful in analyzing the performance and usage of your application.

The application routing add-on exposes the Prometheus metrics endpoint at `/metrics`

on port 10254 and a private Service `nginx-metrics`

.

## Prerequisites

- An Azure Kubernetes Service (AKS) cluster with the
[application routing add-on enabled](/en-us/azure/aks/app-routing). - A Prometheus instance, such as Azure Monitor managed service for Prometheus.

## Validating the metrics endpoint

To validate the metrics are being collected, you can set up a port forward from a local port to port 10254 on the `nginx-metrics`

service.

```
kubectl port-forward -n app-routing-system service/nginx-metrics :10254
```


```
Forwarding from 127.0.0.1:43307 -> 10254
Forwarding from [::1]:43307 -> 10254
```


Note the local port (`43307`

in this case) and open http://localhost:43307/metrics in your browser. You should see the ingress-nginx controller metrics loading.

You can now terminate the `port-forward`

process to close the forwarding.

## Configuring Azure Monitor managed service for Prometheus

Azure Monitor managed service for Prometheus is a fully managed Prometheus-compatible service that supports industry standard features such as PromQL, Grafana dashboards, and Prometheus alerts. This service requires configuring the metrics addon for the Azure Monitor agent, which sends data to Prometheus. If your cluster isn't configured with the add-on, you can follow this article to configure your Azure Kubernetes Service (AKS) cluster to send data to Azure Monitor managed service for Prometheus.

### Enable Service Monitor based scraping

Once your cluster is updated with the Azure Monitor agent, you need to configure the agent to enable scraping the metrics endpoint. You can [create a Pod or a Service Monitor](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-crd) to accomplish this.

The following creates a Service Monitor scrape metrics from the ingress-nginx controller deployed by the application routing add-on.

```
kubectl apply -f - <<EOF
apiVersion: azmonitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
name: nginx-monitor
namespace: app-routing-system
spec:
labelLimit: 63
labelNameLengthLimit: 511
labelValueLengthLimit: 1023
selector:
matchLabels:
app.kubernetes.io/component: ingress-controller
app.kubernetes.io/managed-by: aks-app-routing-operator
app.kubernetes.io/name: nginx
endpoints:
- port: prometheus
EOF
```


In a few minutes, the `ama-metrics`

pods in the `kube-system`

namespace should restart and pick up the new configuration.

## Review visualization of metrics in Azure Managed Grafana

Now that you have Azure Monitor managed service for Prometheus and Azure Managed Grafana configured, you should [access your Managed Grafana instance](/en-us/azure/managed-grafana/quickstart-managed-grafana-portal#access-your-managed-grafana-instance).

There are two [official ingress-nginx dashboards](https://github.com/kubernetes/ingress-nginx/tree/main/deploy/grafana/dashboards) dashboards that you can download and import into your Grafana instance:

- Ingress-nginx controller dashboard
- Request handling performance dashboard

### Ingress-nginx controller dashboard

This dashboard gives you visibility of request volume, connections, success rates, config reloads and configs out of sync. You can also use it to view the network IO pressure, memory and CPU use of the ingress controller. Finally, it also shows the P50, P95, and P99 percentile response times of your ingresses and their throughput.

You can download this dashboard from [GitHub](https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/grafana/dashboards/nginx.json).

### Request handling performance dashboard

This dashboard gives you visibility into the request handling performance of the different ingress upstream destinations, which are your applications' endpoints that the ingress controller is forwarding traffic to. It shows the P50, P95 and P99 percentile of total request and upstream response times. You can also view aggregates of request errors and latency. Use this dashboard to review and improve the performance and scalability of your applications.

You can download this dashboard from [GitHub](https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/grafana/dashboards/request-handling-performance.json).

### Importing a dashboard

To import a Grafana dashboard, expand the left menu and click on **Import** under Dashboards.

Then upload the desired dashboard file and click on **Load**.

## Next steps

- You can configure scaling your workloads using ingress metrics scraped with Prometheus using
[Kubernetes Event Driven Autoscaler (KEDA)](/en-us/azure/aks/keda-about). Learn more about[integrating KEDA with AKS](/en-us/azure/azure-monitor/essentials/integrate-keda#scalers). - Create and run a load test with
[Azure Load Testing](/en-us/azure/load-testing/quickstart-create-and-run-load-test)to test workload performance and optimize the scalability of your applications.
