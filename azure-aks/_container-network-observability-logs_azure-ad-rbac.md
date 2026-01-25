---
merged_at: 2026-01-25T12:06:27.858001
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: container-network-observability-logs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-logs -->

# What is container network logs (preview)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Component renaming (starting November 11, 2025)

We are renaming components in the Container Network Logs feature to improve clarity and consistency:

What's changing

**CRD**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`

**CLI flag**:`--enable-retinanetworkflowlog`

→`--enable-container-network-logs`

**Log Analytics table**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`


Action items for existing users to enable new naming

**Update Azure CLI**(MUST - First step!):`az upgrade`

**Update Preview CLI Extension**(MUST):`az extension update --name aks-preview`

**Disable Monitoring**:`az aks disable-addons -a monitoring -n <cluster-name> -g <resource-group>`

**Re-enable Monitoring**:`az aks enable-addons -a monitoring --enable-high-log-scale-mode -g <resource-group> -n <cluster-name>`

**Re-enable ACNS Container Network Logs**:`az aks update --enable-acns --enable-container-network-logs -g <resource-group> -n <cluster-name>`

**Apply new ContainerNetworkLog CRD**: Apply your updated CRD configuration with the new naming.**Reimport Grafana Dashboards**: Import the updated dashboards to reflect the new table names.

Note

- Previously collected data stays in your workspace in old table RetinaNetworkFlowLogs.
- After re-enabling, allow a short delay before new data appears in new table ContainerNetworkLog.

Container network logs in [Advanced Container Networking Services](advanced-container-networking-services-overview) for Azure Kubernetes Service (AKS) provide comprehensive, context-rich visibility into every network flow within your cluster. While metrics tell you *what* is happening in your network (such as bandwidth usage or error rates), container network logs tell you *why* by capturing the complete story of each connection—including who initiated it, what protocols were used, and whether the traffic was allowed or blocked.

These logs capture essential metadata for every network flow, including source and destination IP addresses, pod and service names, namespaces, ports, protocols, traffic direction, and policy verdicts. This deep contextual information enables you to correlate network behavior with specific workloads, troubleshoot connectivity issues, validate security policies, and perform forensic analysis.

Container network logs capture Layer 3 (IP), Layer 4 (TCP/UDP), and Layer 7 (HTTP/gRPC/Kafka) traffic, providing the detailed insights you need to monitor connectivity, troubleshoot issues, visualize network topology, enforce security policies, and ensure compliance.

Choose from two modes:

- Stored logs
- On-demand logs

## Stored logs

Stored logs mode ensures continuous log generation and collection in the AKS cluster when you enable Advanced Container Networking Services and set up custom filters. By default, log collection is disabled.

To enable log collection, you define *custom resources* to specify the types of traffic to monitor. Examples include namespaces, pods, services, and protocols. This feature remains active until you disable it.

Stored logs mode supports extended log retention and traffic filtering. For reduced storage costs and easier analysis, you can collect and retain only the logs that are relevant to you.

### How stored logs mode works

Advanced Container Networking Services uses eBPF technology with Cilium to fetch logs from nodes in your cluster. To start collecting logs, you define one or more custom resources to specify the types of traffic to monitor.

Custom resources provide fine-grained control to define and capture the traffic that is relevant to you. The Cilium agent running on each node collects network traffic that matches the criteria set in the custom resources. The logs are stored in JSON format on the host, providing a structured and accessible format for further use.

Alternatively, if the Azure Monitoring add-on is enabled, agents for Container insights collect the logs from the host, apply the default throttling limits, and send them to a Log Analytics workspace. The system aggregates and stores logs efficiently to provide visibility into network traffic for monitoring, troubleshooting, and security enforcement.

To read more about throttling and Container insights, see the [Container insights documentation](https://aka.ms/ContainerNetworkLogsDoc_CI).

### Key capabilities of stored logs mode

*Customizable filters.*You can configure logging by defining custom resources of the[ContainerNetworkLog](how-to-configure-container-network-logs#containernetworklog-crd-template)type. Use custom resources to apply granular filters by namespace, pod, service, port, protocol, verdict, or traffic direction (ingress or egress). This flexibility ensures precise data collection tailored to specific use cases. Only relevant traffic is logged, and storage is optimized for improved performance, compliance, and troubleshooting.*Log storage options.*The container network logs feature has two primary storage options: unmanaged storage and managed storage.**Unmanaged storage:**When a custom resource is applied to begin log collection, network flow logs are stored locally on the host nodes at the`/var/log/acns/hubble`

fixed mount location. This storage location is temporary because the node itself isn't a persistent storage solution. When the log files reach a size of 50 MB, they're automatically rotated and older logs are overwritten. This storage solution is suitable for real-time monitoring, but it doesn't support long-term storage or retention.For additional log management capabilities, you can integrate partner logging services like an OpenTelemetry collector. Partner integrations provide flexibility to manage logs outside the Azure ecosystem and are useful if you've already deployed a specific log management platform.

**Managed storage:**For long-term retention and advanced analytics, we recommend that you configure Azure monitoring in your AKS cluster to collect and store logs in a Log Analytics workspace. This setup ensures secure and compliant log storage. It also provides access to powerful capabilities like anomaly detection, performance tuning, and historical data analysis. You can use historical logs to identify trends, baseline behaviors, and proactively address recurring issues.For example, you can use the managed service for Prometheus to configure alerts on both metrics and logs for real-time monitoring and rapid detection of outliers.

You use the same workspace for log storage. You set up log storage space during onboarding. Both Analytics and Basic log table plans are supported for this feature. For more detailed information on table plans, see

[Azure Monitor Logs](/en-us/azure/azure-monitor/logs/data-platform-logs).

*Simple visualization in Log Analytics and Grafana dashboards.*Logs and data presented in Grafana dashboards simplify complex information, facilitate data comprehension, and help you make decisions more quickly.

### Logs visualization in the Azure portal

You can visualize, query, and analyze flow logs in the Azure portal in the Log Analytics workspace for your cluster.

### Logs visualization in Grafana dashboards

Access the flow logs in an Azure Managed Grafana instance.

To simplify your analysis of logs, we provide two preconfigured Grafana dashboards:

Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs**. This dashboard shows which AKS workloads are communicating with each other, including network requests, responses, drops, and errors. Currently, as an interim step during preview, you must import Grafana dashboards by using a user ID to view the flow logs dashboard in the Azure portal.Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs (External Traffic)**. This dashboard shows which AKS workloads send and receive communications from outside an AKS cluster, including network requests, responses, drops, and errors.For more information, see

[Set up Azure Managed Grafana with Advanced Container Networking Services](how-to-configure-container-network-logs#visualization-in-grafana-dashboards).

Access the flow logs in the Azure portal via the

**Dashboards with Grafana**option.

The Azure portal dashboards have the following major components:

*A comprehensive overview of network health.*You see key metrics like total flow logs, unique requests, dropped requests, and forwarded requests for quick anomaly detection and efficient troubleshooting. The dashboard categorizes statistics by protocol and behavior, including DNS dropped requests, HTTP 2xx responses, Layer 4 request and response rates, and dropped request counts. A service dependency graph visualizes application or cluster interactions, highlighting traffic flow, bottlenecks, and dependencies for performance optimization.*Flow logs and error logs for quick analysis.*You can filter flow logs for root-cause analysis. For example, to troubleshoot Domain Name System (DNS) issues, filter error logs by the DNS protocol.Separating flow logs and error logs helps you analyze issues more quickly. You can identify and address errors without sifting through unrelated information, which improves efficiency in troubleshooting and debugging processes.

Use clear labels and timestamps for each log entry to more easily pinpoint specific events or errors in your systems or processes.

*Top namespaces, workloads, and DNS errors.*Network flow log visualization is vital for monitoring and analyzing communication in an AKS cluster. It provides insight into namespaces, workloads, port usage, and query usage. It helps you identify trends, detect bottlenecks, and diagnose issues. Spot significant network activity, view dropped requests, and assess protocol distribution (for example, TCP versus UDP). This overview section of the dashboard supports cluster health, resource optimization, and security by detecting and displaying unusual traffic patterns.

## On-demand logs

Advanced Container Networking Services offers on-demand capture of network flow logs. Get real-time visibility without prior configuration or persistent storage by using the Hubble CLI and the Hubble UI. This on-demand logs mode is available. To learn how to set up on-demand log storage, see [Configure the Hubble CLI and Hubble UI](how-to-configure-container-network-logs#configure-on-demand-logs-mode).

### Hubble CLI

The Hubble command-line interface (CLI) provides a flexible and interactive way to query, filter, and analyze flow logs directly in the terminal. You can execute real-time commands to inspect traffic flows, view packet metadata, and troubleshoot network issues without leaving your operational environment.

### Hubble UI

The Hubble web-based interface offers an intuitive and visual platform for monitoring. With features like live traffic dashboards, flow summaries, and searchable logs, you can easily track service-to-service communication, detect anomalies, and gain insights into cluster activity.

The Hubble UI tools provide real-time visibility and actionable insights for faster troubleshooting and improved network management.

### Key benefits of on-demand logs

*Faster issue resolution.*With detailed and actionable insights into network traffic, you can identify and resolve connectivity or performance issues more quickly, minimizing downtime and disruptions.*Optimized operational efficiency.*Aggregated and efficiently stored logs reduce data management overhead. Your team can focus on analysis and decision-making instead of managing large volumes of raw data.*Enhanced application reliability.*By monitoring service-to-service communication and detecting anomalies, you can proactively address potential issues and ensure a smoother and more reliable application experience.*Improved decision-making.*Visualizing network patterns in Azure Managed Grafana and applying service maps provide clear insights into your application's network behavior. This leads to improved infrastructure planning and optimization.*Cost savings.*Efficient log aggregation and customizable logging scopes reduce storage and data ingestion costs, providing a cost-effective solution for long-term network monitoring.*Streamlined compliance and security.*Persistent and comprehensive logs support audit trails, regulatory compliance, and quick identification of suspicious traffic. They help you maintain a secure and compliant environment.

## Limitations

- Container network logs in stored logs mode currently works only with the Cilium data plane.
- Layer 7 flow logs are captured only when Layer 7 policy support is enabled. For more information, see
[Configure a Layer 7 policy](how-to-apply-l7-policies). - DNS flows and metrics are captured only when a Cilium Fully Qualified Domain (FQDN) network policy is applied. For more information, see
[Configure an FQDN policy](how-to-apply-fqdn-filtering-policies). - Onboarding by using Terraform currently isn't supported.
- When Log Analytics isn't configured for log storage, container network logs are limited to a maximum of 50 MB of storage. When this limit is reached, new entries overwrite older logs.
- If the table plan is set to Basic logs, prebuilt Grafana dashboards don't work.
- The Auxiliary logs table plan isn't supported.

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- Learn how to set up
[container network logs](how-to-configure-container-network-logs). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.


---

<!-- DOCUMENTO FUSIONADO: azure-ad-rbac.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-ad-rbac -->

# Use Kubernetes RBAC with Microsoft Entra ID in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) can be configured to use Microsoft Entra ID for user authentication. In this configuration, you sign in to an AKS cluster using a Microsoft Entra authentication token. Once authenticated, you can use the built-in Kubernetes role-based access control (RBAC) to manage access to namespaces and cluster resources based on a user's identity or group membership.

This article shows you how to:

Control access using Kubernetes RBAC in an AKS cluster based on Microsoft Entra group membership.

Create example groups and users in Microsoft Entra ID.

Create Roles and RoleBindings in an AKS cluster granting the appropriate permissions, such as to create and view resources.


## Prerequisites

You have an existing AKS cluster with Microsoft Entra integration enabled. If you need an AKS cluster with this configuration, see

[Integrate Microsoft Entra ID with AKS](managed-azure-ad).Kubernetes RBAC is enabled by default during AKS cluster creation. To upgrade an existing cluster with Microsoft Entra integration and Kubernetes RBAC, see

[Enable Microsoft Entra integration on your existing AKS cluster](managed-azure-ad#use-an-existing-cluster).Make sure that Azure CLI version 2.0.61 or later is installed and configured. To find the version, run

`az --version`

. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).If using Terraform, install

[Terraform](/en-us/azure/developer/terraform/overview)version 2.99.0 or later.

Use the Azure portal or Azure CLI to verify Microsoft Entra integration with Kubernetes RBAC is enabled.

To verify using the Azure portal:

- Sign-in to the
[Azure portal](https://portal.azure.com)and navigate to your AKS cluster resource. - In the service menu, under
**Settings**, select**Security configuration**. - Under the
**Authentication and Authorization**section, verify the**Microsoft Entra authentication with Kubernetes RBAC**option is selected.

## Create groups in Microsoft Entra ID

This section teaches you how to create two user roles to show how Kubernetes RBAC and Microsoft Entra ID control access cluster resources. The following two example roles are:

**Application developer**- A user named
*aksdev*that's part of the*appdev*group.

- A user named
**Site reliability engineer**(SRE)- A user named
*akssre*that's part of the*opssre*group.

- A user named

In production environments, you can use existing users and groups within a Microsoft Entra tenant.

First, get the resource ID of your AKS cluster using the

command. Then, assign the resource ID to a variable named`az aks show`

*AKS_ID*so it can be referenced in other commands.`AKS_ID=$(az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query id -o tsv)`

Create the first example group in Microsoft Entra ID for the application developers using the

command. The following example creates a group named`az ad group create`

*appdev*:`APPDEV_ID=$(az ad group create --display-name appdev --mail-nickname appdev --query id -o tsv)`

Create an Azure role assignment for the

*appdev*group using thecommand. This assignment lets any member of the group use`az role assignment create`

`kubectl`

to interact with an AKS cluster by granting them the*Azure Kubernetes Service Cluster User*Role.`az role assignment create \ --assignee $APPDEV_ID \ --role "Azure Kubernetes Service Cluster User Role" \ --scope $AKS_ID`

Tip

If you receive an error such as

`Principal 35bfec9328bd4d8d9b54dea6dac57b82 doesn't exist in the directory a5443dcd-cd0e-494d-a387-3039b419f0d5.`

, wait a few seconds for the Microsoft Entra group object ID to propagate through the directory then try the`az role assignment create`

command again.

## Create users in Microsoft Entra ID

After you create the example Microsoft Entra ID groups for application developers and SREs, the next step is to create two corresponding user accounts. These users are used to sign in to the AKS cluster and validate the Kubernetes RBAC integration described later in this article.

Before you begin, you must set the user principal name (UPN) and password for the application developers. The UPN must include the verified domain name of your tenant. For example, an application developer user, `aksdev@contoso.com`

. In order to figure out (or set) the verified domain names in your tenant, see [Managing custom domain names in your Microsoft Entra ID](/en-us/entra/identity/users/domains-manage).

The following command prompts you for the UPN and sets it to *AAD_DEV_UPN* so it can be used in a later command:

```
echo "Please enter the UPN for application developers: " && read AAD_DEV_UPN
```


The following command prompts you for the password and sets it to *AAD_DEV_PW* for use in a later command:

```
echo "Please enter the secure password for application developers: " && read AAD_DEV_PW
```


### Create user accounts

Create the first user account in Microsoft Entra ID using the

command. The following example creates a user with the display name`az ad user create`

*AKS Dev*, the UPN, and secure password using the values in*AAD_DEV_UPN*and*AAD_DEV_PW*:`AKSDEV_ID=$(az ad user create \ --display-name "AKS Dev" \ --user-principal-name $AAD_DEV_UPN \ --password $AAD_DEV_PW \ --query id -o tsv)`

Add the user to the

*appdev*group created in the previous section using thecommand:`az ad group member add`

`az ad group member add --group appdev --member-id $AKSDEV_ID`


## Create AKS cluster resources

We have our Microsoft Entra groups, users, and Azure role assignments created. Now, you configure the AKS cluster to allow these different groups access to specific resources.

Get the cluster admin credentials using the

command. In one of the following sections, you get the regular`az aks get-credentials`

*user*cluster credentials to see the Microsoft Entra authentication flow in action.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin`

Create a namespace in the AKS cluster using the

command. The following example creates a namespace name`kubectl create namespace`

*dev*:`kubectl create namespace dev`

Note

In Kubernetes,

*Roles*define the permissions to grant, and*RoleBindings*apply them to desired users or groups. These assignments can be applied to a given namespace, or across the entire cluster. For more information, see[Using Kubernetes RBAC authorization](concepts-identity#kubernetes-rbac).If the user you grant the Kubernetes RBAC binding for is in the same Microsoft Entra tenant, assign permissions based on the

**UPN**. If the user is in a different Microsoft Entra tenant, query for and use the*objectId*property instead.Create a Role for the

*dev*namespace, which grants full permissions to the namespace. In production environments, you can specify more granular permissions for different users or groups. Create a file named`role-dev-namespace.yaml`

and paste the following YAML manifest:`kind: Role apiVersion: rbac.authorization.k8s.io/v1 metadata: name: dev-user-full-access namespace: dev rules: - apiGroups: ["", "extensions", "apps"] resources: ["*"] verbs: ["*"] - apiGroups: ["batch"] resources: - jobs - cronjobs verbs: ["*"]`

Create the Role using the

command and specify the filename of your YAML manifest.`kubectl apply`

`kubectl apply -f role-dev-namespace.yaml`

Get the resource ID for the

*appdev*group using thecommand. This group is set as the subject of a RoleBinding in the next step.`az ad group show`

`az ad group show --group appdev --query id -o tsv`

Create a RoleBinding for the

*appdev*group to use the previously created Role for namespace access. Create a file named`rolebinding-dev-namespace.yaml`

and paste the following YAML manifest. On the last line, replace*groupObjectId*with the group object ID output from the previous command.`kind: RoleBinding apiVersion: rbac.authorization.k8s.io/v1 metadata: name: dev-user-access namespace: dev roleRef: apiGroup: rbac.authorization.k8s.io kind: Role name: dev-user-full-access subjects: - kind: Group namespace: dev name: groupObjectId`

Tip

If you want to create the RoleBinding for a single user, specify

*kind: User*and replace*groupObjectId*with the UPN in the previous sample.Create the RoleBinding using the

command and specify the filename of your YAML manifest:`kubectl apply`

`kubectl apply -f rolebinding-dev-namespace.yaml`


## Access AKS cluster resources with Microsoft Entra identities

Now, test that the expected permissions work when you create and manage resources in an AKS cluster. In these examples, you schedule and view pods in the user's assigned namespace, and try to schedule and view pods outside of the assigned namespace.

Reset the

*kubeconfig*context using thecommand. In a previous section, you set the context using the cluster admin credentials. The admin user bypasses Microsoft Entra sign-in prompts. Without the`az aks get-credentials`

`--admin`

parameter, the user context is applied that requires all requests to be authenticated using Microsoft Entra ID.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --overwrite-existing`

Schedule a basic NGINX pod using the

command in the`kubectl run`

*dev*namespace:`kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev`

Enter the credentials for the

*appdev*group account (enter*your*own credentials) at the sign-in prompt. Once you're successfully signed in, the account token is cached for future`kubectl`

commands. The NGINX is successfully scheduled as shown in the following example output:`$ kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code B24ZD6FP8 to authenticate. pod/nginx-dev created`

Use the

command to view pods in the`kubectl get pods`

*dev*namespace:`kubectl get pods --namespace dev`

Ensure the status of the NGINX pod is

*Running*. The output looks like the following output:`$ kubectl get pods --namespace dev NAME READY STATUS RESTARTS AGE nginx-dev 1/1 Running 0 4m`


### Test SRE access to AKS cluster resources

To confirm that our Microsoft Entra group membership and Kubernetes RBAC work correctly between different users and groups, try the previous commands when signed in as the *akssre* user.

Reset the

*kubeconfig*context using thecommand that clears the previously cached authentication token for the`az aks get-credentials`

*aksdev*user.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --overwrite-existing`

Schedule and view pods in the assigned

*SRE*namespace. When prompted, sign in with the*opssre*group account credentials (enter*your*own credentials).`kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre kubectl get pods --namespace sre`

As shown in the following example output, you can successfully create and view the pods:

`$ kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre`

To sign in, use a web browser to open the page

[https://microsoft.com/devicelogin](https://microsoft.com/devicelogin)and enter the code BM4RHP3FD to authenticate.`pod/nginx-sre created $ kubectl get pods --namespace sre NAME READY STATUS RESTARTS AGE nginx-sre 1/1 Running 0`

Try to view or schedule pods outside of assigned SRE namespace.

`kubectl get pods --all-namespaces kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev`

These

`kubectl`

commands fail, as shown in the following example output. The user's group membership and Kubernetes Role and RoleBindings don't grant permissions to create or manager resources in other namespaces.`$ kubectl get pods --all-namespaces Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot list pods at the cluster scope $ kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot create pods in the namespace "dev"`


### Create and view cluster resources outside of the assigned namespace

To view pods outside of the *dev* namespace. Use the [ kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command using

`--all-namespaces`

:```
kubectl get pods --all-namespaces
```


The user's group membership doesn't have a Kubernetes Role that allows this action, as shown in the following example output:

```
Error from server (Forbidden): pods is forbidden: User "aksdev@contoso.com" cannot list resource "pods" in API group "" at the cluster scope
```


In the same way, schedule a pod in a different namespace, such as the *SRE* namespace. The user's group membership doesn't align with a Kubernetes Role and RoleBinding to grant these permissions, as shown in the following example output:

```
$ kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre
Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot create resource "pods" in API group "" in the namespace "sre"
```


### Clean up cluster resources

To clean up all of the resources, run the following commands:

```
# Get the admin kubeconfig context to delete the necessary cluster resources.
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin
# Delete the dev and SRE namespaces. This also deletes the pods, Roles, and RoleBindings.
kubectl delete namespace dev
kubectl delete namespace sre
# Delete the Azure AD user accounts for aksdev and akssre.
az ad user delete --upn-or-object-id $AKSDEV_ID
az ad user delete --upn-or-object-id $AKSSRE_ID
# Delete the Azure AD groups for appdev and opssre. This also deletes the Azure role assignments.
az ad group delete --group appdev
az ad group delete --group opssre
```


## Next steps

For more information about how to secure Kubernetes clusters, see

[Access and identity options for AKS](concepts-identity#kubernetes-rbac).For best practices on identity and resource control, see

[Best practices for authentication and authorization in AKS](operator-best-practices-identity).
